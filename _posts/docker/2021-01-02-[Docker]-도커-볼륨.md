---
title: "[Docker] 도커 볼륨 (데이터 공유)"
tags: "Docker"
author : ""
article_header:
  type: overlay
  theme: dark
  background_color: '#123'
  background_image:
    gradient: 'linear-gradient(135deg, rgba(34, 139, 87 , .4), rgba(139, 34, 139, .4))'
    src: /assets/images/logo/docker_background.jpg
---

<br>

> `apache`와 `mysql` 을 도커 컨테이너로 실행하고, 외부에서 접속이 가능하도록 한다.

<br>

> -v
>
> -volumes-from
>
> docker volume

## l. 웹 서버(아파치) 실행, 포트 포워딩(Port forwarding)

> 외부에서 내부 도커 컨테이너로 접속하기 위해서, `포트 포워딩` 을 해준다.
>
> 포트 포워딩은 외부 주소와 내부 주소를 이어주는 역할을 한다.
>
> 예를들어, 컨테이너의 웹서버를 80번 포트로 설정했을 때, 호스트 80번 포트와 내부 컨테이너 80번 포트를 포워딩 한다.
>
> ```
> 호스트 IP의 80번 포트로 접근 => 호스트의 80번 포트는 컨테이너의 80번 포트로 포워딩 => 웹 서버 접근
> ```
>
> `포트 포워딩`을 위해  `-p [호스트 포트]:[컨테이너 포트]` 옵션을 사용한다.
>
> ```shell
> # 도커 컨테이너 80:80 포트 포워딩
> docker run -it --name mywebserver -p 80:80 ubuntu:14.04
> # 포트포워딩한 컨테이너를 생성 및 실행시킨 후, 컨테이너에 아파치를 설치하고 실행해보자.
> apt-get update
> apt-get install apache2 -y
> service apache2 start
> ```
>
> 이렇게 도커 컨테이너를 실행시킨 후, 웹 브라우저에서 호스트 ip로 접근하여보자.
>
> `http://IP_Address:80` 또는 `http://localhost:80` 로 접근하면 컨테이너에서 실행시킨 아파치 웹서버에 접근할 수 있다.
>
> (호스트 8888 포트번호와 연결하려면 `-p 8888:80` 와 같이 입력하며, 호스트의 특정 IP를 사용하려면 `-p [호스트 IP]:[호스트 포트]:[컨테이너 포트]` 와 같이 입력하면 된다. 여러 개의 포트를 포워딩하려면 `-p` 옵션을 여러 번 써서 입력한다.

<br/>

<br/>

## ll. 데이터베이스 서버(MySQL) 실행, Detached 모드

> 데이터베이스 서버와 웹 서버를 같은 컨테이너에서 실행시킬 수 있지만, 관리와 독립성 및 확장성을 고려하여 컨테이너를 분리하여 사용할 수 있다. 도커 홈페이지에서도 권장하는 구조이다. 한 컨테이너에서는 하나의 프로세스만 실행하는 것이 도커의 철학이라고 한다.
>
> 
>
> 웹서버와 데이터베이스 서버를 실행해보자.
>
> 웹서버는 `wordpress`, 데이터베이스 서버는 `mysql`
>
> ``` shell
> docker run -d \
> --name wordpressdb \
> -e MYSQL_ROOT_PASSWORD=pwd \
> -e MYSQL_DATABASE=wordpress \
> mysql:5.7
> ```
>
> ```shell
> docker run -d \
> --name wordpress \
> --link wordpressdb:mysql \
> -p 80 \
> wordpress
> ```
>
> mysql과 wordpress 이미지를 사용해 두개의 컨테이너를 실행하였다. ( 가독성을 위해 역슬래시 \ 를 사용하였다. )

<br>

### - docker run -d 옵션 ( Detached Mode )

> `-d` 옵션은 detached 모드로써 컨테이너를 백그라운드에서 동작하도록 한다. -it와 달리 입출력이 없는 상태로 컨테이너를 실행하며, 컨테이너 내부에서는 프로그램이 터미널을 차지하는 포그라운드(foreground)로 실행돼 사용자의 입력을 받지 않는다.
>
> mysql은 하나의 터미널을 차지하는 mysqld를, 워드프레스는 apache2-foreground를 포그라운드로 실행하므로 `-d` 옵션을 지정해 각각의 컨테이너를 백그라운드로 설정한 것이다.
>
> 다음은 `-d` 옵션으로 우분투를 실행한 것이다.
>
> ```shell
> docker run -d --name detach_test ubuntu:14.04
> ```
>
> 컨테이너가 생성됐더라도 바로 종료된다. `docker start` 해도 실행되지 않는다. 컨테이너 내부 터미널을 차지하는 포그라운드로써 동작하는 프로세스가 없어 실행해도 실행되지 않는다.
>
> <br>
>
> **반대로 mysql 컨테이너를 -it 옵션으로 생성하면 어떻게 될까?**
>
> ```shell
> docker run -it \ 
> --name mysql_attach_test \
> --e ...
> mysql:5.7
> ```
>
> 실행해보면 하나의 터미널을 차지하는 mtsqld 프로그램이 포그라운드로 실행된 `로그` 를 볼 수 있다. mysql 이미지는 컨테이너가 실행할 때 mysqld가 포그라운드 형태로 실행되기 때문이다. 입출력이 불가능하며, `-d` 옵션을 이용해 컨테이너를 백그라운드로 설정할 수 있는것이다.

<br>

> `-e` 옵션은 컨테이너 내부의 환경변수를 설정한다.
>
> mysql 컨테이너에서 설정한 패스워드를 확인해보자.
>
> `docker attach`로 들어가서 echo로 확인하고 싶지만, `-d` 옵션때문에 불가능하다.
>
> `docker exec` 명령어를 사용하면 컨테이너 내부의 셸을 사용할 수 있다.
>
> ```shell
> docker exec [컨테이너 ID/Name] [명령어]
> ```
>
> exec 명령어는 단순히 컨테이너 내부의 명령어를 실행한 후 결과값을 반환받을 수 있다. 여기에서 `-it` 옵션을 추가해 /bin/bash를 상호 입출력이 가능한 형태로 사용할 수 있다.
>
> ```shell
> docker exec -it wordpressdb /bin/bash
> echo $MYSQL_ROOT_PASSWORD
> // password
> ```
>
> Ctrl + P, Q로 컨테이너에서 빠져나올 수 있으며, exit로 /bin/bash 프로세스를 종료하며 빠져나올 수 있다. exit을 사용해도 컨테이너가 종료되지 않는데, 이는 mysqld 프로세스가 컨테이너 안에서 여전히 포그라운드 모드로 동작하고 있기 때문이다.

<br>

> `--link` 옵션은 컨테이너에서 다른 컨테이너로 접근하는 방법으로 NAT으로 할당받은 IP를 사용하여 접근할 수 있다. 하지만 도커 엔진은 컨테이너에게 내부 IP를 172.17.0.2, 3, 4 ... 와 같이 순차적으로 할당하기 때문에 컨테이너를 재시작하면 IP를 재할당 받아 일정하지 않다.
>
> 이를 해결하기위해 `Alias` 를 사용한다.
>
> IP가 아닌 컨테이너 이름으로 설정하여 접근할 수 있다. 
>
> ```shell
> ...
> --link [컨테이너 Name]:[호스트 Name]
> --link wordpressdb:mysql
> ...
> ```
>
> 워드프레스 컨테이너는 mysql이라는 호스트명으로 요청하면 wordpressdb 컨테이너 내부의 IP를 몰라도 접근할 수 있다.
>
> 유의할 점은, `--link` 에 입력된 컨테이너가 실행중이지 않다면, 이를 실행한 컨테이너도 실행되지 않는다.
>
> `--link` 옵션은 컨테이너간 이름으로 서로를 찾을 수 있지만, 현재는 `도커 브리지(bridge) 네트워크를` 사용하여 더욱 손쉽게 설정할 수 있다.

<br/>

> `-p [호스트 포트]:[컨테이너 포트]` 로 사용하지만, `-p [컨테이너 포투]`로 사용할 수 있다.
>
> 호스트에서 사용할 수 있는 적당한 포트를 컨테이너 80번 포트로 포워딩 해준다.
>
> 컨테이너를 실행 후,
>
> `docker port wordpress `로 웹서버의 포트를 확인할 수 있다.
>
> 다시 `http://IP_Address:[port]` 또는 `http://localhost:[port]` 로 웹브라우저에서 접근해보자.

<br>

<br>

<br/>

<br/>

<br/>

> By Getting Started with Docker/Kubernetes (wiki book)

<br/>

<br/>

<br/>