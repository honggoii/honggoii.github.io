---
layout: post
title:  "Kotlin의 상속과 오버라이딩"
date:   2021-12-26 21:11:24 +0800
categories: [Kotlin]
tags: [kotlin]
mainfont: GowunDodum-Regular
---


## 상속
---
`open` 키워드를 사용하여 상속할 수 있도록 해준다.

```kotlin
open class Parent {   } // 상속할 수 있게 open 키워드 사용
class Child : Parent() {   } // 매개변수가 없는 생성자를 가진 Parent 상속
```

상위 클래스를 상속받는 하위 클래스의 생성자는 상위 클래스의 생성자를 호출해야 한다.

방법 1.

```kotlin
class Child(name: String) : Parent(name) {   } // 매개변수가 있는 상위 클래스 생성자 호출
```

방법 2.

```kotlin
class Child : Parent {
    constructor(name: STring) : super(name) {   }
}
```


## 오버라이딩
---
- 상위 클래스에 선언된 변수와 함수를 같은 이름으로 하위 클래스에 다시 선언하는 것
- 상위 클래스에서 오버라이딩을 허용할 변수와 함수 앞에 `open` 키워드 추가
- 하위 클래스에서 재정의하려면 해당 변수와 함수 앞에 `override` 키워드 추가


## 접근 제한자
---

| 접근 제한자 | 최상위에 사용하는 경우 | 클래스 멤버에 사용하는 경우 | 
|:-----|:----:|:-----------:|
| public    | 모든 파일 내부  | 모든 클래스 내부          |
| internal  | 같은 모듈 내부  | 같은 모듈 내부            |
| protected | 사용 불가      | 상속 받은 하위 클래스 내부 |
| private   | 파일 내부      | 클래스 내부               |

여기서 `모듈`이란, 그래들이나 메이븐 같은 빌드 도구에서 프로젝트 단위나 같은 세트 단위를 말한다.




## 참고 자료
--- 
- Do it! 깡쌤의 안드로이드 앱 프로그래밍 with 코틀린
<iframe src="https://coupa.ng/cbgCRw" width="120" height="240" frameborder="0" scrolling="no" referrerpolicy="unsafe-url"></iframe>
이 포스팅은 쿠팡 파트너스 활동의 일환으로, 이에 따른 일정액의 수수료를 제공받습니다.