---
title: "Kotlin in Action 2챕터-함수"
toc: true
toc_sticky: true
categories:
  - book
tags:
  - 안드로이드
  - 코틀린 인 액션
permalink: /categories/book/KotlinInAction/chapter2/session1
---
# [1장 바로가기](https://park-yina.github.io/categories/book/KotlinInAction/chapter1)
# 함수와 변수
## HelloWorld 찍기
```kotlin
fun main(args:Array<String>) {
    println("Hello world!")
}
```
여기에서 `args:Array<String>`을 삭제하더라도 코드는 정상작동하는 모습을 몰 수 있다.<br>
즉 코틀린은 매개변수에 대해 기본적으로 선택적인 태도를 취하여 유연성을 극대화시켰다는 것을 알 수 있다.<br>

[위의 예제를 통해 알 수 있는 코틀린의 특징]<br>
◼`fun`키워드를 통하여 함수를 선언한다.<br>
◼파라미터 이름 뒤에 그 파라미터의 타입을 작성한다.<br>
◼함수를 최상위 수준에 정의할 수 있기 때문에, 꼭 클래스 안에 함수를 넣지 않아도 된다.<br>
◼배열 처리를 위한 문법이 따로 존재하지 않는다. 즉 배열도 일반적인 클래스와 마찬가지다.<br>
◼`System.out.println` 대신 println이라고 사용한다.이는 코틀린에서 표준 자바 라이브러리를 간단하게 사용할 수 있도록 만든 래퍼를 제공하기 때문이다.<br>
◼끝줄에 세미콜론을 붙이지 않아도 된다.
{: .notice--success}

# 래퍼란 무엇인가
위의 설명에서 나오는 부분중 `wrapper`은 래퍼 함수를 의미한다.<br>
래퍼함수에는 `인터페이스 래퍼 함수`와 `자동 생성 래퍼 함수`가 있다.<br>
특정 인터페이스를더 편리하게 사용할 수 있도록 기능을 간소화 하거나 추가 가능하며, 특정 동작이나 기능을 감싸서 사용자에게 더 쉽게 접근하도록 도와줄 수 있는 기능을 한다.<br>
주로 래퍼함수는 특정 기능에 대한 사용성을 향상 시키는 데에 초점을 맞춘다.<br>
## 래퍼 클래스란
기본 자료 타입을 객체로 다루기 위해 사용하는 클래스를 의미한다.<br>
```kotlin
val myInt: Int = 42 // 기본 데이터 유형
val myWrappedInt: Int? = myInt // 기본 데이터 유형을 감싼 래퍼 클래스
```
위의 코드를 보면 Int 뒤에 `?`을 붙여 nullable하게 만들어주고 myInt를 함싼 것을 알 수 있다.<br>
래퍼 클래스를 사용하여 값이 없는 상황도 처리 가능하게 해준 것이다.<br>
또한 래퍼 클래스는 객체이기 때문에 값 자체를 사용하는 것보다 컬렉션 제너릭 등을 사용할 때에 유연한 사용을 할 수 있도록 도와준다.<br>
일반 클래스와 동일하게 상속이나 확장 역시 가능하다.<br>
(아래의 예시는 gpt가 잘못 가르쳐준 예시를 약간 변용한 코드이다)<br>
```kotlin
import java.io.BufferedReader
import java.io.InputStreamReader

open class MyWrapperClass(value: Int) {
    val wrappedValue: Int = value

    fun doSomething() {
        println("Doing something with $wrappedValue")
    }
}
open class MyExtendedWrapperClass(value: Int, extraValue: Int) : MyWrapperClass(value) {
    val extraWrappedValue: Int = extraValue

    fun doSomethingExtra() {
        println("Doing something extra with $wrappedValue and $extraWrappedValue")
    }
}

fun main() {
    val myWrapper = MyExtendedWrapperClass(42, 10)
    myWrapper.doSomething() 
    myWrapper.doSomethingExtra() 
}
```
# 함수
위에서 작성한 `HelloWorld`예제는 return 값이 따로 없는 함수를 사용하였다.<br>
의미있는 값을 작성하는 함수의 기본 형태는 다음과 같다.<br>
```kotlin
fun max(a: Int, b: Int): Int{
	return if(a>b) a else b
}
```
그리고 위 함수는 하나의 표현식으로만 이루어져 있기 때문에 `fun max(a: Int, b; Int): = if(a>b) a else b`로 줄여서 나타내는 것도 가능하다.<br>
줄여서 정의한 함수의 경우 자바의 3항 연산자와 비슷한데, `if(조건 내용) 참 반환값 거짓 시 반환값`의 구조를 가지고있다.<br>
## 식과 문의 차이
식-expression 문-statement은 코드 단위의 크기에 따라 구문된다.<br>
식의 경우 값을 가지며 평가될 수 있는 코드 단위를 의미한다.<br>따라서 식은 값을 만들어 내고 다른 식의 하위요소로 계산에 참여할 수 있다.<br>
코틀린의 경우 루프를 제외한 대부분의 제어 구조가 `식`의 형태여서 다른 식으로 엮어내는 방식을 통해 아주 간결한 표현이 가능해진다.<br>
문의 경우 프로그램에서 어떤 동작이나 작업을 수행하는 코드 단위로, 통상적으로 그 결과로 값을 반환하지는 않는다.<br>
## 식이 본문인 함수
아까 살펴본 간결한 코드는 등화와 식으로 이루어졌기 때문에 식이 본문인 함수이다.<br>
본문이 중괄호로 둘러싸인 함수의 경우 블록이 본문인 함수라고 부르는데, 인텔리 제이에서는 이 두 방식의 함수를 서로 변환하는 것도 가능하다.<br>
식이 본문인 함수의 경우 kotlin에서는, 대부분의 제어구조가 식이기 때문에 `if,when,try`등을 복잡한 식도 식이 본문인 함수로 만들어낼 수 있다.<br>
참고로 `fun max(a: Int, b; Int): = if(a>b) a else b` 표현이 가능한 것은 코틀린의 타입추론 기능 덕분인데, 식이 본문인 함수의 반환 타입만 생략이 가능하다.<br>
실전에서는 return문이 여럿 들어있는 경우가 있는데 이럴 때에는 return을 사용하고 반환타입을 명시해주어야한다.<br>
# 공부 시 참조한 링크
[래퍼 클래스란 무엇일까](https://medium.com/@s23051/%EB%9E%98%ED%8D%BC-%ED%81%B4%EB%9E%98%EC%8A%A4%EB%9E%80-wrapper-class-cc5aa6f7cdd1)<br>