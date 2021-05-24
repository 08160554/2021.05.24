# 2021.05.24
WEEK14

01
------
```C
#include <GL/glut.h>
void display()
{
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
    glutSolidSphere(0.3,30,30);  ///0.3是半徑，實心的圓球
    glutSwapBuffers();
}

int main(int argc, char** argv)
{
    glutInit( &argc, argv );
    glutInitDisplayMode( GLUT_DOUBLE | GLUT_DEPTH );
    glutCreateWindow("08160554");
    glutDisplayFunc(display);

    glutMainLoop();
}
```

02
-----
```C
#include <GL/glut.h>
void display()
{
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
    glutSolidSphere(0.3,30,30);
    glutSwapBuffers();
}
void timer(int t)
{
    glClearColor(1,0,0,0);///紅色的
    display();
}

int main(int argc, char** argv)
{
    glutInit( &argc, argv );
    glutInitDisplayMode( GLUT_DOUBLE | GLUT_DEPTH );
    glutCreateWindow("08160554");
    glutDisplayFunc(display);
    glutTimerFunc(4000,timer,0); 
    ///4000=>要等多久，timer=>叫誰，0=>參數
    glutMainLoop();
}
```

03
-----
```C
#include <GL/glut.h>
int angle=0;
void display()
{
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
    glPushMatrix();
        glRotatef(angle,0,0,1);
        glutSolidCube(0.3);
    glPopMatrix();
    glutSwapBuffers();
}
void timer(int t)
{
    glutTimerFunc(30,timer,t+1);
    angle++;
    display();
}

int main(int argc, char** argv)
{
    glutInit( &argc, argv );
    glutInitDisplayMode( GLUT_DOUBLE | GLUT_DEPTH );
    glutCreateWindow("08160554");
    glutDisplayFunc(display);
    glutTimerFunc(4000,timer,0);
    glutMainLoop();
}
```

04
------
```C
#include <GL/glut.h>
int angle=0;
void display()
{
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
    glPushMatrix();
        glRotatef(angle,0,0,1);
        glutSolidCube(0.3);
    glPopMatrix();
    glutSwapBuffers();
}
int diff=2;
void timer(int t)
{
    glutTimerFunc(30,timer,t+1);
    angle+=diff;  
    if(angle>180)diff=-diff;
    if(angle<0)diff=-diff;
    ///利用angle+=diff的方法，配合if()調整diff的正負號
    display();
}

int main(int argc, char** argv)
{
    glutInit( &argc, argv );
    glutInitDisplayMode( GLUT_DOUBLE | GLUT_DEPTH );
    glutCreateWindow("08160554");
    glutDisplayFunc(display);
    glutTimerFunc(4000,timer,0);
    glutMainLoop();
}
```

05
----
```C
#include <GL/glut.h>
int angle=0;
void drawArm1()
{
    glPushMatrix();
            glScalef(1,0.5,0.5);
            glColor3f(1,0,0);   ///左手是紅色
            glutSolidCube(0.3);
    glPopMatrix();
}
void display()
{
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);

    glPushMatrix();
        glColor3f(1,1,1);
        glutSolidCube(0.4);
        glPushMatrix();
            glTranslatef(-0.2,+0.2,0);  ///掛到右上角
            glRotatef(angle,0,0,1);  ///轉動
            glTranslatef(-0.15,0,0); 
            ///把旋轉中心的關節軸，放在正中心
            drawArm1();
        glPopMatrix();

    glPopMatrix();
    glutSwapBuffers();
}
int diff=2;
void timer(int t)
{
    glutTimerFunc(30,timer,t+1);
    angle+=diff;
    if(angle>90||angle<0)diff=-diff;
    display();
}

int main(int argc, char** argv)
{
    glutInit( &argc, argv );
    glutInitDisplayMode( GLUT_DOUBLE | GLUT_DEPTH );
    glutCreateWindow("08160554");
    glutDisplayFunc(display);
    glutTimerFunc(0,timer,0);
    glutMainLoop();
}
```
