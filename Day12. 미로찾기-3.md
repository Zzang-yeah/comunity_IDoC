# Day12. 미로찾기-3

```c
// header.h
#ifndef HEADER
#define HEADER

#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <string.h>
#include <Windows.h>

#define SIZE 19
#define XP 40
#define YP 5

void LoadMaze(char num);
void GotoXY(int x, int y);
void PrintMazeGame();
void CursorView(char show);

char maze[SIZE][SIZE];

#endif
// header.c
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

void PrintMazeGame()
{

    for (int i = 0; i < SIZE; i++)
    {
        GotoXY(XP, YP + i);
        for (int j = 0; j < SIZE; j++)
        {
            if (maze[i][j] == '1')
                printf("■");
            else if (maze[i][j] == 'y')
                printf("★");
            else if (maze[i][j] == '0')
                printf("□");
            else
                printf("●");
        }
        puts("");
    }
}

void CursorView(char show)
{
    CONSOLE_CURSOR_INFO ConsoleCursor;
    ConsoleCursor.bVisible = show;
    ConsoleCursor.dwSize = 1;
    SetConsoleCursorInfo(GetStdHandle(STD_OUTPUT_HANDLE), &ConsoleCursor);
}
// main.c

#include "header.h"

int main(void)
{
    char level;
    CursorView(0);

    GotoXY(XP, YP - 3);
    printf("미로 찾기 게임\n");
    GotoXY(XP, YP - 2);
    printf("난이도를 선택하세요. (1, 2, 3) ");
    scanf("%c", &level);

    LoadMaze(level);

    while (1)
    {
        PrintMazeGame();
    }
}
```

## ✅ 오늘의 문제 :  위 아래로 움직이는 'ㅁ' 출력하기

```c
#include "header.h"

int main(void)
{
    CursorView(0);
    int i;
    while (1)
    {
        for (i = 0; i < 20; i++) {
            GotoXY(20,i);
            printf("ㅁ");
            Sleep(100);
            GotoXY(20,i);
            printf("  ");
        }
        for (i = 19; i > -1; i--) {
            GotoXY(20,i);
            printf("ㅁ");
            Sleep(100);
            GotoXY(20,i);
            printf("  ");
        }
    }
    return 0;
}
```

