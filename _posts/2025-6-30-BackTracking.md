---
title: BackTracking
date: 2025-6-30 13:00:00 +0900
categories: [소프트웨어, 알고리즘]
tags: [N-Queens, Sum of subsets, Graph Coloring, Hamiltonian Circuits]
math: true
---
# BackTracking

### DP = BF(?)

knapsack에서 이론적으로 DP와 BF가 거의 동일한 performance를 보인다.

위의 문제를 해결하기 위해 우리는 NEW DESIGN을 생각해낼 수 있다.

### How to implement BF?

1. for-loop → not dynamic
2. Graph 탐사 with DFS, BFS → dynamic하다.

고민해야 할 개수가 늘어나면 for-loop은 1중첩이 추가되지만 DFS의 경우 depth++

### BackTracking의 특징!

1. DFS를 기반으로 한다.
2. **이론적 TC의 향상 X → 실질적 run(execution) time의 향상**
3. **Promising function이 중요하다.**

### Backtracking step

STEP 1: DFS of a tree except that nodes are visited if promising

STEP 2: Backtrack if NON-Promising ⇒ Pruning

STEP 3: Do a DFS of a state-space tree, checking whether each node is promising

             and if it is nonpromising, backtracking to the node’s parent

### Analysis Key

- optimality → 답이 존재한다면 항상 정답을 찾을 수 있다(trivial) ⇒ 입증 필요 X
- Time Complexity = exponential(like BF) ⇒ not polynomial
- empirical test(실험적 성능 향상) → 얼마나 많은 노드들을 줄일 수 있는가
    
    ⇒ run/execution faster (응답 속도 향상)
    

## Example to describe backtracking

### N-Queens

DEF. N x N의 판 위에서 N개의 Queen이 서로를 잡지 않도록 배치하는 방법의 수

**이론적 TC → 매우 큼.**

ex. 8-Queens 문제에서 ⇒ $\text{TC} = 64^8$

State-space tree, search-space tree를 통해 BF를 나타낼 수 있다.

**Idea.**

중간에 틀리다는 것을 알 수 있을 때 모든 탐색 가능한 조합을 검사할 필요가 있을까?

### Sum of subsets

: a special case of 0/1 knapsack

```python
S = { item1, item2 ... , itemN }
weight = { weight1, ... , weightN }
W = fixed weight
```

DEF. find A (subset of S) such that the sum of weights in A equals W

응용분야: Game 서버의 Load Balancing ⇒ 각 서버의 capacity 맞추기

Algo. Design ⇒ Brute Force

All enumerations of possible subsets → for-loop < DFS

⇒ $O(2^n)$

**Backtracking 필요**

1. Promising function 구하기
    1. i-th level: weight + weight(i + 1) > W일 경우 이후 고려 X
    2. weight + 미래 총 weight 합 < W일 경우 고려 X
2. DFS traverse/visit
    
    프로그래밍으로 구현
    

**Analysis**

1. optimal한가? ⇒ 검증 필요 X/ 당연함
2. execution time: by timer ( promising function의 설계에 따라 달라짐)
3. 생성된 노드 수:
    
    31개 중 15개 생성 ⇒ 31 - 15 = 16(performance gain)
    
    **세는 방법**
    
    1. 생성된 Leaf-node의 수
    2. 전체 Leaf-node의 수

**Question**

1. 만약 non-increasing sorted되어 있다면 pruning에 영향을 미칠까?
    
    
2. item들이 random 입력되었을 때 과연 똑같을까?
3. 정렬하는 시간이 우수하다면 → 전처리로 처리 가능하다.
    
    전처리가 시간이 다소 걸리더라도 sorting하고 backtracking이 유리한가?
    

### Graph coloring problem

= vertex-coloring, M-coloring

DEF. color undirected graph with ≤ m colors

조건: 2 Adj. vertices must have different colors

응용 분야: 강의실 무선 마이크, 무선 네트워크 (주파수 share)

⇒ 비싼 자원을 최대한 아껴서 사용하는데 이용됨.

**Solution**

1. BF → Time complexity : T(n(# of node), m(# of edge)) = $O(m^n)$
    
    **Question**
    
    1. How to find minimun m?
        
        → NO(efficient polynomial algo. X)
        
    2. given m이 있을 때 m-colorable한지 확인
        
        → YES(with Backtracking)
        

**Promising function 설계**

: check adj. nodes for the same color

### Hamiltonian Circuits(HC) Problem

= Hamiltonian path or cycle

DEF. Given a connected undirected graph

HC is a path that starts at a given vertex, visits each vertex exactly 

once, and ends at the starting vertex

**Promising function**

1. i-th node → (i + 1) node: connected
2. (n - 1)th node → 출발 노드로 돌아와야함.
3. ith node cannot be 0 ~ (i - 1) nodes

**Analysis**

BF complexity: O(n!)

Backtracking: node 생성 수, running time

Advanced Design issue

상위 레벨: Backtracking design 고려

하위 레벨: promising function의 design 고려

Space state tree의 경우 다양한 방식의 설계 가능

1. 노드 개념 / edge 개념을 잡고
2. branching factor: 부모 → 자식의 edge 개수
    
    위가 몇개인지에 따라 tree의 depth가 달라진다.
    
    **Question**
    
    bf가 적은게 좋을까 많은게 좋을까?
    
    ex. bf = 2 vs bf = 많을 때