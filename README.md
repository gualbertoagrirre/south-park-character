# south-park-character
University project for elective 3
para hacerlo correr : g++ -o a mu.cpp -lGL -lGLU -lglut

#include <GL/glut.h>
#include <unistd.h>
#include <stdio.h>//
#include <stdarg.h>//
#include <math.h>//
#ifdef __APPLE__//
#include <GLUT/glut.h>//
#else//
#define GL_GLEXT_PROTOTYPES//
#endif//
// Medidas del cuerpo
#define BODY_HEIGHT 4.0
#define BODY_WIDTH  2.5
#define BODY_LENGTH 1.0
#define ARM_HEIGHT 3.5
#define ARM_WIDTH  1.0
#define ARM_LENGTH 1.0
#define LEG_HEIGHT 4.5
#define LEG_WIDTH 1.0
#define LEG_LENGTH 1.0
#define HEAD_RADIUS 2.9



void display();
void specialKeys();

double rotate_y=0;
double rotate_x=0;


void display(){
glClear(GL_COLOR_BUFFER_BIT|GL_DEPTH_BUFFER_BIT);
glLoadIdentity();
glDepthFunc(GL_LEQUAL);
glEnable(GL_DEPTH_TEST);


// Activamos el  el Z-Buffer
glClearColor(0.0,0.0,0.0,0.0);
glClearDepth(1.0);
glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);//demass
// Borramos el buffer de color y el Z-Buffer
glMatrixMode(GL_PROJECTION);
glLoadIdentity();//demass
//gluPerspective(120.0,1.0,1.0,200.0);
//glTranslatef(0.0,0.0,-90.0);
gluPerspective(60.0,1.0,1.0,100.0);
//gluPerspective(60.0,8.0,8.0,100.0);
//gluPerspective(60.0,1.0,15.0,100.0);
//gluPerspective(90.0,1.0,1.0,100.0);



glRotatef( rotate_x, 1.0, 0.0, 0.0 );
glRotatef( rotate_y, 0.0, 1.0, 0.0 );





glMatrixMode(GL_MODELVIEW);
glTranslatef(0.0,0.0,-16.0);

glBegin(GL_POLYGON);

  glColor3f( 1.0, 0.0, 0.0 );     glVertex3f(  5.5, -5.5, -0.55 );      // P1 es rojo
  glColor3f( 0.0, 1.0, 0.0 );     glVertex3f(  5.5,  5.5, -0.5 );      // P2 es verde
  glColor3f( 0.0, 0.0, 1.0 );     glVertex3f( -5.5,  5.5, -0.5 );      // P3 es azul
  glColor3f( 1.0, 0.0, 1.0 );     glVertex3f( -5.5, -5.5, -0.5 );      // P4 es morado
  glEnd();


// LADO TRASERO
  glBegin(GL_POLYGON);
  glColor3f(   1.0,  1.0, 1.0 );
  glVertex3f(  0.5, -0.5, 0.5 );
  glVertex3f(  0.5,  0.5, 0.5 );
  glVertex3f( -0.5,  0.5, 0.5 );
  glVertex3f( -0.5, -0.5, 0.5 );
  glEnd();



// Dibujamos el cuerpo
glTranslatef(0,BODY_HEIGHT/4,0);
glPushMatrix();
glScalef(BODY_WIDTH,BODY_HEIGHT,BODY_LENGTH);
glColor3f(0.0,0.3,0.8);
glutSolidCube(1);
glPopMatrix();


// Dibujamos el brazo derecho
glPushMatrix();
glTranslatef(-(BODY_WIDTH)/4,(BODY_HEIGHT-ARM_HEIGHT)/4,0);
glTranslatef(0,ARM_HEIGHT/4,0);
glRotatef(-90,0,0,1);
glTranslatef(0,-ARM_HEIGHT/4,0);
glPushMatrix();
glScalef(ARM_WIDTH,ARM_HEIGHT,ARM_LENGTH);
glutSolidCube(1);
glPopMatrix();


// ya tenemos el brazo... la mano
glTranslatef(0,-(ARM_HEIGHT+ARM_WIDTH)/4,0);
glColor3f(1,0.6,0.6);
glScalef(ARM_WIDTH,ARM_WIDTH,ARM_LENGTH);
glutSolidCube(1);
glPopMatrix();


// Dibujamos el brazo izquierdo
glColor3f(0.0,0.3,0.8);
glPushMatrix();
glTranslatef((BODY_WIDTH)/4,(BODY_HEIGHT-ARM_HEIGHT)/4,0);
glTranslatef(0,ARM_HEIGHT/4,0);
glRotatef(30,0,0,1);
glTranslatef(0,-ARM_HEIGHT/4,0);
glPushMatrix();
glScalef(ARM_WIDTH,ARM_HEIGHT,ARM_LENGTH);
glutSolidCube(1);
glPopMatrix();


// ya tenemos el brazo... la mano
glTranslatef(0,-(ARM_HEIGHT+ARM_WIDTH)/4,0);
glColor3f(1,0.6,0.6);
glScalef(ARM_WIDTH,ARM_WIDTH,ARM_LENGTH);
glutSolidCube(1);
glPopMatrix();


//Dibujamos la pierna derecha
glColor3f(0.0,0.3,0.8);
glPushMatrix();
glTranslatef(-(BODY_WIDTH-LEG_WIDTH)/4,-
(BODY_HEIGHT+LEG_HEIGHT)/4,0);
//glRotatef(-30,0,0,1);
glPushMatrix();
glScalef(LEG_WIDTH,LEG_HEIGHT,LEG_LENGTH);
glutSolidCube(1);
glPopMatrix();



// ahora el píe
glTranslatef(0,-(LEG_HEIGHT+LEG_WIDTH)/4,LEG_LENGTH);
glColor3f(0.3,0.4,0.4);
glScalef(LEG_WIDTH,LEG_WIDTH,LEG_LENGTH*4);
glutSolidCube(1);
glPopMatrix();



//Dibujamos la pierna izquierda
glColor3f(0.0,0.3,0.8);
glPushMatrix();
glTranslatef((BODY_WIDTH-LEG_WIDTH)/4,-
(BODY_HEIGHT+LEG_HEIGHT)/4,0);
glPushMatrix();
glScalef(LEG_WIDTH,LEG_HEIGHT,LEG_LENGTH);
glutSolidCube(1);
glPopMatrix();



// ahora el píe
glTranslatef(0,-(LEG_HEIGHT+LEG_WIDTH)/4,LEG_LENGTH);
glColor3f(0.3,0.4,0.4);
glScalef(LEG_WIDTH,LEG_WIDTH,LEG_LENGTH*4);
glutSolidCube(1);
glPopMatrix();


// Dibujamos la cabeza
glColor3f(1,0.6,0.6);
glPushMatrix();
glTranslatef(0,BODY_HEIGHT/4 + HEAD_RADIUS*3/4,0);
glutSolidSphere(HEAD_RADIUS,10,10);
glPopMatrix();


glFlush();
glutSwapBuffers();
//sleep(20);
//exit(0);
}


void specialKeys( int key, int x, int y ) {
  //  Flecha derecha: aumentar rotación 5 grados
  if (key == GLUT_KEY_RIGHT)
    rotate_y += 5;
  //  Flecha izquierda: disminuir rotación 5 grados
  else if (key == GLUT_KEY_LEFT)
    rotate_y -= 5;
  else if (key == GLUT_KEY_UP)
    rotate_x += 5;
  else if (key == GLUT_KEY_DOWN)
    rotate_x -= 5;
  //  Solicitar actualización de visualización
  glutPostRedisplay();
}


int main(int argc, char ** argv){
glutInit(&argc,argv);////
glutInitDisplayMode(GLUT_SINGLE | GLUT_RGBA | GLUT_DEPTH);////
glutInitWindowPosition(20,20);//
glutInitWindowSize(500,500);//
glutCreateWindow("yuko");////
glEnable(GL_DEPTH_TEST);//
glutSpecialFunc(specialKeys);//
glutDisplayFunc(display);////
glutMainLoop();////
return 0;
}

