---
title: "Kotlin in Action 3챕터-세션 4"
toc: true
toc_sticky: true
categories:
  - book
tags:
  - 안드로이드
  - 코틀린 인 액션
permalink: /categories/book/KotlinInAction/chapter3/session4
---
# 컬렉션 처리
4세션에서 주로 설명할 언어의 특성은 다음과 같다.<br>

vararg키워드를 사용하면 호출시 인자 개수를 유동적으로 조절가능한 함수를 정의할 수 있다.<br>
중위함수 호출을 통해 인자가 하나뿐인 메서드를 간편하게 호출할 수 있다.<br>
구조 분해 선언을 통해 복합적인 값은 분해해서 변수에 남아담을 수 있다.
{: .notice--success}
## 자바 컬렉션 API확장
코틀린의 collection은 자바 라이브러리 클래스의 인스턴스이다.<br>
즉 여기에 기능을 더하는 last와 max같은 것들은 모두 코틀린에서 제공해주는 확장함수인 것이다.<br>
### 컬렉션 만들기
컬렉션을 만드는 함수가 내부적으로 동작하는 방식이 바로 vararg키워드이다.<br>
컬렉션을 만들 때에 우리가 넣는 인자의 개수는 그때그떄 달라지는데, vararg키워드를 사용하면 컴파일 에러가 뜨지 않으면서 우리가 원하는 작업을 수행할 수 있도록 해준다.
## 가변 인자 함수
```kotlin
fun <T> listOf(vararg elements: T): List<T>
```
리스트를 호출하는 함수의 정의를 살펴보면 다음과 같다.<br>
`가변 길이 인자(vararg)`는 메서드를 호출시 원하는 개수만큼 값을 인자로 넘기면 컴파일러가 배열에 그 값들을 넣어준다.<br>
그렇다면 최초의 선언시점이 아닌 이미 배열에 들어간 원소를 가변 길이 인자로 넘기기위해서는 어덯게 코드를 수정해야할까?<br>
이떄에는 전달하려는 배열의 앞에 스프레드 연산자인 `*`을 붙이기만 하면 된다.<br>
### 예시
```kotlin
val list=listOf("args: ", *args)
println(list)
```
이 코드를 출력해보면 "args: args리스트의 원소"가 출력된다.<br>
## 값의 쌍 다루기
값의 쌍을 나타내는 자료구조중 하나인 map을 만들기 위해서는 mapOf함수를 이용한다.<br>
```kotlin
val map = mapOf(1 to "one", 7 to "seven", 53 to "fifty-three")
```
여기에서 to 메서드는 중위 호출 방식으로 선언된 것으로(수신 객체와 메서드 사이의 공백을 통해 알 수 있다) Pair과 유사한 기능을 해준다.<br>
만약 Pair를 호출하여 map의 인자를 나타내고 싶다면
```kotlin
val map = mapOf(
    Pair(1, "one"),
    Pair(7, "seven"),
    Pair(53, "fifty-three")
)
```
다음과 같이 길게 작성했을 코드가 to를 통해 간략하게 나타내진 것이다.<br>
### infix
아까 내가 예시로 보여준 코드는 일반 메서드에 중위호출을 사용한 예시이다.<br>
만약 함수를 중위 호출에 사용하고 싶다면 함수를 선언할 때에 infix를 앞에 추가하면 된다.<br>
```kotlin
public infix fun <A, B> A.to(that: B): kotlin.Pair<A, B> 
```
이 코드는 위에서 작성한 to가 어떻게 컴파일 되는지를 보여주는 코드이다.<br>
infix함수를 직접 만들 때에는 `infix 행동 정의 함수(리시버) 반환값`의 형태로 사용하면 된다.
```kotlin
infix fun Int.addOther(number: Int): Int {
    return this + number
}

fun main() {
    val result = 5 addOther 3
    println(result) // 출력: 8
}
```
### 구조 분해 선언
Pair을 통해 val(number,name)=1 to "one"으로 초기화를 할 수 있다.<br>
이것이 바로 구조분해 선언이다.<br>
참고로 Pair 인스턴스 이외에 다른 객체에도 구조 분해를 적용할 수 있으며 루프 구문에서 역시 사용가능하다.
```kotlin
val arrayOfPairs = arrayOf(Pair("apple", 10), Pair("banana", 5), Pair("orange", 8))

for ((fruit, quantity) in arrayOfPairs) {
    println("Fruit: $fruit, Quantity: $quantity")
}
```
이 코드는 구조분해와 for루프를 통해 arrayOfPiars라는 array의 fruit과 quantity를 비교적 간단하게 순회하며 원하는 출력을 보여준다.
### to
우리가 위에서 사용하던 to는 확장 함수다.<br>
to의 특징 중 하나는 수신객체가 제네릭 하기 때문에 타입과 사완없이 임의의 순서쌍을 만들어낼 수 있다.<br>
또한 타입이 제너릭하여 타입제한을 받지않는다는 특징 역시 가지고있기 때문에 `to list.size()`구문 등도 자유롭게 호출 가능하다.