---
title: "[React] 1. 개요 및 맛보기"
tags: "react"
---



#### 개요

+ React는 Facebook에서 제공해주는 Front-End Library 입니다.
+ React는 Component 기반으로 되어있어 Component에 데이터를 내려주면 개발자가 설계한대로 UI가 만들어져 사용자에게 보여집니다.

#### React를 왜 사용하나?

+ 리액트를 이용한다면 사용자와 상호작용할 수 있는 UI를 보다 쉽게 만들어 줄 수 있습니다.



#### 특징

+ Component
  + React는 Component 기반의 Library 입니다.
  + UI를 하나의 큰 덩어리라고 생각한다면 Component는 그 덩어리를 이루는 요소들이라고 생각하면 됩니다.
  + 이러한 특징 때문에 개발자는 전체 코드를 파악하기가 상대적으로 쉽습니다.
  + Component는 재사용성을 가지고 있기 때문에 반복적으로 같은 코드를 입력할 필요가 없습니다.
  + Component의 종류는 클래스형(Stateful)과 함수형(stateless) 으로 나누어집니다.

+ Unidirectional (단방향) 데이터플로우를 가지고 있다.
  + React는 데이터의 흐름이 한 방향으로 이루어집니다.
  + 데이터가 내려가기만 하지, 밑에서 데이터를 올려줄 수는 없습니다.
  + 부모의 데이터를 바꿔주기 위해서는 'State'를 이용해야 합니다.
+ Props and State
  + Props
    + parent component 에서 children component로 전달해 주는 데이터를 말합니다.
    + props는 읽기 전용 데이터라고 생각하면 됩니다.
    + children component에서 전달받은 props는 변경이 불가능하고, props를 전달해준 최상위 parent component 만 props를 변경할 수 있습니다.
  + State
    + state는 동적인 데이터를 다룰 때 사용.
    + 사용자와의 상호작용을 통해 데이터를 동적으로 변경해야할 때 사용.
    + State는 클래스형 컴포넌트에서만 사용할 수 있는데 각각의 state는 독립적이라 다른 컴포넌트의 직접적인 접근이 불가능합니다.
    + 그러나 자신보다 상위에 있는 state는 변경이 가능한데, state를 변경해주는 함수를 props로 받는다면 state 변경이 가능하다.
    + props로 넘겨줄 때 this의 binding을 신경써줘야 합니다.



+ Javascript 6 ( es6 : ECMAScript 6) 는 편리하고 유용한 기능이 많다.
  + 더 빠르고 편하고 이쁘게 사용할 수 있다.
  + 웹팩을 활용해서 최근 자바스크립트를 브라우저가 이해할 수 있게 변경해 줘야함.

<br>

### JSX

아래의 태그 문법은 문자열도, HTML도 아니다.

JSX라는 Javascript를 확장한 문법입니다.

```react
const element = <h1>Hello, world!</h1>;
```

<br>

### JSX에 표현식 포함하기

```react
const user = {
    firstName:"ShinJong",
    lastName:"Park"
}
const element = <h1>Hello, {user.firstName}</h1>;

ReactDOM.render(
  element,
  document.getElementById('root')
);
```

+ JSX의 중괄호 안에 유효한 모든 JavaScript 표현식을 넣을 수 있습니다.

+ 다음과 같이 if 구문 및 for loop 안에 사용할 수 있다.

```react
function getGreeting(user){
    if(user){
        return <h1>Hello, {user.firstName}</h1>
    }
    return <h1>HEllo, Stranger.</h1>
}
const element = getGreeting(user)
```

+ 중괄호를 사용하여 Attribute에 Javascript 표현식을 삽입할 수 있다.

```react
const element = <img src={user.avatarUrl}></img>
```

<br/>

#### JSX는 객체를 표현합니다.

+ Babel은 JSX를 React.createElement() 호출로 컴파일합니다.

아래의 두 예시는 동일합니다.

```react
const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);
```

```react
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);
```

React.createElement()는 버그가 없는 코드를 작성하는데 도움이 되도록 몇가지 검사를 수행하며, 기본적으로 다음과 같은 객체를 생성합니다.

```react
const element = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello, world!'
  }
};
```

이러한 객체를 "React Element"라고 하며, 이를 화면에 표시하려는 항목에 대한 설명이라고 생각할 수 있습니다.

React는 이러한 객체를 읽은 후 DOM을 구성하고 최신으로 유지하는데 이러한 객체를 사용합니다.

<br/>

#### DOM에 엘리먼트 렌더링하기

```html
<div id="root"></div>
```

이 안에 들어가는 모든 엘리먼트를 React DOM에서 관리하기 때문에 이것을 "루트(root)" DOM 노드라 부릅니다.

<br/>

React로 구현된 애플리케이션은 일반적으로 하나의 루트 DOM노드가 있습니다.

React를 기존 앱에 통합하려는 경우 원하는 만큼 많은 수의 독립된 루트 DOM노드가 잇을 수 있습니다.

<br/>

React 엘리먼트를 루트 DOM 노드에 렌더링하려면  ReactDOM.render()로 전달하면 됩니다.

```react
const element = <h1>Hello, world</h1>;
ReactDOM.render(
    element, 
    document.getElementById('root')
);
```

<br/>

#### 렌더링 된 엘리먼트 업데이트 하기

React 엘리먼트는 불변객체입니다. 앨리먼트를 생성한 이후, 해당 엘리먼트의 자식이나 속성을 변경할 수 없습니다.

따라서, UI를 업데이트하는 유일한 방법은 새로운 엘리먼트를 생성하고, 이를 ReactDOM.render()로 전달하는 것입니다.

<br/>

예시로 똑딱거리는 시계를 구현할 때,

```react
function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  ReactDOM.render(element, document.getElementById('root'));
}

setInterval(tick, 1000);
```

setInterval() 콜백을 이용해 초마다 ReactDOM.render()를 호출합니다.



※ 실제로 대부분의 React앱은 ReactDOM.render()를 한 번만 호출합니다.

<br/>

