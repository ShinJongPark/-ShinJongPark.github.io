---
layout : article
title : "유클리드 호제법(Euclidean Algorithm)이란? Java 구현"
author : ""
tags : "Algorithm"
article_header:
  type: overlay
  theme: dark
  background_color: '#123'
  background_image:
    gradient: 'linear-gradient(135deg, rgba(34, 139, 87 , .4), rgba(139, 34, 139, .4))'
    src: /assets/images/logo/background_Java.jpg
---

<br/>

> 유클리드 호제법(Euclidean Algorithm)을 알아보기로 한다.

<br/>
<br/>

## l. 유클리드 호제법(Euclidean algorithm)이란?

> 두 수(자연수)의 **최대공약수**를 구하는 알고리즘의 하나이며, 기원전 300년경에 만들어진 가장 오래된 알고리즘으로 알려져 있다.
>
> 여기서 **호제법**이란 말은 두 수가 서로 상대방 수를 나누어서 결국 원하는 수를 얻는 알고리즘을 말하며, 유클리드가 제안한 방법이다.

<br>

> 일반적으로 최대 공약수를 얻기 위해서는 두 수를 **소인수 분해** 해야 한다.
>
> 이 방법은 수가 커질수록 소인수 분해하기 어려울 수 있다.

<br>

<br>

## ll. 구하는 방법

> 유클리드 호제법은 큰 값을 작은 값으로 나머지를 구하며, 
>
> 나눴던 값은 다시 나머지로 또다시 나머지를 구한다.
>
> 이 과정을 반복하며, `나머지가 0이 됐을 때, 나눈 수`가 최대공약수가 된다.
>
> ```
> 78696 ＝ 19332×4 ＋ 1368
> 19332 ＝ 1368×14 ＋ 180
> 1368 ＝ 180×7 ＋ 108
> 180 ＝ 108×1 ＋ 72
> 108 ＝ 72×1 ＋ 36
> 72 ＝ 36×2 ＋ 0
> # 여기서 36이 최대 공약수이다.
> ```

<br>

<br>

## lll. 증명

>다음은 귀류법을 이용하여 증명한다.
>
>귀류법은 결과를 부정하면 모순이 나온다는 사실로, 원명제가 참임을 증명하는 방법이다.
>
>```
>G(0, n)일때 n은 최대공약수이다.
>(0은 모든 수로 나누어 떨어지고, n의 약수 중 가장 큰 수는 n이기 때문)
>
>A, B는 모두 자연수이고, A>=B 일때,
>A = Bq + R 가 성립하며,
>G(A, B) == G(B, R) 이다.
>따라서 R == 0 일때, B를 구하면 된다.
>
>
>다음은 G(A, B) == G(B, R)임을 증명한다.
>```
>
>A, B는 모두 자연수이고, A>=B 일때,
>
>A = Ga, B = Gb 라고 가정하자. (G는 최대 공약수, a,b는 서로소이다) 
>
><br>
>
>A = Bq + R
>
>R = A - Bq
>
>R = Ga - Gbq
>
>R = G(a-bq)
>
>Ga = Gbq + G(a-bq)
>
>A와 B는 가정하에 a,b는 서로소이므로 최대 공약수는 G이다.
>
>B와 R의 최대 공약수가 G이려면, `b와 a-bq가 서로소임을 증명`하면 된다.
>
><br>
>
><br>
>
>증명할 명제는 `귀류법`을 이용하여 증명한다.
>
>b와 a-bq가 서로소가 아니라면, 공약수 m이 존재해야 한다.
>
><br>
>
>b = mk, a-bq = mk' (k와 k'는 서로소)
>
>a = bq + mk'
>
>a = mkq + mk'
>
>a = m(kq + k')
>
>b = mk
>
>a와 b는 공약수 m을 갖게 된다.
>
><br>
>
>1) m == 1 이라면,
>
>> b = k
>>
>> a-bq = k'
>>
>> `b 와 a-bq는 서로소`가 된다. (**모순**)
>
>2) m != 1 이라면,
>
>> m이 2이상의 공약수를 갖게 되어
>>
>> 원명제에서 a,b는 서로소라는 전제가 **모순**된다.
>>
>> 따라서 `b와 a-bq는 서로소`이다.
>
><br>
>
>`b와 a-bq는 서로소이다.`
>
>즉, G(A, B) == G(B,R) 이며, 
>
>**R == 0 일때, B가 최대공약수가 된다.**

<br>

<br>

## llll. Java 구현

> ```java
> class Solution {
>     public int gcd(int a, int b) {
>         int A = Math.max(a,b);
>         int B = Math.min(a,b);
>         int R = 0;
>         while(R > 0){
>             R = A % B;
>             A = B;
>             B = R;
>         }
>       //R이 0일때 A가 gcd
>         return A;
>     }
> }
> ```
>
> 

<br>

<br>



> **Reference**
>
> - namu wiki

<br>

<br>



