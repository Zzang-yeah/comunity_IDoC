# Day8. 문자열 함수

## 버퍼

**버퍼** : 임시 메모리 공간

- 버퍼를 사용하지 않는 경우 : 키 입력시 프로그램에 바로 전달
- 버퍼를 사용하는 경우 : 키 입력을 버퍼에 전달 및 저장 후 개행문자가 들어오거나, 버퍼가 가득차면 버퍼를 프로그램에 전달

## 문자열 함수

```c
#include<stdio.h>
#include<string.h>

//stdio.h헤더파일
//표준 입력 스트림의 버퍼에서 문자열을 읽는 함수
//성공시 입력된 문자열을 반환, 실패하면 NULL반환
char *gets_s(char* _Buffer, rsize_t _Size);

//표준 출력에 문자열을 쓰는 함수
//성공시 음수가 아닌 값을 반환, 실패하면 -1 반환
int puts(char const *_Buffer);

//string.h헤더파일
//문자열의 길이 리턴
strlen(문자열 포인터/문자 배열);

//문자열을 다른 배열이나 포인터로 복사
strcpy(대상 문자열, 원본 문자열);

//문자열을 붙이는 함수
strcat(대상 문자열, 붙일 문자열);

//문자열 비교
/*
-1: 문자열 2가 클 때
0 : 문자열이 같을 때
1 : 문자열 1이 클 때
*/
strcmp(문자열1, 문자열2);

```

## ✅ **오늘의 문제 : 문자열 길이 비교 후 출력하기**

**두 개의 문자열을 입력 받은 후, 두 문자열 중 긴 문자열의 길이를 출력하세요.**

- 두 문자열의 길이가 같으면, 두 문자열을 하나의 문자열로 합쳐서 출력하세요.
- 공백도 문자열의 길이에 포함해주세요.

```c
#include<stdio.h>
#include<string.h>

int main(void) {
	char a[50], b[50];
	scanf("%[^\n]s", a);
	getchar();
	scanf("%[^\n]s", b);

	if (strlen(a) >= strlen(b)) {
		printf("%d", strlen(a));
	}
	else {
		printf("%d", strlen(b));
	}

	return 0;
}
```

