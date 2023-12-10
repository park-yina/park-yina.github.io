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
# 공부 시 참조 링크
[공식 레퍼런스 array](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin/-array/)<br>

