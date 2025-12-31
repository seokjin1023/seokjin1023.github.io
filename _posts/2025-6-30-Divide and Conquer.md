---
title: Divide and Conquer
date: 2025-6-30 9:00:00 +0900
categories: [소프트웨어, 알고리즘]
tags: [Binary Search, Merge Sort, Quick Sort]
math: true
description: Divide and Conquer의 원리 및 특징, 예시들을 통한 design 및 analysis
---

# Divide and Conquer

## Divide and Conquer

### 기본 Step

Step 1: Divide into ≥ 2 smaller problems(instances)

Step 2: Solve each instance(conquer)

Step 3: Combine the subsolutions(Optional)

Optional이라는 것은 Search 등에서는 필요가 없기 때문이다.

### **Question**

1. 어떻게 Subsolution을 해결할 수 있을까?
2. subsolution을 위한 detailed design이 없다.

위의 2개는 같은 질문이며 Divide and Conquer의 핵심 원리와 겹쳐서 의미가 없다.

이유: Subsolution 해결법은 Conquer 과정에 포함되는 개념이다.

# 1. Binary-Search design and analysis

### Search에서 Step2의 Solve 방법

1. **recursively : 다시 D&C를 통해 계속 나눠 주는 것**
    
    concise, natural, clear, 기계적 해법
    
    recursion depth(in binary search): $\log_2 n+ 1$
    
2. **iterationaly, sequentially : subproblem이 충분히 작아졌을 때 사용**
    
    faster → recursive는 함수 호출마다 process context를 저장하고 복원하는 overhead가 발생함.
    
    save memory space → recursive는 stack에 새로운 함수 호출 기록을 계속 쌓음.
    

### Design

S = {10, 12, 13, 14, 18, 20, 25, 27, 30, 35, 40} 의 sorted array가 주어졌다고 하자.

Problem : Find x, locate x in S

**D&C_Search(binary_Search)**

```python
if x == S[mid] return mid
Step 1: Divide S into 2 subarrays
	if x < S[mid] return left array
	else          return right array
Step 2: Conquer(Solve) the chosen array
Step 3: Combine(Obtain) the solutions => Search에서 필요하지 않다.
```

**Step 2: Detailed ver. recursive**

```python
D&C_Search(S, x, low, high):
	if low > high:
		return nil;
	else:
		mid = (low + high) / 2
		if x == S[mid]:
			return mid
		else if x < S[mid]:
			return D&C_Search(S, x, low, mid - 1)
		else:
			return D&C_Search(S, x, mid + 1, high)
```

### Implementation

Let x = 18

10 12 13 14 18 20 25 27 30 35 40

-> S[mid] = 20

10 12 13 14 18

-> S[mid] = 13

14 18

-> S[mid] = 14

S[mid] = 18 ⇒ True

### Analysis

Best-Case: O(1)

Worst-Case: O($\log_2 n$)

⇒ Mathematical analysis is required

핵심: basic Operation(무조건 수행해야하는 연산)의 개수

$$
\begin{aligned}
    T(n) &= Divide + Conquer + Combine \\
         &= 1 + T(n/2) + 0 \\
         &= 1 + T(n/2) \\
         &= 1 + 1 + T(n/4) \\
         &= T(n/2^k) + k \\
    \text{Let} \quad & n = 2^k \text{(n은 매우 큰수이다)} \\  
    T(n) &= T(n/n) + \log n \\
         &= T(1) + \log n \\
         &= 1 + \log n \leq O(\log n)
\end{aligned}
$$

# 2. Merge-Sort design and analysis

### 교수님의 Quiz

1. k-way merge sort에서  k개의 subarray로 나눌 때 Optimal(최적)의 k가 존재할까?
    
    일단.. chatgpt는 3, 4가 최적이라고 함. → 상황에 따라 다르지 않을까 싶은데
    
2. 2-way merge sort가 3-way merge sort보다 좋을까? 10-way merge sort보다 나쁠까?

⇒ 1, 2번 둘 다 이론 상 동일하지만 세부적인 부분에서 차이가 날수도

k-way merge Sort의 경우

이론적으로 모두 $O(N\log_k N)$이기 때문에 k가 커질수록 조금씩 작아지긴한다.

하지만

1. 실제 실행 속도의 경우 Combine 과정에서의 연산 등을 계산하면 유의미한 차이가 날수도..?
    
    ⇒ k-way일 경우 우선순위 큐에서 $\log k$만큼의 시간을 사용하게 됨.
    
2. k가 너무 클 경우 cache miss가 난다고 한다..

결론: k가 커질 수록

1. 재귀 깊이($\log_k N$)가 작아진다.
2. Merge 비용이 증가한다. ($\log k$)
3. 캐시 효율성이 저하된다.

$$
\begin{aligned}T(N) &= \text{Divide} + \text{Conquer} + \text{Combine} \\     &= kT\left(\frac{N}{k}\right) + (N-1) \\     &\leq kT\left(\frac{N}{k}\right) + N \\     &= k \cdot \left( kT\left(\frac{N}{k^2}\right) + \frac{N}{k} \right) + N \\     &= k^2T\left(\frac{N}{k^2}\right) + 2N \\     &= k^3T\left(\frac{N}{k^3}\right) + 3N \\     &= k^\alpha T\left(\frac{N}{k^\alpha}\right) + k \times N \quad \text{(where } N = k^\alpha \text{)} \\     &= N T(1) + N \log_k N \\     &= N \cdot 0 + N \log_k N \\     &= N \log_k N \\     &\Rightarrow O(N \log_k N)\end{aligned}
$$

### Design

```python
D&C_Sort(orginal array)
Step 1: Divide into >= 2 subarrays
Step 2: Solve(Conquer) each subarrays => sort left and right
Step 3: Combine the subsolutions => merge left, right array
```

### example and Implementation

Let. S = { 27, 10, 12, 20, 25, 13, 15, 22 }, n = 8

```python
Step 1: Divide => {27, 10, 12, 20} / {25, 13, 15, 22}
Step 2: Solve(Conquer) => {10, 12, 20, 27 } / {13, 15, 22, 25}
	위의 Step 2에서 어떤 방식으로 정렬하는지에는 초점을 두지 않는다.
Step 3: Combine(merge) => {10, 12, 13, 15, 20, 22, 25, 27}
```

```python
def D&C_Sort(array S):
	//Step 1: Divide
	leftArray = S[1 ~ mid]
	rightArray = s[mid + 1 ~ n]
	//Step 2: Conquer
	if divided Array is big
	D&C_Sort(leftArray)
	D&C_Sort(rightArray)
	//Step 3: Combine
	Combine(leftArray, rightArray)

//위의 D&C_Sort에서 개발자의 코딩스타일에 따라 termination condition은 달라질 수 있다.
//D&C는 natural, top-down방식이고 systematic하다.
```

### Analysis

직관적으로 n개의 element가 $\log n$의 깊이로 반복되므로 $n\log n$

**체계적으로 유도해보자.**

아래의 식에서

1. Divide는 필수적이지 않으므로 basic opertaion이 아니라 0이므로 생략되었음.
    
    이유: 위의 Implementation에서 leftArray를 만드는 대신 Step2에 그대로 가져다 넣어도 됨.
    
2. Combine이 (N - 1)
    
    이유: leftArray와 rightArray를 비교해서 merge하는데 left와 right를 비교하면서 넣을 때 마지막 element는 비교하지 않고 그대로 넣기 때문에 n - 1번 비교하므로 n -1이 됨.
    
3. $N = 2^k$의 경우 수학적 trick을 이용해서 N이 충분히 큰 수임을 이용한 것임.
4. T(1) = 0
    
    이유: T(1)이라는 것은 1을 Sort하는데 드는 Time Complexity ⇒ Sort할 필요 X ⇒ 0
    

$$
\begin{aligned}T(N) &= \text{Divide} + \text{Conquer} + \text{Combine} \\     &= 2T\left(\frac{N}{2}\right) + (N-1) \\     &\leq 2T\left(\frac{N}{2}\right) + N \\     &= 2 \cdot \left( 2T\left(\frac{N}{4}\right) + \frac{N}{2} \right) + N \\     &= 4T\left(\frac{N}{4}\right) + 2N \\     &= 8T\left(\frac{N}{8}\right) + 3N \\     &= 2^k T\left(\frac{N}{2^k}\right) + k \times N \quad \text{(where } N = 2^k\text{)} \\     &= N T(1) + N \log N \\     &= N \cdot 0 + N \log N \\     &= N \log N \\     &\Rightarrow O(N \log N)\end{aligned}
$$

# 3. Quick-Sort Design and analysis

## Design

Quick-Sort는 Combine 과정 없이 D&C를 통해서 Sort를 하는 과정이다.

Combine을 하지 않는다는 것은 Divide 과정에서 더 많은 고민을 해야한다는 것을 의미한다.

```python
def QuickSort():
	Step 1: 특정 pivot을 잡고 그 값을 기준으로 작은 것은 left 큰 것은 right array로 구분
	Step 2: Solve each subproblems
```

## Example

### Example

```python
//Divide를 하는 방법에는 여러 가지가 존재하지만 그 중 유명한 것 중 하나로 partitioning
//i = for문을 통해서 pivot(첫 값)을 제외한 모든 index를 순회함.
//j = pivot과 가까운 곳으로 i를 돌다가 이동시킴.
S = { 15, 22, 13, 27, 12, 10, 20, 25}
 15   22  13  27  12  10  20  25
pivot  i
 15   22   13  27  12  10  20  25
pivot j <=> i
 15   13   22  27  12  10  20  25
pivot j         i
 15   13   22  27  12  10  20  25
pivot      j  <=>   i //작은 값을 찾을 때 j가 한 칸 뒤로 이동해서 i와 교환됨.
 15   13   12  27  22  10  20  25
pivot      j            i
 15   13   12  27  22  10  20  25
pivot           j  <=>  i
 15   13   12  10  22  27  20  25
pivot           j           i
 15   13   12  10  22  27  20  25
pivot           j               i
 15   13   12  10  22  27  20  25
pivot    <=>   j                i 
//다 끝나면 pivot과 j를 교환 => left와 right를 pivot을 기준으로 나눌 수 있음
 10   13   12  15  22  27  20  25
 이런 과정이 Divide 과정임.
```

## Analysis

### Best Time Complexity

$$
\begin{aligned}
T(n) &= \text{Divide} + \text{Conquer} + \text{Combine} \\
     &= ? + ? + 0 \\
     &= (N - 1) + T(N/2) + T(N/2) + 0 \\
     &= (N - 1) + 2T(N/2) \\
     &\leq 2T(N/2) + N \text{(Merge-Sort와 동일한 수식)} \\
     &= O(N \log N)
\end{aligned}
$$

### Worst Time Complexity

$$
\begin{aligned}T(n) &= \text{Divide} + \text{Conquer} + \text{Combine} \\     &= (N - 1) + T(\text{left}) + T(\text{right}) + 0 \\     &= (N - 1) + T(N - 1) + T(1) \\     &= T(N - 1) + N - 1 \\     &= T(N - 2) + (N - 2) + (N - 1) \\     &= T(N - 3) + (N - 3) + (N - 2) + (N - 1) \\     &= T(1) + 1 + 2 + \dots + (N - 2) + (N - 1) \\     &= 0 + 1 + 2 + \dots + (N - 1) \\     &= \frac{N (N - 1)}{2} = \frac{1}{2} N^2 - \frac{1}{2} N = O(N^2)\end{aligned}
$$