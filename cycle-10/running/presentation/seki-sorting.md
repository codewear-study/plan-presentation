# 정렬

## 교환 정렬

### Bubble sort

![bubble sort](https://raw.githubusercontent.com/codewear-study/plan-presentation/seki/cycle-10/running/presentation/seki-resources/sort-buble.gif)
|||
|:-:|:-|
|설명|인접한 요소를 비교해서 교환함으로써 정렬하는 방법.|
|시간 복잡도|`O(n²)`|
|공간 복잡도|`O(1)`|
|특징|구현이 쉬움, in-place, adaptive|

### Comb sort

![comb sort](https://raw.githubusercontent.com/codewear-study/plan-presentation/seki/cycle-10/running/presentation/seki-resources/sort-comb.gif)
|||
|:-:|:-|
|설명|bubble sort의 느린 이동을 간격을 둠으로써 해소한 정렬 방법.|
|시간 복잡도|`O(n²)`|
|공간 복잡도|`O(1)`|
|특징|in-place, adaptive|

### Quicksort

![quicksort](https://raw.githubusercontent.com/codewear-study/plan-presentation/seki/cycle-10/running/presentation/seki-resources/sort-quick.gif)
|||
|:-:|:-|
|설명|divide and conquer의 전형. 구현이 간결하고 충분히 빠름.|
|시간 복잡도|`O(n²)`|
|공간 복잡도|`O(1)`|
|특징|빠름. in-place|

## 삽입 정렬

### Insertion sort

![insertion sort](https://raw.githubusercontent.com/codewear-study/plan-presentation/seki/cycle-10/running/presentation/seki-resources/sort-insertion.gif)
|||
|:-:|:-|
|설명|정렬된 요소들 사이의 적절한 위치에 놓음으로써 정렬하는 방법.|
|시간 복잡도|`O(n²)`|
|공간 복잡도|`O(1)`|
|특징|in-place, adaptive, stable, online|

### Shell sort

![shellsort](https://raw.githubusercontent.com/codewear-study/plan-presentation/seki/cycle-10/running/presentation/seki-resources/sort-shell.gif)
|||
|:-:|:-|
|설명|insertion sort의 느린 이동을 간격을 둠으로써 해소한 방법|
|시간 복잡도|`O(n√n)`|
|공간 복잡도|`O(1)`|
|특징|간격을 계산하는 방법에 따라서 복잡도가 달라짐, in-place|

## 선택 정렬

### Selection sort

![selection sort](https://raw.githubusercontent.com/codewear-study/plan-presentation/seki/cycle-10/running/presentation/seki-resources/sort-selection.gif)
|||
|:-:|:-|
|설명|필요한 값을 찾아 옮기는 방법. 가장 간단한 방법으로 가장 큰 값 또는 가장 작은 값을 선택한다.|
|시간 복잡도|`O(n²)`|
|공간 복잡도|`O(1)`|
|특징|in-place|

### Heap sort

![heap sort](https://raw.githubusercontent.com/codewear-study/plan-presentation/seki/cycle-10/running/presentation/seki-resources/sort-heap.gif)
|||
|:-:|:-|
|설명|selection sort에서 heap을 사용하여 값을 선택하는 시간을 줄임. heap이 배열에 구현이 가능하다는 것을 이용함.|
|시간 복잡도|`O(nlogn)`|
|공간 복잡도|`O(1)`|
|특징|in-place, heapify 오버헤드가 있음|

## 비교하지 않는 정렬 (분포 정렬)

### Counting sort

![counting sort](https://raw.githubusercontent.com/codewear-study/plan-presentation/seki/cycle-10/running/presentation/seki-resources/sort-counting.gif)
|||
|:-:|:-|
|설명|존재할 수 있는 모든 key에 대해서 개수를 세어 정렬하는 방법|
|시간 복잡도|`O(n)`|
|공간 복잡도|`O(k + n)`|
|특징|구현 방법에 따라서 stable|

### Radix sort

![radix sort](https://raw.githubusercontent.com/codewear-study/plan-presentation/seki/cycle-10/running/presentation/seki-resources/sort-radix.gif)
|||
|:-:|:-|
|설명|counting sort에서 key를 나누어 메모리 사용을 줄인 정렬 방법|
|시간 복잡도|`O(wn)`|
|공간 복잡도|`O(n)`|
|특징|구현 방법이 다양함, 구현 방법에 따라서 stable|

## 그 외의 정렬

### Bitonic mergesort

![bitonic mergesort](https://raw.githubusercontent.com/codewear-study/plan-presentation/seki/cycle-10/running/presentation/seki-resources/sort-bitonic-merge.gif)
|||
|:-:|:-|
|설명|정렬을 병렬로 진행할 수 있도록 고안된 정렬 방법. 순수 bitonic mergesort는 2의 제곱수만큼의 요소가 있을 때만 정렬할 수 있음.|
|시간 복잡도|`O(log²n)` 병렬 처리|
|공간 복잡도|`O(nlog²n)` 비병렬 처리|
|특징|병렬 처리 가능|

### Topology sort

구체적인 정렬이 아니라 하나의 범주이고,\
일차원 데이터를 정렬하는 방법이 아니기 때문에 정렬하는 프로그램은 만들지 않았습니다.

|||
|:-:|:-|
|설명|그래프의 노드를 일정한 순서로 나열하는 방법|
|시간 복잡도|구현에 따라 다름|
|공간 복잡도|구현에 따라 다름|
|특징|구현에 따라 다름|
