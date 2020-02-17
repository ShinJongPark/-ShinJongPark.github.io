---
title: "AWS(Ubuntu 18.04.1 LTS)에 Nginx + Vue.js + Spring Boot 배포하기 with SSL"
tag: "aws"
---





# 1. NginX 설치 및 vue.js 배포하기

### 1) NginX 설치

**nginx 설치**

```shell
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install nginx
```

### 2) conf 파일 설정

$ cd /etc/nginx/sites-availables/

**![img](https://user-images.githubusercontent.com/46040293/74617570-3294fa80-5171-11ea-8426-cc966326dbf4.png)**

다음과 같이 수정합니다

![img](https://user-images.githubusercontent.com/46040293/74617585-43de0700-5171-11ea-8dc7-cdf94e3962e6.png)

<br>

### 3) 웹서버(Nginx)에 vue.js 소스 올리기

\>npm run build 한 vue.js의 dist 폴더를 아래의 경로에 넣어줍니다

$ cd /var/www/html/

\>   /var/www/html/dist

<br>

### 4) nginx 실행

**nginx 실행**

```shell
$ sudoservice nginx start     #(restart/reload/stop/force-reload)
```



**이미 실행중이라면 restart**

```shell
$ sudoservice nginx restart   #(restart/reload/stop/force-reload)
```

<br>

### 5) 상태확인

**상태확인**

```
$ service nginx status 
or 
$ systemctl status nginx
```



![img](https://user-images.githubusercontent.com/46040293/74617593-4cced880-5171-11ea-846f-81684765b7c4.png)

## **6) 배포완료 ( SSL 적용 이전 )**

![img](https://user-images.githubusercontent.com/46040293/74617606-5c4e2180-5171-11ea-833b-d73ce97a1f22.png)

<br>

<br>

# 2. SSL 적용(HTTPS 설정하기) 및SpringBoot proxy 설정

### 1) letsencrypt 설치하기

```shell
$ sudo apt-get update -y & sudo apt-get install letsencrypt -y
```

<br>

### 2) nginx 중지

인증서 발급을 위해 실행중인 nginx service를 잠시 중지 시킵니다.

```shell
$ sudo systemctl stop nginx
```

\> 80포트 사용중이면 에러

![img](https://user-images.githubusercontent.com/46040293/74617607-5d7f4e80-5171-11ea-83c0-88d25222165c.png)

<br>

### 3) 인증서 발급

```
$ sudo letsencrypt certonly --standalone -d [도메인 네임]
ex)$ sudo letsencrypt certonly --standalone -d i02ast5.p.ssafy.io
```

정상적으로 발급되었다면 다음과 같은 축하글과 인증서 키값들을 얻을 수 있다.

![img](https://user-images.githubusercontent.com/46040293/74617608-5e17e500-5171-11ea-9b14-aac6818530d1.png)

<br>

### 4) nginx 설정파일 수정

![img](https://user-images.githubusercontent.com/46040293/74617609-5e17e500-5171-11ea-9cf6-5f00b628007d.png)

① 80포트로 진입했을 때 443포트로 리다이렉트 시켜줍니다.

② 위에서 발급받은 인증서 경로 적어줍니다.

③ / 로 접근했을 때 빌드했던 dist 의 index.html에 매핑합니다.

④ 프록시 서버 매핑, 클라이언트로부터 요청이 들어오면 프록시 서버로 던져주고, 응답시 클라이언트로 던져줍니다.

<br>

### 5) nginx 가동

```
$ sudo systemctl start nginx
```

<br>

### 6) 실행결과

![img](https://user-images.githubusercontent.com/46040293/74617610-5eb07b80-5171-11ea-8dc6-65b9cc67bbd8.png)

![img](https://user-images.githubusercontent.com/46040293/74617603-5bb58b00-5171-11ea-96fd-314b5517f8a1.png)