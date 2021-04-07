# Day14. 미로찾기-4

```c
// main.c
#include "header.h"

int main(void)
{
    int row = 2, col = 1;
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
        MoveMaze(&row, &col);
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
void MoveMaze(int* row, int* col);
int IsBlock(int i, int j);
int IsFinish(int i, int j);

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

void MoveMaze(int* row, int* col)
{
    int nkey;


    if (_kbhit())
    {
        nkey = _getch();

        if (nkey == 224)
        {
            nkey = _getch();
            switch (nkey)
            {
            case UP:
                if (!(IsBlock(*row - 1, *col)))
                {
                    maze[*row][*col] = '0';
                    maze[*row - 1][*col] = 'x';
                    *row -= 1;
                }
                else if (IsFinish(*row - 1, *col))
                {
                    exit(0);
                }
                break;

            case DOWN:
                if (!(IsBlock(*row + 1, *col)))
                {
                    maze[*row][*col] = '0';
                    maze[*row + 1][*col] = 'x';
                    *row += 1;
                }
                else if (IsFinish(*row + 1, *col))
                {
                    exit(0);
                }
                break;

            case LEFT:
                if (!(IsBlock(*row, *col - 1)))
                {
                    maze[*row][*col] = '0';
                    maze[*row][*col - 1] = 'x';
                    *col -= 1;
                }
                else if (IsFinish(*row, *col - 1))
                {
                    exit(0);
                }
                break;

            case RIGHT:
                if (!(IsBlock(*row, *col + 1)))
                {
                    maze[*row][*col] = '0';
                    maze[*row][*col + 1] = 'x';
                    *col += 1;
                }
                else if (IsFinish(*row, *col + 1))
                {
                    exit(0);
                }
                break;
            }
        }
    }
}

//주어진 좌표가 막힌 곳, 혹은 도착지인지(1리턴 그 외는 0리턴) 판정하는 함수
int IsBlock(int i, int j)
{

    if (maze[i][j] == '1' || maze[i][j] == 'y')
        return 1;
    else
        return 0;
}

//도착지라면 1리턴 그 이외엔 0리턴
int IsFinish(int i, int j)
{

    if (maze[i][j] == 'y')
        return 1;
    else
        return 0;
}
```

## ✅ **오늘의 문제 :  선에 닿으면 게임이 끝나는 프로그램 만들기**

**일정 위치에 선을 긋고 그 선에 닿으면 게임이 종료되는 프로그램을 만들어보세요**

```c
//header.c
int x = 0, y = 0;
int flag = 0;
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
                if (IsBlockFinish(x,y)==2) y--;
                break;

            case DOWN:
                if (IsBlockFinish(x, y) == 2) y++;
                break;

            case LEFT:
                if (IsBlockFinish(x, y) == 2) x--;
                break;

            case RIGHT:
                if (IsBlockFinish(x, y) == 2) x++;
                break;
            }
        }
        if (IsBlockFinish(x, y) == 1) {
            system("cls");
            flag = 1;
            return;
        }
        GotoXY(x, y);
        printf("0");
    }
}

//주어진 좌표가 막힌 곳(0),도착지(1),아무것도 아님(2)
int IsBlockFinish(int i, int j)
{
    if (i < 0 || j < 0) return 0;
    else if (maze[j][i] == '|') return 1;
    else return 2;
}

// main.c
#include "header.h"

int main(void)
{
    int where;
    scanf("%d",&where);
    system("cls");
    PrintMazeGame(where);
    extern int x, y, flag;
    CursorView(0);
    while (1)
    {
        MoveMaze();
        if (flag == 1) break;
        else continue;
    }
    return 0;
}
```

