---
title: Interest rates, Duration and Convexity
date: 2026-1-11 10:00:00 +0900
categories: [금융, Fixed Income Securities - Veronesi]
tags: [Veronesi]
math: true
description: 
---

## Discount Factors

돈의 가치는 시간이 흐르면서 점차 감소한다.

공정한 비교를 위해서 같은 시점에서 가치를 비교하는 것이 중요한데 이를 위해서 Discount Factor라는 개념을 도입했으며 이는 미래의 $1가 현재 얼마의 가치를 지니고 있는지를 나타내준다.

**표기 방법**: T시점의 $1가 t 시점의 얼마인지 나타낼 때 $Z(t,T)$로 표기한다.

**Fact 2.1** $T_1 < T_2$라고 할때 $Z(t,T_1) \ge Z(t, T_2)$

Fact 2.1의 경우 반대가 성립하게 되면 더 이른 $T_1$시점에 $1를 달성하게 되는데 이는 arbitrage 기회를 창출한다.
- $T_1$이 만기인 채권 구매, $T_2$인 채권 판매

물가가 변하면서 돈의 시간가치는 계속 변화하는데 이에 따라 Discount Factor는 변화해야 한다.

## Interest rates

이자의 지급횟수에 따라서 최종적인 payoff가 결정되는데 같은 final payoff를 받는다고 할 때, 이자지급 횟수가 증가할수록 이자율이 작다.
- 이때, 이자는 항상 재투자 가정을 하므로 복리이다.(수학적 편의를 위해 연속 복리를 많이 사용한다.)

### Term Structure


