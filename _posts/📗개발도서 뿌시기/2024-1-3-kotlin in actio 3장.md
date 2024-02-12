---
title: "Kotlin in Action 3챕터-세션 1~2"
toc: true
toc_sticky: true
categories:
  - book
tags:
  - 안드로이드
  - 코틀린 인 액션
permalink: /categories/book/KotlinInAction/chapter3/session1
---
# 함수 정의와 호출
앞선 내용과 달리 3장은 함수 정의와 호출 기능을 코틀린이 어떻게 개선하였는지를 보여준다.<br>
또한 확장 함수와 프로퍼티를 사용하여 자바 라이브러리를 코틀린 스타일로 적용하는 방법을 살펴본다는 내용으로 미루어보아 코틀린이 가질 수 있는 장점에 대해 보여주고자 하는 챕터로 추정된다.
# 코틀린에서 컬렉션 만들기
코틀린에서 hash set of나 arrayListOf등을 사용하면 어떤 라이브러리가 import될까?<br>
만약 이런 게 궁금하다면 `println(변수명.getClass())`로 출력값을 찍어보면 쉽게 알 수 있다.<br>
참고로 코틀린에서 컬렉션에 대한 getClass를 해보면 `class java.util`이 뜨는 모습을 확인할 수 있다.<br>
`그렇기 때문에 자바와의 호환이 자유로우며` 더 많은 기능을 사용하는 것 역시 가능하다.
## 컬렉션 만드는법
```kotlin
val set=hashSetOf(1,7,53)
val list=arrayListOf(1,7,53)
val map=hashMapOf(1 to "one",2 to "two")
```
여기에서 to는 일종의 매핑 기능으로 1이라는 key에 "one"이라는 value를 매치시킨다고 이해하면 된다.<br>
참고로 to의 경우 언어가 제공하는 특별 키워드가 아닌 일반 함수로 분류된다.
# 쉬운 함수호출
우리가 주로 사용하는 joinToString을 구현하기 위해서는 어떡해야할까<br>
우선 글자를 연결할 때 사용할 구분자와 필요하다면 맨 앞에 호출할 접두, 맨 뒤에 호출할 접미가 필요할 것이다.<br>
따라서 나는 책에 나온 예제를 아주 약간 변용하였다.
```kotlin
import kotlin.collections.Collection
fun <T> joinToString(collection:Collection<T>, seperator:String, prefix:String, postfix:String):String{
    val result=StringBuilder(prefix)
    for((index,element)in collection.withIndex()){
        if(index>0)result.append(seperator)
        result.append(element)
    }
    result.append(postfix)
    return result.toString()
}
fun main() {
    val list=listOf(1,2,3)
    println(joinToString(list,",","(",")"))
}
```
하지만, 코틀린을 조금이라도 다루어본 사람이라면 이 코드 뭔가 지저분하고 익숙하지 않은 느낌이다라는 인상을 받을 것이다.<br>
# 이름 붙이기
위에서 작성한 함수의 문제점 중 하나는 가독성이 지나치게 떨어진다는 것이다.<br>
지금은 함수가 딱 2개 뿐이니 호출할 함수의 인자를 외워서 작성하여도 되지만, 실제 현장에서는 수많은 함수가 존재하고 그때마다 모든 타입을 맞추어 작성하는 것은 어려울 뿐더러 읽는 입장에서도 함수 내용이 이해가 어려울 수 있다.<br>
그래서 자바에서는 enum타입을 사용하고, 코틀린에서는 함수에 전달하는 인자의 이름을 명확히 표현하는 방식을 사용한다.
## 코드
```kotlin
fun main() {
    val list=listOf(1,2,3)
    println(joinToString(list,",", prefix = "(", postfix = ")"))
}
```
참고로 하나의 인자 이름을 명시했다면, 내가 작성한 코드처럼 하는 것이 아니라 모든 인자의 이름을 명시하는 것이 정석이다.
# 디폴트 파라미터 값
만약 perfix와 postfix없이 seperator만 필요한 경우 어떡해야할까?<br>
코틀린에서는 이러한 문제를 해결하기 위해 디폴트 값을 함수 선언의 단계에서 사용할 수 있다.<br>
이렇게 코드를 수정할 시 내가 필요한 부분에 한하여 인자를 전달하는 등의 표현이 가능하다.
## 코드
```kotlin
import kotlin.collections.Collection
fun <T> joinToString(collection:Collection<T>, seperator:String, prefix:String="", postfix:String=""):String{
    val result=StringBuilder(prefix)
    for((index,element)in collection.withIndex()){
        if(index>0)result.append(seperator)
        result.append(element)
    }
    result.append(postfix)
    return result.toString()
}
fun main() {
    val list=listOf(1,2,3)
    println(joinToString(list,","))
}
```
## 자바에서
자바에서는 디폴트 파라미터 값의 개념이 없기 때문에 위와 같이 작성된 코드를 자바로 마이그레이션할 시 문제가 생길 수 있다.<br>
그럴 때에는 jotinToString에 `@JvmOverloads`애너테이션을 추가하면 코틀린 컴파일러가 알아서 생략된 파라미터에 대해 오버로딩한 자바 메서드를 추가하여준다.
## 최상위 함수와 프로퍼티
JDK의 Collections클래스를 보면 비슷한 역할을 하는 api들이 모여있는 것을 확인할 수 있다.<br>
이는 자바가 객체지향 언어이기 때문에 모든 코드를 클래스의 메서드로 작성해야하기 때문이다.<br>
Collections의 내부에 있는 arrayList에 대해 잘 생각해보자.<br>
우리가 arrayList를 import 하기만 하면 arrayList에 대한 모든 연산들이 가능해진다.<br>
이는 arrayList라는 인스턴스 api안에 우리가 사용하고자 하는 기능(정적 메서드)들을 모두 모아두었기 때문이다.
### 코틀린에서
코틀린에서는 이러한 무의미한 클래스는 굳이 사용하지 않는다.<br>
대신 함수를 직접 최상위 수준에 위치시키면, 그 함수 역시 패키지의 멤버이기 때문에 다른 패키지에서도 패키지만 import하면 함수를 사용할 수 있다.<br>
JVM은 원칙대로라면 클래스 안에 들어있는 코드만을 실행할 수 있다.<br>
그래서 컴파일러는 파일을 컴파일 할 때마다 새로운 클래스를 정의하여준다.<br>
자바에서는 코틀린에서 만든 최상위 함수인 joinToString의 패키지인 strings를 통해 pulicClass로 불러와진다.<br>
즉 우리가 코틀린에서 만든 코드를 자바는 클래스를 생성한 뒤 그 안에 메서드나 필드로 만들어서 사용한다.
#### 클래스 이름 바꾸기
만약 JVM의 클래스 이름을 변경하고 싶다면 파일에 `@ JvmName`애너테이션을 추가하도록 한다.
### 최상위 프로퍼티
함수와 마찬가지로 코틀린에서는 프로퍼티도 최상위 수준에 놓을 수 있다.<br>
어떠한 데이터를 클래스 밖에 놓은 뒤 값을 읽어오는 방식으로 사용할 수 있다.<br>
이때 주의할 점은 최상위에 val과 var을 모두 놓을 수 있다는 것인데 코틀린 코드를 자바로 바꿀 때에 상수와 같이 보이는 것을 게터를 사용하면 부자연스럽게 된다.<br>
따라서 최상위 계층에 위치한 val이 상수처럼 쓰이는 게 자연스러운 상황에서는 `const val`의 사용하는 것이 좋다.<br>
이 const val의 경우 원시타입과 string에서만 사용가능하다는 것을 유의하여야한다.
#### 원시타입이란
원시타입은 실제 데이터가 담기는 방식으로 스택 영역에 정의된다.<br>
참조 타입은 원시타입의 데이터를 읽을 수 있는 주소값이 스택 영역에 들어가게 된다.<br>
int i=0의 경우 i라는 그릇에 0이 들어가는 원시 타입이라고 생각하면 된다.<br>
참조 타입은 자바에서 new를 통해 만들어내는 객체들을 떠올리면 된다.