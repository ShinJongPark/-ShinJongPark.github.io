title: "[Vue.js] 개발 꾸르팁 ( 작성중 )"
tags: "vue.js"



## import alias @

vue-cli 2.x 에서는 webpack.config.js(웹팩 설정파일) 에서 @를 사용하는 경로가 정의되어 있습니다.

따라서 다음과 같이 @를 통한 단축 경로를 사용할 수 있습니다.

```vue
import Main from '@/views/components/Main.vue'
```

다만, vue cli 3.x 버전 이상(2020.01.04 기준 4.x 버전) 에서는 webpack.config.js가 없어졌습니다.

그래서 @ 단축경로도 사라졌습니다....

<br>

하지만..?

vue.config.js 파일을 생성하여 다음과 같이 alias 경로를 적습니다.

```vue
#vue.config.js
const path = require('path');

module.exports = {
    configureWebpack: {
        resolve: {
            alias: {
                '@': path.join(__dirname, 'src/')
            }
        }
    }
}
```

#### vue.config.js 에 대해서..

- 루트 디렉토리(package.json 옆)에 vue.config.js를 생성하면 vue-cli가 파일을 자동으로 로드합니다.

- package.json 의 vue 필드에 설정 값을 적을 수 있지만, 웬만하면 vue.config.js에 적습니다.

<br>

<br>

## 인증한 유저만 접근할 수 있는 기능 ( router )

인증한 유저만 접근할 수 있는 Admin 페이지를 만들어 보자.

vue-router에는 **beforeEnter** 라는 인터셉터가 있는데 라우팅 직전에 실행되는 함수이다.

인터셉터 로직에 따라 라우팅을 계속 수행하거나 말거나 할 수 있다.

requireAuth() 함수를 추가해서 인증 여부에 따라 /Admin 라우팅을 결정한다.

```Vue
# router/index.js

const requireAuth = () => (from, to, next) => {
	const isAuthenticated = false
	if (isAuthenticated) return next()
	next('/') // 인증되지 않았을 때 Main 페이지로 넘어간다.
}

export default new Router({
	{
		path: '/admin',
		name: 'Admin',
		components: 'Admin',
		beforeEnter: requireAuth()
	}
})
```

