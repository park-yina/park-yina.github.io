---
title: "Kotlin in Action 3챕터-세션 6"
toc: true
toc_sticky: true
categories:
  - book
tags:
  - 안드로이드
  - 코틀린 인 액션
permalink: /categories/book/KotlinInAction/chapter3/session6
---
# 코드 다듬기: 로컬 함수와 확장

개발자들이 중요시하는 좋은 코드의 특징 중 하나는 `중복 없는코드`이다.<br>
그렇다면 자바와 코틀린은 각각 이러한 목표에 어떻게 도달할까
{: .notice--success}

# 자바에서의 코드 다듬기
자바에서는 `반복하지 않기`를 실천하는 것이 상당히 어렵다.<br>
그 이유 중 하나는 자바에서 메서드 추출을 하게될 시 클래스 안에 작은 메서드가 많아지고 각 메서드 간의 관계를 파악하기 복잡해지기 때문이다.<br>
물론 inner class를 통해 추출된 메서드를 정리하는 방법도 있으나 그에 따른 불필요한 코드가 늘어나는 것도 감수해야한다.
## 코드를 통해 보는 상황
```java
public class ComplicatedTaskProcessor {

    public void processComplicatedTask() {
        // 여러 복잡한 작업들이 이곳에 포함되어 있음
        step1();
        step2();
        step3();
        step4();
        step5();
    }

    private void step1() {
        // Step 1의 작업 수행
        System.out.println("Step 1 completed.");
    }

    private void step2() {
        // Step 2의 작업 수행
        System.out.println("Step 2 completed.");
    }

    private void step3() {
        // Step 3의 작업 수행
        System.out.println("Step 3 completed.");
    }

    private void step4() {
        // Step 4의 작업 수행
        System.out.println("Step 4 completed.");
    }

    private void step5() {
        // Step 5의 작업 수행
        System.out.println("Step 5 completed.");
    }

    public static void main(String[] args) {
        ComplicatedTaskProcessor processor = new ComplicatedTaskProcessor();
        processor.processComplicatedTask();
    }
}

```
이렇게 보면 우리에게 생긴 문제상황을 보다 분명하게 알 수 있을 것이다.<br>
짤막하게 보아도 알 수 있듯 오류가 생겼을 때에는 찾아봐야할 부분이 늘어날 뿐 아니라, 각가의 함수가 어디에 있고 어떤 역할을 하는지 한눈에 알아보기 여려워진다.
# 코틀린에서의 해법
코틀린에서는 함수에서 추출한 원 함수를 내부에 중첩시키는 것이 가능하다.<br>
즉 로컬 함수로 분리하는 과정을 통해 중복을 없애고 코드의 구조를 바꾸는 것이 가능하다.<br>
또한 로컬함수는 자신이 속한 원함수의 모든 파라미터와 변수를 사용할 수 있기 때문에, 불필요한 파라미터 역시 제거 가능하다.
# 단계별 코드로 살펴보기
## 1단계: 중복의 문제가 있는 코드
```kotlin
class User(val id:Int, val name:String, val address:String)
fun saveUser(user:User){
    if(user.name.isEmpty()){
        throw IllegalArgumentException(
            "Cant save user ${user.id} empty name"
        )
    }
    if(user.address.isEmpty()){
        throw IllegalArgumentException(
            "Cant save user ${user.id} empty address"
        )
    }
}
fun main(){
   return saveUser(User(1,"",""))
}

```
## 2단계: 로컬함수로 코드 중복 없애기
validate라는 함수를 만들어서 중복을 제거하는 단계이다.<br>
```kotlin
class User(val id:Int, val name:String, val address: String)

fun saveUser(user:User){
    fun validate(user:User,
                 value:String,
                 fieldName:String){
        if(value.isEmpty()){
            throw IllegalArgumentException(
                "Can't save user ${user.id}: empty $fieldName"
            )
        }
    }

    validate(user,user.name,"Name")
    validate(user,user.address,"Address")
}
```
위의 코드에서는 user.필드.isEmpty()가 반복된 반면, 2단계에서는 validate를 통해 user의 필드 두개를 검사하는 모습을 보여준다.<br>
검사를 요하는 name과 address필드가 모두 string이기 때문에 함수의 파라미터를 String으로 설정해준 것을 알 수 있다.
## 최종 단계: 로컬함수의 특징을 이용한다
로컬함수의 주요 특징 중 하나는, 자신이 속한 바깥쪽 함수의 모든 파라미터와 변수를 사용할 수 있다는 것이다. 따라서 User파라미터를 없애고 바로 바깥쪽 함수의 파라미터를 읽는 방식으로 코드를 짜는 것 역시 가능하다.
```kotlin
class User(val id:Int, val name:String, val address: String)

fun saveUser(user:User){
    fun validate(value:String,
                 fieldName:String){
        if(value.isEmpty()){
            throw IllegalArgumentException(
                "Can't save user ${user.id}: empty $fieldName"
            )
        }
    validate(user.name,"Name")
    validate(user.address,"Address")
    }
}
```
이런 식으로 로컬함수의 특징을 이용하면, 바깥 함수에서 호출한 user을 코드상으로는 다시 호출하지 않더라도 컴파일 에러가 일어나지 않고 원하는 대로 작동한다.
### 그럼 메모리 상으로는?
책에서는 나와있지 않은 내용이나, 궁금해진 내용 중 하나가 바로 로컬함수와 외부함수(바깥 함수)가 어떻게 호출을 하는가였다.<br>
만약 그때그때 우리가 필요할 때마다 재귀를 하는 형태라면 실질적인 서비스를 구상할 때에는 로컬 함수가 외부 함수를 호출을 잦게 할 시 코루틴 등으로 별도 처리를 해주어야할 것이다
- 결론<br>
로컬함수 내에서 외부 함수의 값에 접근하면 값이 복사되는 것이지, 함수가 재귀적으로 호출되는 것은 아니다.<br>
따라서 로컬함수의 호출이 완료되면 해당 복사본은 소멸하고 값만 남게 되며 메모리 상에서는 복사된 값만이 독립적으로 유지된다.


## 확장 함수로 변경한다.
```kotlin
fun User.validateBeforeSave() {
    fun validate(value: String, fieldName: String) {
        if (value.isEmpty()) {
            throw IllegalArgumentException(
               "Can't save user $id: empty $fieldName")
        }
    }

    validate(name, "Name")
    validate(address, "Address")
}

fun saveUser(user: User) {
    user.validateBeforeSave()
}
```
이와 같이 User클래스의 확장함수로 변경을 하게 되면 User과 검증함수 사이의 관계를 잘 표현하면서 중복을 없애는 것도 가능하다.
## 번외: 초기화 블럭 사용
책에는 나와있지 않은 부분이지만, User의 클래스 내에 init이라는 초기화 블럭과 require이라는 특정 조건을 확인하는 함수를 통해서 코드를 보다 경제적으로 작성하는 방법도 있다<br>
```kotlin
class User(val id: Int, var name: String, var address: String) {
    init {
        require(name.isNotEmpty()) { "Can't save user $id: empty Name" }
        require(address.isNotEmpty()) { "Can't save user $id: empty Address" }
    }
}

```