---
title: Dynamic Programming
date: 2025-6-30 11:00:00 +0900
categories: [소프트웨어, 알고리즘]
tags: [CMM, Floyd-Warshall]
math: true
description: Dynamic Programming의 원리 및 특징, 예시들을 통한 design 및 analysis
---

# Dynamic Programming

## CMM
$$
A[p\times q] * B[q\times r] = AB[p\times r]
$$

**Define**

Given a given ordered sequence of matrices, Find an optimal order for CMM

연속된 행렬을 곱할 때 행렬의 연산을 최소화 할 수 있는 값을 찾는 방법

**BF : $O(2^n)$**

### Design

**Step 0 : examples**

쉬운 subproblem(hand computation)으로 시작한다 → 통찰 가능

$A_1 \times A_2 \times A_3 \times A_4 \times A_5 \times A_6$ 의 CMM을 구한다고 하자.

$A_1 = [5\times 2] \quad A_2 = [2\times 3] \quad A_3 = [3\times 4] \\ A_4 = [4\times 6] \quad A_5 = [6\times 7] \quad A_6 = [7\times 8]$

M[i, j]에서 $A_i$부터 $A_j$까지 연산의 최솟값 = M[i, j]

**가장 쉬운 subproblem**

$A_1 \times A_1 = 0$

**다음으로 쉬운 subproblem**

$A_1 \times A_2 \quad or \quad A_2 \times A_3 … \\
A_2 \times A_3 = 2 \times 3 \times 4 = M[2, 3]$

**다음으로 쉬운 subproblem**

$A_4 \times A_5 \times A_6 = min(P, Q) = M[4,6]$

1. $P = (A_4 \times A_5) \times A_6 = 4 \times 6 \times 7 \quad + \quad4 \times 7 \times 8 = M[4,5] + 4\times 7 \times 8$ 
2. $Q = A_4 \times (A_5 \times A_6) = 6 \times 7 \times 8 \quad + \quad4 \times 6 \times 8 = 6\times 7 \times 8 + M[5,6]$ 

**이런 식의 과정을 밟아나가서 M[1,6]을 구해보자.**

$$
\begin{align*}A_1 \times (A_2 \times \cdots \times A_6) &= M[1,1] + M[2,6] + 5 \times 2 \times 8 \\(A_1 A_2)(A_3 \cdots A_6) &= M[1,2] + M[3,6] + 5 \times 3 \times 8 \\(A_1 A_2 A_3)(A_4 \cdots A_6) &= M[1,3] + M[4,6] + 5 \times 4 \times 8 \\(A_1 \cdots A_4)(A_5 A_6) &= M[1,4] + M[5,6] + 5 \times 6 \times 8 \\(A_1 \cdots A_5) A_6 &= M[1,5] + M[6,6] + 5 \times 7 \times 8\end{align*}
$$

**Step 1**

Step 0의 example을 보고 Recurrence equation을 구해보자.

$$
\begin{align*}M[1,6] &= \min \left( M[1,k] + M[k+1,6] + c(0) \times c(k) \times c(6) \right) \quad (1 \leq k \leq 5) \\M[i,j] &= \min \left( M[i,k] + M[k+1,j] + c(i-1) \times c(k) \times c(j) \right) \quad (i \leq k \leq j - 1) \\M[i,i] &= 0\end{align*}
$$

**Step 2**

```python
#해당 코드는 optimzation이 가능하다.
def DP_CMM(matrices_seq, dimension_row_col): #행렬과 각 행렬의 행, 열의 값 input
    for i in range(0, n):
        for j in range(0, n):
            for k in range(i - 1, j):
                M[i, j] = recurrence: function of subproblem(min)
```

### Analysis

$$
T(n) = \mathcal{O}(n^2) * 
\underset{\mathclap{= n(rough하게)}}{
\underset{\mathclap{= \Theta(k)}}{\text{time of subproblem}}}
\Rightarrow \mathcal{O}(n^3)
$$

## Floyd-Warshall

### Question.

1. 이 Floyd-Warshall algorithm의 경우 전체 계산을 위해서 주어진 D array 이외의 공간을 사용하지 않고도 충분히 해결할 수 있다. 그 이유는 무엇일까?
2. Shortest distance를 계산하는 이 algorithm에서 shortest path를 찾는 방법은?
    
    D(k)를 계산할 때 만약 최솟값이 k를 통과해야 한다면 그 이전 path를 기억하게 하는 방식을 통해 구함
    

### APSP(All-pair shortest path) def.

Pair (u, v)가 주어졌을 때 u부터 v까지의 최단 경로를 찾는 문제

**Model** 

Graph

**Solution Algorithm**

Design → Analysis → Best Algorithm의 방법으로 최선의 알고리즘을 찾는다.

**사용 가능한 방법**

1. Brute-force, enumeration → $O(n!)$
2. Divide & Conquer
    
    방법을 설명해주는 척하다가 우리 보고 생각해보라고 던져줌.
    
3. Dynamic Programming → $O(n^3)$

## Dynamic Programming을 통한 풀이

### Step 0: example

어떤 D0가 아래와 같이 존재한다고 가정하자.

|  →  | v1 | v2 | v3 | v4 | v5 |
| --- | --- | --- | --- | --- | --- |
| v1 | 0 | 1 | inf | 1 | 5 |
| v2 | 9 | 0 | 3 | 2 | inf |
| v3 | inf | inf | 0 | 4 | inf |
| v4 | inf | inf | 2 | 0 | 3 |
| v5 | 3 | inf | inf | inf | 0 |

D1[i, j] ⇒ i에서 j까지 가는데 1번 도시를 경유할 수 있다고 할 때의 최솟값(direct 가능)

D2[i, j] ⇒ i에서 j까지 가는데 2번 도시를 경유할 수 있다고 할 때의 최솟값(direct, 1번 경유 가능)

위와 같은 방법의 방법을 통해서 구할 수 있다.

```java
D1[5, 4] = Math.min(D0[5, 4], D0[5, 1] + D0[1,4]); // inf vs 3 + 1 = 4 => 4
D1[5, 2] = Math.min(D0[5, 2], D0[5, 1] + D0[1, 2]); // inf vs 3 + 1 = 4 => 4
D1[2, 4] = Math.min(D0[2, 4], D0[2, 1] + D0[1, 4]); // 2  vs 9 + 1 = 10 => 2
```

위와 같은 방법으로 D1을 모두 채울 수 있다.

```java
D2[5, 4] = Math.min(D1[5, 4], D1[5, 2] + D1[2, 4]); // 4 vs 4 + 2 = 6 => 4
```

D2를 구할 때 D1을 사용하는 이유는 D1이 direct와 1번을 경유한 경로 중 최솟값이기 때문이다.

즉, 이렇게 계속 계산한다면 k번을 경유할 때 k - 1번 D-array만을 사용하면 된다.

### Step1 : Recurrence Equation

$$
D(k)[i, j] = min(D(k-1)[i, j], D(k-1)[i, k] + D(k-1)[k, j])
$$

위의 방식으로 코드를 구현해보자.

```python
def floyd(graph D):
	for k in range(1 ~ last_Vertex):
		for i in range(1 ~ last_Vertex):
			for j in range(1 ~ last_Vertex):
				D(k)[i, j] = min(D(k-1)[i, j], D(k-1)[i, k] + D(k-1)[k, j])
```

### Time Complexity

$$
Let \quad N=\left| V \right|\text{(N은 Vertex의 수)} \\
\sum_{k=1}^{n} \sum_{i=1}^{n} \sum_{j=1}^{n} \Theta(1) \\
\text{Time Complexity} = O(n^3)

$$

$\theta(1)$이 계산 값인 이유는 D(k)[i, j]를 구하는데 min연산이 사용되고 이는 상수시간 내에 계산되기 때문이다.
### Principle of optimality = optimal substructure

**“All subsolutions of an optimal solution are optimal”**

**“Optimal subsolutions can build up a global(final) optimal solution)**

⇒ $\sum \text{opt. subsolution} \Leftrightarrow \text{global subsolutions}$

**주의 사항**

만약 problem A가 principle of optimality를 만족한다면

⇒ DP는 best design을 제공한다.(optimal results) == 정답을 보장하는 설계

BUT, DP가 가장 **효율적**이라는 것을 나타내는 것은 **아니다**.

### DP를 사용하는 방법 2가지

**Recursive + memoization**

```python
memo = {}
def fibo(n):
	f = 0
	if memo[n] != None:
		return memo[n]
	if memo[n] <= 2:
		f = 1
	else:
		f = fibo(n - 1) + fibo(n - 2)
	memo[n] = f
	return f
```

**Bottom-up(look-up table)**

```python
table = {}
for k in range(1, n):
	if k <= 2:
		table[k] = 1
	else
		table[k] = table[k - 1] + table[k - 2]
```

### DP

DP의 경우 Code optimization을 해야 잘 풀었다고 한다!

**Design**

Step 0

Example을 찾아서 해결해보기.

Step 1

Establish a recursive property from the problem

= Identify(Find out, Derive) a **recurrence equation** from the problem

⇒ 큰 문제 = 작은 문제 +/* 작은 문제 …

Step 2

Solve in a bottom-up fashion programming

= Solve smaller problem first

⇒ Solve and save them in arrays(tables, dict…)

⇒ Use them later(from look-up tables)

**Time Complexity**

시간 복잡도 = Table의 크기 * 각 칸을 구하기 위한 연산의 수

분석의 경우 for-loop의 시행횟수이며 table의 build-up에 근접한다.