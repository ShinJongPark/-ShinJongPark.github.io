---
title: "[React] 2. React 시작하기"
tags: "react"
---



## 1. Getting Start

서론은 거두절미 하고 React 앱 생성부터 시작하도록 하겠습니다.

<br>

create-react-app 은 이름과 같이, React 앱을 만들어주는 도구입니다. 터미널에 다음과 같이 CRA(Create React App)를 설치합니다.

```shell
npm install -g create-react-app
npx create-react-app react-base
```

<br>

---

####  > npx란, 

npx는 npm >= 5.2.0 에서 사용할 수 있는 패키지 매니저입니다.

npm의 경우, -g 옵션을 통해 같은 모듈을 공유해서 사용할 수 있지만, 최신 버전으로 재설치 하지않으면 모듈의 업데이트 상태를 확인할 수 없습니다.

업데이트를 진행 했을 때 변동사항이 생겨 다른 프로젝트에도 영향을 끼칠 수 있습니다.

npx는 모듈을 로컬에 저장하지 않고, 매번 최신 버전의 파일을 임시로 불러와 실행 시킨 후, 다시 그 파일은 없어지는 방식으로 모듈이 작동하고 있습니다.

따라서 CRA와 같은 보일러 플레이트 모듈에 효과적입니다. CRA를 설치할 때 마다 매번 최신 버전만 가져와서 설치해 주기 때문에 지금 어떤 버전을 사용하고 있는지 신경 쓸 필요가 없습니다.

---

<br>

<br>

## 2. Directory Structure

CRA 후 생성된 프로젝트입니다.

```
my-app/
  README.md
  node_modules/
  package.json
  public/
    index.html
    favicon.ico
  src/
    App.css
    App.js
    App.test.js
    index.css
    index.js
    logo.svg
```

위와 같은 구조로 생성되며, 

```public/index.html``` 는 페이지 템플릿,

```src/index.js``` 는 JavaScript 시작점입니다.



Webpack은 빠른 처리를 위해 ```/src``` 하위 폴더에만 작업에 관여합니다.

따라서 JS나 CSS와 같은 파일은 ```/src``` 폴더 하위에 위치하는 것이 올바릅니다.







