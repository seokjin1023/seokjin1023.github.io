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

spot rate curve, yield curve라고 불리며 특정 시점에서 만기와 이자율의 level 사이 관계를 나타낸다.
- Term spread는 장단기 이자율의 차이를 의미한다.

Term structure는 위아래로 크게 움직이며 같은 방향으로 움직이는 성질을 확인할수 있는데 이때 장단기 금리는 항상 같은 양만큼 이동하지 않는다. 즉, 기간구조는 평행이동하지 않는다는 의미이다.

### Coupon Bond

미국채 중 T-Bill(단기채)는 기본적으로 zero-coupon bond의 형식이다.

Coupon Bond의 경우 가격을 구하기 위해서는 각 시점에서의 현금흐름을 그 시점의 Discount factor를 곱해주고 합산하여 현재 가치가 얼마인지 구할 수 있다.

즉, 가격과 coupon 및 원금의 합산은 같아야하지만 유동성 부족과 같은 문제가 발생할 경우 arbitrage 기회가 발생할 수 있다.

### Bootstrap

Bootstrap은 Discount factor를 단기부터 순차적으로 장기까지 Discount factor를 coupon bond를 이용하여 구하는 방법이다. zero-coupon bond의 경우 그대로 Discount factor로 변환 가능하지만 coupon bond의 경우 각 채권의 가격 공식을 사용하여 Discount factor를 역산할 수 있다는 원리를 사용해 구한다.

### Yield to Maturity

Coupon bond를 각 Discount factor로 나누어 price를 구할 수 있는데 Bond의 가격은 만기에 따라 천차만별이다. 유일한 값인 YTM을 사용하여 만기가 다른 bond를 비교할 수 있다. 

수식적으로 표현하면 미래의 현금흐름을 현재 가격에 맞출 수 있는 유일한 할인율이다.

**Example.** 동일한 만기를 지닌 채권이 coupon이 다를 경우

수익률 곡선은 일반적으로 우상향하는 곡선이다. 이에 따라 미래 현금흐름일수록 더 높은 금리가 적용된다고 볼 수 있다. 

표면 금리가 높은 채권의 경우 상대적으로 낮은 채권에 비해 낮은 이자율이 적용되는 Coupon의 비중이 높다. YTM의 경우 시장이자율의 복합적인 가중평균이기 때문에 낮은 시장이자율인 단기의 영향을 많이 받는 표면금리가 높은 채권이 더 낮은 YTM을 가진다.

**YTM이 높은 상품이 무조건 유리할까?**

YTM이 낮다는 의미는 표면 금리가 높다는 의미이므로 초반에 자금창출이 가능해 재투자 시 더 높은 이익을 취할 수 있다.

고쿠폰 채권의 경우 2가지 특징을 가지는데 Duration이 낮아 채권 가격에 덜 민감하다는 점과 재투자 가정 시 금리 변화가 중요하다는게 특징이다.

### Treasury Bill, Note, Bond

T-Bill은 단기채로 아래와 같이 quote한다.

$$d = \frac{100 - P_{bill}(t, T)}{100} \times \frac{360}{n}$$

Coupon이 존재하는 T-Note, T-Bond의 경우 채권이 이자 지급일이 아닌 날 인도될 경우 이에 대한 경과 이자를 고려해주어야 한다.

$$\text{Invoide(Dirty) price = Quoted price + Accrued interest}$$

이때, 경과 이자는 이자율 * 이자지급일 이후 보유 기간으로 계산한다.

### Floating Rate Bonds

변동금리부 채권은 일정 기간마다 이자를 시장금리에 맞추어 지급하는 채권이다.

향후 future cash flow를 알 수 없지만 forward rate을 사용한다면 계산이 가능하다.

이 채권의 특이한 점은 각 이자지급일에 채권 그 자체의 가격이 명목금액으로 수렴한다는 점이다. 그 이유는 채권의 금리가 시장 금리와 맞춰지면서 이자율과 할인율이 동일해지면서 액면가와 같아지기 때문이다.
- 더 간단하게 말하자면 이자가 변동하는 날 변동금리부 채권은 그날 발행한 채권과 같은 채권이라고 볼 수 있다.



