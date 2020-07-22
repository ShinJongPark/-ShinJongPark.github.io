---
title : "[Java] Bitwise Operators"
tags : "java"
---





Bitwise operation is performed by splitting data into bits. For data, only data that can be represented by 0 and 1 can be operated.

and Bitwise operation include **bitwise shift operators** and **bitwise logical operator** depending on the function.

<br>

<br>

비트 연산자는 데이터를 비트 단위로 쪼개어 연산합니다. 데이터는 0 과 1로 표현할 수 있는 데이터만을 연산할 수 있습니다. 비트 연산은 기능에 따라서 **비트 이동 연산자** 와 **비트 논리 연산자**로 나뉩니다.



<br>

<br>

## 비트 이동 연산자 ( Bitwise Shift Operator )

비트 이동 연산자는 정수 데이터를 비트로 전환  후 오른쪽 또는 왼쪽으로 이동시는 연산을 말한다.

( 다음 예시는 정수 데이터를 **8비트**로 연산하는 과정입니다. )

- Bitwise Left-Shift Operation
  - 2 << 3
  - 2의 비트에서 왼쪽으로 세칸 이동시키고, 이동된 오른쪽 공간은 0으로 채웁니다.
  - 고로 답은 **2 << 3** 은 0000 0010 => 0001 0000 으로 연산되어 **16**
- Bitwise Right-Shift Operation
  - 32 >> 3
  - 32의 비트에서 오른쪽으로 세칸 이동시키고, 이동된 왼쪽 공간은 **최상위 부호비트**로 채워집니다.
  - 32 >> 3 은 0010 0000 => 0000 0100 => **4**
  - -32 >> 3 은 1110 0000 => 1111 1100 => **-4** 
  - '>>'은  signed right shift 
- Bitwise Unsigned Right-Shift Operation
  - -32 >>> 3
  - 자바에만 해당되며, **최상위 부호비트 관계없이** 이동된 공간은 0으로 채워집니다.
  - 1110 0000 => 0001 1100 => **28**

<br>

<br>

## 비트 논리 연산자 ( Bitwise Logical Operator )

<br>

- **Bitwise OR (** **l )**
  - `논리합` 이라고 하며, 2진수로 표현된 비트중 1의 갯수가 1개 이상일 때 1을 리턴합니다.
  - 3 | 13 == 15
  - 3 : 0000 0011
  - 13 : 0000 1101
  - 15 : 0000 1111
- **Bitwise AND ( & )**
  - `논리곱` 이라고 하며, 2진수로 표현된 2개의 비트가 같으면 1을 리턴, 다르면 0을 리턴합니다.
  - 3 & 13 == 1
  - 03 : 0000 0011
  - 13 : 0000 1101
  - 01: 0000 0001
- **Bitwise XOR ( ^ )**
  - `배타적 논리합` 이라고 하며, 2진수로 표현된 2개의 비트가 다르면 1을 리턴, 같으면 0을 리턴합니다.
  - 3 & 13 == 14
  - 03 : 0000 0011
  - 13 : 0000 1101
  - 14 : 0000 1110
- **Bitwise Complement ( ~ )**
  - `논리부정` 이라고 하며, 2진수로 표현된 비트 값을 반전(보수)시켜 표현합니다.
  - 13 : 0000 1101
  - ~13 : 1111 0010 
  - 논리부정은 1의 보수를 취해주기 때문에,
  - **~13 : -14**

<br>

<br>

<br>

<br>

<br>