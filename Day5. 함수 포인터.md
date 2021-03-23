# Day5. 함수 포인터

## 함수 포인터

함수를 가리킬 수 있는 포인터

**1. 반환값과 매개변수가 없는 함수**

```c
void (*함수 포인터 이름)();

//예시
#include <stdio.h>

void hello()
{
    printf("Hello, world!\n");
}

void from()
{
    printf("I'm from Korea.\n");
}

int main()
{
    void (*fptr)();

    fptr = hello;
    fptr();

    fptr = from;
    fptr();

    return 0;
}

/*
Hello, world!
I'm from Korea.
*/
```

**2. 반환값과 매개변수가 있는 함수**

```c
반환자료형 (*함수포인터이름)(매개변수자료형1, 매개변수자료형2,...);


//예시
#include <stdio.h>

int sum(int a, int b)
{
    return a + b;
}

int sub(int a, int b)
{
    return a - b ;
}
int main()
{
    int (*fptr)(int, int);

    fptr = sum;
    printf("%d\n", fptr(20, 10));

    fptr = sub;
    printf("%d\n", fptr(20, 10));

    return 0;
}

/*
30
10
*/
```

## 함수 포인터 사용 이유

=>코드의 간결성

```c
//1. switch-case문
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

void zero()
{
    printf("0 입니다.");
}
void one()
{
    printf("1 입니다.");
}
void two()
{
    printf("2 입니다.");
}
void three()
{
    printf("3 입니다.");
}

int main(void) {
    int sel;
    printf(" 0 ~ 3중에 골라주세요. \n");
    scanf("%d", &sel);
    switch (sel)
    {
    case 0:
        zero();
        break;
    case 1:
        one();
        break;
    case 2:
        two();
        break;
    case 3:
        three();
        break;
    }

    return 0;
}

//2. 함수 포인터
int main(void) {
    int sel;
    printf(" 0 ~ 3중에 골라주세요. \n");
    scanf("%d", &sel);

    void (*fptr[4])() = { zero, one, two, three };
    fptr[sel]();


    return 0;
}
```

위와 아래의 코드는 같은 내용

## ✅ **오늘의 문제 : 사칙연산 계산기 만들기**

**함수 포인터를 활용해서 사칙연산 계산기를 만들어 보세요.**

- 두 수를 먼저 입력받습니다.
- 연산할 기호를 입력받습니다.
- 해당 기호에 맞는 연산을 실시합니다.

```c
#include<stdio.h>

int calculation(int a, int b, char cal) {
	if (cal=='+'){
		return a + b;
	}
	else if (cal == '-') {
		return a - b;
	}
	else if (cal == '*') {
		return a * b;
	}
	else if (cal == '/') {
		return a / b;
	}
}

int main(void) {
	int a, b;
	char what;
	int (*fp)(int, int, char);

	printf("연산 종류 (+, -, *, /) : ");
	scanf("%c", &what);
	printf("a : ");
	scanf("%d", &a);
	printf("b : ");
	scanf("%d", &b);

	fp = calculation;
	printf("a %c b = %d", what, fp(a, b, what));

	return 0;
}
```

