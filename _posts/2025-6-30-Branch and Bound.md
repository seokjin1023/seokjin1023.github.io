---
title: Branch and Bound
date: 2025-6-30 15:00:00 +0900
categories: [소프트웨어, 알고리즘]
tags: [TSP, h-value]
math: true
---

# Branch and Bound

## TSP(Traveling Salesman Problem)

HC에 edge cost가 추가된 문제

### h-value in TSP

TSP는 minimization optimization문제이다.

⇒ 0 < h < h*처럼 h가 underestimate되어야 한다.

$h = h^* -\alpha$

### Example - 5 city TSP

Solve

→ BF, D&C, DP, Greedy, Backtracking, B&B 등을 통해 solution을 제공하고 비교 필요

**BF =** $O(n!)$

실제 실행 시간을 향상시키기 위해서 Branch and Bound를 통해 해결할 수 있다.

**B&B**

극단적인 예시를 들어서 만약 edge cost가 모두 1이라고 가정하자.

→ start node(1)의 h = 5이다(총 5개의 edge 남음)

→ (1→2) 이후 h = 4이다(총 4개의 edge 남음)

위의 극단적인 예시를 통해서 insight을 얻어 h를 더욱 발전시켜 나가볼 것이다.

- h1 idea
    
    우리는 어떤 edge를 지나가할지 모르지만 각 edge의 ingoing edge의 최솟값과 outgoing edge의 최솟값보다 작다는 사실을 알고 있다.
    
    $$
    TSP \geq \text{min outgoing edges of node A} \\
    \geq \text{min incoming edges of node B}
    $$
    
    즉 핵심 idea: 가장 min edge로 나가고 min edge로 들어온다.
    
    이때의 h를 측정하면 이는 underestimate가 되고 h < h*을 만족한다.
    
- h2 idea
    
    위의 h1을 활용하여 이미 지나온 노드를 h1에서의 idea에서 h값을 구할 때 배제해도 된다는 생각을 가질 수 있다.
    
    이를 통해 아래처럼 h값을 구할 수 있다.
    
- h3 idea
    
    우리는 h2에서 항상 나가는 edge들을 계산하여 h값을 계산하였다.
    
    이때, **일반적으로 bound function is not unique**라는 점을 이용하여 idea를 얻을 수 있다.
    
    1. min. cost of entering vertex n
        
        = min cost of nth column 
        
    2. min. cost of exiting vertex n
        
        = min cost of nth row
        
    
    ⇒ avg = min cost of vertex n = [1. + 2.] / 2
    

**Question**

1. 위의 h2와 h3를 비교했을 때 무엇이 더 우위인지 논할 수 있어야 한다. 어떻게 위의 두 개의 비교 우위를 논할 수 있는가?
    - 우리는 문제를 풀 때 search tree를 그리면서 답변해야 한다.
    - 각 incoming/outgoing edges ⇒ 1/2를 계산하는 이슈를 어떻게 해결할 것인가

**Further issues**

1. Branch factor and DFS/BFS
    
    A: big branch factor / B: small branch factor
    
    A + backtracking & B + B&B vs A + B&B & B + backtracking 중 무엇이 더 좋을까
    
    위의 문제로 branch factor의 크기에 대한 문제를 바꾸어 말할 수 있다.
    
    **답**
    
    1. Branch factor는 tree visit type과 관계가 있다.
    2. Branch factor는 그러므로 설계와 관련되어 있다.
    
    ⇒ Root에서 어떤 item을 먼저 배치하는지가 중요하다.
    

1. h-value를 구하는 구체적인 guideline은 없을까?
    - 존재한다(Relaxation) → 인공지능 시간에 배울 것이다.
    - Relaxation = simple constraint를 제거한 Model을 만들고 이를 적용하는 것이다.
        - ex. 0/1 KS에서 **sack을 나누어 담을 수 있게 제한 제거** h = fractional K/S이 된다.
2. 만약 |V|가 커지게 된다면 TSP에서는 어떻게 해결해야할까
    
    이를 위해서 우리는 New Design Approach가 필요하다.
    
    왜 문제가 어렵고 다른 접근을 어떻게 할 수 있을까?
    
    ⇒ NP class problems에 대해 배우면서 13주차부터 배울 것
    
    ⇒ NP class problem들은 approximation algorithm들이 필요하다.

## Backtracking vs Branch and Bound

Backtracking: DFS + bound function

Branch and Bound: BFS + bound function

### Backtracking vs Branch and Bound

실제 field 에서는 Branch and Bound >> Backtracking

**BFS가 DFS보다 reliable하기 때문이다.**

- DFS의 경우 지속적 계산량이 높음.

**이후의 h-value에 관한 문제에서도** 

h-value의 값을 점진적으로 더 발전시켜 나갈 경우 Branch and Bound는 효율 개선 가능

### f = g + h < Best에서 bound function 관점에서 비교

Backtrack vs B&B는 tree visit 순서에 따라서 g, h value의 update 차이가 발생한다.

이때, h-value를 구하는 수식을 정확하게 하면 할수록 BFS의 효율이 극대화된다.

⇒ short root 근처에서 pruning이 가능하기 때문이다.

h-value를 정확하게 구할 수 없다면

Backtracking의 경우 g-value를 빠르게 갱신하고 h-value가 그에 맞추어 교정되면서 불확실성이 BFS 대비 더욱 빨리 감소하는 특징을 지니고 있어 h-value가 정확하지 않다면 Backtracking이 더 나을 수 있다.

### 결론

h-value의 값의 정확성이 높을수록 Branch and Bound를 사용하자.

## Improve Branch and Bound

idea: visit order 조정을 통한 방법

BFS, DFS ⇒ fixed order로 수행한다.

DFS의 경우 traverse 순서를 고정하고 BFS의 경우 depth에 맞추어 계산한다.

이때, BFS가 Queue를 사용한다는 점을 통해 Best-first를 통해 이를 개선할 수 있다.

### Best-first Branch and Bound

이 방법은 greedy algorithm의 방법을 사용해 그 때 최선의 값을 먼저 가지를 내리는 것이다.

**문제: greedy를 사용하기 때문에 local optimal → global optimal인지 proof required**

## How to estimate h-value

h: mathmetical expression for estimation/prediction

예를 들어서 0/1 KS의 경우 fractional KS을 h로 사용한다.

### Guideline for h-value

h의 range를 설정하며 범위를 좁혀간다.

1. h > 0, h < inf ⇒ 0 < h < inf
2. h*: global optimal value라고 하자.(이는 우리가 알 수 없다)
    1. h > h* : overestimate(maximization optimization problem)
    2. h < h* : underestimate(minimization optimization problem)
3. overestimate의 장점(in max op. prob)
    1. optimal로 진행 가능한 가지를 pruning out하지 않는다.
        
        = 절대로 optimal한 답을 배제하지 않는다.
        
    2. 보수적, 안정적인 pruning을 한다.
    3. pruning되는 가지의 수는 적을 수 있다.
        
        ⇒ 효율이 조금 안 좋을 수 있다.
        
4. 0 < h* < h < inf여야 한다.(overestimate)
    
    이때 h의 경우 h*보다 커야 하지만 최대한 가까운 것이 좋다.
    
    이유: h*에 근접할수록 pruning power가 커지기 때문이다.
    
    **Question.**
    
    0/1KS에 사용가능한 frac KS보다 더 pruning이 많은 h-value 수식을 제공할 수 있는가?
    

위의 3번에서 설명했듯이 underestimate이 항상 좋지 않은 것은 아니다.

오히려 minimization optimization problem의 경우 underestimate을 사용해야 한다,

## Lower bound

어떤 문제를 해결하기 위해 우리는 2가지의 접근법을 취할 수 있다.

1. 더 효율적인 algorithm 개발
2. 더 이상 효율적인 algorithm이 없다는 것을 증명
    
    → Quit/Stop
    

### Computational complexity

위는 주어진 문제에 대해서 모든 알고리즘의 효율성에 대한 lower bound를 결정

**연구자의 입장**

Lower bound를 만약에 찾는다면

1. Try to find more efficient algorithm with New Design
    
    Upper bound를 줄여감
    
2. Try to find a greater(better) lower bound using computational analysis
    
    비현실적인 Lower bound를 점점 더 현실적으로 높여감.
    

위의 Upper bound와 lower bound가 만나는 시점에서 develop은 종료된다.