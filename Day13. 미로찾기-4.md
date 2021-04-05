# Day13. 미로찾기-4

```c
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
        MoveMaze();
    }
}
// header.h
#ifndef HEADER
#define HEADER

#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <string.h>
#include <Windows.h>
#include <conio.h>

#define SIZE 19
#define XP 40
#define YP 5
#define LEFT 75
#define RIGHT 77
#define UP 72
#define DOWN 80
#define ARROW 224

void LoadMaze(char num);
void GotoXY(int x, int y);
void PrintMazeGame();
void CursorView(char show);
void MoveMaze();

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

void MoveMaze()
{
    int nkey;

    if (_kbhit())
    {
        nkey = _getch();

        if (nkey == ARROW)
        {
            nkey = _getch();
            switch (nkey)
            {
            case UP:
                printf("위 ");
                break;

            case DOWN:
                printf("아래 ");
                break;

            case LEFT:
                printf("왼쪽 ");
                break;

            case RIGHT:
                printf("오른쪽 ");
                break;
            }
        }

    }

}
```

## ✅ **오늘의 문제 :  방향키를 통해 움직이는 0 만들어보기**

**오늘 학습하신 내용을 바탕으로 방향키를 통해 움직이는 0 을 만들어보세요!**

- 화면 깜빡임은 무시하셔도 좋습니다.

```c
//header.c
int x = 10, y = 10;
void MoveMaze()
{
    int nkey;
    static x, y;
    if (_kbhit())
    {
        nkey = _getch();
        GotoXY(x, y);
        printf("  ");
        if (nkey == ARROW)
        {
            nkey = _getch();
            switch (nkey)
            {
            case UP:
                y=y - 1;
                break;

            case DOWN:
                y= y + 1;
                break;

            case LEFT:
                x=x -2;
                break;

            case RIGHT:
                x=x + 2;
                break;
            }
        }
        GotoXY(x, y);
        printf("ㅁ");
    }

}
// main.c
#include "header.h"

int main(void)
{
    extern int x, y;
    CursorView(0);
    while (1)
    {
        MoveMaze();
    }
}
```

