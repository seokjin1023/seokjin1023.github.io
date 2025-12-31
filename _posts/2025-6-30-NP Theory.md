---
title: NP Theory
date: 2025-6-30 16:00:00 +0900
categories: [소프트웨어, 알고리즘]
tags: [P, NP, NP-Complete, NP-Hard]
math: true
---

# NP Theory

### 배경

우리가 효율적인 algorithm을 찾을 수 없을 때

1. optimal solution을 제공하는 매우 느린 algorithm 사용
2. optimal solution을 포기하고 approximation solution 채택
    
    (suboptimal, near-optimal solutions)
    
3. Massive 병렬화 with supercom, GPU, 분산 처리

위 3가지 방법이 존재한다.

### Problem의 category

Problem이 주어진다면 P ≤ NP ≤ EXP ≤ Solvable ≤ Countable 등으로 나눔.

하지만 위의 경계는 불분명하고 명확하게 나뉘지 않는다.

**Countable Problem**

1. 0과 10 사이의 정수의 개수 → finite countable
2. 0과 10 사이의 실수의 개수 → infinite countable
3. 0과 1 사이의 실수가 0과 10 사이의 정수 개수보다 많은가?

**만약 A 문제가 B문제보다 쉬움을 증명하고 싶다면.**

A: Sort, B: KS이라고 하자.

Sort의 경우 P-문제이고 KS의 경우 NP-문제이다.

- 우리는 각 문제의 난이도 class를 확인하고
    
    그 문제의 분류에 맞는 적절한 desgin과 분석을 할 수 있어야 한다.
    

**Easy Problem vs interactable Problem**

Easy: good algorithm 존재 / polynomial TC

Interactable: difficult to treat or work / No Polynomial TC

**P-class의 정의**

The class of decision problems that are polynomially bounded.

T(n) = polynomial function of input ‘n’

⇒ Problem들이 polynomial time 이내에 solvable하다.

—> EXP-class는 exponential time 이내에 problem이 solvable함.

**유의하자!**

본인의 자의적 판단에 따라 polynomial time complexity를 찾지 못했다고 해서 

P-class가 아닌지 판단 불분명하다.

마찬가지로 Exp algorithm을 찾았다고 exp-class라고 하는 것은 올바르지 못하다.

⇒ 수학적 정의에 따라 정의하는 것이 필요함.

**3-category**

1. Problem **proven** to be in P-class
    - sort, search, CMM, SP, dijkstra 등
    - easy, fast, efficient, optimal, tractable하다.
2. Problem **proven** to be Not in P-class ⇒ few하고 intractable함.
    - O(n!)등의 TC를 지님.
    - Determine All Hamiltonian paths (only BF ⇒ O(n!))
    - Halting problem
        - given a computer program does it stop/halt 판단
        - 즉 어떤 알고리즘과 data set이 주어졌을 때 그 프로그램이 P-time 이내에 작동하는가?
        - Not in P-class라고 증명되어 있다.
        - uncomputable(undecidable)이라고 증명된 첫번째 문제이다.
3. Problem proven neither to be P nor to be intractable
    - KS, Graph Coloring, TSP, subset sum 등
    - 아직 증명되지 않았지만 심증 상 난이도로 인해 예측
        - 이 문제들은 1번이 될 가능성이 있어서 여기에 관심 집중
    - NP-class라고 불릴 수 있다..?

### NP Definition

NP is the class of decision problems for which a given solution can be checked quickly(in P-time) to see if it is true solution

- 만약 solution이 주어졌을 때 이게 맞는 정답인지 P-time 내에 검증 가능한가?

**Solution은 어떻게 주어지는가?**

Nondeterministic Algorithm에 의해서 주어진다. 

1. Nondeterministic Guess
2. Deterministic Verification

의 순서로 NP임을 검증할 수 있다.

**Polynomial time Nondeterministic Algorithm이란?**

Nondeterminstic Algorithm 중 Verification이 P-time이내에 가능한 알고리즘을 의미한다.

즉, 위의 NP의 정의를

- P-time Nondet. Algo.으로 solvable한 모든 문제들의 집합들 중 Nondet. Algo.에 의해 solvable한 문제들이라고 정의할 수 있다.

$$
P \subset NP
$$

위의 포함관계는 증명되었지만 그 역은 증명되지 않아 $P=NP$임을 확신할 수 없다.

우리는 어떤 최적화 문제가 주어졌을 때 이를 최적화 or 결정 문제의 형태로 만들어 냄.

**Example**

1. TSP
    
    opt. ver. : optimal tour
    
    Decision ver. : is there a tour with cost < 200?
    
2. KS
    
    Opt. ver. : max total profit
    
    Decision ver. : is there a set with profit > 100?
    
3. Graph Coloring
    
    Opt. ver. : min # of colors
    
    Decision ver. : m-colorable
    
4. Clique Problem
    - Graph가 주어졌을 때, Complete subgraph를 찾는 문제이다.
        - bioinformatics, SNS 등에서 사용됨.
    
    opt. ver. : find max clique
    
    Decision ver. 
    
    : determine whether a graph contains a clique of at least a given size ‘k’
    

**Question**

1. TSP is P or NP?
2. Sort is P or NP?

### NP-Complete

현존하는 문제들 중 P-time으로 해결할 수 없는 문제가 상당히 많다.

이때, NP 문제중 대표적, 어려운, 완전한 문제를 P-time이내로 풀 수 있다면 이 문제로부터 변환 가능한 NP문제들이 P-time이내에 풀 수 있다라는 생각을 가지고 이런 class 분류를 만들게 되었다.

**Definition**

Problem B is NP-Complete if

1. B is NP Problem
2. for all A(in NP) $A \le_p B$

위의 정의가 너무 어렵다면

Problem C is NP-Complete if

1. C is NP
2. for NP-C B,  $B \le_p C$

로 표현할 수 있다.

**위의 정의의 활용(with Cook’s Theorem)**

Cook의 정리에 의하면 

CNF Problem is P then P = NP이다.

그리고 이것이 의미하는 것은 CNF problem은 NP문제임을 증명했다는 의미이다.

**CNF-Satisfiability(SAT) Problem**

$(x_1 \lor x_2) \land (\neg x_1 \lor x_2)$ 등의 bool expression 집합이 참인지를 찾는 문제이다.

**결론**

주어진 문제를 NP-Complete문제로 변환(증명) 가능할까?

- CNF를 통해서 내가 알고자 하는 문제로 변환하면 그 문제가 NP일 때 NP-Complete이다.

**Transformation Algo. Tech**

Problem A와 B가 있다고 하자.

만약 A의 instance를 B의 instance로 transform할 수 있는 Algo.이 존재한다면 x is yes = y is yes이다.

- A to B로 만드는 p-time Algo.이 존재한다면 A is p-time reducible to B라고 한다.

$$
A \le_p B
$$

위의 수식에서 $A \in P$라고 할때 B가 P임을 보장할 수 없음.

하지만 $B \in P$라면 A도 P임을 보장할 수 있음.

### NP-Hard

보통 Decision의 경우 P-time이내에 solution의 참/거짓을 판단할 수 있음.

하지만 p-time이내에 판별하지 못한다면?

NP-Hard는 이러한 문제 분류(ex. 최적화)를 위해서 만들어짐.

**Definition**

A is NP-Hard if

for NP-C B, $B \le_p A$

즉, NP-Complete문제가 A로 변환되기만 하면 NP-Hard이다.