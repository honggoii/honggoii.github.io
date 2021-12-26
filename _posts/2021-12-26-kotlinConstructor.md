---
layout: post
title:  "Kotlin의 생성자"
date:   2021-12-26 20:59:45 +0800
categories: [Kotlin]
tags: [kotlin]
mainfont: GowunDodum-Regular
---

## 코틀린의 생성자
---
- 객체를 생성할 때 new 키워드를 사용하지 않는다.
- `constructor` 키워드를 사용한다.
- 코틀린의 생성자는 `주 생성자`와 `보조 생성자` 두가지가 있다.

## 주 생성자
---
한 클래스에 하나만 가능하다.

```kotlin
class Test contructor() {   }
class Test() {   } // constructor 키워드 생략
class Test {   } // 컴파일러가 매개변수가 없는 주 생성자 자동 생성
```

## init 키워드
---
객체를 생성할 때 자동 실행되고, `주 생성자`의 본문을 구현하는 용도로 사용한다.
 
```kotlin
class Student(name: String, id: Int) {
    init {   }
}
```

## 생성자의 매개변수를 멤버 변수로 사용하는 방법
---
방법 1.
```kotlin
class Student(name: String, id: Int) {
    var name: String
    var id: Int
    init {
        this.name = name
        this.id = id
    }
}
```

방법 2. 원래 함수 매개변수에 var/val 키워드를 추가할 수 없지만, `주 생성자만 유일하게 추가 가능하다.`
```kotlin
class Student(val name: String, val id: Int) {   }
```


## 보조 생성자
클래스 본문에 constructor 키워드를 이용하여 선언하는 함수로 여러개를 추가할 수 있다. 
만약 주 생성자, 보조 생성자 모두를 선언하면 반드시 생성자끼리 연결해주어야 한다.

```kotlin
class Student(name: String) {
    constructor(name: String, id: Int) : this(name) { // this(name) 으로 주 생성자와 연결
        
    }
}
```

만약 보조 생성자가 여러개라면 다른 보조 생성자를 호출해서 어떻게든 주 생성자가 호출되어야 한다.

```kotlin
class Student(name: String) {
    constructor(name: String, id: Int) : this(name) { // this(name) 으로 주 생성자와 연결

    }
    constructor(name: String, id: Int, age: Int) : this(name, id) { // this(name, id)로 보조 생성자와 연결

    }
}
```


## 주 생성자와 보조 생성자로 나눈 이유?
- 필수 매개변수와 실행 구문은 주 생성자에 작성해서 보조 생성자가 실행될 때 주 생성자도 함께 실행하려는 의도를 가지고 있다.
- 공통된 코드는 주 생성자에 작성하라는 의미를 나타낸다.




## 참고 자료
--- 
- Do it! 깡쌤의 안드로이드 앱 프로그래밍 with 코틀린
<iframe src="https://coupa.ng/cbgCRw" width="120" height="240" frameborder="0" scrolling="no" referrerpolicy="unsafe-url"></iframe>
이 포스팅은 쿠팡 파트너스 활동의 일환으로, 이에 따른 일정액의 수수료를 제공받습니다.