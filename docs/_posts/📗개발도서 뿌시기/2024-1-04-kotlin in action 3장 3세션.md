---
title: "Kotlin in Action 3챕터-세션 3"
toc: true
toc_sticky: true
categories:
  - book
tags:
  - 안드로이드
  - 코틀린 인 액션
permalink: /categories/book/KotlinInAction/chapter3/session3
---
# [1~2세션 바로가기](https://park-yina.github.io/categories/book/KotlinInAction/chapter3/session1)
# 메서드 추가: 확장함수와 확장 프로퍼티
코틀린은 기존의 자바 코드와 자연스러운 통합을 지향한다.<BR>
그 과정에서 대부분의 코드들은 서로 자연스러운 마이그레이션이 되지만, 간혹 일부 코틀린 코드나 자바 코드는 직접 변환이 어려울 수도 있다.<BR>
이때 자바 API를 재작성하지 않고, 코틀린 언어의 편의기능만을 똑 떼어서 사용할 수 있도록 도와주는 것이 확장함수의 역할이다.
## 확장함수
### 정의
어떤 클래스의 멤버 메서드처럼 호출 가능하지만, 해당 클래스의 밖에 선언된 함수<BR>
### 만들기
함수의 이름 앞에 그 함수가 확장할 클래스의 이름을 덧붙이면 된다.<BR>
이때 클래스의 이름은 `수신 객체 타입`이라고 부르며, 확장함수가 호출되는 대상이 되는 값이 `수신 객체`가 된다.
### 예시코드
기본 형태는 `fun 클래스명.함수명:리턴타입=수신객체`의 형태이다.<br>
```kotlin
fun List<Int>.checkingOdd():List<Int>{
    val result= arrayListOf<Int>()
    for(item in this){
        if(item%2!=0)
            result.add(item);
    }
    return result;
}
fun main() {
    val number=listOf(1,2,3)
    println(number.checkingOdd())
}
```
위 예시는 filter로도 만들 수 있는 간단한 예제인데, int로 된 리스트가 들어오면 그중에서 홀수인 멤버들만 result에 넣어서 다시 결과 리스트를 만드는 방식이다.<br>
위 코드에서는 수신객체인 number직 list가 수신객체이다.
### 특징
자바 클래스로 컴파일한 클래스 파일이 있는 한 그 클래스에서 원하는대로 확장의 추가가 가능하다.<br>
즉 그루비와 같은 다른 JVM 언어로 작성된 클래스도 확장 가능하다.<br>
또한 확장 함수의 본문에서도 this를 생략하는 것이 가능하다.<br>
또한 확장함수 내에서는 private나 protected로 정의된 멤버를 사용할 수 없기 때문에, 확장함수는 캡슐화를 깨는 존재가 아닌 일종의 메서드라고 볼 수 있다.
## 임포트와 확장 함수
확장함수를 정의한 뒤에도 곧바로 사용하는 것이 아니라, import를 해야한다.<br>
그 이유는 확장 함수를 정의하자마자 어디서든 그 함수를 쓸 수 있게 되면, 이름의 중복으로 인한 충돌이 일어날 수도 있기 때문이다.<br>
그래서 코틀린에서는 클래스를 import할 때와 동일한 구문을 통해 개별 함수를 임포트 하도록 제한해두었다.<br>
### import하는법
코틀린의 문법상 확장 함수는 반드시 짧은 이름을 써야한다.<br>
따라서 확장함수를 import할 때 이름을 변경하여 사용하고 싶다면 as키워드를 사용하면 된다.<br>
{: .notice--success}

첫번째 방법: 일반 클래스처럼 import하기<br>
`import 패키지.확장함수 정의 클래스`의 형태로 하고 사용시 `val 결과=인스턴스.확장함수`로 사용하면 된다.<br>
두번째 방법: *을 사용한 import<br>
`import 패키지.*`의 형태로 사용한다.<br>
세번째 방법: as사용하기<br>
`import 패키지.확장함수 클래스 as 바꿀이름`
### 자바에서 확장함수 호출하기
