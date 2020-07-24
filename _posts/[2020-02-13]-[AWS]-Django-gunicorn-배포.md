

---
title: "[AWS] Django + gunicorn 배포"
tags: "aws"
---

<br>



환경

```
OS : Ubuntu 18.04.3 LTS
Python : Python3
```







### 준비

```shell
sudo apt-get install python3		# 파이썬 설치
sudo apt-get install python3-venv	# 가상환경 설치
```

<br>

### 가상환경 준비

가상환경 세팅해줄 폴더에서 다음과 같은 명령어를 실행

```shell
python3 -m venv [경로]
ex) python3 -m venv /home/project/venv
```

<br>

### 가상환경 활성화

```shell
source venv/bin/activate
(venv)
```

<br>

### 패키지 설치

독립된 가상환경에서 필요한 Django, gunicorn 을 설치한다

```shell
(venv): pip install Django gunicorn
```

<br>

### 프로젝트 및 저장소 생성

```shell
mkdir repo run
cd repo
django-admin.py startproject conf
```

<br>

### STATIC_ROOT 디렉토리 지정

`conf/settings.py` 파일의 끝에 다음 줄을 추가 입력해줍니다.

````shell
STATIC_ROOT = os.path.join(BASE_DIR, 'static/')
````

<br>

### 마이그레이션

작성중...



<br>

<br>

<br>

<br>

