---
title: "[React] 1. 개요 및 맛보기"
tags: "react"
---

### 1. 개요

+ React는 Facebook에서 제공해주는 Front-End Library 입니다.
+ React는 Component 기반으로 되어있어 Component에 데이터를 내려주면 개발자가 설계한대로 UI가 만들어져 사용자에게 보여집니다.

#### > React를 왜 사용하나?

+ 리액트를 이용한다면 사용자와 상호작용할 수 있는 UI를 보다 쉽게 만들어 줄 수 있습니다.

<br>

#### > 특징

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

<br>

### 2. JSX

JSX는 자바스크립트의 확장 문법이며, XML과 매우 흡사합니다.

이런식으로 작성된 코드는 브라우저에서 실행되기 전에 코드가 번들링되는 과정에서 바벨을 사용하여 일반 자바스크립트 형태의 코드로 변환됩니다.

```react
function App(){
	return {
		<div>
            Hello <b> react </b>
        </div>
	}
}
```

위의 코드는 다음과 같이 변환됩니다.

```react
function App(){
    return React.createElement("div", null, "hello", React.createElement("b",null,"react"));
}
```

만약 컴포넌트를 렌더링할 때마다 JSX 코드를 작성하는 것이 아니라 위 코드처럼 매번 React.createElement() 함수를 사용해야 한다면 매우 불편할 것 입니다.

JSX를 사용하면 매우 편하게 UI를 렌더링할 수 있습니다.

<br>

#### >  JSX에 표현식 포함하기

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

#### > JSX는 객체를 표현합니다.

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

### 3. DOM에 엘리먼트 렌더링하기

```html
<div id="root"></div>
```

이 안에 들어가는 모든 엘리먼트를 React DOM에서 관리하기 때문에 이것을 "루트(root)" DOM 노드라 부릅니다.

<br/>

React로 구현된 애플리케이션은 일반적으로 하나의 루트 DOM노드가 있습니다.

React를 기존 앱에 통합하려는 경우 원하는 만큼 많은 수의 독립된 루트 DOM노드가 있을 수 있습니다.

<br/>

React 엘리먼트를 루트 DOM 노드에 렌더링하려면  ReactDOM.render()로 전달하면 됩니다.

```react
src/index.js

import React from 'react';
import ReactDom from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

ReactDOM.render(<App />, document.getElementById('root'));

serviceWorker.unregister();
```

#### > ReactDOM.render ?

```
이 코드는 컴포넌트를 페이지에 렌더링하는 역할을 하며, react-dom 모듈을 불러와 사용할 수 있습니다. 첫번째 파라미터에는 렌더링 할 내용을 JSX 형태로 작성하고, 두번째 파라미터는 렌더링 할 document 내부 요소를 설정합니다. 여기서는 id가 root인 요소 안에 렌더링을 하도록 설정했는데, public/index.html 파일을 열어보면 확인할 수 있습니다.
```

<br>

#### > 렌더링 된 엘리먼트 업데이트 하기

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

<br>

※ 실제로 대부분의 React앱은 ReactDOM.render()를 한 번만 호출합니다.

<br/>

React 개발 환경 구축을 위해 개념들을 하나씩 보도록 하겠습니다.

<br>

<br>

### 4. 번들러란 ? ( Bundler )

번들러(Bundler)란 **묶는다**는 뜻의 **Bundle**에서 나타난 말인데요.

파일을 묶듯이 연결하는 역할을 합니다.

<br>

대표적인 번들러로 웹팩(Webpack), Parcel, Browserify 라는 도구들이 있으며, 리액트에서는 주로 웹팩을 사용하는 추세입니다. 

편의성과 확장성이 다른 도구보다 뛰어나기 때문입니다.

번들러 도구를 사용하면 (import, require)로 모듈을 불러왔을 때, 불러온 모듈을 모두 합쳐서 하나의 파일을 생성합니다. 또, 최적화 과정에서 여러 개의 파일로 분리될 수도 있습니다.

<br>

프로젝트에서 index.js를 시작으로 필요한 파일을 다 불러와서 번들링하게 됩니다.

<br>

### 5. Loader

```react
import logo from './logo.svg';
import './App.css'
```

웹팩을 사용하면 SVG 파일과 CSS 파일도 불러와서 사용할 수 있습니다.

이렇게 파일을 불러오는 것은 웹팩의 **로더(loader)**라는 기능이 담당합니다.

css-loader 는 css파일을, file-loader는 웹 폰트나 미디어 파일들을 불러올 수 있게 해줍니다.

**babel-loader**는 자바스크립트 파일들을 불러오면서 최신 자바스크립트 문법으로 작성된 코드를 바벨이라는 도구를 사용하여 **ES5** 문법으로 변환해 줍니다.

<br>

<br>

웹팩의 로더는 원래 직접 설치하고 설정해야 하지만 리액트 프로젝트를 만들 때 사용했던 create-react-app(CRA)이 번거로운 작업을 모두 대신 해주기 때문에 우리는 별도의 설정을 할 필요가 없습니다.

<br><br>

```react
function App(){
    return {
        <div className="App">
        	<header className="App-header">
            	<img src={logo} className="App-logo" alt="logo" />
                <p>Edit
                </p>
            </header>
			<a className="App-link"
            	cl
                >
                
                
            </a>        
        </div>
    }
}
```

<br>

<br>