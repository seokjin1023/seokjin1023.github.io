---
title: Knapsack
date: 2025-6-30 14:00:00 +0900
categories: [소프트웨어, 알고리즘]
tags: [Optimization, 0/1 knapsack]
math: true
description: Knapsack이라는 유명 문제 중 0/1 knapsack이라는 조합 최적화 문제에 대한 각 방법론의 복잡도 계산
---

# Knapsack

CS에서 가장 fundamental한 문제

### Optimization Problem

**Optimization Problem**

최적화 문제의 경우 최댓값 구하기 등을 수행 → 0/1 knapsack 등

어려운 이유: DP이 좋은 polynomial time을 제공하지 않기 때문이다.

**Non-optimization problem**

Y/N 판별 → N-Queens, subset sum 등의 문제가 있다

### Definition

- Constraint (Combinational) optimization(제약 최적화)

**문제 구성 요소**

```python
S = {item1, item2, ... , itemN}
W_i = {weight1, weight2, ... , weightN}
P_i = {profit1, profit2, ... , profitN}
W = sack_size
```

**문제 조건**

$$
\text{Find }A \sub S \text{ such that} \\
\text{1. maximaize the profit in A}\\
\text{2. sum of weight in }A \leq W
$$

## 0/1 Knapsack(조합 최적화 문제)

**Formal description**

$$
\text{two n tuples }=<v_1,v_2,\cdots,v_n> \& <w_1,w_2,\cdots,w_n> \\
W>0\text{ 일 때, determine subset T} \\
\text{1. maximize} \sum_{i\in T} v_i \\
\text{2. subject to} \sum_{i\in T}w_i \leq W
$$

**How to solve?**

1. BF → O($2^n$)
    
    exponential time complextiy 
    
    → n이 클 때를 가정하므로 현실적으로 불가
    
2. D&C
    1. optimal을 찾을 수 있는가?
    2. optimal할 때 efficient한가?
3. Greedy → 현재까지 발견 안됨.
    - ranking을 어떻게 매길 지에 따라 정할 수 있음.
    1. Largest Profit first
        
        Ex. (w1, w2, w3) = (5, 10, 10) / (p1, p2, p3) = (10, 9, 9)
        
        W = 30
        
        idea대로 하면 total profit: 10
        
        but optimal profit: 18
        
        ⇒ optimal substurcture X
        
    2. Largest Profit per Unit weight first
        
        Ex. (w1, w2, w3) = (5, 10, 20) / (p1, p2, p3) = (50, 60, 140)
        
        W = 30
        
        (pi/wi) = (10, 6, 7)
        
        idea대로 하면 total profit: 190
        
        but optimal profit: 200
        
        ⇒ optimal substructure X
        
    
    위의 아이디어를 통해서 greedy가 optimal subsolution을 제공하기 위해서는 idea b에서 0/1이 아닌 Fractional(남은 sack에 item 분할해서 담기 가능) KnapSack일 경우 optimal하다.
    
4. DP
    
    **Ques. 0/1 knapsack이 optimal structure를 만족하는가?**
    
    정답: 
    
    **Find recurrence equation**
    
    1. 1차원 array
        
        idea. 아이템 선택, 담은 상태에서 profit 최대치를 기록함.
        
        P[i]는 i번째 item까지 선택한 상태의 profit 누적
        
        ⇒ similar as APSP
        
        $p[i] = \text{max}(p[i - 1], p[i - 1] + p_i)$
        
        **Wrong ⇒ weight를 고려하지 않음.**
        
    2. 2차원 array
        
        p[i, w] = max(item을 못 담는 경우, 담는 경우)
        
        $⇒ p[i,w] = \text{max}(p[i-1,w],p[i - 1,w] + p_i)$
        
        **Wrong ⇒ i 번째 item을 담기 위해 sack이 w만큼 비었는지 검사 필요**
        
    3. 2차원 array + weight 고려(with sack)
        
        $p[i,w] = \text{max}(p[i - 1, w], p[i - 1,w - w_i] + p_i)$
        
    
    **Analysis**
    
    $$
    T(n, w) = \text{TC for each subproblem} \times \text{number of subproblem} \\
    = \theta(1)\times nw\\
    =O(nw)
    $$
    
    위의 분석은 polynomial한 time처럼 보일 수 있다.
    
    하지만, w의 경우 입력되는 값에 따라 분리해야 하므로 0.1, 0.001 등으로 매우 잘게 쪼개질 경우 w가 기하급수적으로 커지는 상황 발생
    
    ⇒ polynomial time: input인 ‘n’에 따라서 성능이 결정됨.
    
    하지만 위의 O(nw)는 w에 의해서 결정되기 때문에 polynomial이 아니다.
    
    ⇒ 이런 time complexity: pseudo polynomial time complexity
    
    **Optimiztion**
    
    위의 idea를 더욱 성능 향상을 위해 improve한다면 i번째 item의 최고 profit을 계산하기 위해서는 
    
    i - 1번째 item을 가지는 element의 weight가 w일때, w - $w_i$일때만 확인하면 되므로 이때의 
    
    $\text{Time Complexity} = 1 + 2 + 2^2 + \cdots + 2^{n-1} = O(2^n)$
    
    **Final Time Complexity**
    
    $$
    \text{Time Complexity} = \text{min}(O(nw), O(2^n)
    $$
    
    이렇게 DP가 Brute-Force와 비슷한 time complexity를 가지는 이유
    
    → 문제의 난이도가 매우 어렵기 때문이다.
    
    ### Solution with Backtracking
    
    **Promising function 구하기**
    
    1. weight > W ⇒ STOP(nonpromising)
    2. (by subset sum)
        - current weight sum + w > W : STOP
        - current weight sum + w(total sum for future) < W : STOP
        
        subset sum 문제에서 W는 fixed였다. 하지만 0/1 KS의 경우 기준점(BEST PROFIT)이 변한다.
        
    
    **Bound function(=Nonpromising)**
    
    = 현재까지의 profit + 남은 item profit의 최대 추정치(expect)
    
    = g + h 라고 적을 수 있다.
    
    이때, g = exact / h = estimate 값이다.
    
    g + h < BEST라면 stop하는 것으로 pruning을 할 수 있다.
    
    $g = \sum_{j = 1}^{i}p_j$
    
    $h = \sum_{j = i + 1}^{k} + (W-\sum_{n = 1}^{k}) \times \frac{p_{k + 1}}{w_{k + 1}}$
    
    h(fractional KS을 따라 결정) = 현재 담을 수 있는 만큼 담고 남은 부분은 부분으로 나눠서 합산
    
    **Question**
    
    1. estimator h는 큰 값을 예측토록 설계하는 것이 좋을까?
        
        (= overestimate이 더 좋을까?)
        
        **정답: YES(In Maximization Optimization Problem)**
        
        이 경우 Pruning power가 약화될 수는 있지만, 더 넓은 범위를 계산함으로써 incorrect한 값을 반환하지 않는다.