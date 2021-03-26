# Day7. 동적 메모리 할당

## ✅ **오늘의 문제 : 소수 개수 출력하기**

**임의의 N개의 숫자를 입력받고, 그 중에서 소수인 수의 개수를 출력하는 프로그램을 만들어보세요.**

```c
#include<stdio.h>
#include<stdlib.h>
#include<stdbool.h>

int main(void) {
	int n;
	int *arr;
	int i,j;
	int result = 0;
	bool flag;

	printf("숫자의 개수 : ");
	scanf("%d", &n);
	arr = malloc(sizeof(int) * n);
	for (i = 0; i < n; i++) {
		scanf("%d", &arr[i]);
	}
	
	//소수 판별
	for (i = 0; i < n; i++) {
		flag = false;
		for (j = 2; j < arr[i]; j++) {
			//1과 자기자신 제외하고 나누어지는 수가 1개라도 있다면
			if (arr[i] % j == 0){
				flag = true;
				break;
			}
			else {
				continue;
			}
		}
		if (!flag) {
			result++;
		}
	}
	
	printf("소수의 개수는 %d입니다.", result);
	free(arr);
	return 0;
}
```

