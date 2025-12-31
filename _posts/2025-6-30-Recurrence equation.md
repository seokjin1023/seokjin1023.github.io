---
title: Recurrence equation
date: 2025-6-30 10:00:00 +0900
categories: [소프트웨어, 알고리즘]
tags: [Recurrence, math, Fibonacci, Merge Sort]
math: true
---

# Recurrence(s) equation

## Divide and Conquer ≠ recurrence

recurrence 문제를 Divide and Conquer로 바꿀 때 비효율적인 문제들이 존재한다.

⇒ linear recurrence가 이에 해당한다.

## Recurrence란 어떤 것인가?

### 1. Describes a sequence of numbers

1. Early terms(numbers) are specified explicitly
2. Later terms are calculated(expressed) a function of their predecessors

Ex) $T(1) = 1, T(n) = T(n - 1) + 1$ 

⇒ 초반의 값은 명확하게 정의되어 있으며 뒤의 값들은 그 것의 전의 것으로 표현 가능함.

### 2. Reduces a big problem into smaller problems until easy cases(terms) are reached ⇒ progressively

### 3. Useful and powerful to analyze the performance of recursive algorithm

Time Complexity를 구하는데 도움이 된다.

## Two big Recurrence in CS

### 1. Linear recurrence

later terms = linear combination of early terms 일 경우 linear recurrence이다.

**Ex. Fibonacci recurrence**

$f(0) = 1, f(1) = 1 / f(n) = f(n - 1) + f(n - 2)$

⇒ linear combination으로 later term을 나타내고 있으므로 linear recurrence다.

**Time Complexity**

$T(n) = T(n - 1) + T(n - 2)$

$T(n) = O(n^2)$ for not tight bound

$\sim O\left( \frac{1.618^n}{\sqrt{5}} \right)$
 is tight upper bound

### 2. Divide and Conquer recurrence

**Ex. Merge-Sort recurrence**

$T(1) = 0 / T(n) = 2T(\frac{n}{2}) + (n - 1)$

⇒ T(n) is function of T(n/2)

⇒ T(n)이 preceding terms의 linear combination으로 이루어지지 않았음.

**Time Complexity**

$T(n) \sim O(n\log n)$

## 결론

**요약**

부수적인 연산을 줄이는 것보다 더 작은 문제를 생성하는 것이 알고리즘의 속도에 더 중요하다. Linear Recurrence는 큰 부분 문제를 포함하므로 매우 비효율적이며, D&C Recurrence는 보통 다항식 시간으로 제한되므로 좋은 설계 방식이다. 하지만 Fibonacci Recurrence처럼 중복된 부분 문제가 발생하는 경우, 반복(Iterative) 접근 방식이 더 효율적이며, 이를 일반화한 개념이 Dynamic Programming(DP)이다.

**원본**

1. Generating smaller problems is more important to algorithmic speed(efficiency) than reducing the extra steps per recursive calls
2. More generally, linear recurrences(have big subproblems) typically have Exponential solution
    
    ⇒ extremely inefficient
    
    while D&C recurrences(have smaller problems) usally have solutions bounded by a polynomial
    
3. If the subproblems are only a fraction of the size of the original, then the solution is typically bounded by a polynomial
    
    ⇒ D&C design is good
    
4. Even worse, Fibonacci recurrence have subproblems “overlapped”
    
    ⇒ Repeated caculation for the some terms are performed
    
    ⇒ extremely inefficient
    
5. How to deal with Fibonacci
    
    ⇒ We know that recurrence can be implemented recursively as well as iteratively
    
    (for, while loop를 사용)
    
    ⇒ New design is introduced(Dynamic programming)