```
title: "[SpringBoot] 개발 꾸르팁 ( 작성중 )"
tags: "springboot"
```


# Spring Boot properties



## 자동 리로드

##### dependency

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <optional>true</optional>
</dependency>
```
Eclipse 인경우 Project - Build Automatically 체크한다.
저장할 때, java파일을 class파일로 자동저장한다.


##### application.properties
다음 설정은 default가 true이기 때문에, 안해줘도 되지만, 자동리로드를 멈추고 싶다면 false로 설정해주면 된다.
```
Spring.devtools.livereload.enabled=true
```


<br>

<br>

## Root-Path 설정

##### application.properties

```
server.servlet.context-path=/api
```

<br><br>

## Swagger2



<br>

<br>

## 이미지 절대 경로 지정

<br>

<br>

## Naming



<br><br>

## Multiple Database

한 프로젝트에 두개의 데이터베이스 연결하기

<br>

<br>

## Domain Mapping







