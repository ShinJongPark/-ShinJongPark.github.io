## > 개요

<img src="/Users/shinjongpark/Library/Application Support/typora-user-images/image-20200805000830359.png" alt="image-20200805000830359" style="zoom:50%;" />

- '차례를 기다리는 열' 이라는 사전적 의미.
- 선입선출 ( FIFO : First In First Out )
- 가장 먼저 큐에 추가된 데이터가 먼저 제거됩니다.
- 활용사례
  - 우선순위 작업 ( 프린트 인쇄 )
  - 프로세스 관리
  - 티켓팅 대기열
  - 너비 우선 탐색 ( BFS : Breadth - First Search ) 구현

​	<br>

## > 사용법

<img src="/Users/shinjongpark/Library/Application Support/typora-user-images/image-20200805000302625.png" alt="image-20200805000302625" style="zoom:50%;" />

### - 연산

- 삽입 - Enqueue(item)
  - 큐(Queue)의 마지막 순서에 데이터를 삽입합니다.
- 삭제 - Dequeue()
  - 큐(Queue)의 첫 번째 순서에 있는 데이터를 반환하고, 삭제합니다.
- 읽기 - Peek()
  - 큐(Queue)의 첫번째 순서에 있는 데이터를 반환한다.
- 초기화 - Clear()
  - 큐에 저장된 모든 데이터를 삭제합니다.



## > 구현

구현방법은 `배열(Array)` 과 `연결리스트(LinkedList)` 방법이 있습니다.

### - 배열(Array) 구현

```java
public class Queue {
	private int front;
	private int rear;
	private int maxSize;
	private Object[] queue;
	
	public Queue(int maxSize) {
		this.front = -1;
		this.rear = -1;
		this.maxSize = maxSize;
		queue = new Object[maxSize];
	}
	
	public boolean isEmpty() {
		return (rear == front);
	}
	
	public boolean isFull() {
		return (rear == maxSize-1);
	}
	
	public void enqueue(Object item) {
		if(isFull())
			throw new ArrayIndexOutOfBoundsException();
		queue[++rear] = item;
	}
	
	public Object peek() {
		if(isEmpty())
			throw new ArrayIndexOutOfBoundsException();
		return queue[front+1];
	}
	
	public Object dequeue() {
		Object item = peek();
		front++;
		return item;
	}
	
	public void clear() {
		if(isEmpty()) {
			System.out.println("Queue is already empty.");
		}else {
			queue = new Object[maxSize];
			front = -1;
			rear = -1;
		}
	}
	public static void main(String[] args) {
		Queue qu = new Queue(100);
		qu.enqueue(1);
		qu.enqueue(2);
		System.out.println(qu.dequeue());
		qu.enqueue(3);
		System.out.println(qu.peek());
		System.out.println(qu.dequeue());
		System.out.println(qu.dequeue());
	}
}

/*
1
2
2
3
*/
```

<br>

### - 연결리스트(LinkedList) 구현

```java
public class Queue<T extends Comparable<T>> {
	
	private Node front;
	private Node rear;
	
	private class Node{
		T item;
		Node next;
		
		Node(T item){
			this.item = item;
			next = null;
		}
	}
	
	public boolean isEmpty() {
		return (front == null);
	}
	
	public void enqueue(T item) {
		Node node = new Node(item);
		if(isEmpty()) {
			rear = node;
			front = node;
		}else {
			rear.next = node;
			rear = node;
		}
	}
	
	public T peek() {
		if(isEmpty())
			throw new ArrayIndexOutOfBoundsException();
		return front.item;
	}
	
	public T dequeue() {
		T item = peek();
		front = front.next;
		if(front == null) {
			rear = null;
		}
		return item;
	}
}
```

<br>

<br>