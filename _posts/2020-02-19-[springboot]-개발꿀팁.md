---
title: "[SpringBoot] 개발 꾸르팁 ( 작성중 )"
tags: "springboot"
---



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

##### application.properties

```
Spring.devtools.livereload.enabled=true
```

<br>

## Root-Path 설정

##### application.properties

```
server.servlet.context-path=/api
```

