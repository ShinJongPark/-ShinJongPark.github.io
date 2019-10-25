---
title: [Linux] Shell 작성법
tags: linux
article_header:
  type: cover
  image:
    src: /screenshot.jpg
---



## Shell 파라미터 작성법



```
vi test.sh
```

```
echo " 파라미터 개수 : $#"
echo " 첫번째 파라미터 : $1"
echo " 두번째 파라미터 : $2"
echo " 모든 파라미터 : $@"
```



## if 문 사용법, 조건식

### 기본 형식

```
if [값 조건식 값 조건식...]
then
    수행문
elif [값 조건식 값 조건식...]
then
    수행문
else
    수행문
fi
```



### 조건식 종류

|     조건식      | 설명                              |
| :-------------: | :-------------------------------- |
|       -z        | 문자열의 길이가 0이면 참          |
|       -n        | 문자열의 길이가 0이 아니면 참     |
|       -eq       | 값이 같으면 참. = 연산자 동일     |
|       -ne       | 값이 다르면 참                    |
|       -gt       | 값1 > 값2                         |
|       -ge       | 값1 >= 값2                        |
|       -lt       | 값1 < 값2                         |
|       -le       | 값1 <= 값2                        |
|       -a        | &&연산과 동일 and 연산            |
|       -o        | \|\|연 산과 동일 xor 연산         |
|       -d        | 파일이 디렉토리면 참              |
|       -e        | 파일이 있으면 참                  |
|       -L        | 파일이 심볼릭 링크면 참           |
|       -r        | 파일이 읽기 가능하면 참           |
|       -s        | 파일의 크기가 0 보다 크면 참      |
|       -w        | 파일이 쓰기 가능하면 참           |
|       -x        | 파일이 실행 가능하면 참           |
| 파일1 -nt 파일2 | 파일1이 파일2보다 최신파일이면 참 |
| 파일1 -ot 파일2 | 파일1이 파일2보다 이전파일이면 참 |
| 파일1 -ef 파일2 | 파일1이 파일2랑 같은 파일이면 참  |



### 예시

```
if [ "$#" != 2 ]; then
    echo 'Incorrect number of arguments. Expecting 2, parameter { Name, version } '
else
    echo 'updating chaincode is actived.'
fi
```
