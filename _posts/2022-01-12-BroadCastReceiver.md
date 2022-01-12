---
layout: post
title:  "Broadcast Receiver"
date:   2022-01-12 22:53:28 +0800
categories: [Android]
tags: [android]
mainfont: GowunDodum-Regular
---


## Broadcast Receiver
---
`부팅`, `화면 켜고 끄기`, `배터리 상태` 등과 같은 시스템의 특정 이벤트 모델로 실행되는 컴포넌트. 


## 생명주기
---
`onReceive()` 하나. 오래 걸리는 작업은 권장하지 않으며 메서드가 끝나면 `Broadcast Receiver` 객체는 소멸된다.


## 생성
---
```kotlin
class MyReceiver : BroadcastReceiver() {
    override fun onReceive(context: COntext, intent: Intent) {

    }
}
```







## 참고 자료
---
- Do it! 깡쌤의 안드로이드 앱 프로그래밍 with 코틀린
<iframe src="https://coupa.ng/cbgCRw" width="120" height="240" frameborder="0" scrolling="no" referrerpolicy="unsafe-url"></iframe>
이 포스팅은 쿠팡 파트너스 활동의 일환으로, 이에 따른 일정액의 수수료를 제공받습니다.