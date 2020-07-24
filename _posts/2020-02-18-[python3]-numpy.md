---
title: "[Python3] Numpy "
tag: "Python"
author : ""
article_header:
  type: overlay
  theme: dark
  background_color: '#123'
  background_image: false
---



# Numpy

`Numpy` 는 파이썬이 계산과학분야에 이용될 때 핵심 역할을 하는 라이브러리입니다.

`Numpy` 는 고성능의 다차원 배열 객체와 이를 다룰 도구를 제공합니다.

### 배열

`Numpy` 배열은 동일한 자료형을 가지는 값들이 격자판 형태로 있는 것 입니다. 각각의 값들은 튜플( 양의 정수만을) 형태로 색인 됩니다. *rank* 는 배열이 몇 차원인지를 의미합니다. *shape*는 각 차원의 크기를 알려주는 정수들이 모인 튜플입니다.

```python
import numpy as np

a = np.array([1, 2, 3])  	# rank가 1인 배열 생성
print (type(a))           	# 출력 "<type 'numpy.ndarray'>"
print (a.shape)           	# 출력 "(3,)"
print (a[0], a[1], a[2])  	# 출력 "1 2 3"
a[0] = 5               		# 요소를 변경
print (a)               	# 출력 "[5, 2, 3]"

b = np.array([[1,2,3],[4,5,6]])   	# rank가 2인 배열 생성
print (b.shape)                    	# 출력 "(2, 3)"
print (b[0, 0], b[0, 1], b[1, 0])   # 출력 "1 2 4"
```

<br>

```python
import numpy as np

a = np.zeros((2,2))  		# 모든 값이 0인 배열 생성
print (a)              		# 출력 "[[ 0.  0.]
                    		#       [ 0.  0.]]"

b = np.ones((1,2))   		# 모든 값이 1인 배열 생성
print (b)              		# 출력 "[[ 1.  1.]]"

c = np.full((2,2), 7) 		# 모든 값이 특정 상수인 배열 생성
print (c)              		# 출력 "[[ 7.  7.]
                      		#       [ 7.  7.]]"

d = np.eye(2)        		# 2x2 단위행렬 생성
print (d)              		# 출력 "[[ 1.  0.]
                     		#       [ 0.  1.]]"

e = np.random.random((2,2)) # 임의의 값으로 채워진 배열 생성
print (e)                   # 임의의 값 출력 "[[ 0.91940167  0.08143941]
                            #                  [ 0.68744134  0.87236687]]"
```

<br>

### 배열 인덱싱

`Numpy` 는 배열을 인덱싱하는 몇 가지 방법을 제공합니다.

**슬라이싱** : 파이썬 리스트와 유사하게, Numpy 배열도 슬라이싱이 가능합니다. Numpy 배열은 다차원인 경우가 많기에, 각 차원별로 어떻게 슬라이스 할건지 명확해야 합니다.

```python
import numpy as np

# Create the following rank 2 array with shape (3, 4)
# [[ 1  2  3  4]
#  [ 5  6  7  8]
#  [ 9 10 11 12]]
a = np.array([[1,2,3,4], [5,6,7,8], [9,10,11,12]])

# 슬라이싱을 이용하여 첫 두 행과 1열, 2열로 이루어진 부분배열을 만들어 봅시다;
# b는 shape가 (2,2)인 배열이 됩니다:
# [[2 3]
#  [6 7]]
b = a[:2, 1:3]

# 슬라이싱된 배열은 원본 배열과 같은 데이터를 참조합니다, 즉 슬라이싱된 배열을 수정하면
# 원본 배열 역시 수정됩니다.
print (a[0, 1])   	# 출력 "2"
b[0, 0] = 77    	# b[0, 0]은 a[0, 1]과 같은 데이터입니다
print (a[0, 1])   	# 출력 "77"
```





