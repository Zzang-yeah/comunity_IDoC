# Day10. 미로찾기-1

## 콘솔창의 출력 위치 변경

```c
//윈도우 개발자들이 필요한 모든 매크로와 함수들을 모아둔 헤더파일
#include <windows.h>

typedef struct _COORD {
	SHORT X;
	SHORT Y;
} COORD, *PCOORD;

void GotoXY(int x, int y){
    COORD Pos;
    Pos.X=x;
    Pos.Y=y;
    /*
    SetConsoleCursorPosition : 콘솔의 핸들값과 좌표값을 받아서 해당 위치로 콘솔 커서 이동
    GetStdHandle(STD_OUTPUT_HANDLE) : 콘솔 ID 리턴
    */
    SetConsoleCursorPosition(GetStdHandle(STD_OUTPUT_HANDLE), Pos);
}

```

## ✅ **오늘의 문제 :  계단 만들기**

**어떠한 양수를 입력받은 뒤, 그 양수와 같은 층의 계단을 만들어보세요**

- GotoXY 함수만을 사용하세요

```c
#include<stdio.h>
#include<Windows.h>

void GotoXY(int x, int y) {
    COORD Pos;
    Pos.X = x;
    Pos.Y = y;
    SetConsoleCursorPosition(GetStdHandle(STD_OUTPUT_HANDLE), Pos);
}

int main(void) {
	int n;
    int i;
	scanf("%d", &n);
    
    for (i = 0; i < n; i++) {
        GotoXY(i, i);
        printf("ㄱ");
    }

	return 0;
}
```

