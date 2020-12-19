---
title : "[SpringBoot] 자동 리로드 ( Livereload, Auto Reload ) "
author : ""
tags : "SpringBoot"
article_header:
  type: overlay
  theme: dark
  background_color: '#123'
  background_image:
    gradient: 'linear-gradient(135deg, rgba(34, 139, 87 , .4), rgba(139, 34, 139, .4))'
    src: /assets/images/logo/background_Java.jpg
---



## 자동 리로드 ( Auto Reload )

> 다음과 같이 디펜던시를 추가한다.

<br>

### dependency

``` java
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <optional>true</optional>
</dependency>
```

>  Eclipse 인경우 Project - Build Automatically 체크한다. 
>  저장할 때, java파일이 class파일로 자동저장된다.

<br>

### application.properties

>  다음 설정은 default가 true이기 때문에, 안해줘도 되지만, 자동리로드를 멈추고 싶다면 false로 설정해주면 된다.

``` java
spring.devtools.livereload.enabled=true
```

<br>

<br>

<br>

<br>