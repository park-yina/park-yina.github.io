---
title: "Kotlin in Action 2챕터 세션 5-예외처리"
toc: true
toc_sticky: true
categories:
  - book
tags:
  - 안드로이드
  - 코틀린 인 액션
permalink: /categories/book/KotlinInAction/chapter2/session5
---
# [2챕터 세션1- 함수 바로가기](https://park-yina.github.io/categories/book/KotlinInAction/chapter2/session1)
# [2챕터 세션1-변수 바로가기](https://park-yina.github.io/categories/book/KotlinInAction/chapter2/session1/1)
# [2챕터 세션2 바로가기](https://park-yina.github.io/categories/book/KotlinInAction/chapter2/session2)
# [2챕터 세션 3-4 바로가기](https://park-yina.github.io/categories/book/KotlinInAction/chapter2/session3)
# 코틀린의 예외처리
기본적인 형태는 `catch`와 `throw`로 이해할 수 있다.<br>
오류가 발생하면 예외를 던지고, 발생한 예외를 함수 호출단에서 처리하지 않으면 예외 처리 부분이 나올 때까지 예외를 다시 던지는 형태이다.<br>
또한 코틀린에서 throw는 식이기 때문에 다른 식에도 포함될 수 있다
# try, catch, finally
try를 통해 어떤 식을 검사할 것인지 명시한다.<br>
이후 catch를 통해 예외의 타입과 예외 시 return 할 내용에 대해 작성한다.<br>
finally를 통해서 예외와 상관없이 무조건적으로 실행되는 파트로, `Try->catch->finally`또는 `Try->finally`순으로 실행되게 된다.<br>
## try를 식으로 사용하기
우선 try키워드는 if나 when과 마찬가지로 `식`이기 때문에 try의 값을 변수에 대입하는 것도 가능하다.<br>
### 예시코드
```kotlin
val number = try {
    println("try")
    Integer.parseInt("7") //마지막 문장이 결과 값이 된다.
} catch (e: NumberFormatException) {
    null
}
    println("catch")
```
이 코드를 보면 number라는 변수에 try의 값을 집어넣는 것을 확인할 수 있다.<br>
또한 catch에서 예외가 생겨도 다음 코드가 실행되기를 원한다면 값을 만들어주면 된다.<br>
이 경우 역시 catch 식의 결과는 마지막 식의 값이 된다.
# 에러의 종류
책에서는 짧게 지나가는 부분이지만, 한 대제목의 내용으로 추가하였다.
## NumberFormatException
숫자형 포멧에 문제가 생겼음을 의미한다.<br>
예를 들어 int의 범위를 초과하였다거나, 숫자형이 아닌 문자열을 억지로 숫자형으로 변화하려고 하는 경우 등이 포함된다.<br>
이러한 오류들은 예외 객체이기 때문에, 직접적으로 무언가를 반환한다는 개념보다는 예기치 못한 상황을 알려줌과 동시에 프로그램이 특정 부분을 안전하게 처리할 수 있도록 도와주는 개념에 가깝다.
## IOException
주로 입출력의 문제로 발생한다.<br>
또한 직접적으로 예외를 발생시켜야하는 상황에서 `throws`를 작성하지 않아도 발생할 수 있는 에러이다.<br>
