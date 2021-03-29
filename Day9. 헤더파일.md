# Day9. 헤더파일

## 헤더파일

c파일로 만들어진 오브젝트 파일에 있는 함수들의 내용을 다른 소스 파일에서 사용할 수 있도록 하기 위해

선언부들을 모아둔 파일

```c
// header.h
#ifndef HEADER

#define HEADER
#include <stdio.h>

struct Score 
{
    int kor;
    int eng;
    int math;
};

void PrintStruct(struct Score person);

#endif
```

```c
// main.c
#include "header.h"
#include "header.h"

int main(void) {
    struct Score p;

    p.kor = 30;
    p.eng = 100;
    p.math = 100;

    PrintStruct(p);

    return 0;
}

// 실행결과
국어: 30
영어 100
수학 100
```

## ✅ **오늘의 문제 : 사칙연산이 가능한 함수 (더하기, 빼기, 곱하기, 나누기) 가 정의되어 있는 "calc.h" 헤더파일을 만들어서 사용해 보세요**

```c
#include<stdio.h>

void p(int a, int b) {
	printf("%d + %d = %d\n", a, b, a + b);
}

void s(int a, int b) {
	printf("%d - %d = %d\n", a, b, a - b);
}

void m(int a, int b) {
	printf("%d * %d = %d\n", a, b, a * b);
}

void d(int a, int b) {
	printf("%d / %d = %d\n", a, b, a / b);
}
```

```c
#include<stdio.h>
#include "calc.h"

int main(void) {
	int a, b;
	scanf("%d", &a);
	scanf("%d", &b);

	p(a, b);
	s(a, b);
	m(a, b);
	d(a, b);

	return 0;
}
```

