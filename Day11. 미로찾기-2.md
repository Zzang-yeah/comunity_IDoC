# Day11. 미로찾기-2

## 미로 생성

```c
#include <stdio.h>
#define SIZE 19

int main(void) 
{
	char maxe[SIZE][SIZE];
}
```

## 미로 내부 구성

텍스트 파일 다운로드

```c
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <string.h>

void LoadMaze(char num)
{
char path[20] = "./Maze";
    strcat(path, &num);
    strcat(path, ".txt");

    char str_tmp[50] = { 0, };
    FILE* f = fopen(&path, "r");

    for (int i = 0; i < SIZE; i++)
    {
        fgets(str_tmp, 50, f);
        char* ptr = strtok(str_tmp, "\t");
        for (int j = 0; j < SIZE; j++)
        {
            maze[i][j] = *ptr;
            ptr = strtok(NULL, "\t");
        }
    }
    fclose(f);
}
```

## ✅ **오늘의 문제 :  복습하기**

복습이 중요한 만큼 오늘의 실습을 복습해서 소스코드와 실행결과를 캡처해서 올려주세요!

```c
// header.h
#ifndef HEADER
#define HEADER

#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <string.h>
#include <Windows.h>
#define SIZE 19


void LoadMaze(char num);
void GotoXY(int x, int y);
char maze[SIZE][SIZE];

#endif

//header.c
#include "header.h"


void LoadMaze(char num)
{
    char path[20] = "./Maze";
    strcat(path, &num);
    strcat(path, ".txt");

    char str_tmp[50] = { 0, };
    FILE* f = fopen(&path, "r");

    for (int i = 0; i < SIZE; i++)
    {
        fgets(str_tmp, 50, f);
        char* ptr = strtok(str_tmp, "\t");
        for (int j = 0; j < SIZE; j++)
        {
            maze[i][j] = *ptr;
            ptr = strtok(NULL, "\t");
        }
    }
    fclose(f);
}

void GotoXY(int x, int y)
{
    COORD Pos;
    Pos.X = x;
    Pos.Y = y;
    SetConsoleCursorPosition(GetStdHandle(STD_OUTPUT_HANDLE), Pos);
}

//main.c
#include "header.h"

int main(void)
{
    char level;
    printf("난이도를 선택하세요. (1, 2, 3) ");
    scanf("%c", &level);
    LoadMaze(level);

    for (int i = 0; i < SIZE; i++)
    {
        for (int j = 0; j < SIZE; j++)
        {
            printf("%c", maze[i][j]);
        }
        printf("\n");
    }
}
```

