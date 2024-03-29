---
title: "Kotlin in Action 2챕터-세션 2 클래스와 프로퍼티"
toc: true
toc_sticky: true
categories:
  - book
tags:
  - 안드로이드
  - 코틀린 인 액션
permalink: /categories/book/KotlinInAction/chapter2/session2
---
# [2챕터 세션1- 함수 바로가기](https://park-yina.github.io/categories/book/KotlinInAction/chapter2/session1)
# [2챕터 세션1-변수 바로가기](https://park-yina.github.io/categories/book/KotlinInAction/chapter2/session1/1)
# 클래스와 프로퍼티
```java
//자바코드
public class Person {
    private final String name;

    public Person(String name) {
        this.name = name;
    }

    public String getName() {
        return name;
    }
}

//코틀린 코드
class Person(val name: String)
```
우선 클래스는 논리적인 분류체계 중 하나로 내용물과 행동을 통해 객체를 정의해낸다.<br>
즉 클래스는 객체를 보여주기 위한 수단 중 하나이며, 프로퍼티는 객체의 속성과 상태를 나타내준다.<br>
이 상태를 구현해내주는 것이 바로 멤버변수이고, 위 코드에서는 `name`이 그런 역할을 해주는 것이다.<br>
그런데, 자바에서는 필드가 둘 이상으로 늘어나면 Person의 본문에서 파라미터와 필드의 대입을 위한 대입문(위 코드 기준 getNmae())도 늘어나게 된다.<br>
코틀린에서는 코드없이 데이터만 저장하는 값객체를 제공해주기 때문에 경제적인 코드 작성이 가능해진다.<br>

코틀린에서는 코드의 간결성을 위하여 불필요한 getter과 setter을 작성하지 않아도 괜찮다.<br>
이러한 작업들을 컴파일러가 알아서 해주기 때문이다.
{: .notice--success}
# 필드란
클래스 내에 있는 변수를 의미하며, 객체의 속성을 정의해주는 공간이다.<br>
지역변수나 클래스 단위의 변수까지 모두 포함하는 개념으로, 클래스 내에 있는 모든 변수들을 논리적으로 묶는 단위이다.<br>
따라서 필드는 클래스가 가지는 데이터와 행동을 논리적으로 묶어서 표현해주는 중요한 요소이다.
# 프로퍼티
클래스의 목적 중 하나는 `캡슐화`로 서로 연관성 있는 속성과 기능들을 묶어놓음으로써 외부에서의 접근을 차단하는 것이다.<br>
이러한 캡슐화는 단순히 정보를 은닉하는 역할만 하는 것이 아니라, 데이터를 다루는 코드를 한 주체 아래 가두는 방식을 통해 응집력을 강화해주는 역할도 한다.<br>
## 자바에서의 프로퍼티
자바에서는 데이터를 필드에 저장하며, 보통 멤버 필드는 private로 정의된다.<br>
Person클래스를 보아도 알 수 있듯 private에 접근하기 위하여 getter을 사용하며, 변경이 필요할 때에는 setter을 사용한다는 것을 알 수 있다.<br>
즉 클래스 내에 데이터에 접근하기 위해서는 접근자 메서드가 필요한데, 이 접근자 메서드에는 필드를 읽는 데에 사용되는 `getter`가 필수요소이고 변경을 위한 `setter`은 추가제공 요소인 것이다.<br>
자바에서는 필드와 접근자를 한 데에 묶어 `프로퍼티`라고 부르며 이 개념을 바탕으로한 프로퍼티가 많다.
## 코틀린에서는
기본적으로 프로퍼티만으로 필드와 접근자 메서드를 대신하는 것이 가능하다.<br>
프로퍼티 선언시에도 변수 선언과 마찬가지로 val과 var을 사용하는데 val은 읽기 전용 var은 변경가능(쓸 수 있다)한 속성을 가지게 된다.<br>
val의 경우 `읽기 전용`이기 때문에 getter만을 가지게 되며, 비공개 필드를 만들어내게 된다.<br>
var의 경우 `변경`역시 가능해야하기 때문에, 자연스럽게 getter과 함께 setter도 만들어내게 된다.
## 코드를 통한 비교
```java
//java 코드
Person person=newPerson("Bob",true);
System.out.println(person.getName());
//코틀린
val person=Person("Bob",true);
println(person.name)
```

참고로 자바에서는 이름이 is로 시작하는 프로퍼티의 게터에는 get이 붙지 않고 원래 이름대로 사용하고, 세터에서는 set으로 바꾼 이름을 사용한다.
{: .notice--success}
코틀린에서는 위 코드를 보아도 알 수 있듯 게터를 호출하지 않아도 자동으로 호출해주는 모습을 확인할 수 있다.<br>
참고로 프로퍼티에는 그 프로퍼티의 값을 저장하기 위한 필드(뒷받침 필드)가 있는데, 커스텀 게터를 작성하면 프로퍼티의 값을 그때그때 계산하게 할 수도 있다.
# 커스텀 접근자
기본적으로 코틀린에서는 접근자를 컴파일러가 알아서 만들어주기 때문에 굳이 게터를 쓰지 않아도 된다는 언급을 하였다.<br>
그러나, 위에서 말했다시피 `getter`의 동작을 직접 계산하게 만드는 등의 커스텀을 하고싶을 때가 있다.<br>
그럴 때에 사용하는 것이 바로 `get()`메서드로 getter의 동작을 커스터마이징하는 역할을 해준다.
## 예시 코드
```java
class Rectangle(val height: Int, val width: Int) {
    val isSquare: Boolean
        get() {
            return height == width
        }
}
```
여기에서는 get을 통해 height와 width가 같은 값을 가진다면 true를 반환하는 동작을 커스터마이징 하였다.<br>
참고로 isSquare는 값을 자체로 저장하는 것이 아니라 그때그때 계산하여 `true/false`를 반환하는 방식으로 작동하게 된다.<br>
파라미터가 없는 식과는 구현이나 성능에서는 거의 차이가 없다.<br>
하지만,보통 클래스의 특성을 정의하기 위해서는 프로퍼티로 그 특성을 정의한다는점에서 가독성은 차이가 날 수 있다.
# 코틀린 소스코드 구조
자바의 경우 모든 클래스를 패키지 단위로 묶어서 관리한다.<br>
코틀린에서도 유사한데, 모든 코틀린 파일의 맨 앞에는 pacakge문을 넣을 수 있고, 그 파일 안에 있는 모든 선언들이 해당 패키지에 들어가게 된다.<br>
같은 패키지 안에 있다면, 다른 파일에서 정의한 선언도 직접 사용 가능하며 다른 패키지에서 정의한 선언은 import를 통해 사용하여야 한다.<br>
패키지 이름 뒤에 ` .*`을 추가하면, 패키지 안에 모든 선언을 import할 수 있고 이것을 스타틱 임포트라고 부른다.<br>
`자바와 코틀린을 함께 사용하는 프로젝트에서`는 `자바`의 규칙을 따르는 것이 좋다.<br>
하지만, 코틀린에서는 클래스의 소스코드가 아주 작은 경우도 있기 때문에 여러 클래스를 한 파일에 넣는 등의 상황이 생길 수 있다.<br>

자바와 함께 협업을 하는 경우, 자바 클래스를 코틀린 클래스로 마이그레이션 하는 과정에서 문제가 생길 수도 있기 때문이다.<br>
코틀린과 자바는 원칙적으로는 변환 가능하지만, 디렉터리 구조가 다를 시 문제가 생길 수 있다
{: .notice--success}

## 디렉터리 구조
자바:패키지 구조와 일치하는 디렉터리 계층 구조를 만들고<br>
클래스의 소스코드를 그 클래스가 속한 패키지와 같은 디렉터리에 위치 시켜야한다.<br>
코틀린:원하는 대로 소스코드를 구상하는 것이 가능하다.
# 마이그레이션
어떤 시스템이나 소프트웨어를 다른 환경으로 옮기는 일이다.<br>
코틀린과 자바는 원칙적으로 마이그레이션이 자유롭지만 상황에 따라 문제가 생길 수 있다.<br>
## 코틀린->자바
우리가 사용하는 코루틴의 작동방식은 자바의 스레드 기반과는 차이가 있다.<br>
따라서 코틀린에서 자바로 옮길 때에는 비동기 방식의 처리에 유의해야한다.<br>
또한 null에 대한 안전성이 자바와 코틀린은 접근 방식이 다르기 때문에 `null`처리를 유의해야한다.
## 자바->코틀린
주로 자바에서 코틀린은 문제가 발생하지 않는다.<br>
이는 코틀린이 좀 더 나중에 나온 언어인데, 처음 나오는 시점에서부터 자바와의 호환성에 초점을 두고 나왔기 때문이다.

# 공부 시 참조 링크
[자바 필드 개념](https://ittrue.tistory.com/118)<br>
[마이그레이션이란](https://www.redhat.com/ko/topics/automation/what-is-it-migration#%EA%B0%9C%EC%9A%94)