---
title: Interest rates, Duration and Convexity
date: 2026-1-11 10:00:00 +0900
categories: [금융, Fixed Income Securities - Veronesi]
tags: [Veronesi]
math: true
description: Vernoesi 2-4장
---

## Discount Factors

돈의 가치는 시간이 흐르면서 점차 감소한다.

공정한 비교를 위해서 같은 시점에서 가치를 비교하는 것이 중요한데 이를 위해서 Discount Factor라는 개념을 도입했으며 이는 미래의 $1가 현재 얼마의 가치를 지니고 있는지를 나타내준다.

**표기 방법**: T시점의 \$1가 t 시점의 얼마인지 나타낼 때 $Z(t,T)$로 표기한다.

**Fact 2.1** $T_1 < T_2$라고 할때 $Z(t,T_1) \ge Z(t, T_2)$

Fact 2.1의 경우 반대가 성립하게 되면 더 이른 $T_1$시점에 $1를 달성하게 되는데 이는 arbitrage 기회를 창출한다.
- $T_1$이 만기인 채권 구매, $T_2$인 채권 판매

물가가 변하면서 돈의 시간가치는 계속 변화하는데 이에 따라 Discount Factor는 변화해야 한다.

## Frequency of Interest rates

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

$$\text{Invoice(Dirty) price = Quoted price + Accrued interest}$$

이때, 경과 이자는 이자율 * 이자지급일 이후 보유 기간으로 계산한다.

### Floating Rate Bonds

변동금리부 채권은 일정 기간마다 이자를 시장금리에 맞추어 지급하는 채권이다.

향후 future cash flow를 알 수 없지만 forward rate을 사용한다면 계산이 가능하다.

이 채권의 특이한 점은 각 이자지급일에 채권 그 자체의 가격이 명목금액으로 수렴한다는 점이다. 그 이유는 채권의 금리가 시장 금리와 맞춰지면서 이자율과 할인율이 동일해지면서 액면가와 같아지기 때문이다.
- 더 간단하게 말하자면 이자가 변동하는 날 변동금리부 채권은 그날 발행한 채권과 같은 채권이라고 볼 수 있다.

### Interest rates

**Definition.** level of interest rates is the average yield across maturities

**Definition.** P라는 가격을 지닌 증권의 Duration은 이자율 level의 작은 평행이동에 대한 가격 P의 민감도(percent sensitivity)이다.
- Duration은 현재 채권 가격에 대한 회수 속도를 의미하기도 한다.

$$\text{Duration}=D_P=-\frac{1}{P}\frac{dP}{dr}$$

Zero coupon Bond에 대해서 Duration은 T-t, 즉 만기까지 남은 기간을 의미한다. 이때, 이자의 frequency는 연속 복리를 기준으로 한다.

Portfolio의 Duration을 계산할 때 각 증권의 Duration을 구한 후 현재 가치를 기준으로 가중평균을 통해 Duration을 계산한다.

$$D_W=\sum_{i=1}^{n}w_iD_i$$

- Coupon bond의 경우 zero coupon Bond로 나눌 수 있으므로 각각을 증권이라고 생각하면 portfolio의 Duration을 구하는 것과 같이 Coupon Bond의 duration을 구할 수 있다.

**Floating Rate Bond**의 경우 reset date(이자율)에 채권 가격이 명목금액으로 돌아온다. 이 경우 금리에 따라 채권 가격의 평가 손익을 보는 것이 다음 이자지급일에 무조건적으로 회수되기 때문에 회수 속도에 있어서 매우 빠른 효과를 내는 것으로 이해할 수 있다.

### Duration의 특징

1. 표면 금리가 높을수록 초중반의 현금흐름이 상대적으로 많기 때문에 Duration이 짧아지는 효과를 불러온다.

2. 표면 금리가 높다면 현재 시점에서 가까운 현금흐름은 이자율의 변동에 영향을 장기 현금흐름에 비해 덜 받는다.

### Duration의 종류들

**Modified Duration**

위에서 연속 복리를 기준으로 Duration을 계산했지만 현실적으로 연속복리는 불가능하다. 이를 개선하기 위해 연속 복리를 semi-annual 등의 frequency로 변환할 수 있는데 이걸 modified duration이라고 한다.

**Dollar Duration**

위의 Macaulay Duration(일반 Duration)과 Modified duration이 모두 percent sensitivity를 의미했다면 dollar duration의 경우 절대적인 값을 통해 이자율 변동에 대해 가격의 변화를 알려준다.

**Question.** Borrow at the 6-month term repo = shorting a 6-month floating rate bond와 같다고 한다. 이유가 무엇일까?

6개월 동안 차입 이자를 repo rate으로 고정한다고 생각해보자. 그렇다면 FRN의 경우 6개월 뒤가 이자 변경일이라고 했을 때 채권 가격이 par로 돌아오므로 채권 가격에 있어서 손해를 보지 않고 금리를 지불하고 돈을 빌린 것과 같은 효과를 낼 수 있다.

## VAR & ES

VAR은 Value-at-Risk의 약자로 T 시점까지 $1-\alpha$%의 확률로 내가 잃을 수 있는 최대 금액이 얼마인지 나타내는 값이다.

Example. 95%, 1-month VaR of $3 million.

$$\text{Prob}(L_T>VaR) = \alpha \%$$

Bond portfolio의 경우 이자율의 변동에 따라 portfolio의 가치가 변동한다. 즉, 이자율을 어느 분포로 정의할 수 있다면 우리는 Bond Portfolio에 대한 VaR을 수식을 통해 산출할 수 있다.

1) 역사적 기록을 통한 접근

2) 정규분포를 가정한 접근

VaR은 좋은 risk를 추정하기 좋은 방법일 수 있지만 **접근법에 따른 편차가 크고** duration을 통해 VaR을 측정할 때 **이자율의 큰 변화에 대해 근사가 부정확**할 수 있다.

위의 문제를 해결하기 위해 **Expected Shortfall**이라는 개념을 도입하였다.

$$\text{Expected shortfall} = E[L_T|L_T>VaR]$$

 VaR을 기준으로 그것보다 더 크게 손해를 볼 것까지 포함하여 계산하기 위하여 기댓값을 취한 값이다.

 ## Cash flow Matching and Immunization

 **Cash flow Matching**은 금융기관이 현금흐름에 해당하는 증권을 모두 찾아서 매칭시키는 방법이다. 하지만 **Immunization**의 경우 같은 현재 가치와 duration이 일치하는 portfolio를 찾아 구매하는 방식으로 이를 해결한다. 이때, Immunization이 유동성, 거래수수료 등의 장점이 있어 더욱 선호된다.

 ## Asset-Liability management

 보험사와 같은 회사의 경우 부채의 만기가 길어 duration이 상대적으로 높게 측정되는데 그에 비해 현실에서 유동적으로 거래되는 자산은 duration이 짧다. 이런 duration mismatch의 경우 금리 하락 시 지불해야하는 부채가 보유한 자산의 양 대비 매우 높게 측정되는 문제가 발생한다.

 위의 문제를 해결하기 위해 duration matching을 이용한다. Duration matching은 금리의 level 변화와 관계 없이 평가 손익을 안정적으로 관리하는데 큰 도움이 된다.

