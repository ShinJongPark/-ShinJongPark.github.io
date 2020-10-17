---
layout : article
title : "[알고리즘] 배열회전, Rotation of Array in Java"
author : ""
tags : "algorithm"
article_header:
  type: overlay
  theme: dark
  background_color: '#123'
  background_image:
    gradient: 'linear-gradient(135deg, rgba(34, 139, 87 , .4), rgba(139, 34, 139, .4))'
    src: /assets/images/logo/background_Java.jpg

---

<br>

<br>

>  배열회전

로직을 제대로 알고 넘어가기로 한다.

시계방향으로 90도, 180도, 270도 순으로 구현하였다.

다음은 NxM 배열을 회전하였다.

```java
public class Rotate {
	static int[][] rotate(int[][] arr, int degree){
		int n = arr.length;
		int m = arr[0].length;
		int[][] rotate = null;
		
		switch(degree) {
		case 90:
			rotate = new int[m][n];
			break;
		case 180:
			rotate = new int[n][m];
			break;
		case 270:
			rotate = new int[m][n];
			break;
		default:
			break;
		}
		
		for(int i=0; i<rotate.length; i++) {
			for(int j=0; j<rotate[i].length; j++) {
				switch(degree) {
				case 90:
					rotate[i][j] = arr[n-1-j][i];
					break;
				case 180:
					rotate[i][j] = arr[n-1-i][m-1-j];
					break;
				case 270:
					rotate[i][j] = arr[j][m-1-i];
					break;
				default:
					break;
				}
			}
		}
		return rotate;
	}
}

```

