---
layout : article
title : "[Spring boot] Failed to load driver class"
author : ""
tags : "History"
article_header:
  type: overlay
  theme: dark
  background_color: '#123'
  background_image:
    gradient: 'linear-gradient(135deg, rgba(34, 139, 87 , .4), rgba(139, 34, 139, .4))'
    src: /assets/images/logo/background_Java.jpg
---

<br/>

Spring Boot 취약점 이슈로 tomcat 업그레이드 하려다 발생한 에러..

잘 동작하던 어플리케이션이 갑자기 에러나서 당황스러웠다.

<br/>
<br/>

```
Failed to bind properties under '' to com.zaxxer.hikari.HikariDataSource:


    Property: driver-class-name
    Value: com.mysql.cj.jdbc.Driver
    Origin: "driverClassName" from property source "source"
    Reason: Failed to load driver class com.mysql.cj.jdbc.Driver in either of HikariConfig class loader or Thread context classloader


```

<br>

2시간 뻘짓 이후...

<br>

프로젝트 마우스 우클릭 후 **reload from disk** 로 해결하였다.

<br>

<br>

<br>

