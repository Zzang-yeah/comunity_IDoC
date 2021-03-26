# Day6. 동적 메모리 할당

## 메모리

1. 코드 영역 : 실행할 프로그램의 코드가 저장되는 메모리 공간
2. 데이터 영역 : 전역 변수와 static 변수가 할당되는 영역, 프로그램 시작과 동시에 메모리 할당, 프로그램 종료시까지 남아있음
3. 스택 영역 : 지역변수와 매개 변수가 할당되는 영역, 함수를 벗어나면 소멸
4. 힙 영역 : 동적 할당된 메모리들이 존재하는 공간

## 메모리 할당하는 방법

### 1.정적 메모리 할당

변수 선언을 통해 필요한 메모리를 확보하는 방법, 컴파일 단계에서 메모리 공간을 할당받는 것

장점 : 메모리 누수를 걱정하지 않아도 됨

단점 : 메모리 공간의 크기가 정해져 있어서 추가불가능, 메모리 낭비 발생

### 2. 동적 메모리 할당

실행 단계에서 메모리 공간을 할당

포인터를 사용해서 직접 힙 영역을 가리켜 공간을 빌리는 것

장점 : 메모리 낭비 방지

단점 : 메모리 누수를 free를 통해 방지해야함

```c
#include <stdlib.h>
//동적할당 -> 값들이 쓰레기 값으로 초기화
void *malloc(size_t size);

//동적할당 _> 값들이 0으로 초기화
void* calloc ( size_t n, size_t byte );

//이미 할당된 공간의 크기를 바꿀 때
void* realloc(void* mem, size_t size);
```

## ✅ **오늘의 문제 : 점수의 평균 구하기**

**학생의 수를 입력받은 뒤, 그 수만큼 학생의 점수를 입력받아 평균을 구하는 프로그램을 작성해보세요.**

```c
#include<stdio.h>
#include<stdlib.h>

int main(void) {
	int n;
	int* student;
	int i;
	int result = 0;

	printf("학생의 수 : ");
	scanf("%d", &n);
	student = malloc(sizeof(int) * n);
	for (i = 0; i < 10; i++) {
		printf("학생%d : ", i + 1);
		scanf("%d", &student[i]);
	}
	for (i = 0; i < 10; i++) {
		result += student[i];
	}
	
	(int)result /= n;
	printf("평균 : %d", result);

	free(student);

	return 0;
}
```

