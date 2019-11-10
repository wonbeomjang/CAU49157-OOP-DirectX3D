# Project#3 : OOP for Billiard Game  

## Student Infromation  
*Name*        : Wonbeom Jang 장원범  
*Student ID*  : 20182592  
*Depertment*  : School of Computer Science and Engineering  

## System Encironment
OS          : Window10
IDE         : Visual Studio 2019
compliter   : MSC 18.0.21005.1

## How to run
1. double click click BilliardBoardGame.exe  
2. Move blue with left cursor drag  
3. shoot the ball with space bar  

The white ball takes first, then the yellow ball takes its turn.

## What I modified
#### Implement following function
virtualLego.cpp  
```c++
boolean CSphere::asIntersected(CSphere& ball)
void CSphere::hitBy(CSphere& ball) 

boolean CWall::asIntersected(CSphere& ball)  
void CWall::hitBy(CSphere& ball) 
```

#### Add the factor of controll the FPS of the game
d3dUtility.h  
```c++
#define SPEEDUPFACT 10
```

virtualLego.cpp  
```c++
void CShpare::ballUpdate(float timeDiff) {
    ...
	double rate = 1 -  (1 - DECREASE_RATE)*timeDiff * 400 * SPEEDUPFACT;
    ...
}
LRESULT CALLBACK d3d::WndProc(HWND hwnd, UINT msg, WPARAM wParam, LPARAM lParam) {
    ...
    g_sphere[2 + tern].setPower(distance * cos(theta) * SPEEDUPFACT, distance * sin(theta) * SPEEDUPFACT);
    ...
}
```
d3dUtility.cpp  
```c++
int d3d::EnterMsgLoop( bool (*ptr_display)(float timeDelta) ) {
    double timeDelta = (currTime - lastTime)*0.0007/SPEEDUPFACT;
}
```

#### Modified function
virtualLego.cpp  
```c++
LRESULT CALLBACK d3d::WndProc(HWND hwnd, UINT msg, WPARAM wParam, LPARAM lParam)  

...
static tern = 1;
...
D3DXVECTOR3	whitepos = g_sphere[2 + tern].getCenter();
...

g_sphere[2 + tern].setPower(distance * cos(theta) * SPEEDUPFACT, distance * sin(theta) * SPEEDUPFACT); // edit
tern++;
tern %= 2;
```
