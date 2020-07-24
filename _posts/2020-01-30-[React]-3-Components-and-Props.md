---
title: "[React] 3. Components and Props"
tags: "React"
author : ""
article_header:
  type: overlay
  theme: dark
  background_color: '#123'
  background_image: false
---

<br>

<br>

컴포넌트를 통해 UI를 재사용 가능한 개별적인 여러 조각으로 구성하기 때문에 개발자는 더욱 편리하고 전체코드를 쉽게 확인 할 수 있습니다.

<br>

## 1. 함수 컴포넌트와 클래스 컴포넌트

컴포넌트를 정의하는 가장 간단한 방법은 JavaScript 함수를 작성하는 것 입니다.

```react
function Welcome(props){
	return <h1>Hello, {props.name}</h1>;	
}
```

이 함수는 데이터를 가진 하나의 "props" 객체 인자를 받은 후 react 엘리먼트를 반환하므로 유효한 React 컴포넌트입니다. 이러한 컴포넌트는 JavaScript 함수이기 때문에 말 그대로 "함수 컴포넌트" 라고 호칭합니다.

또한 ES6 class를 사용하여 컴포넌트를 정의할 수 있습니다.

```react
class Welcome extends react.Compoenet{
    render(){
        return <h1>Hello, {this.props.name}</h1>
    }
}
```

React 관점에서 두 유형의 컴포넌트는 동일합니다.

<br>

<br/>

## 2. 컴포넌트 렌더링

이전까지는 React 엘리먼트를 DOM 태그로 나타냈습니다.

```react
const element = <div />;
```

React 엘리먼트는 사용자 정의 컴포넌트로도 나타낼 수 있습니다.

```react
const element = <Welcome name="Sara" />;
```

React가 사용자 정의 컴포넌트로 작성한 엘리먼트를 발견하면 JSX 어트리뷰트를 해당 컴포넌트에 단일 객체로 전달합니다. 이 객체를 ```Props``` 라고 합니다.

<br/>

다음은 페이지에 "Hello,Sara"를 렌더링하는 예시입니다.

```react
function welcome(props){
    return <h1>Hello, {props.name}</h1>
}

const element = <Welcome name="Sara" />;

ReactDOM.render(
	element,
    document.getElementById('root')
);
```

+ 컴포넌트의 이름은 항상 대문자로 시작합니다.

  +  React는 소문자로 시작하는 컴포넌트를 DOM 태그로 처리합니다.
+  <div />는 HTML div 태그를 나타내지만, <Welcome /> 은 컴포넌트를 나타내며 범위안에 Welcome이 있거나 import 시켜야 합니다.

<br>

<br>

## 3. 컴포넌트 합성

컴포넌트는 자신의 출력에 다른 컴포넌트를 참조할 수 있습니다, 이는 모든 세부 단계에서 동일한 추상 컴포넌트를 사용할 수 있음을 의미합니다.

React 앱에서는 버튼, 폼, 다이얼로 그 화면 등의 모든것들이  흔히 컴포넌트로 표현됩니다.

```react
function Welcome(props){
    return <h1>Hello, {props.name}</h1>
}

function App(){
    return(
        <div>
        	<Welcome name="Sara" />
            <Welcome name="Cahal" />
            <Welcome name="Edite" />
        </div>
    );
}

ReactDOM.render(
	<App />,
    document.getElementById('root')
);
```

일반적으로 새 React 앱은 최상위에 단일 app 컴포넌트를 가지고 있습니다. 하지만 기존 앱에 React를 통합하는 경우네는 Button 과 같은 작은 컴포넌트부터 시작해서 뷰 계층의 상단으로 올라가면서 점진적으로 작업해야 할 수 있습니다.

</br>

<br>

## 4. 컴포넌트 추출

컴포넌트를 여러 개의 작은 컴포넌트로 나누는 것을 두려워 하지 마세요.

다음 Comment 컴포넌트를 살펴봅시다.

```react
function Comment(props){
    return(
        <div className="Comment">
        	<div className="UserInfo">
            	<img className="Avatar"
                    src={props.author.avatarUrl}
                    alt={props.author.name}
                />
                <div className="UserInfo-name">
                	{props.author.name}
                </div>
            </div>
            <div className="Comment-text">
            	{props.text}
            </div>
            <div className="Comment-date">
            	{formateDate(props.date)}
            </div>
        </div>
    );
}
```

이 컴포넌트에서 몇 가지 컴포넌트를 추출하겠습니다.

```react
function Avatar(props){
    return (
        <img className="Avatar"
            src={props.user.avatarUrl}
            alt={props.user.name}
        />
   	)
}
```

Avatar 는 자신이 Comment 내에서 렌더링 된다는 것을 알 필요가 없습니다. 따라서 props의 이름을 author에서 더욱 일반화된 user로 변경하였습니다.

props의 이름은 사용돌 context가 아닌 커포넌트 자체의 관점에서 짓는 것을 권장합니다.

이제 Comment가 살짝 단순해졌습니다.

```react
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <Avatar user={props.author} />
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

다음은 Avatar 상위에 사용자 이름을 렌더링 하는 UserInfo 컴포넌트를 추출합니다.

```react
function UserInfo(props){
    return (
    	<div className="UserInfo">
        	<Avatar user={props.user} />
            <div className="UserInfo-name">
            	{props.user.name}
            </div>
        </div>
    )
}
```

</br>

Comment 컴포넌트가 더욱 단순해졌습니다.

```react
function Comment(props) {
  return (
    <div className="Comment">
      <UserInfo user={props.author} />
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

컴포넌트를 추출하는 작업은 다소 지루할 수 있습니다. 하지만 재사용 가능한 컴포넌트를 만들어 놓는 것은 더 큰 앱에서 작업할 때 두각을 나타냅니다.

UI 일부가 여러번 사용되거나 ( Button, Panel, Avatar ), UI 일부가 자체적으로 복잡한 (App, FeedStory, Comment ) 경우에는 자새용 가능한 컴포넌트로 만드는 것이 좋습니다.

<br/>

<br/>

## 5. Props 는 읽기 전용입니다.

함수 컴포넌트나 클래스 컴포넌트 모두 컴포넌트의 자체 props를 수정해서는 안 됩니다.

```react
function sum(a,b) {
	return a+b;
}
```

이런 함수는 ```"순수 함수"``` 라고 호칭합니다. 입력값을 바꾸려하지 않고 항상 동일한 입력값에 대해 동일한 결과를 반환하기 때문입니다.

반면에 다음 함수는 자신의 입력값을 변경하기 때문에 `순수함수`가 아닙니다.

```react
function withdraw(account, amount){
	account.total -= amount;
}
```

React 는 매우 유연하지만 한 가지 엄격한 규칙이 있습니다.

모든 React 컴포넌트는 자신의 props를 다룰 때 반드시 순수함수처럼 동작해야 합니다.

물론 애플리케이션 UI는 동적이며 시간에 따라 변합니다.

React 컴포넌트는 State를 통해 위 규칙을 위반하지 않고 사용자 액션, 네트워크 응답 및 다른 요소에 대한 응답으로 시간에 따라 자신의 출력값을 변경 할 수 있습니다.

