---
layout: post
title:  "Kotlin의 컬렉션 타입"
date:   2021-12-26 20:40:15 +0800
categories: [Kotlin]
tags: [kotlin]
mainfont: GowunDodum-Regular
---

## Array
---

```kotlin
<init>(size: Int, init: (Int) -> T) // 생성자
```

```kotlin
val data: Array<Int> = Array(5, {0}) // 크기가 5인 배열을 0으로 초기화
data[0] = 100 // data.set(0, 100)
println(data[0]) //data.get(0)
```

- 기초 타입의 배열은 Array를 사용하지 않고 각 기초 타입 배열을 사용할 수 있다. (`BooleanArray`, `IntArray`, `DoubleArray` 등)
- arrayOf() 함수를 이용해서 배열 선언시 값을 할당할 수 있다. 기초 타입 대상 `booleanArrayOf()`, `intArrayOf()`, `doubleArrayOf()` 등도 있다.

```kotlin
val data = arrayOf<Int>(100, 200, 300)
```

## List
---
순서가 있고 중복을 허용한다.


## Set
---
순서가 없고 중복을 허용하지 않는다.


## Map
---
순서가 없고 key-value 쌍으로 자료를 저장하고 key는 중복을 허용하지 않는다. `Pair(key, value)`를 사용하거나 `key to value`를 사용한다.


## 가변클래스와 불변 클래스
---
코틀린은 `List`, `Set`, `Map`에 대해 각각 가변클래스와 불변클래스를 제공한다.
- `불변 클래스` : 내용을 변경할 수 없으므로 `size()`, `get()` 메소드만 사용할 수 있다.
- `가변 클래스` : 내용을 변경할 수 있으므로 불변 클래스가 사용하는 메소드(`size()`, `get()`)와 더불어 `add()`, `set()` 메소드를 사용할 수 있다.

| 컬렉션 | 특징 | 타입 | 함수 | 
|:-----|:----:|:-----------:|:---------------:|
| List | 불변 | List        | listOf()        | 
| List | 가변 | MutableList | mutableListOf() | 
| Set  | 불변 | Set         | setOf()         |
| Set  | 가변 | MutableSet  | mutableSetOf()  | 
| Map  | 불변 | Mao         | mapOf()         |
| Map  | 가변 | MutableMap  | mutableMapOf()  | 


## 참고 자료
--- 
- Do it! 깡쌤의 안드로이드 앱 프로그래밍 with 코틀린
<iframe src="https://coupa.ng/cbgCRw" width="120" height="240" frameborder="0" scrolling="no" referrerpolicy="unsafe-url"></iframe>
이 포스팅은 쿠팡 파트너스 활동의 일환으로, 이에 따른 일정액의 수수료를 제공받습니다.