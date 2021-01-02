---
layout : article
title : "[Java] Java, JVM 원리"
author : ""
tags : "Java"
article_header:
  type: overlay
  theme: dark
  background_color: '#123'
  background_image:
    gradient: 'linear-gradient(135deg, rgba(34, 139, 87 , .4), rgba(139, 34, 139, .4))'
    src: /assets/images/logo/background_Java.jpg
---

<br/>

> Java가 어떻게 동작하는지 개념과 원리를 좀 더 잡아보자.

<br/>
<br/>

## ㅣ. 개요

> C/C++, Java, Python 등 사람이 작성하고 이해할 수 있는 언어를 고급언어라고 일컫는다. 
>
> 컴퓨터는 0, 1로 이루어진 기계어만을 이해할 수 있는데, 고급언어를 기계어로 변환하는 것을 컴파일(Compile)이라 하며, 이 작업을 할 수 있게 하는 것을 컴파일러(Compiler)라 한다.
>
> <br>
>
> 즉, 내가 작성한 소스를 컴퓨터에서 실행하기 위해서는 컴파일을 꼭 해주어야 한다.
>
> <br>
>
> 언어마다 작성한 소스코드를 기계어로 변환시키는 방법이 조금씩 다른데,

> C/C++ 는 **각각의 OS ( Windows, Linux, Mac OS 등) 컴파일러**를 통해 **각각의 다른 0,1 바이너리 코드**를 읽어 **동일한 결과값**을 얻을 수 있다.
>
> <br>
>
> 반면, Java는 조금 다른데,
>
> Java 는 **하나의 Java 컴파일러**를 통해 **동일한 0,1의 바이트 코드**를 생성한다. (.java 에서 .class 파일로 컴파일 되는 작업)
>
> 컴파일 된 바이트 코드를 **각각 OS에 해당하는 JVM**이 해석하여 **동일한 결과값**을 얻는다.
>
> 즉, C/C++은 OS마다 다른 바이너리 코드를 읽어내지만,  Java는 OS의 관계없이 동일한 바이트 코드를 만들어 실행할 수 있다.
>
> 하지만 컴파일되어 바로 실행되는 C/C++에 비해 속도측면에서는 단점이 될 수 있겠다.
>
> Java는 이를 극복하기 위해 JIT(Just In Time) 방식을 사용한다. JIT는 자주 사용하는 코드를 기계어로 미리 변환하여 저장하였다가, 재사용하는 방식을 말한다.

<br>

### * 기계어, 바이너리 코드, 바이트 코드 차이

> 간단하게 설명하면, 
>
> **기계어**는 0,1 이진코드로 이루어져 있으며, CPU마다 기계어가 다르다.
>
> 보통 .exe 실행파일을 기계어라 할 수 있다.
>
> **바이너리 코드** 역시 0,1 이진코드로 이루어져 있지만, 기계어와는 다르다. 소스 파일을 오브젝트 파일로 변환한 것을 바이너리 코드라고 하며, 완전한 기계어가 아니다. 변환된 바이너리 코드는 **링커**를 통해 실행파일(.exe), 즉 기계어가 된다.
>
> ( 보통 컴파일 과정을 compiling +  Linking 을 일컫는다. )
>
> **바이트 코드** 역시 0,1 이진코드로 구성되어있으며, 바이너리 코드와 다르게 CPU가 이해할 수 없고, **가상머신**에서 이해할 수 있는 코드이다.

<br>

<br>

## ll. JVM ( Java Virtual Machine )

> Java는 하나의 컴파일러로 동일한 바이트 코드(.class)를 생성한다.
>
> 바이트 코드는 중간 단계의 코드이기 때문에 해석하고 실행할 수 있는 가상의 운영체제가 필요하다. 이것이 자바 가상 기계(JVM)이다. 
>
> JVM은 실 운영체제를 대신하여 자바 프로그램을 실행하는 가상 운영체제 역할을 한다.
>
> 운영체제별로 프로그램을 실행하고 관리하는 방법이 다르기 때문에 중간에 JVM을 두어 OS에 상관없이 개발할 수 있다.
>
> <br>
>
> 바이트 코드는 모든 JVM에서 동일한 결과를 보장하지만, OS에 종속적이다. 
>
> 따라서 운영체제에 맞는 JVM을 설치해야 한다.
>
> <br>
>
> JVM은 JDK(Java Development Kit) 또는 JRE(Java Runtime Enviroment)를 설치하면 자동으로 설치되는데 JDK, JRE는 운영체제별 제공된다.
>
> JDK 와 JRE 모두 JVM과 라이브러리 API를 제공하지만 JDK에 이름에 맞게 컴파일러와 같은 개발도구가 추가로 포함되어있다. 
>
> 즉, JVM < JRE < JDK 순으로 추가 기능을 포함하고 있다.
>
> 프로그램 실행만 하고자 하면 JRE, 빌드까지 할 경우 JDK를 사용하면 되겠다.
>
> 그냥 JDK를 설치하여 사용하자.

<br>

> 보통 Java 버전을 JDK 버전으로 생각하면 된다.
>
> JDK는 오라클에서 무료로 설치할 수 있으며, JDK 8 부터 람다를 지원하며 JDK11에 처음 LTS를 지원한다.
>
> LTS는 장기 지원 버전으로써, 안정성이 있으며 해당 버전을 사용할 것을 권장한다. ( JDK 8도 LTS인줄 알았다 ㅎ; )

<br>

> Windows 에서 jdk를 설치한다면 어디서든 java를 실행할 수 있게 환경설정을 해두자.
>
> 설정방법은 시스템 환경변수를 추가/수정 해주면 되는데, 이 부분은 생략 ( 자료가 많다. )
>
> 설치하면 기본위치는 윈도우 기준으로 `'C:\Program FIles\Java'` 인데 jdk를 설치하면 jre도 함께 설치되어 있는 것을 볼 수 있다(11버전부터 정책이 변경되어 jre는 나오지 않는다. [JDK 11 Release](https://www.oracle.com/java/technologies/javase/jdk-11-relnote.html)).
>
> Mac OS 는 `'라이브러리\Java\JavaVirtualMachines'` 이다.
>
> <br>
>
> JDK 내부의 bin 폴더를 열어보면 **javac.exe(컴파일러)** 와 **java.exe(JVM 구동 명령어)** 가 포함되어 있는 것을 볼 수 있따.

<br>

<br>

## lll. 소스 작성부터 실행까지

> 자바 프로그램을 개발하려면 다음과 같은 순서로 진행해야 한다.
>
> 1. Java 소스 작성(.java)
> 2. 컴파일러(javac.exe)로 바이트 코드 파일(.class) 작성
> 3. JVM 구동 명령어(java.exe) 실행
>
> <br>
>
> Hello.java 파일을 작성하고, javac.exe(컴파일러)로 컴파일 한다.
>
> ```shell
> javac Hello.java
> ```
>
> Hello.class 바이트 코드가 생성되며, java.exe(JVM 구동 명령어)로 실행한다.
>
> 주의할 점은 java.exe 로 실행할 때, class 파일의 확장명을 제외하여야 한다.
>
> ```shell
> java Hello
> ```
>
> java.exe 명령어가 실행되면 JVM은 바이트 코드 파일(Hello.class)을 메모리에 로드하고, 최적의 기계어로 번역한다.
>
> 그리고 `main()`메소드를 찾아 실행시킨다.

<br>

<br>

> by 
>
> 이것이 자바다 ( 한빛 미디어 ) - 신용권
>
> https://jojuim.tistory.com

<br>

<br>



