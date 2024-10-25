# New-repository











// DENEYİN YAPILIŞI KODUNU BURADAN İTİBAREN YAZABİLİRSİNİZ

if (FireEnemyMissile) {
	// Merminin başlangıç konumunu düşman tankının namlusunun ucuna ayarla
	XMFLOAT4X4 worldEnemyMatrix;
	XMStoreFloat4x4(&worldEnemyMatrix, g_World_Enemy);  // Düşman tankının dünya matrisini al

	// Namlunun ucunun pozisyonunu hesapla
	XMVECTOR barrelEnd = XMVectorSet(
		worldEnemyMatrix._41,
		worldEnemyMatrix._42 + 1.0f,  // Namlunun ucunu biraz yukarıda varsayıyoruz
		worldEnemyMatrix._43 + 2.5f,  // Tanktan ileri doğru 2.5 birim
		1.0f
	);

	// Başlangıç konumunu matrislere aktar
	XMFLOAT4 initialPosition_F4;
	XMStoreFloat4(&initialPosition_F4, barrelEnd);

	g_World_Enemy_Missile = g_World_Enemy;  // Mermi düşman tankıyla aynı yön ve pozisyonda başlar
	XMStoreFloat4x4(&g_World_Enemy_Missile_4x4, g_World_Enemy_Missile);

	// Mermiyi namlunun ucuna yerleştir
	g_World_Enemy_Missile_4x4._41 = initialPosition_F4.x;
	g_World_Enemy_Missile_4x4._42 = initialPosition_F4.y;
	g_World_Enemy_Missile_4x4._43 = initialPosition_F4.z;

	g_World_Enemy_Missile = XMLoadFloat4x4(&g_World_Enemy_Missile_4x4);

	// Ateşleme sesi çal
	PlaySound(TEXT("explosion.wav"), NULL, SND_FILENAME | SND_ASYNC | SND_NODEFAULT);
}

if (TraceEnemyMissile) {
	// Mermiyi ilerletmek için pozisyonları al
	XMStoreFloat4x4(&g_World_Enemy_Missile_4x4, g_World_Enemy_Missile);
	XMVECTOR missileEnemyPos = XMVectorSet(
		g_World_Enemy_Missile_4x4._41,
		g_World_Enemy_Missile_4x4._42,
		g_World_Enemy_Missile_4x4._43,
		1.0f
	);

	XMFLOAT4X4 worldTankMatrix;
	XMStoreFloat4x4(&worldTankMatrix, g_World_Tank);
	XMVECTOR playerTankPos = XMVectorSet(
		worldTankMatrix._41,
		worldTankMatrix._42,
		worldTankMatrix._43,
		1.0f
	);

	// Mermiyi oyuncu tankına yönlendir
	Rd_Enemy_Missile = XMVector3Normalize(playerTankPos - missileEnemyPos);

	// Mermiyi ilerlet
	g_World_Enemy_Missile_4x4._41 += 0.1f * XMVectorGetX(Rd_Enemy_Missile);
	g_World_Enemy_Missile_4x4._42 += 0.1f * XMVectorGetY(Rd_Enemy_Missile);
	g_World_Enemy_Missile_4x4._43 += 0.1f * XMVectorGetZ(Rd_Enemy_Missile);

	g_World_Enemy_Missile = XMLoadFloat4x4(&g_World_Enemy_Missile_4x4);

	// Patlama kontrolü
	float distance = XMVectorGetX(XMVector3Length(playerTankPos - missileEnemyPos));
	if (distance < 0.5f) {  // Belirli bir eşik değeri (0.5 birim)
		PlaySound(TEXT("hit.wav"), NULL, SND_FILENAME | SND_ASYNC); // Patlama sesi çal

		renderTank = false;
		renderTankMissile = false;  // Mermiyi sahneden kaldır

	}
}





//
