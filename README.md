#include <stdio.h>
#include <stdlib.h>
#include <glut.h>

void ayarlar(void){
	glClearColor(0.0, 0.0, 0.0, 0.0);
	glOrtho(-100.0, 100.0, -100.0, 100.0, -1.0, 1.0);
}
void display(void)
{
	glClear(GL_COLOR_BUFFER_BIT);
	glColor3f(1.0, 0.0, 0.0);
	glBegin(GL_POLYGON);
	glVertex2f(-80, -80);
	glVertex2f(-80, 0);
	glVertex2f(0, 0);
	glVertex2f(0, -80);
	glEnd();
    
    glColor3f(1.0, 0.0, 0.0);
    glBegin(GL_POLYGON);
    glVertex2f(0, 0);
    glVertex2f(0, -80);
    glVertex2f(0, -40);
    glEnd();
    
    glColor3f(0.0, 0.0, 1.0);
    glBegin(GL_POLYGON);
    glVertex2f(-10, -10);
    glVertex2f(-10, -30);
    glVertex2f(-30, -10);
    glVertex2f(-30, -30);
    glEnd();
    
    glColor3f(1.0, 0.0, 0.0);
    glBegin(GL_POLYGON);
    glVertex2f(-50, -10);
    glVertex2f(-50, -30);
    glVertex2f(-70, -10);
    glVertex2f(-70, -30);
    glEnd();
    /*
    glColor3f(1.0, 0.0, 0.0);
    glBegin(GL_POLYGON);
    glVertex2f(-80, -80);
    glVertex2f(-80, 0);
    glVertex2f(0, 0);
    glVertex2f(0, -80);
    glEnd();
    */
	glFlush();
}

int main(int argc, char **argv){
	glutInit(&argc, argv);
	glutInitDisplayMode(GLUT_SINGLE | GLUT_RGB);
	glutInitWindowPosition(0, 0);
	glutInitWindowSize(500, 400);
	glutCreateWindow("OpenGL Uygulamalar˝-I");
	ayarlar();
	glutDisplayFunc(display);
	glutMainLoop();
	return 0;
}











