# Day15. 미로찾기-6

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
    start = clock();
    LoadMaze(level);

    while (1)
    {
        PrintMazeGame();
        MoveMaze(&row, &col);
    }
}
//header.h
#ifndef HEADER
#define HEADER

#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <string.h>
#include <Windows.h>
#include <conio.h>
#include <time.h>

#define SIZE 19
#define XP 40
#define YP 5
#define LEFT 75
#define RIGHT 77
#define UP 72
#define DOWN 80
#define ARROW 224

clock_t start, end;
float res;

void LoadMaze(char num);
void GotoXY(int x, int y);
void PrintMazeGame();
void CursorView(char show);
void MoveMaze(int* row, int* col);
int IsBlock(int i, int j);
int IsFinish(int i, int j);
void Complete();

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
                    maze[*row][*col] = '0';
                    maze[*row - 1][*col] = 'x';
                    PrintMazeGame();
                    Complete();
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
                    maze[*row][*col] = '0';
                    maze[*row + 1][*col] = 'x';
                    PrintMazeGame();
                    Complete();
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
                    maze[*row][*col] = '0';
                    maze[*row][*col - 1] = 'x';
                    PrintMazeGame();
                    Complete();
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
                    maze[*row][*col] = '0';
                    maze[*row][*col + 1] = 'x';
                    PrintMazeGame();
                    Complete();
                    exit(0);
                }
                break;
            }
        }
    }
}

int IsBlock(int i, int j)
{
    if (maze[i][j] == '1' || maze[i][j] == 'y')
        return 1;
    else
        return 0;
}

int IsFinish(int i, int j)
{
    if (maze[i][j] == 'y')
        return 1;
    else
        return 0;
}

void Complete()
{
    end = clock();
    res = (float)(end - start) / CLOCKS_PER_SEC;

    GotoXY(XP, YP + SIZE);
    printf("Complete!\n");
    GotoXY(XP, YP + SIZE + 1);
    printf("경과시간 : %.2f초", res);
    exit(0);
}
```

