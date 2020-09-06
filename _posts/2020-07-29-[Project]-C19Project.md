---
title: "[Project] C19Project"
tags: "Project"
author : ""
article_header:
 type: overlay
 theme: dark
 background_color: '#123'
 background_image: false

---





# C19Project





## > Description

- 프로젝트 명 : C19Project (private)
- 기간 : 2020.02 중 ~ 2020.03 중 ( 약 4주 )
- 인원 : 10명 ( 7프론트, 1백엔드, 2데이터 )
- 장소 : 비대면 온라인

코로나 사태에 대응하기 위한 프로젝트로, 코로나 전국/해외 실시간 현황과 확진자 동선을 체크하며, Group 기능으로 공지사항, 설문조사, 그리고 설문조사를 기반으로한 여러 컨텐츠가 있습니다.

<br>

## > Features

- 코로나 관련 데이터 시각화
  - 국내
  - 해외
  - 국내 확진자 동선
- 그룹
  - 공지사항
  - 설문조사
  - 설문조사를 기반한 컨텐츠
    - 체온 추이 ( 개인, 그룹별 )

<br>

## > Part

- 백엔드
  - 팀원들과 함께 요구명세서를 정의
  - 데이터 모델링
  - 각 기능에 필요한 api 명세서 작성 ( Swagger 활용 )
  - Spring Boot로 백엔드 구축
  - JPA
  - JWT
- 서버 배포
  - NginX 활용한 로드밸런싱
  - 운영서버 / 개발서버 분리
  - SSL 적용

<br>

## > Skills

`Vue.js`  `Vuex`   `Spring Boot`  `JPA`  `MySql`  `DB Multiple`  `NginX`  `AWS ES2`  `Gitlab`   `Jira`

<br>

## > Strategy

### - Git

- 홀로 백엔드 개발을 하지만, 컨벤션을 정하고 지키도록 노력했다.
- branch 전략 : master - release - bugfix - develop - feature(기능단위)
- 커밋메세지 :  `Add` `Fix` `Update` `Delete` 등의 간단한 키워드를 사용했으며, 사진에는 없지만 Jira와 연동하여 관련된 이슈에 연결하기 위한 이슈넘버를 기재하였다.

<img src="/assets/images/projects/c19project/5.git-commit-history2.png" alt="image-queue" style="zoom:50%; float:left" />

### - Jira

- 주차별 스프린트를 구성하고, 팀원들과 아침 스크럼 회의에 적극 활용 하였다.
- 회의를 위해 무언가를 준비할 시간이 필요가 없으며, 이슈관리와 동시에 각 팀원의 진행척도를 체크할 수 있다.

### - SpringBoot

- 생산성을 위한 JPA를 학습하면서 개발 하였다.
- 개발하면서 난해했던 부분은 CamelCase와 SnakeCase를 함께 사용했다는 점이다.
- DB컬럼명은 SnakeCase를 명시하고, JPA에서 Camelcase를 사용했기 때문에 Entity에서 DTO로 매핑할때 실수하는 부분이 조금 있었다.
- Inner Class 사용.
- 각 API마다 DTO를 만들어주었다. API가 늘어날수록 증가하는 DTO Class들이 보기에 좋지않았다.
- 개인적으로 package를 사용하는 것 보다 Inner Class를 사용하는게 깔끔하고 보기에 좋았다.

### - Swagger

- 백엔드 개발에 필수라고 생각한다.
- 개발중, 프론트엔드 개발자와 의사소통시 각 api 스펙을 따로 만들필요가 없어 매우 편리하다.
- 개발서버에는 포함시키되, 운영서버에는 필히 제외하고 배포하였다.

### - Server

- 개발서버와 운영서버를 분리하였다.
- 초기 100여명을 대상으로 사내운영테스트를 지속적으로 진행했기 때문에 서버를 분리하게 되었다.
- 개발서버에서 버그리포팅을 완료한 후, 프론트와 함께 완성된 빌드본을 운영서버에 동시에 배포한다.
- WebServer는 로드밸런싱을 쉽게 경험할 수 있는 `Nginx`를 활용하였고,
- 무료인증서를 발급받아 테스트 하였다.  `Letss Encrypt`

### - Database

- 본 프로젝트의 방향은 사원관리측면의 `그룹기능 서비스`와 `코로나 공용데이터 API구축`을 나누어 진행하였다.
- 내가 담당했던 파트는 `그룹기능 서비스`였지만, `코로나 공용데이터`를 함께 취급해야하는 상황을 가졌다.
- 그렇게 찾은 기술(?) `Multiple Database`, Auto configuration이 되지않기 때문에 Datasource를 수동설정 해주어야 한다. 초기 설정은 다소 복잡한 편이었지만, 예제를 보면서 하나씩 해보니 크게 어렵지는 않았다.
- DB스키마에서 가장 생각이 많았던 부분은 `설문조사` 기능이었다.
- 두가지 이슈가 있었다.
- 첫째, 설문 항목이 갯수는 유동적이어야 한다.
- 둘째, 설문 항목에 대한 응답을 카테고리에 맞게 수집해야 함.
- 글로 설명하기 복잡하지만, 간단하게, 설문항목은 Json형식, 응답은 설문항목의 개수만큼 카테고리별로 저장한다. 아래사진은 설문기능에 대한 부분 ERD이다.

<img src="/assets/images/projects/c19project/6.erd-survey.png" alt="image-queue" style="zoom:70%; float:left" />

<br>

<br>

## > Images

### - main

![img](/assets/images/projects/c19project/1.main.png)

### - main(mobile)

![img](/assets/images/projects/c19project/1.main_m.png)

### - layout

![img](/assets/images/projects/c19project/2.layout.png)

### - content option

![img](/assets/images/projects/c19project/2.option.png)

### - content - 코로나 현황판

![img](/assets/images/projects/c19project/3.content1.png)

### - content - 코로나 현황 막대 그래프

![img](/assets/images/projects/c19project/3.content2.png)

### - content - 코로나 현황 맵

![img](/assets/images/projects/c19project/3.content3.png)

### - content - 코로나 현황 표

![img](/assets/images/projects/c19project/3.content4.png)

### - content - 코로나 현황 타임라인

![img](/assets/images/projects/c19project/3.content5.png)

### - content - 코로나 확진자 맵 ( 동선 )

![img](/assets/images/projects/c19project/3.content6.png)

### - content - 코로나 선별 진료소

![img](/assets/images/projects/c19project/3.content7.png)

### - content - 공적 마스크 판매점

![img](/assets/images/projects/c19project/3.content8.png)

### - content - 도/시별 코로나 현황 사이트

![img](/assets/images/projects/c19project/3.content9.png)

### - content - 그룹 컨텐츠 - 체온 추이

![img](/assets/images/projects/c19project/4.group.png)

### - content - 그룹 공지사항/설문조사 

![img](/assets/images/projects/c19project/4.group2.png)

### - content - 그룹 설문조사

![img](/assets/images/projects/c19project/4.group3.png)



<br>

<br>

<br>

