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
확장함수는 수신 객체를 첫 번째 인자로 받는 메서드의 성격을 지닌다.<br>
그래서 자바에서는 확장함수 호출 시 다른 어댑터 객체나 실행 시점에 대한 부가 비용이 들지 않는다.<br>
자바에서 확장함수를 호출하는 방법 역시 코틀린에서와 큰 차이는 없다.<br>
`char c=파일명.확장함수("인자");`의 형태로 사용한다.
#### 확장함수의 작동원리
그렇다면 자바에서는 코틀린 코드의 확장함수를 어떤 방식으로 사용하길래 다른 어댑터 객체에 대한 부가 비용이 들지 않는 것일까?<br>
인텔리 제이를 통해 아까 작성한 코드를 자바로 마이그레이션 하면 다음과 같은 코드가 나오게 된다.<br>
```java
public final class MainKt {
   @NotNull
   public static final List checkingOdd(@NotNull List $this$checkingOdd) {
      Intrinsics.checkNotNullParameter($this$checkingOdd, "$this$checkingOdd");
      ArrayList result = new ArrayList();
      Iterator var3 = $this$checkingOdd.iterator();

      while(var3.hasNext()) {
         int item = ((Number)var3.next()).intValue();
         if (item % 2 != 0) {
            result.add(item);
         }
      }

      return (List)result;
   }

   public static final void main() {
      List number = CollectionsKt.listOf(new Integer[]{1, 2, 3});
      List var1 = checkingOdd(number);
      System.out.println(var1);
   }

   // $FF: synthetic method
   public static void main(String[] var0) {
      main();
   }
}
```
눈 여겨 보아야할 지점은 우리가 작성한 확장함수가 자바에서는 static final 함수로 변환되어있다는 것이다.<br>
따라서 자바는 우리가 만든 확장함수들을 상수처럼 static final로 변환하기 때문에 인스턴스가 만들어질 때마다 새로운 공간을 만들지 않아서 경제적이다.
### 확장 함수로 유틸리티 함수 정의하기
확장함수는 정적 메서드를 보다 편하게 호출하도록 도와주는 문법적인 도구일 뿐이다.<br>
그렇기 때문에 수신 객체의 타입을 클래스가 아닌 보다 구체적인 타입(list와 같은)으로 지정해주는 것도 가능하다.<br>
확장함수는 정적 메서드와 같은 특징을 지니기 때문에 확장함수를 하위 클래스에서 오버라이드 하는 것은 불가능하다.
### 오버라이드에 관련된 예시
코틀린에서의 메서드 오버라이드는 일반적인 객체지향의 메서드 오버라이드와 마찬가지이다.<br>
하지만, 확장함수는 클래스의 바깥에서 선언되어있기 때문에 우리가 생각하는 방식의 일반적인 오버라이드는 불가능하다.
#### 오버라이드란
오버라이딩은 부모 클래스의 메서드를 자식 클래스에서 재정의(수정/추가)하는 것을 의미한다.<br>
예시코드<br>
```kotlin
open class View{
    open fun click()=println("clicker")
}
class Btn:View(){
    override fun click()=println("Button Clicked")
}
```
이렇게 Btn클래스에서 click를 불러왔을 때에 과연 Btn클래스에서 어떤 함수가 호출될까?<br>
원래 click이 정의되어있던 부모클래스일까 아니면 오버라이드된 함수일까?<br>
정답은 Btn에서 오버라이드된 click가 호출되는 것이다.
#### 확장함수는?
확장함수는 클래스의 바깥에서 선언한다.<br>
그렇기 때문에, 수신객체로 지정된 변수의 타입에 의해 확장함수의 호출이 결정되지 그 변수에 저장된 객체의 동적인 타입에 의해 확장함수가 결정될 수는 없다.<br>
따라서 이름과 파라미터가 완전히 동일한 확장함수를 재정의하는 방식으로 코드를 짜더라도, 위에서 작성한 코드처럼 작동할 수는 없다.<br>
## 확장 프로퍼티
확장 프로퍼티는 이름은 프로퍼티지만, 상태를 저장할 방법이 없기 때문에 아무런 상태도 가질 수 없다.<br>
주의점 중 하나는 확장 프로퍼티를 사용하면 일반적인 코틀린의 방식과는 달리 최소한의 게터를 꼭 정의해주어야한다.<br>
### 선언법
기본적인 선언법<br>
```kotlin
val String.lastChar:char
get()=get(length-1)
```
만약 var처럼 변경이 가능한 프로퍼티를 선언하고 싶다면 다음과 같이 쓰면 된다.<br>
```kotlin
var String.lastChar:char
get()=get(length-1)
set(value:char){
   this.setCharAt(length-1,value)
}
```
위에 코드와는 달리 세터까지 추가된 모습을 볼 수 있다.<br>
변경이 가능한 프로퍼티의 경우 `가변성`때문에 세터의 사용역시 강제화된다.