---
title: "Array와 List"
toc: true
toc_sticky: true
categories:
  - kotlin
tags:
  - 우테코
  - 안드로이드
  - array
permalink: /categories/kotlin/arrayList
---
# Array와 List

## 들어가기에 앞서
코테 공부를 c++로만 했던 나의 기준에서는 둘 다 비슷한 개념 아닌가 싶긴 했다<br>
평소 코딩할 때에는 mutable이냐 읽기만 가능한 List이냐만 신경을 썼지<br>
Array와 List중 무엇을 쓸 지에 대한 고민은 한 적도 없었다.<br>

# 평소 생각하던 Array와 List의 개념
굳이 생각해본 적은 없었으나, Array와 List의 차이에 대해<br>
처음으로 질문을 받고 생각한 것은 바로 인덱스에 대한 접근이었다.<br>
`val array=arrayof(1,2,3)`이 있으면<br>
array의 경우 `array[0]`과 같은 직관적 방식으로 접근이 가능하다.<br>
그러나 List의 경우 `list.indices` for문을 사용하는 등 한 단계를 더 거쳐야한다<br>
그러나 이 설명에는 몇가지 내가 잘못 알고있던 오개념이 있는데<br>
나와 같은 생각을 한 사람이라면 이 글을 끝까지 읽어보거나, 아래에 적은 참조 링크를 들어가보는 것을 권한다.<br>

# 컬렉션 인터페이스와 스탠다드 라이브러리
코틀린 레퍼런스를 찾아보면 list는 컬렉션(컬렉션 인터페이스) Array는 스탠다드 라이브러리로 구분되어있는 것을 확인할 수 있다.<br>
## 왜 한쪽은 라이브러리 한쪽은 인터페이스?
라이브러리에 대한 설명은 아래에 있는 참조 링크에 잘 나와있다<br>
직접적인 예시를 통해서 설명하자면, c++로 문제를 풀 때에 사용하는<br>
`#inclue<iostream>`에서 #include가 라이브러리를 가져오는 예약어, iostream이 라이브러리명이다.<br>
### 그래서 라이브러리는 왜 쓸까
사람이 일일이 코딩하는 것에 비해 개발시간이 적게 든다<br>거기에 플러스로 컴파일이 미리 되어있기 때문에 컴파일 시간도 적게 들며, 코드의 내용을 숨겨 기술의 유출 역시 가능하기 때문에 굳이 안 쓸 이유가 있을까 싶다<br>
### 본론으로 돌아와서
List는 컬렉션 인터페이스를 구현한 클래스이기 때문이다.<br>코틀린에서 원론적으로 말하고 싶은 것은 List나 Set 등은 컬렉션 인터페이스이며,<br>
인터페이스의 속성은 추상적인 타입이기 때문에 메서드와 속성만 구현하면 된다는 것이 아닐까 싶다<br>
즉, 개발자의 입장에서 보자면 라이브러리인 Array보다는<br>
구현의 자유도가 높을 확률이 크다<br>
# Array와List의 용도

## 공통점
💙읽기 쓰기 모두 가능하다<br>
Array의 경우엔 `val로 선언하느냐/var로 선언하느냐`에 따라서<br>
List의 경우엔  `원칙적으로는 읽기만 가능` 하지만,mutbleListOf를 통하여 읽기 쓰기 모두 가능하게 만들 수도 있다.<br>
💙Array와 List 모두 인덱스에 대한 접근은 가능하다.<br>
💙타입 제한`<T>`를 활용하여 효과적인 요소 관리가 가능하다.<br>
💙뒤에서 언급할 차이를 잘 이해한다면, 둘 다 집합의 개념으로 사용 가능하다<br>
💙둘 다 filter 함수의 사용이 가능하다<br>
### 도대체 왜 filter는 사용가능하지
그 이유는 filter가 Collection에서 제공하는 편의 기능이 아니라<br>
Iterable인터페이스에서 제공하는 기능이기 때문이다<br>
Array와 List는 모두 Iterable인터페이스를 구현하기 때문에,<br>
forEach함수도 Array에서 사용 가능하다<br>
## 차이점
### Array
컬렉션에서 제공하는 기능인 add,remove,isEmpty.contains를 사용할 수 없다<br>
생성될 때에 크기가 고정되어있으며, 변경이 불가하다.<br>
기본 타입 배열의 지원에 따라 각 요소가 해당 원시값으로 초기화되며<br>
메모리의 사용을 최적화해준다<br>
#### Iterable 구현의 차이
위에 filter는 Iterable인터페이스를 구현했다는 설명에 따라<br> Array와 LiSt는 이터레이터를 가진다고 생각할 수 있다.<br>

#### 역순 순회
일반적으로 탐색 시 크기가 고정되어있는 배열의 속성에 따라서<br>
indices보다는 직접 인덱스에 접근하는 방식을 사용한다<br>
##### 코드
```kotlin
val array = Array(3) { it + 1 } // [1, 2, 3]

// 역순으로 배열 순회
for (index in array.size - 1 downTo 0) {
    println("Index: $index, Value: ${array[index]}")
}

```

.asReversed()함수 사용 코드<br>
```kotlin
val array = Array(3) { it + 1 } // [1, 2, 3]

// 역순으로 배열 순회
for (value in array.asReversed()) {
    println("Value: $value")
}
```

### List
add와 remove 등 컬렉션에서 지원하는 다양한 메서드 사용이 가능하다<br>
List는 동적으로 크기를 조절할 수 있어서 유연하다<br>

# 공부 시 참조 링크
[공식 레퍼런스 array](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-array/)<br>

[공식 레퍼런스 list](https://kotlinlang.org/docs/list-operations.html#binary-search-in-sorted-lists)<br>

[라이브러리,프레임워크,api에 관해서](https://velog.io/@bcl0206/API-vs-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC-%ED%92%80%EB%A6%AC%EC%A7%80-%EC%95%8A%EB%8A%94-%EB%AF%B8%EC%8A%A4%ED%84%B0%EB%A6%AC%EC%97%90-%EA%B4%80%ED%95%98%EC%97%AC)<br>
[라이브러리와 모듈화](https://velog.io/@dev-taewon-kim/Chapter-10-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC%EC%99%80-%EB%AA%A8%EB%93%88)<br>
