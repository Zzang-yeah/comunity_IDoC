# Day4. 2차원 배열+이중 포인터

2차원 배열의 경우 "가로 크기"를 지정한 포인터에만 할당 가능

## ✅ **오늘의 문제 : 행렬 곱 구하기**

**3X3 행렬 2개를 선언하고, 값을 입력받은 뒤 두 행렬의 곱을 구해보세요.**

```c
#include<stdio.h>

int main(void) {
	int A[3][3];
	int B[3][3];
	int i, j;

	printf("[행렬 A]\n");
	for (i = 0; i < 3; i++) {
		for (j = 0; j < 3; j++) {
			scanf("%d", &A[i][j]);
		}
	}
	printf("[행렬 B]\n");
	for (i = 0; i < 3; i++) {
		for (j = 0; j < 3; j++) {
			scanf("%d", &B[i][j]);
		}
	}
	
	printf("[행렬 A]\n");
	for (i = 0; i < 3; i++) {
		for (j = 0; j < 3; j++) {
			printf("%4d", A[i][j]);
		}
		printf("\n");
	}
	printf("[행렬 B]\n");
	for (i = 0; i < 3; i++) {
		for (j = 0; j < 3; j++) {
			printf("%4d", B[i][j]);
		}
		printf("\n");
	}

	printf("[행렬 곱]\n");
	for (i = 0; i < 3; i++) {
		for (j = 0; j < 3; j++) {
			printf("%4d", A[i][0] * B[0][j] + A[i][1] * B[1][j] + A[i][2] * B[2][j]);
		}
		printf("\n");
	}

	return 0;
}
```

