---
title: "MacOS backquote(`) 설정하기"
tag: "etc"
author : ""
article_header:
  type: overlay
  theme: dark
  background_color: '#123'
  background_image: false
---



# Mac backquote 설정하기 ( ₩ -> `)

첫 Mac에서 markdown글을 작성하면서 backquote (`) 가 입력이 안되는 현상이 있어 다급하게 검색하였습니다. Markdown을 사용하는 개발자들이라면 매우 불편할 것으로 예상됩니다 ㅠ..ㅜ

<br>

### 원인은..

`MacOS` 의 버전이 `Sierra`로 올라가며 한글키보드에서는 `backquote(')` 가 기본적으로 `₩` 으로 입력되도록 바뀌었다고 합니다..

<br>

`간단한`설정을 하게되면

### 결과적으로

- 한글일 때, ₩

- 영문일 때, ` 를 사용할 수 있습니다.



## 방법

```shell
cd ~/Library
mkdir KeyBindings
cd KeyBindings
vi DefaultKeyBinding.dict
```

vi 편집기를 열어서 아래의 코드를 추가

```
#DefaultKeyBinding.dict
{
	"₩" = ("insertText:", "`");
}
```



<br>

<br>



