---
layout: post
title:  "5.1 람다 식과 멤버 참조"
date:   2022-11-06 19:24:43 +0900
categories: jekyll update
---

"이벤트가 발생하면 이 핸들러를 실행하자"나 "데이터 구조의 모든 원소에 이 연산을 적용하자"와 같은 생각을 코드로 표현하기 위해 일련의 동작을 변수에 저장하거나 다른 함수에 넘겨야 하는 경우가 자주 있다.

1. 자바에서는 코드를 함수에 넘기거나 변수에 저장하여 사용하기 위해 <span style="background-color:white; color:blue">**무명 내부 클래스**</span>를 사용했다. => 번거롭다.
2. <span style="background-color:white; color:blue">**함수형 프로그래밍**</span>에서는 함수를 값처럼 다루어, 함수를 직접 다른 함수에 전달한다. => 클래스를 선언하고 그 클래스의 인스턴스를 함수에 넘기는 작업을 줄여준다. 
3. <span style="background-color:white; color:blue">**람다식**</span>을 사용하면 함수를 선언할 필요가 없고 코드 블록을 직접 함수의 인자로 전달할 수 있다. => 코드가 더욱 더 간결해진다.

**(예제)** 클릭 이벤트를 처리하는 리스너를 추가해서 버튼 클릭에 따른 동작을 정의해보자. 버튼 클릭 리스너는 `onClick`이라는 메소드가 들어있는 `OnClickListener`를 구현해야 한다.

#### 무명 내부 클래스로 리스너 구현하기
```java
button.setOnClickListener(new OnClickListener() {
    @Override
    public void onClick(View view) {
        // 클릭 시 수행할 동작
    }
})
```

코드가 번잡스럽다. 코틀린에서는 자바 8과 마찬가지로 람다를 쓸 수 있다.

#### 람다로 리스너 구현하기
```java
button.setOnCLickListener {
    // 클릭 시 수행할 동작
}
```

훨씬 더 간결하고 읽기 쉽다. 

이러한 예제를 통해 <span style="background-color:white; color:blue">**람다는 메소드가 하나뿐인 무명 클래스 대신 사용할 수 있다**</span>는 것을 알 수 있다.

---


컬렉션을 편리하게 처리할 수 있는 라이브러리를 제공할 수 있게 도와준 람다에 대해 알아보자.


**(예제)**  사람의 이름과 나이를 저장하는 `Person` 클래스를 사용하자. `Person` 클래스 리스트가 있고 그중에 가장 연장자를 찾아보자.

#### 컬렉션을 직접 검색하기
[play](https://pl.kotl.in/fDGY1Yv39)
```kotlin
data class Person(val name: String, val age: Int)

fun findTheOldest(people: List<Person>) {
    var maxAge = 0 // 가장 많은 나이
    var theOldest: Person? = null // 가장 연장자인 사람 이름
    for (person in people) {
        if (person.age > maxAge) {
            maxAge = person.age
            theOldest = person
        }
    }
    println(theOldest)
}

fun main(args: Array<String>) {
    val people = listOf(Person("Alice", 29), Person("Bob", 31))
    findTheOldest(people)
}

// Person(name=Bob, age=31)
```

이러한 코드는 비교연산자를 비교연산자를 잘못 사용하면 최댓값 대신 최솟값을 찾게 된다는 문제가 있다. 


### 람다를 사용해 컬렉션 검색하기
[play](https://pl.kotl.in/-OEE0D2BV)
```kotlin
data class Person(val name: String, val age: Int)

fun main(args: Array<String>) {
    val people = listOf(Person("Alice", 29), Person("Bob", 31))
    println(people.maxBy { it.age })
}
// Person(name=Bob, age=31)
```

모든 컬렉션에 대해 `maxBy` 함수를 호출할 수 있다. `maxBy`는 가장 큰 원소를 찾기 위해 비교에 사용할 값을 돌려주는 함수를 인자로 받는다. 중괄호로 둘러싸인 코드 `{ it.age }` 가 비교에 사용할 값을 돌려주는 함수다. 이 코드는 컬렉션의 원소를 인자(`it`)로 받아서 비교에 사용할 값을 반환한다. 이 예제에서는 컬렉션의 원소가 `Person` 객체였으므로 이 함수가 반환하는 값은 `Person` 객체의 `age` 필드에 저장된 나이 정보다. 
이런 식으로 단지 함수나 프로퍼티를 반환하는 역할을 수행하는 람다는 <span style="background-color:white; color:blue">**멤버 참조**</span>로 대치할 수 있다.

### 멤버 참조를 사용해 컬렉션 검색하기
[play](https://pl.kotl.in/800YCTIjD)
```kotlin
data class Person(val name: String, val age: Int)

fun main(args: Array<String>) {
    val people = listOf(Person("Alice", 29), Person("Bob", 31))
    println(people.maxBy(Person::age))
}
```

자바 컬렉션에 대해 (자바 8 이전에) 수행하던 대부분의 작업은 람다나 멤버 참조를 인자로 취하는 라이브러리 함수를 통해 개선할 수 있다. 이렇게 <span style="background-color:white; color:blue">**람다**</span>나 <span style="background-color:white; color:blue">**멤버 참조**</span>를 인자로 받는 함수를 통해 개선한 코드는 더 짧고 더 이해하기 쉽다.

--- 

람다는 <span style="background-color:white; color:blue">**값처럼 여기저기 전달할 수 있는 동작의 모음**</span>이다. 

다음은 람다식을 선언하기 위한 문법이다.

![image](https://user-images.githubusercontent.com/46019755/200175053-942fb0ba-b314-482a-aa2d-1ad1dc98ae57.png)


코틀린 람다식은 항상 중괄호로 둘러싸여 있다. 화살표(`->`)가 파라미터와 람다 본문을 구분해준다. 파라미터 주변에는 괄호가 없다.

람다식을 <span style="background-color:white; color:blue">**변수에 저장할 수 있다.**</span> 람다가 저장된 변수 이름 뒤에 괄호를 놓고 그 안에 필요한 인자를 넣어서 람다를 호출할 수 있다.

[play](https://pl.kotl.in/fXtkLD7Hx)
```kotlin
fun main(args: Array<String>) {
    val sum = { x: Int, y: Int -> x + y}
    println(sum(1, 2)) // 변수에 저장된 람다 호출
}

// 3
```

람다식을 직접 호출해도 된다.
[play](https://pl.kotl.in/zhUJu7wFJ)
```kotlin
fun main(args: Array<String>) {
    { println(42) }()
}

// 42
```

이와 같은 구문은 읽기 어렵고 그다지 쓸모도 없다. 람다를 만들자마자 바로 호출하느니 람다 본문을 직접 실행하는 편이 낫다. 

이렇게 코드의 일부분을 블록으로 둘러싸 실행할 필요가 있다면 `run`을 사용한다. `run`은 <span style="background-color:white; color:blue">**인자로 받은 람다를 실행해주는 라이브러리 함수**</span>다.

[play](https://pl.kotl.in/6PVG0qfCy)
```
fun main(args: Array<String>) {
    run { println(42) } // 람다 본문에 있는 코드를 실행한다.
}

// 42
```

실행 시점에 코틀린 람다 호출에는 아무 부가 비용이 들지 않으며, 프로그램의 기본 구성 요소와 비슷한 성능을 낸다.


[사람 목록에서 가장 연장자를 찾는 예제](#람다를-사용해-컬렉션-검색하기)를 정식으로 작성하면 다음과 같다.

```kotlin
people.maxBy({p: Person -> p.age})
```

1. 중괄호 안에 있는 코드는 람다식이다.
2. 그 람다식을 `maxBy` 함수에 넘긴다. 
3. 람다식은 `Person` 타입의 값을 인자로 받아서 인자의 `age`를 반환한다.

이 코드는 다음과 같이 개선할 수 있다.
1. 코틀린에는 함수 호출시 맨 뒤에 있는 인자가 람다식이라면 그 람다를 괄호 밖으로 빼낼 수 있다는 문법 관습이 있다. 둘 이상의 람다를 인자로 받는 함수라고 해도 인자 목록의 **맨 마지막 람다만** 밖으로 뺄 수 있다. 그런 경우에는 괄호를 사용하는 일반적인 함수 호출 구문을 사용하는 편이 낫다.
    ```kotlin
    people.maxBy() { p:Person -> p.age }
    ```
2. 람다가 어떤 함수의 유일한 인자이고 괄호 뒤에 람다를 썼다면 호출시 빈 괄호를 없애도 된다.
    ```kotlin
    people.maxBy { p: Person -> p.age }
    ```
3. 컴파일러가 문맥으로부터 유추할 수 있는 인자 타입을 굳이 적을 필요는 없다. 로컬 변수처럼 <span style="background-color:white; color:blue">**컴파일러는 람다 파라미터의 타입도 추론할 수 있다.**</span> `maxBy` 함수의 경우 파라미터의 타입은 항상 컬렉션 원소 타입과 같다. 컴파일러는 `Person` 타입의 객체가 들어있는 컬렉션에 대해 `maxBy`를 호출한다는 사실을 알고 있으므로 람다의 파라미터도 `Person`이라는 사실을 이해할 수 있다.
    ```kotlin
    people.maxBy { p -> p.age }
    ```
4. 인자가 단 하나뿐인 경우 굳이 인자에 이름을 붙이지 않고 디폴트 이름인 `it`을 사용한다. 람다의 파라미터가 하나뿐이고 그 타입을 컴파일러가 추론할 수 있는 경우 `it`을 바로 쓸 수 있다.
    ```kotlin
    people.maxBy { it.age }
    ```

    it을 사용하는 관습은 코드를 아주 간단하게 만들어준다. 하지만 이를 남용하면 안된다. 특히 람다 안에 람다가 중첩되는 경우 각 람다의 파라미터를 명시하는 편이 낫다. 파라미터를 명시하지 않으면 각각의 it이 가리키는 파라미터가 어떤 람다에 속했는지 파악하기 어려울 수 있기 때문이다. 문맥에서 람다 파라미터의 의미나 파라미터의 타입을 쉽게 알 수 없는 경우에도 파라미터를 명시적으로 선언하면 도움외 된다.

 3장에서 열심히 개선했던 `joinToString` 예제를 다시 살펴보자. 코틀린 표준 라이브러리에도 `joinToString` 이라는 함수가 있지만, 표준 라이브러리의 `joinToString`은 맨 마지막 인자로 함수를 더 받는다는 차이가 있다. 리스트의 원소를 `toString`이 아닌 <span style="background-color:white; color:blue">**다른 방식을 통해 문자열로 변환하고 싶은 경우**</span> 이 인자를 활용한다. 

**(예제)** 각 사람의 이름만 출력하기 위해 `joinToString`에 람다를 사용해보자.

### 이름 붙인 인자를 사용해 람다 넘기기
[play](https://pl.kotl.in/woWcHJaHj)
```kotlin
data class Person(val name: String, val age: Int)

fun main(args: Array<String>) {
    val people = listOf(Person("이몽룡", 29), Person("성춘향", 31))
    val name = people.joinToString(separator = " ", 
                                  transform = { p: Person -> p.name })
    println(name)
}

// 이몽룡 성춘향
```

<span style="background-color:white; color:blue">**이름 붙인 인자**</span>를 사용해, 람다를 넘김으로써 람다를 어떤 용도로 쓰는지 더 명확히 했다.

이 함수 호출에서 함수를 괄호 밖으로 뺀 모습은 다음과 같다. 

### 람다를 괄호 밖에 전달하기
[play](https://pl.kotl.in/bL3cKuVwg)
```kotln
data class Person(val name: String, val age: Int)

fun main(args: Array<String>) {
    val people = listOf(Person("이몽룡", 29), Person("성춘향", 31))
    val name = people.joinToString(" ") { p: Person -> p.name }
    println(name)
}

// 이몽룡 성춘향
```

더 간결하지만 람다의 용도를 분명히 알아볼 수는 없다. 

람다를 변수에 저장할 때는 파라미터의 타입을 추론할 문맥이 존재하지 않는다. 따라서 파라미터 타입을 명시해야 한다.

```kotlin
val getAge = { p:Person -> p.age }
people.maxBy(getAge)
```

본문이 여러 줄로 이뤄진 경우 <span style="background-color:white; color:blue">**본문의 맨 마지막에 있는 식이 람다의 결과 값**</span>이 된다.
[play](https://pl.kotl.in/VOXaiK0oz)
```kotlin
fun main(args: Array<String>) {
    val sum = { x: Int, y: Int ->
        println("Computing the sum of $x and $y...")
        x + y
    }
	println(sum(1, 2))
}

// Computing the sum of 1 and 2...
// 3
```

자바 메소드 안에서 무명 내부 클래스를 정의할 때, 메소드의 로컬 변수를 무명 내부 클래스에서 사용할 수 있다. 람다를 함수 안에서 정의하면 함수의 파라미터뿐 아니라 람다 정의의 앞에 선언된 로컬 변수까지 람다에서 모두 사용할 수 있다.

이런 기능을 보여주기 위해 `forEach` 표준 함수를 사용해보자. `forEach`는 컬렉션의 모든 원소에 대해 람다를 호출해준다. `forEach`는 일반적은 `for` 루프보다 훨씬 간결하지만 그렇다고 다른 장점이 많지는 않다.

**(예제)** 메시지의 목록을 받아 모든 메시지에 똑같은 접두사를 붙여서 출력해보자.

### 함수 파라미터를 람다 안에서 사용하기
[play](https://pl.kotl.in/4pBLRvJxQ)
```kotlin
fun printMessagesWithPrefix(messages: Collection<String>, prefix: String) {
    messages.forEach { // 각 원소에 대해 수행할 작업을 람다로 받는다.
        println("$prefix $it") 
    }
}

fun main(args: Array<String>) {
    val errors = listOf("403 Forbidden", "404 Not Found")
    printMessagesWithPrefix(errors, "Error: ")
}

// Error:  403 Forbidden
// Error:  404 Not Found
```

자바와 다른 점 중 중요한 한 가지는 <span style="background-color:white; color:blue">**코틀린 람다 안에서는 람다 밖 함수에 있는 final 변수가 아닌 변수에 접근할 수 있다**</span>는 점이다. 또한, 람다 안에서 <span style="background-color:white; color:blue">**바깥의 변수를 변경해도 된다.**</span> 

**(예제)** 전달받은 상태 코드 목록에 있는 클라이언트와 서버 오류의 횟수를 세보자.

### 람다 안에서 바깥 함수의 로컬 변수 변경하기
[play](https://pl.kotl.in/wXpGbHSDl)
```kotlin
fun printProblemCounts(responses: Collection<String>) {
	var clientErrors = 0
    var serverErrors = 0
    
    responses.forEach {
        if (it.startsWith("4")) {
            clientErrors++ // 람다 밖의 변수 변경
        } else if (it.startsWith("5")) {
            serverErrors++ // 람다 밖의 변수 변경
        }
    }
    
    println("$clientErrors client errors, $serverErrors server errors")
}

fun main(args: Array<String>) {
    val responses = listOf("200 OK", "418 I'm a teapot",
                       "500 Internal Server Error")
    printProblemCounts(responses)
}

// 1 client errors, 1 server errors
```

이 예제의 `prefix`, `clientErrors`, `serverErrors` 와 같이 <span style="background-color:white; color:blue">**람다 안에서 사용하는 외부 변수**</span>를 <span style="background-color:white; color:blue">**람다가 포획한 변수**</span>라고 부른다.

기본적으로 함수 안에 정의된 로컬 변수의 생명주기는 함수가 반환되면 끝난다. 하지만 어떤 함수가 자신의 로컬 변수를 포획한 람다를 반환하거나 다른 변수에 저장한다면 로컬 변수의 생명주기와 함수의 생명주기가 달라질 수 있다. 포획한 변수가 있는 람다를 저장해서 함수가 끝난 뒤에 실행해도 람다의 본문 코드는 여전히 포획한 변수를 읽거나 쓸 수 있다.  
어떻게 그런 동작이 가능할까? <span style="background-color:white; color:blue">**final 변수를 포획한 경우**</span>에는 람다 코드를 변수 값과 함께 저장한다. <span style="background-color:white; color:blue">**final이 아닌 변수를 포획한 경우**</span>에는 변수를 특별한 래퍼로 감싸서 나중에 변경하거나 읽을 수 있게 한 다음, 래퍼에 대한 참조를 람다 코드와 함께 저장한다.

### 변경 가능한 변수 포획하기: 자세한 구현 방법
<span style="background-color:white; color:blue">**자바에서는 final 변수만 포획할 수 있다.**</span> 하지만 변경 가능한 변수를 저장하는 원소가 단 하나뿐인 배열을 선언하거나, 변경 가능한 변수를 필드로 하는 클래스를 선언해서 변수를 포획할 수 있다. 안에 들어있는 원소는 변경 가능할지라도 배열이나 클래스의 인스턴스에 대한 참조를 final로 만들면 포획이 가능하다.

이를 코틀린으로 작성하면 다음과 같다.

```kotlin
class Ref<T>(var value: T) // 변경 가능한 변수를 포획하는 방법을 보여주기 위한 클래스

fun main(args: Array<String>) {
    val counter = Ref(0)
    println(counter.value) // 0
	val inc = { counter.value++ } // 변경 불가능한 변수를 포획했지만 그 변수가 가리키는 객체의 필드 값을 바꿀 수 있다.
	inc()
    println(counter.value) // 1
}
```

실제 코드에서는 이런 래퍼를 만들지 않고 변수를 직접 바꾼다.

```kotlin
fun main(args: Array<String>) {
    var counter = 0
    println(counter) // 0
	val inc = { counter++ }
    inc()
    println(counter) // 1
}
```

첫 번째 예제는 두 번째 예제가 작동하는 내부 모습을 보여준다. 람다가 final 변수(`val`)를 포획하면 자바와 마찬가지로 <span style="background-color:white; color:blue">**그 변수의 값이 복사된다.**</span> 하지만 람다가 변경 가능한 변수(`var`)를 포획하면 변수를 `Ref` 클래스 인스턴스에 넣는다. 그 `Ref` 인스턴스에 대한 참조를 final로 만들면 쉽게 람다로 포획할 수 있고, 람다 안에서는 `Ref` 인스턴스의 필드를 변경할 수 있다.

람다를 이벤트 핸들러나 다른 비동기적으로 실행되는 코드로 활용하는 경우 함수 호출이 끝난 다음에 로컬 변수가 변경될 수도 있다. 예를 들어 다음 코드는 버튼 클릭 횟수를 제대로 셀 수 없다.

```kotlin
fun tryToCountButtonClicks(button: Button): Int {
    var clicks = 0
    button.onClick { clicks++ }
    return clicks
}
```

<span style="background-color:white; color:blue">**이 함수는 항상 0을 반환한다.**</span> `onClick` 핸들러는 `tryToCountButtonClicks`가 `clicks`를 반환한 다음에 호출되기 때문이다. 이 함수를 제대로 구현하려면 클릭 횟수를 세는 카운터 변수를 함수의 내부가 아니라 클래스의 프로퍼티나 전역 프로퍼티 등의 위치로 빼내서 나중에 변수 변화를 살펴볼 수 있게 해야 한다.


`::`를 사용하는 식을 <span style="background-color:white; color:blue">**멤버 참조**</span>라고 부른다. 멤버 참조는 <span style="background-color:white; color:blue">**프로퍼티나 메소드를 단 하나만 호출하는 함수 값을 만들어준다.**</span> `::`는 클래스 이름과 참조하려는 멤버(프로퍼티나 메소드) 이름 사이에 위치한다.

![image](https://user-images.githubusercontent.com/46019755/200178593-e6053e4d-4965-4d9a-b9ca-69a32f0e35fa.png)

`Person::age`는 다음 람다식을 더 간략하게 표현한 것이다.

```kotlin
val getAge = { person: Person -> person.age }
```

멤버 참조는 그 멤버를 호출하는 람다와 같은 타입이다. 따라서 다음 예처럼 자유롭게 바꿔 쓸 수 있다.

```kotlin
people.maxBy(Person::age)
people.maxBy { p -> p.age }
people.maxBy { it.age }
```

최상위에 선언되고 다른 클래스의 멤버가 아닌 함수나 프로퍼티를 참조할 수도 있다.

```kotlin
fun salute() = println("Salute!")
run(::salute) // 최상위 함수를 참조한다.
```

클래스 이름을 생략하고 `::`로 참조를 바로 시작한다. `::salute`라는 멤버 참조를 `run` 라이브러리 함수에 넘긴다.

람다가 인자가 여럿인 다른 함수한테 작업을 위임하는 경우 람다를 정의하지 않고 직접 위임 함수에 대한 참조를 제공하면 편리하다.

[play](https://pl.kotl.in/GNO_OwfAd)
```kotlin
data class Person(val name: String, val age: Int)

fun sendEmail(person: Person, message: String) {
    println(person)
    println(message)
    println("=============================")
}

fun main(args: Array<String>) {
    val action = { person: Person, message: String ->
    	sendEmail(person, message) // 이 람다는 sendEmail 함수에게 작업을 위임한다.
    }

    val nextAction = ::sendEmail // 람다 대신 멤버 참조를 쓸 수 있다.
    
    action(Person("Bob", 30), "Test")
    nextAction(Person("Bob", 30), "Test")
}

// Person(name=Bob, age=30)
// Test
// =============================
// Person(name=Bob, age=30)
// Test
// =============================
```

`::` 뒤에 클래스 이름을 넣으면 <span style="background-color:white; color:blue">**생성자 참조**</span>를 만들 수 있다. 생성자 참조를 사용하면 클래스 생성 작업을 저장해둘 수 있다. [play](https://pl.kotl.in/T-oW_Lv7e)

```kotlin
data class Person(val name: String, val age: Int)

fun main(args: Array<String>) {
    val createPerson = ::Person // "Person"의 인스턴스를 만드는 동작을 값으로 저장한다.
    val p = createPerson("Alice", 29)
    println(p)
}

// Person(name=Alice, age=29)
```

<span style="background-color:white; color:blue">**확장 함수도**</span> 멤버 함수와 똑같은 방식으로 참조할 수 있다. [play](https://pl.kotl.in/iAq2HWjjV)
```kotlin
data class Person(val name: String, val age: Int)

fun Person.isAdult() = age >= 21 // 확장 함수

fun main(args: Array<String>) {
	val perdicate = Person::isAdult
    
    println(perdicate(Person("Bob", 30)))
}

// true
```

`isAdult`를 호출할 때 `person.isAdult()`로 인스턴스 멤버 호출 구문을 쓸 수 있는 것처럼 `Person::isAdult`로 멤버 참조 구문을 사용해 확장 함수에 대한 참조를 얻을 수 있다.

### 바운드 멤버 참조
코틀린 1.0에서는 클래스의 메소드나 프로퍼티에 대한 참조를 얻은 다음에 그 참조를 호출할 때 항상 인스턴스 객체를 제공해야 했다. 코틀린 1.1부터는 <span style="background-color:white; color:blue">**바운드 멤버 참조**</span>를 지원한다. 바운드 멤버 참조를 사용하면 <span style="background-color:white; color:blue">**멤버 참조를 생성할 때 클래스 인스턴스를 함께 저장한 다음 나중에 그 인스턴스에 대해 멤버를 호출해준다.**</span> 따라서 호출 시 수신 대상 객체를 별도로 지정해 줄 필요가 없다.

[play](https://pl.kotl.in/HO9cV6JtN)
```kotlin
val p = Person("Dmitry", 34)
val personsAgeFunction = Person::age
println(personsAgeFunction(p))

val dmitrysAgeFunction = p::age // 코틀린 1.1부터 사용할 수 있는 바운드 멤버 참조
println(dmitrysAgeFunction())

// 34
// 34
```

여기서 `personsAgeFunction`은 인자가 하나이지만, `dmitrysAgeFunction`은 인자가 없는, p가 가리키던 사람의 나이를 반환하는 함수라는 점에 유의하라. 코틀린 1.0에서는 `p::age` 대신에 `{ p.age }`라고 직접 객체의 프로퍼티를 돌려주는 람다를 만들어야만 한다.


---
#### 참고 자료
> Kotlin in Action - 드미트리 제메로프, 스베트라나 이사코바 저