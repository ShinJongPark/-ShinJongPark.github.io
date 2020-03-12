---
title: "[COVID] api spec"
tag: "project"
---

## 회원 관련 API

### 0. Rule

#### 0.1 common status

> success : 200 ( Success )
>
> fail : 202 ( Accepted )
>
> Error : 400~500 

<br>

<br>

### 1.로그인 인증

#### 0) uri

```
POST: ~/authenticate
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

#### 0) uri

```
POST: ~/validate/email
```

#### 1) request

```
email : (string)
```

#### 2) response

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