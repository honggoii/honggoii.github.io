---
layout: post
title:  "Kotlin의 함수"
date:   2021-12-26 21:28:43 +0800
categories: [Kotlin]
tags: [kotlin]
mainfont: GowunDodum-Regular
---

## 함수 선언
--- 
<ins>fun</ins> <ins>함수명</ins>(<ins>매개변수명</ins>: <ins>타입</ins>): <ins>반환 타입</ins> {     }

- 반환 타입을 생략하면 자동으로 `Unit` 타입이 적용된다.
- 매개변수에는 var, val를 사용할 수 없고 `val`이 자동으로 적용되기 때문에 함수내에서 매개변수를 변경할 수는 없다.
- 매개변수에 기본값을 선언하면 해당 인자를 전달하지 않아도 함수내에서는 기본값을 사용한다.
- 매개변수명을 지정하여 호출하면(`명명된 매개변수`) 매개변수 순서에 맞춰 호출하지 않아도 된다.


## 람다 함수
---

- 선언 : { 매개 변수 -> 함수 본문 }
- 매개 변수가 없으면 함수 본문만 작성할 수 있다.
- 함수 본문의 마지막 표현식이 반환값이 된다.
- 람다 함수는 이름이 없어서 변수에 대입해서 사용한다.

```kotlin
val sum = {a:Int, b:Int -> a + b}
sum(10, 20) // 람다 함수 호출
```

- 변수에 대입하지 않고 사용할 수도 있다.

```kotlin
{a: Int, b: Int -> a + b}(10, 20)
```

- 매개변수가 1개인 경우 `it` 키워드를 사용한다.

```kotlin
val data: (Int) -> Unit = {println(it)}
```


## 함수 타입
---
변수에 함수를 대입하려면 함수 타입을 선언해주어야 한다.

```kotlin
val sum: (Int, Int) -> Int = {a:Int, b:Int -> a + b}
```

- 함수 타입 : <ins>(Int, Int) -> Int</ins> 
- 함수 내용 : <int>{a:Int, b:Int -> a + b}</ins>


## 함수 타입 별칭
---
`typealias` 키워드를 사용하면 함수 타입에 별칭을 사용할 수 있다.

```kotlin
typealias SumType = (Int, Int) -> Int

fun main() {
    val sum: SumType = {a:Int, b: Int -> a + b}
}
```


## 타입을 생략할 수 있는 경우
---
변수의 타입을 유출할 수 있으면 타입을 생략할 수 있다.

```kotlin
val sum = {a: Int, b: Int -> a + b}
val sum: (Int, Int) -> Int = {a, b -> a + b}
```


## 고차 함수
---
`함수를 매개변수에 전달`하거나 `함수를 반환`하는 함수. 함수를 변수에 대입할 수 있기때문에 가능하다.

```kotlin
fun higherOrderFun(arg: (Int) -> Boolean) : () -> String {
    val result = if (arg(100)) {    
        "양수 입니다."
    } else {
        "음수 입니다."
    }

    return {"higherOrderFun result : $result"}
}

fun main() {
    val result = higherOrderFun(a -> a > 0)
    println(result())
}
```


## 참고 자료
--- 
- Do it! 깡쌤의 안드로이드 앱 프로그래밍 with 코틀린
<iframe src="https://coupa.ng/cbgCRw" width="120" height="240" frameborder="0" scrolling="no" referrerpolicy="unsafe-url"></iframe>
이 포스팅은 쿠팡 파트너스 활동의 일환으로, 이에 따른 일정액의 수수료를 제공받습니다.