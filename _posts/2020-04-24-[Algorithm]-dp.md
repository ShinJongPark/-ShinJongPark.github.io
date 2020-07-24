---
title: "[자료구조] DP ( Dynamic Programming )"
tag: "DataStructure"
author : ""
article_header:
  type: overlay
  theme: dark
  background_color: '#123'
  background_image: false
---



## DP( Dynamic Programming )

- Top down 방식

```java
static int[] d[100];
public int dp(int x){
    if(x == 1) return 1;
    if(x == 2) return 2;
    return d[x] = dp(x-1) + dp(x-2);
}
```

이 방식은 만약 50번째 값을 출력 할 시 **2^50** 의 연산을 수행하며,

대략 2^10 = 1000, 1000^5의 연산을 수행합니다. 어마어마 하죠.

시간 복잡도 : **O(2^n)**

그래서 아래의 Memoization 방식을 활용 합니다.

- Bottom up 방식

```java
public long fib(int n){
    dp[0]=0;
    dp[1]=1;
    for(int i=2; i<=n; i++){
        dp[i]=dp[i-1]+dp[i-2];
    }
    return dp[n];
}
```

<br>

<br>

## Memoization

```java
public int dp(int x){
    if(x == 1) return 1;
    if(x == 2) return 2;
    if(d[x] != 0 ) return d[x];
    return d[x] = dp(x-1) + dp(x-2);
}
```

시간 복잡도 : **O(n)**

