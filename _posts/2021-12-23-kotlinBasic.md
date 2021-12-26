---
layout: post
title:  "Kotlin의 조건문과 반복문"
date:   2021-12-26 20:50:58 +0800
categories: [Kotlin]
tags: [kotlin]
mainfont: GowunDodum-Regular
---

## 표현식
---
결과값을 반환하는 식  

`if~else`를 표현식에 사용하려면 else를 생략할 수 없고 반환하는 결과값은 각 영역의 마지막 줄이다.

```kotlin
var result = if (num > 0) {
    true
} else {
    false
}
```


## 조건문 when
---

사용방법 1
 
```kotlin
when(조건) {
    조건1 -> println("조건1")
    조건2 -> println("조건2")
    else -> println("일치하는 조건 없음")
}
```

사용방법 2

```kotlin
when {
    num > 0 -> println("양수")
    num < 0 -> println("음수")
    else -> println("0")
}
```

사용방법 3

표현식에 넣어 사용한다.


## 반복문 for
---
1. `for (i in 1..10)` : 1부터 10까지 1씩 증가 (10 포함)
2. `for (i in 1 until 10)` : 1부터 10까지 1씩 증가 (10 미포함)
3. `for (i in 2..10 step 2)` : 2부터 10까지 2씩 증가
4. `for (i in 10 downTo 1)` : 10부터 1까지 1씩 감소
5. `for (i in data.indices)` : data 배열의 개수만큼 반복. i는 인덱스를 나타낸다.
6. `for ((index, value) in data.withIndex())` : data 배열의 인덱스와 값을 같이 가져온다.


## repeat()
---
argument에 수를 넣어주면 해당 수 만큼 반복을 할 수 있다.
```kotlin
fun main() {
    repeat(5) {
	    println("Hello, world!")    
    }
}
```
```
// 출력결과
Hello, world!
Hello, world!
Hello, world!
Hello, world!
Hello, world!
```


## 참고 자료
--- 
- Do it! 깡쌤의 안드로이드 앱 프로그래밍 with 코틀린
<iframe src="https://coupa.ng/cbgCRw" width="120" height="240" frameborder="0" scrolling="no" referrerpolicy="unsafe-url"></iframe>
이 포스팅은 쿠팡 파트너스 활동의 일환으로, 이에 따른 일정액의 수수료를 제공받습니다.