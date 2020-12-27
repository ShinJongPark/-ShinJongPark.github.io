---
layout : article
title : "[알고리즘] 소수 만들기 시간복잡도 in Java"
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

<br>

<br>

> **일반적인 방법**과 **에라토스테네스의 체**, **비트연산자**를 활용한 소수 만드는 알고리즘의 시간복잡도를 비교하고자 한다.
>
> Last_Number = (10,000 ~ 1억) 을 대상으로 각 알고리즘 시간복잡도를 비교하였다.

<br>

### 일반적인 방법

> 가장 일반적인 방법이다.
>
> 제곱근까지의 숫자와 나눈 나머지 값이 0이라면 소수가 아니다.

```java
for(int i=2; i<=LAST_NUM; i++) {
	boolean prime = true;
	for(int j=2; j*j<=i; j++) {
		if(i % j == 0) {
			prime = false;
			break;
		}
	}
	if(prime) System.out.print(i+" ");
}
```

<br>

### 에라토스테네스의 체

> 이름이 잘 외워지지 않는... 에라토스테네스의 체이다.
>
> 숫자 2부터 시작하여 시작 숫자를 제외한 배수의 숫자를 지워나가는 방법이다.

```java
int[] nums = new int[LAST_NUM+1];
for(int i=2; i<=LAST_NUM; i++) {
	nums[i] = i;					// 각 위치에 숫자를 채워넣고,
}
for(int i=2; i*i<=LAST_NUM; i++) {
	if(nums[i] == 0) continue; 			// 이미 체크된 수의 배수는 확인하지 않음. 
	for(int j = i*i; j<=LAST_NUM; j+=i) 
		nums[j] = 0;				// i를 제외한 i의 배수들은 0으로 체크 
}
for(int i=2; i<=LAST_NUM; i++) {
	if(nums[i] != 0) {
		System.out.print(nums[i]+" ");
  	}	
}
```

<br>

### 비트마스크를 사용한 방법

> 에라토스테네스의 체를 비트마스크를 활용하여 구현한 방법이다.
>
> 비트마스크를 활용하여 하나의 원소에 8개의 자연수를 담아 소수여부를 파악하는 것이 핵심이다.
>
> 따라서, 필요한 배열의 크기를 1/8 줄일 수 있다.

```java
// 비트연산자를 활용한 소수 만들기 
eratosthenes();
// 소수만 출력
for (int i = 0; i <= LAST_NUM; i++) {
	if (isPrime(i)) {
		System.out.print(i + " ");
	}
}
```

<br>

> k >>> 3은 사실상 k / 8과 같으며, 8개의 숫자를 한 원소에 담기 위한 인덱스 역할을 한다.
>
> 1 << ( k & 7 ) 는 k % 8과 같으며, 위에서 찾은 위치에서 8비트의 원하는 위치에 접근할 수 있다.
>
> 해당 비트가 1이라면 소수라고 판단할 수 있다.
>
> 이 외 메커니즘은 일반적인 에라토스테네스의 체와 같다.

<br>

```java
public static char prime[] = new char[(LAST_NUM + 7) / 8 + 1];

public static boolean isPrime(int k) {
  return (prime[k >>> 3] & (1 << (k & 7))) == 0 ? false : true;
}

// 숫자 k가 소수가 아님을 마스킹(해당 비트에 0 설정)
public static void setComposite(int k) {
  prime[k >>> 3] &= ~(1 << (k & 7));
}

public static void eratosthenes() {
  java.util.Arrays.fill(prime, (char) 255); // 모든 비트를 1로 초기화
  setComposite(0); // 0과 1은 소수가 아님
  setComposite(1);
  int i, j;
  for (i = 2; i*i <= LAST_NUM; i++)
    if (isPrime(i))
      for (j = i*i; j <= LAST_NUM; j += i)
        setComposite(j);
}
```

<br>

<br>

### 각 방법의 시간복잡도 비교

> 숫자는 **10,000** 부터 **100,000,000 (1억)** 까지 10배씩 곱한 숫자를 대입하여 시간복잡도를 비교한다.
>
> (10,000 이전의 숫자는 크기가 작아 비교불가)
>
> 시간은 Java의 **System.*currentTimeMillis*()** 메소드를 활용하였으며, 
>
> print는 생략하였다.

#### > 10,000 ( 1만 )

![image](https://user-images.githubusercontent.com/46040293/103174490-f7417d00-48a5-11eb-9156-4703da53d955.png)

#### > 100,000 ( 10만 )

![image](https://user-images.githubusercontent.com/46040293/103174402-2b686e00-48a5-11eb-8ae1-18a961f49f00.png)

#### > 1,000,000 ( 100만 )

![image](https://user-images.githubusercontent.com/46040293/103174411-41762e80-48a5-11eb-95ff-635558e9ea11.png)

#### > 10,000,000 ( 1000만 )

![image](https://user-images.githubusercontent.com/46040293/103174426-623e8400-48a5-11eb-9d95-28f109d9e952.png)

#### > 100,000,000 ( 1억 )

![image](https://user-images.githubusercontent.com/46040293/103174473-ccefbf80-48a5-11eb-9431-877804bb7291.png)

<br>

### 결론

>1) 1만 단위에서는 차이가 거의 없으나 숫자가 커질 수 록 일반적인 방법과 **에라토스테네스 체의 방법** 차이가 커짐을 알 수 있었다.
>
>2) 1000만이 넘는 숫자에서는 에라토스테네스 체의 방법에서도 **비트마스크**를 활용하면 더욱 빠른 시간복잡도를 확인할 수 있다.
>
>수치는 환경에 따라 달라질 수 있기 때문에 대략적인 수치만 감안하면 좋을 것 같다.
