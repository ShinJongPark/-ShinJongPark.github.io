---
title: "[Project] BlockCar"
tags: "Project"
author : ""
article_header:
 type: overlay
 theme: dark
 background_color: '#123'
 background_image:
    gradient: 'linear-gradient(135deg, rgba(34, 139, 87 , .4), rgba(139, 34, 139, .4))'
    src: /assets/images/projects/blockcar/logo_blockcar.PNG
---


# Block Car

[삼성 청년 소프트웨어 아카데미](https://www.ssafy.com/ksp/jsp/swp/swpMain.jsp) ( 이하 SSAFY ) 프로젝트 기간 중 특화(ai, bigdata, blockchain) 프로젝트 부문에서 **대전지역 1위**의 성과를 얻었습니다.


### > Description
- 프로젝트 명 : BlockCar
- 기간 : 2019.08 말 ~ 2019.10 초 ( 약 5주 )
- 인원 : 5명 ( 2프론트 2백엔드 1블록체인 )
- 장소 : 대전 SSAFY 삼성연수원

블록체인 기반으로한 중고차 거래 서비스 입니다.<br/>
블록체인 네트워크를 [프로젝트 목적에 맞게 구축](https://github.com/ShinJongPark/FabricNetwork-BlockCar)하여, 자동차 등록부터 보험이력, 정비이력, 거래내역 등을 기록하고, 소비자들이 신뢰할 수 있는 데이터를 웹 서비스에서 제공합니다.

<br>

### > Features

Fabric 블록체인에 저장된 데이터를 바탕으로 중고차를 거래합니다.

- 중고차 판매
  - 휴대폰 번호와 차량 번호를 입력하여 인증
    - 휴대폰으로 인증문자 발송
    - 인증번호 입력
    - 중고차는 차 번호판이 아닌 시리얼 넘버로 관리
    - (블록체인 데이터) 차량 번호 => 시리얼 넘버 => 차 검색 => 해당 핸드폰 번호 일치 여부 확인
  - 검증 후, 해당 차량의 모든 데이터 출력 ( 블록체인 데이터 )
  - 판매 등록
- 중고차 구매
  - 배송일, 배송장소 입력
  - 카카오 페이를 연동하여 계약금 결제
  - 결제가 완료되면 차량 배송 ( 시나리오이므로 x )
- 검색 필터
  - 블록체인에 등록되어 있는 차량 데이터를 바탕으로 데이터를 제공

<br>

### > Part

- Hyperledger Fabric 분석 및 활용법 학습.

- Hyperledger Fabric을 활용한 블록체인 네트워크를 구축.
  - 프로젝트 목적에 맞는 여러 기관노드(생산,보험,정비기관 등)을 생성하고 연결(채널 생성).
  - 네트워크에 구동될 체인코드를 작성하고, 해당 채널에 배포.
  - 동작 테스트 및 sdk를 활용한 백엔드 연결.

<br>


### > How can we trust this service?

블록카는 각 기관끼리 네트워크를 갖추기 때문에 `private`한  **`Hyperledger Fabric`** 네트워크가 적합합니다. 블록체인 네트워크에 기록되는 데이터는 변/조작이 *`매우 어렵기` 때문에, 소비자들이 믿고 사용할 수 있습니다.

*매우 어렵다고 표현한 것은 네트워크 환경에 따라 아주 불가능한 것이 아니기 때문입니다. 가능하기 위해서는 아주 강력한 하드웨어(슈퍼슈퍼컴)가 요구되지만, 현재로서는 불가능에 가깝습니다.

<br>


### > Skills

`React` `Spring Boot` `JPA` `MySql`  `Hyperledger Fabric`  `sdk`  `NginX`   `Javascript` `AWS ES2` `Gitlab` `Jira`

<br>


### > URI

- [http://13.125.112.95/](http://13.125.112.95/#/)


### > Images

![main](/assets/images/projects/blockcar/main.png)

![main](/assets/images/projects/blockcar/detail.png)

![main](/assets/images/projects/blockcar/buy.png)

![main](/assets/images/projects/blockcar/filter.png)

<br><br>



