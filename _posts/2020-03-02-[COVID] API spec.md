---
title: "[COVID] api spec"
tag: "project"
---

## Rule

#### common status

> success : 200 ( Success )
>
> fail : 202 ( Accepted )
>
> Error : 400~500 

<br>

## 회원 관련 API

<br>

### 1.로그인 인증

#### 1) uri

```
POST: ~/authenticate
```

#### 2) request

```
email : (string)
password : (string)
```

#### 3) response

200

```
#response.data
token: (string)
user : userInfo (object)
Groups : GroupList (array<object>)
dashboards: {
	structure : dashboardList (json)
	contents : contentList (array<object>)
}
```

202

```
#response.data
message : (string)
```

<br>

### 2. 회원가입

#### 0) uri

```
POST: ~/account
```

#### 1) request

```
email : (string)
password : (string)
```

#### 2) response

200

```
#response.data
null
```

202

```
#response.data
message : (string)
```

<br>

### 3. 이메일 중복체크

#### 1) uri

```
POST: ~/validate/email
```

#### 2) request

```
email : (string)
```

#### 3) response

200

```
#response.data
validate: true (boolean)
```

202

```
#response.data
validate: false (boolean)
message : (string)
```

<br>

<br>

## 그룹 관련 API

<br>

### 1. 그룹 선택

#### 1) uri

```
Get: ~/groups/{group_id}
```

#### 2) request

```
group_id: (Long)
```

#### 3) response

200

```
#response.data
groupInfo: (object)
notices: (Array<object>)
surveys: (Array<object>)
```

202

```
#response.data
message : (string)
```

<br>

