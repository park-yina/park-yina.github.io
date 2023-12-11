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
# 컬렉션 인터페이스와 스탠다드 라이브러리
코틀린 레퍼런스를 찾아보면 list는 컬렉션(컬렉션 인터페이스) Array는 스탠다드 라이브러리로 구분되어있는 것을 확인할 수 있다.<br>
## 왜 한쪽은 라이브러리 한쪽은 인터페이스?
라이브러리에 대한 설명은 아래에 있는 참조 링크에 잘 나와있다<br>
직접적인 예시를 통해서 설명하자면, c++로 문제를 풀 때에 사용하는<br>
`#inclue<iostream>`에서 #include가 라이브러리를 가져오는 예약어, iostream이 라이브러리명이다.<br>

# 공부 시 참조 링크
[공식 레퍼런스 array](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-array/)<br>

[공식 레퍼런스 list](https://kotlinlang.org/docs/list-operations.html#binary-search-in-sorted-lists)<br>

[라이브러리,프레임워크,api에 관해서](https://velog.io/@bcl0206/API-vs-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC-%ED%92%80%EB%A6%AC%EC%A7%80-%EC%95%8A%EB%8A%94-%EB%AF%B8%EC%8A%A4%ED%84%B0%EB%A6%AC%EC%97%90-%EA%B4%80%ED%95%98%EC%97%AC)<br>
