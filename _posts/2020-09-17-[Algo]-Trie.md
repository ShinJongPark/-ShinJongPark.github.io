---
layout : article
title : "[알고리즘] Trie in Java"
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

## > 목표 

우리는 Java 8, 람다를 활용하여 Trie를 구현할 수 있습니다.

<br>

## 람다 사용

누군가의 별명을 여러개로 구성한다고 했을 경우, 다음 순서로 구현할 수 있다.

1. 해당 이름으로 별명을 가져온다.
2. 없다면 리스트를 생성하여 추가한다.
3. 해당 이름으로 리스트를 저장한다.

```java
// getNormalStrategy.java
public void putNickname(Map<String, List<String>> map, String[] values) {
  List<String> list = map.get(values[0]);
  if (list == null) {
    list = new ArrayList<String>();
  }
  list.add(values[1]);
  map.put(values[0], list);
}
```

<br>

기존의 `다섯줄` 을 다음과 같이 `세줄 `로 줄일 수 있다.

```java
// GetOrDefaultStrategy.java
public void putNickname(Map<String, List<String>> map, String[] values) {
  List<String> list = map.getOrDefault(values[0], new ArrayList<String>());
  list.add(values[1]);
  map.put(values[0], list);
}
```

<br>

하지만 위 방법은 필요하지 않은 경우에도 항상 `new ArrayLis<String>()` 을 실행하는 문제점을 가진다.

다음과 같이 `computeIfAbsent` 를 사용함으로써 문제를 해결할 수 있고,

`세줄` 에서 `한줄` 로 줄일 수 있다.

```java
// ComputeIfAbsentStrategy.java
public void putNickname(Map<String, List<String>> map, String[] values) {
  map.computeIfAbsent(values[0], k -> new ArrayList<String>()).add(values[1]);
}
```



## Trie 구현 및 테스트

```java
package algo;
import java.util.*;

public class Trie {
	public static void main(String[] args) {
		Trie trie = new Trie();
		// insert 메서드
		System.out.println(trie.isRootEmpty());
		trie.insert("PI");
		trie.insert("PIE");
		trie.insert("POW");
		trie.insert("POP");
		System.out.println(trie.isRootEmpty());

		// Contains 메서드
		System.out.println(trie.contains("POW"));
		System.out.println(trie.contains("PIES"));
		// Delete 메서드
		trie.delete("POP");
		System.out.println(trie.contains("POP"));
		System.out.println(trie.contains("POW"));
		// 없는 단어를 지울 때 > 에러발생하는 예
		trie.delete("PO");
		trie.delete("PIES");
		trie.delete("PEN");

	}

	private class TrieNode {
		// 자식 노드 맵
		private Map<Character, TrieNode> childNodes = new HashMap<>();
		// 마지막 글자여부 체크
		private boolean isLastChar;

		// 자식 노드 맵 Getter
		Map<Character, TrieNode> getChildNodes() {
			return this.childNodes;
		}

		// 마지막 글자여부 Getter
		boolean isLastChar() {
			return this.isLastChar;
		}

		// 마지막 글자여부 Setter
		void setIsLastChar(boolean isLastChar) {
			this.isLastChar = isLastChar;
		}
	}
	// 루트 노드
	private TrieNode rootNode;

	// 생성자
	Trie() {
		rootNode = new TrieNode();
	}

	// 자식 노드 추가
	void insert(String word) {
		TrieNode thisNode = this.rootNode;
		for (int i = 0; i < word.length(); i++) {
			thisNode = thisNode.getChildNodes()
					.computeIfAbsent(word.charAt(i), c -> new TrieNode());
		}
		thisNode.setIsLastChar(true);
	}

	// 특정 단어가 들어있는지 확인
	boolean contains(String word) {
		TrieNode thisNode = this.rootNode;
		for (int i = 0; i < word.length(); i++) {
			char character = word.charAt(i);
			TrieNode node = thisNode.getChildNodes().get(character);
			if (node == null)
				return false;
			thisNode = node;
		}
		return thisNode.isLastChar();
	}

	// 특정 단어 지우기
	void delete(String word) {
		delete(this.rootNode, word, 0); // 최초로 delete 던지는 부분
	}

	private void delete(TrieNode thisNode, String word, int index) {
		char character = word.charAt(index);
		// APPLE, PEN과 같이 아예 없는 단어인 경우 에러 출력
		if (!thisNode.getChildNodes().containsKey(character))
			throw new Error("There is no [" + word + "] in this Trie.");
		TrieNode childNode = thisNode.getChildNodes().get(character);
		index++;
		if (index == word.length()) {
			// 삭제조건 2번 항목
			// PO와 같이 노드는 존재하지만 insert한 단어가 아닌 경우 에러 출력
			if (!childNode.isLastChar())
				throw new Error("There is no [" + word + "] in this Trie.");
			childNode.setIsLastChar(false);
			// 삭제조건 1번 항목
			// 삭제 대상 언어의 제일 끝으로써 자식 노드가 없으면(이 단어를 포함하는 더 긴 단어가 없으면) 삭제 시작
			if (childNode.getChildNodes().isEmpty())
				thisNode.getChildNodes().remove(character);
		} else {
			delete(childNode, word, index); // 콜백함수부분
			// 삭제조건 1,3번 항목
			// 삭제 중, 자식 노드가 없고 현재 노드로 끝나는 다른 단어가 없는 경우 이 노드 삭제
			if (!childNode.isLastChar() && childNode.getChildNodes().isEmpty())
				thisNode.getChildNodes().remove(character);
		}
	}

	boolean isRootEmpty() {
		return this.rootNode.getChildNodes().isEmpty();
	}

}

```

<br>



