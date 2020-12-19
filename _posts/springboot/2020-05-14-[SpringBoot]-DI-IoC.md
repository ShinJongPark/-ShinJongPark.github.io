---
title: "[Spring] DI 와 IoC Container"
tag: "SpringBoot"
author : ""
article_header:
  type: overlay
  theme: dark
  background_color: '#123'
  background_image: false
---
<br>
<br>
스프링이 가지고있는 가장 기본적인 역할, DI 와 IoC Container 에 대해 설명합니다.
<br>
# DI (Dependency Injection)

``DI``란 간단히 ``부품 조립``이라고 할 수 있으며, ``종속성 주입``의 의미를 가지고 있습니다

<br>

프로그램을 객체지향으로 만들게 될 경우에는 객체들의 조립관계를 통해 만들어 진다. 다음과 같은 두가지 형태로 구성할 수 있습니다.

### Composition has a ( 일체형 )

```java
class A {
	private B b;
	public A(){
		b = new B();
	}
}
```

"A가 B를 일체형으로 부품을 가졌다"라고 할 수 있으며, 부품은 dependency ( 종속성, 종속객체 ) 라고 할 수 있습니다.

### Association has a ( 조립형 )

```java
class A {
	private B b;
	public A(B b) {
        this.b = b;
    }
    public void setB(B b){
        this.b = b;
    }
}
```

부품을 갈아끼우거나 업데이트를 생각하는 경우가 많기 때문에, 일체형보다 조립형을 자주 사용하고있습니다.

Spring 에서는 기본적으로 부품들을 내가 원하는 방법으로 조립할 수 있게 해주는데, 이것을 DI(Dependency Injection), "부품들을 주입(조립)한다." 라고 표현할 수 있습니다.

DI는 생성자(Construction Injection) 또는 Setter(Setter Injection) 등을 통해 조립할 수 있습니다.

<br>

<br>

# IoC Container

**IoC ( Inversion Of Control )**, 제어의 역전의 의미를 가지며, 객체 또는 의존성을 관리하는 컨테이너입니다. 작성된 프로그램 또는 객체의 재사용 라이브러리의 흐름 제어를 받게 되는 **소프트웨어 디자인 패턴**을 말합니다.

부품을 구입해서 컨테이너에 넣을 것인데, Dependency Container 라고 하지않고, IoC Container 라고 할까? 바로, 작은 부품이 먼저 생성되고, 순차적으로 큰 부품이 만들어집니다. 

일체형으로 만들어진다면, 큰것을 만들었을 때 순차적으로 작은 부품이 만들어 질것이며,

조립형은 작은것부터 큰 부품으로 순차적으로 만들어집니다.



IoC Container 방식으로 서비스를 구현한다면, 서비스 개발 팀장이 기능에 대한 인터페이스를 정의하고, 각 개발 팀원들이 기능에 대한 객체를 생성하여 주입(Injection)하여 서비스를 완성합니다.

<br>

설계 목적상 제어 반전(IoC)의 목적은 다음과 같습니다.

- 작업을 구현하는 방식과 작업 수행 자체를 분리한다.
- 모듈을 제작할 때, 모듈과 외부 프로그램의 결합에 대해 고민할 필요 없이 모듈의 목적에 집중할 수 있다.
- 다른 시스템이 어떻게 동작할지에 대해 고민할 필요 없이, 미리 정해진 협약대로만 동작하게 하면 된다.
- 모듈을 바꾸어도 다른 시스템에 부작용을 일으키지 않는다.



