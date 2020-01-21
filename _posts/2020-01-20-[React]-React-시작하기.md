---
title: "[React] 2. React 시작하기"
tags: "react"
---





React 개발 환경 구축을 위해 개념들을 하나씩 보도록 하겠습니다.

<br>

<br>

### 1. 번들러란 ? ( Bundler )

번들러(Bundler)란 **묶는다**는 뜻의 **Bundle**에서 나타난 말인데요.

파일을 묶듯이 연결하는 역할을 합니다.

<br>

대표적인 번들러로 웹팩(Webpack), Parcel, Browserify 라는 도구들이 있으며, 리액트에서는 주로 웹팩을 사용하는 추세입니다. 

편의성과 확장성이 다른 도구보다 뛰어나기 때문입니다.

번들러 도구를 사용하면 (import, require)로 모듈을 불러왔을 때, 불러온 모듈을 모두 합쳐서 하나의 파일을 생성합니다. 또, 최적화 과정에서 여러 개의 파일로 분리될 수도 있습니다.

<br>

프로젝트에서 index.js를 시작으로 필요한 파일을 다 불러와서 번들링하게 됩니다.

<br>

### 2. Loader

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

<br>

웹팩의 로더는 원래 직접 설치하고 설정해야 하지만 리액트 프로젝트를 만들 때 사용했던 create-react-app(CRA)이 번거로운 작업을 모두 대신 해주기 때문에 우리는 별도의 설정을 할 필요가 없습니다.

<br><br><br>

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

<br>

### 3. JSX 란?

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

<br>

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


이 코드는 컴포넌트를 페이지에 렌더링하는 역할을 하며, react-dom 모듈을 불러와 사용할 수 있습니다.<br> 첫번째 파라미터에는 렌더링 할 내용을 JSX 형태로 작성하고, 두번째 파라미터는 렌더링 할 document 내부 요소를 설정합니다.<br> 여기서는 id가 root인 요소 안에 렌더링을 하도록 설정했는데, public/index.html 파일을 열어보면 확인할 수 있습니다.


<br><br>



