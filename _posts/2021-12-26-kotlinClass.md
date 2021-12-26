---
layout: post
title:  "Kotlin의 클래스 종류"
date:   2021-12-26 21:17:35 +0800
categories: [Kotlin]
tags: [kotlin]
mainfont: GowunDodum-Regular
---

## 데이터 클래스
---

`data` 키워드를 사용한다.

```kotlin
data class Student(val name: String, val id: Int)
```

- 데이터를 다루는데 편리한 기능을 제공하는 것이 주목적이다.
- `equals()` 메소드로 객체를 비교하면 객체 자체가 아니라 `객체의 데이터를 비교한다.` (주 생성자의 멤버 변수가 같은지만 판단)
- `toString()` 함수는 객체가 포함하는 멤버 변수 데이터를 출력한다. (주 생성자의 매개변수에 선언된 데이터만 출력)


## 오브젝트 클래스
---
익명 클래스를 만들 목적으로 사용한다. 이름이 없기 때문에 클래스를 선언함과 동시에 생성해야한다. 

```kotlin
val obj = object A {   }
```

여기서 A가 클래스면 A 클래스를 상속받은 하위 클래스를 익명으로 선언하고, A가 인터페이스면 A 인터페이스를 구현한 익명 클래스를 선언한다.


## 컴패니언 클래스
---
객체를 생성하지 않고 클래스 이름으로 멤버 변수와 멤버 함수에 접근하는 클래스이다.

```kotlin
class Test {
    companion object {
        var data = 10
    }
}

fun main() {
    Test.data = 500
}
```

자바의 static 키워드와 동일한 역할을 한다고 볼 수 있기때문에 그냥 static을 쓰면 안되나? 하고 생각이 들었다. 
자바는 최상위가 클래스밖에 올 수 없기때문에 클래스에 묶일 필요가 없더라도 클래스에 묶어야하고, 이처럼 클래스에 묶일 필요가 없는데 묶인 변수나 함수는 static 키워드를 사용하면 되었다. 하지만 코틀린으 최상위에 클래스뿐만 아니라 변수와 함수 모두 올 수 있기 때문에 굳이 클래스 내에 묶어서 static을 사용할 필요가 없는 것이다.
하지만 클래스에 선언한 멤버 변수를 자바의 static 처럼 이용해야할 경우가 있을 수 있기때문에 `companion` 클래스를 지원하는 것이다.




## 참고 자료
--- 
- Do it! 깡쌤의 안드로이드 앱 프로그래밍 with 코틀린
<iframe src="https://coupa.ng/cbgCRw" width="120" height="240" frameborder="0" scrolling="no" referrerpolicy="unsafe-url"></iframe>
이 포스팅은 쿠팡 파트너스 활동의 일환으로, 이에 따른 일정액의 수수료를 제공받습니다.