---
title: "Java Bubble 정렬"
date: 2020-05-13 14:00:00 -0900
categories: ""
---

## 1. 개요
Java8 Stream 클래스를 활용하여 Bubble 정렬을 구현. 
Bubble 정렬이란? 인접한 2개의 요소를 중첩되게 비교하여  정렬하는 방식입니다.


## 2. 처리절차
배열을 정렬하기 위해 인접한 요소를 비교하고 필요한 경우 교체하면서 배열을 반복합니다. 크기가 _n_ 인 배열의 경우 _n-1_ 개의 반복을 수행합니다.

배열을 오름차순으로 정렬하고 싶습니다.

4 2 1 6 3 5

4와 2를 비교하여 첫 번째 반복을 시작합니다.

**[2 4]** 1 6 3 5

이제 4와 1에 대해 동일하게 반복합니다.

2 **[1 4]** 6 3 5
2 1 **[4 6]** 3 5
2 1 4 **[3 6]** 5
2 1 4 3 **[5 6]**

여기까지 오면 가장 큰수가 가장 우측에 배치하게 되며, 다시 n-1 까지 비교합니다.

**[1 2]** 4 3 5 6
1 **[2 4]** 3 5 6
1 2 **[3 4 ]** 5 6
1 2 3 **[4 5]** 6

_n-1_ 반복 이 끝나면 오름차순으로 정렬 된 배열을 얻을 수 있습니다.

## 3. 구현
Java8 Stream을 사용하여 Bubble 정렬된 소스입니다.
```java
public class BubbleSort {	
	public int[] execute( int[] arr ) {
	    int n = arr.length;
	    IntStream.range(0, n - 1)
	    .flatMap(i -> IntStream.range(1, n - i) )
	    .forEach(j -> {
	        if (arr[j - 1] > arr[j]) {
	            int temp = arr[j];
	            arr[j] = arr[j - 1];
	            arr[j - 1] = temp;
	            }
	     });
	    return arr;
	} 
}
```
테스트 코드
```java
public class BubbleSortTests {	
	@Test
	public void _Test_execute() {		
		int[] array = new int[] { 3,7,8,5,4 };
		int[] sortedArray = new int[] { 3,4,5,7,8 };		
		BubbleSort bubbleSort = new BubbleSort();		
		array = bubbleSort.execute( array );	
		assertThat(array, is(sortedArray));
	}
}
```
## 4. 시간 복잡도
최악의 경우 시간복잡도(Time Complexity) 는 O(n^2)
공간복잡도는 Swap을 하기 위한 1개 따라서 O(1)
또한 알고리즘을 살펴보면 내부 루프에서 교환이 한번도 없는 경우는 이미 정렬이 되었다고 판단할 수 있습니다.
이대는 시간복잡도 O(n) 이 됩니다.

최적화된 코드(한번도 교환이 없는 경우 적용)
```java
public int[] optimizedBubbleSort(int[] arr) {
	    int i = 0, n = arr.length;
	    boolean swapNeeded = true;
	    while (i < n - 1 && swapNeeded) {
	        swapNeeded = false;
	        for (int j = 1; j < n - i; j++) {
	            if (arr[j - 1] > arr[j]) {
	                int temp = arr[j - 1];
	                arr[j - 1] = arr[j];
	                arr[j] = temp;
	                swapNeeded = true;
	            }
	            System.out.println(j);
	        }
	        i++;
	    }
	    return arr;
	}
```

## 4. 결론
- 최악의 경우 : 배열이 역순 일 때 O (n * n)
- 최선의 경우 : 배열이 이미 정렬 된 경우 O (n)

**최선의 경우를 적용하여 최적화된 버블Sort를 구현**


> 작성자 : [eyebora32](https://github.com/eyebora)
> 참조 : https://www.baeldung.com/java-bubble-sort
> Written with [StackEdit](https://stackedit.io/).
