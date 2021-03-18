# Day1. 구조체

## 변수들의 집합, 구조체

```c
//구조체 정의하는 방법
//1.struct키워드
struct 구조체이름 변수이름 = {변수값1, 변수값2,...};

//사용법
struct 구조체이름 변수이름;
변수이름.멤버변수이름1=변수값1;
변수이름.멤버변수이름2=변수값2;
...
    
#include <stdio.h>

struct Person
{
    char name[10];
    char id[20];
    int age;
};

int main(void)
{
    struct Person person;
    printf("이름: ");
    scanf("%s", person.name); //홍길동
    printf("학번: ");
    scanf("%s", person.id);   //201511156
    printf("나이: ");
    scanf("%d", &person.age); //25
    printf("%s씨는 %d세 이고, 학번은 %s 입니다.", person.name, person.age, person.id);
    return 0;
}
```

```c
//2.typedef
typedef struct 구조체이름{
    자료형 멤버변수이름1;
    자료형 멤버변수이름2;
    ...
}구조체별칭;

//사용법
구조체별칭 변수이름 ={변수값1, 변수값2,...};

#define _CRT_SECURE_NO_WARNINGS    
#include <stdio.h>

typedef struct _Person
{
    char name[10];
    char id[20];
    int age;
} Person ;

int main(void)
{
    Person person;
    printf("이름: ");
    scanf("%s", person.name); //홍길동
    printf("학번: ");
    scanf("%s", person.id);   //201511156
    printf("나이: ");
    scanf("%d", &person.age); //25
    printf("%s씨는 %d세 이고, 학번은 %s 입니다.", person.name, person.age, person.id);
    return 0;
}
```

✅ **오늘의 문제 : 학생 정보 입력 받기**

사용자로부터 학생의 이름, 나이, 학년, 수학, 영어, 국어 점수를 입력 받고 이를 평균과 함께 출력하는 프로그램을 작성하세요.

```c
#include<stdio.h>
#include<string.h>

typedef struct student {
	char name[10];
	int age;
	int grade;
	int math;
	int english;
	int korean;
} Student;

int main(void) {
	Student a;
	printf("이름 : ");
	scanf("%s", &a.name);
	printf("나이 : ");
	scanf("%d", &a.age);
	printf("학년 : ");
	scanf("%d", &a.grade);
	printf("수학 : ");
	scanf("%d", &a.math);
	printf("영어 : ");
	scanf("%d", &a.english);
	printf("국어 : ");
	scanf("%d", &a.korean);

	printf("[학생]\n");
	printf("이름 : %s\n", a.name);
	printf("나이 : %d\n", a.age);
	printf("학년 : %d\n", a.grade);
	printf("수학 : %d\n", a.math);
	printf("영어 : %d\n", a.english);
	printf("국어 : %d\n", a.korean);
	printf("평균 점수 : %d", (a.math + a.english + a.korean) / 3);


	return 0;
}
```

