---
layout : article
title : "[Java] Comparable and Comparator"
author : ""
tags : "Java"
article_header:
  type: overlay
  theme: dark
  background_color: '#123'
  background_image:
    gradient: 'linear-gradient(135deg, rgba(34, 139, 87 , .4), rgba(139, 34, 139, .4))'
    src: /assets/images/logo/background_Java.jpg
---


<br/>
We can change the position of an obejct with a `Comparable` and `Comparator`   in Java.
<br/>
<br/>
우리는 Comparable 과 Comparator 을 이용하여 Java 객체를 정렬할 수 있습니다.

## Interface Comparable

- 정렬 수행 시 `기본적으로 적용되는` 정렬 기준이 되는 메서드를 정의해 놓은 인터페이스.
- Class에 Comparable 인터페이스를 Implements 한 후, 내부 메서드 CompareTo를 사용하여 원하는 정렬 기준으로 구현한다.
- CompareTo 작성법
  - 현재 객체 < 파라미터 객체 : 음수 리턴
  - 현재 객체 == 파라미터 객체 : 0 리턴
  - 현재 객체 > 파라미터 객체 : 양수 리턴
  - 0 또는 음수가 리턴된다면 자리는 그대로 유지되며, 양수일 경우 두 자리가 바뀐다.
  - 오름차순이라면 이대로 사용하고, 내림차순 정렬을 원한다면, 리턴값을 반대로 해주면 된다.
  - String 은 compareTo 메소드를 사용하여 비교하고 음/양수를 리턴받을 수 있다.

- 다음은 `이름 오름차순` 다음  `seq 오름차순` 의 예시이다.

```java
public class ComparableTest {
	public static void main(String[] args) {
		List<Position> list = new ArrayList<>();
		list.add(new Position(3,"aab"));
		list.add(new Position(1,"abd"));
		list.add(new Position(2,"aaa"));
		list.add(new Position(1,"abc"));
		list.add(new Position(5,"abc"));
		list.add(new Position(4,"abc"));

		Collections.sort(list);
		
		for(int i=0; i<list.size(); i++)		{
			System.out.println(list.get(i).toString());
			}
	}
	
	static class Position implements Comparable<Position>{
		int seq;
		String name;
		
		public Position(int seq, String name) {
			this.seq = seq;
			this.name = name;
		}

		@Override
		public int compareTo(Position o) {
			if(this.name.equals(o.name)) {
				if(this.seq == o.seq) return 0;
				else return this.seq - o.seq;
        // Integer.compare(this.seq, o.seq);
        // 로 사용할 수 있다.
			}else return this.name.compareTo(o.name);
		}

		@Override
		public String toString() {
			return "[" + seq + ", " + name + "]";
		}
		
	}
}

/* Return
[2, aaa]
[3, aab]
[1, abc]
[4, abc]
[5, abc]
[1, abd]
*/
```

<br>

위에서 `Integer.compare`는 첫번째 매개변수와 두번째 매개변수를 비교하여 오름차순으로 정렬할 수 있게 해주는 메소드 이다.

```java
public static int compare(int x, int y){
	return (x<y) ? -1 : ((x==y) ? 0 : 1));
}
// x < y 일경우 -1 리턴
// x == y 일 경우 0 리턴
// x > y 일 경우 1 리턴
```

<br>

<br>

## Interface Comparator

- Comparable은 하나의 객체에서 정렬기준을 정해주었다면, Comparator는 하나의 객체에 `여러 기준`으로 정렬을 해줄 수 있다.
- 주로 `익명 클래스(Anonymous Class)` 로 많이 사용된다.
  - 위와 같은 예시 ( `name 오름차순, seq 오름차순`)

```java
public class ComparatorTest {
	public static void main(String[] args) {
		List<Position> list = new ArrayList<>();
		list.add(new Position(3,"aab"));
		list.add(new Position(1,"abd"));
		list.add(new Position(2,"aaa"));
		list.add(new Position(1,"abc"));
		list.add(new Position(5,"abc"));
		list.add(new Position(4,"abc"));

		Collections.sort(list, new MyComparator());
		
    /*
    # 익명 클래스의 경우
    Collections.sort(list, new Comparator<Position>(){
			@Override
			public int compare(Position o1, Position o2) {
				if(o1.name.equals(o2.name)) {
					return Integer.compare(o1.seq, o2.seq);
				}
				return o1.name.compareTo(o2.name);
			}
		});
    */
    
		for(int i=0; i<list.size(); i++)		{
			System.out.println(list.get(i).toString());
			}
	}
	
	static class MyComparator implements Comparator<Position>
		@Override
		public int compare(Position o1, Position o2) {
			if(o1.name.equals(o2.name)) {
				return Integer.compare(o1.seq, o2.seq);
        // 만약, 내림차순의 경우 o1 와 o2의 위치를 바꿔준다.
			}
			return o1.name.compareTo(o2.name);
		}
	}

	static class Position {
		int seq;
		String name;
		public Position(int seq, String name) {
			this.seq = seq;
			this.name = name;
		}
		@Override
		public String toString() {
			return "[" + seq + ", " + name + "]";
		}
		
	}
}
```

<br>

<br>

#### > 우선순위 큐 ( PriorityQueue ) 생성자에서도 Comparator Interface를 익명 클래스로 받을 수 있다.

```java
public class PriorityQueueTest {
	public static void main(String[] args) {
	//Queue<Position> pq = new PriorityQueue<>(new MyComparator());
		Queue<Position> pq = new PriorityQueue<>(new Comparator<Position>() {
			@Override
			public int compare(Position o1, Position o2) {
				if(o1.name.equals(o2.name)) {
					return Integer.compare(o1.seq, o2.seq);
				}
				return o1.name.compareTo(o2.name);
			}
		});
```

<br>

<br>

<br>



