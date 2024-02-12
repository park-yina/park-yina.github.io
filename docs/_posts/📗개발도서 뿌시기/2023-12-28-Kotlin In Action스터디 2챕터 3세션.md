---
title: "Kotlin in Action 2챕터 세션 3~4, 선택과 표현"
toc: true
toc_sticky: true
categories:
  - book
tags:
  - 안드로이드
  - 코틀린 인 액션
permalink: /categories/book/KotlinInAction/chapter2/session3
---
# [2챕터 세션1- 함수 바로가기](https://park-yina.github.io/categories/book/KotlinInAction/chapter2/session1)
# [2챕터 세션1-변수 바로가기](https://park-yina.github.io/categories/book/KotlinInAction/chapter2/session1/1)
# [2챕터 세션2 바로가기](https://park-yina.github.io/categories/book/KotlinInAction/chapter2/session2)
# 선택과 표현의 처리
when은 자바의 switch를 대체하되 더욱 강력하다.<br>
switch와 when은 조건이 많을 때에 if를 대체하면 가독성이 좋아진다는 장점이 있다.<br>
또한 정말 온갖 것들(범위 지정,다양한 타입 등)을 코틀린의 when에서는 사용 가능하기 때문에, 자바의 switch보다 유연한 사용이 가능하다.
## enum클래스 정의
코틀린에서 enum은 자바보다 선언에 더 많은 키워드를 써야한다.<br>
[양식]<br>
```java
enum class 클래스명{
    요소
}
```
{: .notice--success}
의 양식으로 코틀린에서는 사용하는 데에 비해 java에서는 `enum`클래스명의 형태로 나타낼 수 있다.<BR>
하지만, 코틀린에서는 enum이 `소프트 키워드`로 분류되어있기 때문에, Class의 앞에 사용하면 우리가 아는 `enum`의 용도로 사용가능하지만 다른 곳에서는 이름으로 사용할 수도 있다.<br>
(그런데 혼선을 빚지 않기 위해서는 저런 애매한 키워드들은 사용하지 않는 것이 좋을 것 같다.)<br>
참고로 enum의 코틀린에서 몇 안되게 세미콜론이 필수적인 부분이다.<br>
## 코드 예시
```kotlin
// enum 클래스 선언
enum class Direction {
    // 각 enum 상수와 함께 프로퍼티와 메서드 정의
    NORTH {
        override val axis: Char = 'Y'
        override fun printDescription() {
            println("Moving NORTH along the $axis-axis")
        }
    },
    EAST {
        override val axis: Char = 'X'
        override fun printDescription() {
            println("Moving EAST along the $axis-axis")
        }
    },
    SOUTH {
        override val axis: Char = 'Y'
        override fun printDescription() {
            println("Moving SOUTH along the $axis-axis")
        }
    },
    WEST {
        override val axis: Char = 'X'
        override fun printDescription() {
            println("Moving WEST along the $axis-axis")
        }
    };

    // enum 상수에 대한 프로퍼티
    abstract val axis: Char

    // enum 상수에 대한 메서드
    abstract fun printDescription()
}

fun main() {
    // enum 상수 사용
    Direction.NORTH.printDescription()
    Direction.EAST.printDescription()
    Direction.SOUTH.printDescription()
    Direction.WEST.printDescription()
}

```
코드 출처: chat gpt<br>
여기 이 enum을 보면 열거가 끝난 뒤 메서드 시작 지점 직전에 세미콜론을 사용하여 열거부분(상수)과 메스드 정의 부분을 분리한 것을 알 수 있다.<br>
또한 enum의 상수정의 부분에는 단순한 초기화값 이외에도 상수에 대해 구현할 함수가 함께 들어갈 수 있다는 것 역시 확인 가능하다.
## when으로 enum 다루기
when은 if와 마찬가지로 값을 만들어내는 식이다.<br>
kotlin에서는 주로 조건이 3개 이상으로 나뉘는 경우 if대신 when의 사용을 권장하며, 자바와 달리 각 분기의 끝에 brak를 넣지 않아도 된다.<br>
### 하나의 분기, 여러개의 값
when을 사용하면서 가끔 하나의 분기 안에 여러개의 값을 넣고 싶은 경우가 있다.<br>
성적이 'a+,a,a-'인 경우 우수를 출력하도록 하고 싶은 경우
`Score.aplus,Score.a,Score.aminus->"우수"`와 같이 각 값들을 콤마로 구분하여 사용하면 된다.
### when과 임의의 객체
위에서 자바의 switch보다 코틀린의 when이 강력하다고 했던 이유이다.<br>
자바의 switch에 상수만을 사용할 수 있지만, 코틀린의 when은 임의의 객체를 하용한다.<br>
```kotlin
fun mix(c1:Color, c2:Color) = 
	when(setOf(c1, c2)){
    	setOf(RED, YELLOW) -> ORANGE
		setOf(YELLOW, BLUE) -> GREEN
        setOf(BLUE, VIOLET) -> INDIGO
        else -> throw Exception("Dirty color")
	}
```
이 코드를 보면 when식이 두 색을 혼합하여 다른 색을 만들 수 있는 경우 특정 색을 반환하고 그렇지 않은경우 else를 통해 예외상황임을 나타내준다.<br>
setOf의 경우 읽기 전용 집합을 만들어내는 역할을 하기 때문에, 단일값을 비교하는 데에 특화된 switch문에서는 이런 표현을 사용하기 어렵다.<br>
#### 특징
여기에서 알 수 있는 특징에는 한가지가 더 숨어있다.<br>
바로 when의 경우 위에서부터 순차적으로 분기가 진행되며, 조건 값을 찾을 때까지 각 분기를 검사한다는 것이다.<br>
위와 같이 문자열을 반환하는 경우 이게 왜 중요할까 알기 어렵지만, Int를 통해 범위를 정한다거나 특정 범위에 대한 print를 반환하는 등 값의 크기가 중요한 경우 순차적 검사라는 특징 역시 중요하다.
```kotlin
when {
    benefitPrice >= 20000 -> println(SANTA)
    benefitPrice >= 10000 -> println(TREE)
    benefitPrice >= 5000 -> println(STAR)
    else -> printlnt("없음")
}
```
이렇게 범위가 중요한 when문의 경우 순서를 바꾸어 출력을 시도할 시 잘못된 값을 출력하게 된다.
## 인자가 없는 when
미리 말하자면, 인자가 없는 when은 가독성이 떨어진다는 단점이 있다.<br>
하지만, setOf와 같이 호출이 될 때마다 인스턴스를 생성하는 라이브러리를 과도하게 호출하면 불필요한 객체가 늘어나 성능의 저하가 발생할 수 있다.<br>
이럴때 사용 가능한 것이 바로 인자가 없는 when이다.
### code
```kotlin
fun mixOptimized(c1:Color, c2:Color) = 
	when{
    	(c1 == RED && c2 == YELLOW) ||
        (c1 == YELLOW && c2 == RED) ->
        ORANGE
        (c1 == YELLOW && c2 == BLUE) ||
        (c1 == BLUE && c2 == YELLOW) ->
        GREEN
        (c1 == BLUE && c2 == VIOLET) ||
        (c1 == VIOLET && c2 == BLUE) ->
        INDIGO
        else -> throw Exception("Dirty color")
	}
```
## 스마트 캐스트
두 수를 더하기 위해서는 숫자와 합계가 존재한다.<br>
만약 숫자가 3개라면 이전의 합계값에 새로 입력된 숫자를 더하는 방식으로 함수를 짜면 된다.<br>
이때 이 변수가 sum을 하고자하는지 num인지를 판단한 뒤 자동으로 형변환까지 해주는 것이 스마트 캐스트이다.
### code
```kotlin
interface Expr
class Num(val value: Int) : Expr
class Sum(var left: Expr, val right: Expr) : Expr

fun eval(e: Expr): Int =
        when (e) {
          is Num -> e.value
          is Sum -> eval(e.left) + eval(e.right)
          //is를 통해 값 점검 후 자동으로 캐스팅
          else -> throw IllegalArgumentException()
        }
```
### is
is를 사용하면 변수의 타입을 검사 가능하다.<br>
책에서 나온 예제 같이 내가 만든 인터페이스에 대해 속하는지 나타내는 것 이외에도 `Int`인지 검사하는 등의 기능으로 사용도 가능하다.<br>
## if와 when
만약 저 when문을 if로 바꾸고자 한다면 좀 더 코드가 복잡해지게 된다.<br>
```kotlin
fun eval(e: Expr): Int =
if(e is Num){
  e.value
}
else if(e is Sum){
  eval(e.right)+eval(e.left)
}
else{
  오류 반환
}
```
의 형태로 작동한다.<br>
이렇게 코드를 정리하여 보면 when이 단순히 동등성 검사를 수행하는 역할 이외에도 받은 값에 대해 스마트 캐스트를 하는 데에 사용하거나, 일정 조건에 따른 함수 반환을 하는 등의 역할로 사용할 수 있음을 알 수 있다
## 주의점
`if/when`은 둘다 블록의 마지막 문장이 블록 전체의 결과가 된다.<br>
try본문과 catch절 역시 마찬가지인데, 주의해야할 점은 함수에서는 위 규칙이 성립하지 않는다.<br>
그래서 식이 본문인 함수는 블록을 본문으로 가질 수 없다.<BR>
또한 블록이 본문인 함수의 경우 무조건 내부에 return문을 필요로 한다.
# 이터레이션
코틀린의 while은 자바와 동일, for는 자바의 for-each루프와 동일하다.<br>
## while
while에는 while과 do-while이 있다.<br>
do-while의 경우 맨처음 본문을 무조건 한번 실행 이후, 뒤에 나오는 while은 조건이 참인동안 본문을 반복실행하는 형태다.<br>
[while기본](https://pang2h.tistory.com/312)
## 수 이터레이션
코틀린에서는 우리가 자바나 c++에서 접하던 기본 for문이 없다.<br>
그래서 코틀린은 `for(초기값;증가에 대한 부분; 최종값)`의 형태로 이루어진 대신 range를 사용한다.<br>
`..`을 사용하여 탐색하는 방식으로 양쪽 끝 값을 표시하는 형태로 사용한다.<br>
### down To
보통의 for문은 1부터 100까지 1씩 증가 이런 식으로 사용하지만, 역박향의 탐색이 필요한 경우도 있다.<br>
이때 사용하는 것이 downTo로 `i in 시작값 downTo 끝값 step 다운값 `으로 나타낼 수 있다.<br>
until의 사용하면 한쪽 범위만 표시한 뒤 특정 배열의 크기만큼 탐색하는 등의 작업을 할 수 있다.
## 맵 이터레이션
우선 TreeMap을 사용하면 키에 대한 정렬이 가능하다.<br>
get과 put을 사용하는 다른 언어와 달리 코틀린에서는 `map[키]=값`과 같은 직관적인 값을 가져오거나 설정하는 것이 가능하다.<br>
또한 arrayList에서도 `for((index,element)in list.withIndex())`와 같은 형태로 인덱스와 요소에 대한 검색 및 출력을 하는 것이 가능하다
## in을 통한 검사
in 연산자를 사용하면 값이 어떤 범위에 속해있는지를 검사할 수 있고, !in을 사용하면 어떤 값이 범위에 속하지 않는지에 대한 검사가 가능하다.<br>
또한 예문은 문자로 사용하였으나, 문자나 Int 이외에도 비교 가능한 모든 클래스의 인스턴스 객체를 사용하여 범위를 만들 수 있다.<br>
즉 string을 통해 어떠한 집합에 이 문자가 들어가있는지를 탐색하는 작업도 in을 사용해서 검사하는 게 가능하다는 것이다.