---
title: "[ 자료구조 ] ArrayList vs LinkedList 시간복잡도"
tags: "Data Structure"
article_header:
  type: cover
  image:
    src: /screenshot.jpg

---


# [ 자료구조 ] ArrayList vs LinkedList 시간복잡도




## ArrayList

ArrayList 는 삽입과 삭제를 할 일이 없거나 리스트 맨 끝에서만 이루어질 때 유용하게 쓰일 수 있습니다.

원소들이 메모리에 연속해 배치되어 있어 CPU 캐시 효율이 좋습니다.

빠르게 접근이 가능한데요.



하지만 원소를 삽입/삭제시 데이터가 뒤로 밀리거나, 빈 공간애 대해 당겨야 하기때문에

CPU의 부담을 줄 수 있습니다.





## LinkedList


원소들이 메모리에 연속해 배치되어 있는 ArrayList 와는 달리, LinkedList는 자료의 주소값이 서로 연결되어 있는 구조를 가지고 있습니다.

원소들의 주소값만 변경하여 삽입/삭제를 하기 때문에 이러한 작업이 빈번할 때 유용합니다.







## 시간복잡도

| 작업                                   | Array List   | Linked List  |
| -------------------------------------- | ------------ | ------------ |
| 이전 원소/다음 원소 찾기               | O(1)         | O(1)         |
| 맨 뒤에 원소 추가/삭제하기             | O(n) or O(1) | O(1)         |
| 맨 뒤 이외의 위치에 원소 추가/삭제하기 | O(n)         | O(1)         |
| 임의의 위치의 원소 찾기                | O(1)         | O(n)         |
| 크기 구하기                            | O(n)         | O(n) or O(1) |






## 결론


리스트의 삽입/삭제가 빈번하다. 		==>		LinkedList

빈번하지 않다.									  ==>		ArrayList



