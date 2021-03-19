# Day3. 이중 포인터

## 이중 포인터

**포인터** : 어떤 값의 주소를 가리키는 변수

**이중포인터** : 포인터를 값으로 갖는 포인터

2차원 배열에서 배열의 이름은 이중포인터

포인터의 주소를 저장할 땐 이중포인터 사용

## ✅ **오늘의 문제 : 최대값 구하기**

**이중 포인터와 크기가 5인 배열을 선언하고, 함수를 사요해서 입력된 수 중 최대값을 출력해보세요.**

- 함수는 void형입니다.
- 최대값을 저장하는 이중 포인터 변수는 main함수에 초기화해야합니다.

```c
#include<stdio.h>

void whatmax(int* arr,int** p) {
	for (int i = 1; i < 5; i++) {
		if (**p < arr[i]){
			**p = arr[i];
		}
	}
}

int main(void) {
	int arr[5];
	int* pp=arr;
	int i;

	for (i = 0; i < 5; i++) {
		scanf("%d", &arr[i]);
	}
	whatmax(arr, &pp);
	printf("최대값 : %d",*pp);
	
	return 0;
}
```

