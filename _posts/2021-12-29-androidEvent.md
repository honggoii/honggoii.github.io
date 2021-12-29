---
layout: post
title:  "이벤트 처리하기"
date:   2021-12-29 22:10:49 +0800
categories: [Android]
tags: [android]
mainfont: GowunDodum-Regular
---


## 콜백 함수
---
보통 함수는 개발자가 만들고 코드에서 호출해야 실행이 된다. 이와 다르게 `콜백 함수`는 특정 이벤트가 발생하거나 어느 시점에 도달하면 자동으로 호출하는 함수이다.


## 터치 이벤트
---
화면을 터치했을 때 `onTouchEvent()` 메소드가 자동으로 호출된다. 

```kotlin
override fun onTouchEvent(event: MotionEvent?): Boolean {
    when (event?.action) {
        MotionEvent.ACTION_DOWN -> {
            Log.d("onTouchEvent", "화면을 손가락으로 누른 순간")
            Log.d("onTouchEvent", "ACTION_DOWN 이벤트가 발생한 뷰의 x 좌표: ${event.x} 화면의 x 좌표${event.raxX}")
        }
        MotionEvent.ACTION_UP -> {
            Log.d("onTouchEvent", "화면에서 손가락을 뗀 순간")
            Log.d("onTouchEvent", "ACTION_UP 이벤트가 발생한 뷰의 x 좌표: ${event.x} 화면의 x 좌표${event.raxX}")
        }
        MotionEvent.ACTION_MOVE -> {
            Log.d("onTouchEvent", "화면을 손가락으로 누른 채로 이동하는 순간")
            Log.d("onTouchEvent", "ACTION_MOVE 이벤트가 발생한 뷰의 x 좌표: ${event.x} 화면의 x 좌표${event.raxX}")
        }
    }
    return super.onTouchEvent(event)
}
```
`MotionEvent` 객체에는 터치의 종류와 좌표값(발생 지점)이 담긴다. 보통 앱에서는 화면을 터치하는 이벤트가 많아서 이 메소드를 많이 사용할 것 같다! 라고 생각할 수 있지만 
이 메소드보다는 각 뷰들이 제공하는 `뷰 이벤트`를 사용한다. `onTouchEvent()`를 사용하게 되면 화면의 좌표값을 이용해 어느 뷰를 선택할 것인지 분기 처리를 해야하므로 
뷰에 터치 이벤트를 주기 위해서는 각 뷰에서 제공하는 이벤트를 사용하는 것이 코드를 더 간결하게 할 수 있다. 


## 뷰 이벤트
---
터치 이벤트 같은 경우에는 `onTouchEvent()` 메소드를 선언해 놓으면 자동으로 호출이 되지만 뷰 이벤트는 선언으로 끝나지 않는다. 뷰 이벤트를 처리하기 위해서는 3가지가 필요하다.
1. `이벤트 소스` : 이벤트 발생 객체
2. `이벤트 핸들러` : 이벤트 발생시 실행할 로직이 구현된 객체
3. `리스너` : 이벤트 소스와 이벤트 핸들러를 연결해주는 함수

체크박스 뷰에 체크 상태 변경 이벤트가 발생하는 경우를 예시로 들어보면 다음과 같다.
1. `이벤트 소스` : binding.checkbox
2. `이벤트 핸들러` : OnCheckedChangeListener
3. `리스너` : setOnCheckedChangeListener

`binding.checkbox` 객체에 `setOnCheckedChangeListener`로 `OnCheckedChangeListener` 객체를 등록해 놓으면, 이벤트가 발생할 때마다 콜백함수가 호출된다. 
`OnCheckedChangeListener` 인터페이스르르 구현한 객체를 이벤트 핸들러로 등록하는 방법은 3가지가 있다.

#### SAM(Single Abstract Method) 기법으로 구현 
하나의 추상 함수를 포함하는 인터페이스를 구현하는 기법으로, 자바 API를 람다 표현식으로 쉽게 이용하기 위해 코틀린에서 제공하는 기법이다. 
```kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        // 생략

        binding.checkbox.setOnCheckedChangeListener {
            compoundButton, b -> Log.d ("onCheckedChanged", "onCheckedChanged 호출")
        }
    }
}
```

자주 사용하는 뷰 이벤트에는 `OnClickListener`와 `OnLongClickLister`가 있다. 

```java
binding.btn.setOnClickListener(new View.OnClickListener()) {
    @Override
    public void onClick(View view) {

    }
}
```

```kotlin
binding.btn.setOnClickListener(object: View.OnClickListener {
    override fun onClick(view: View?) {

    }
})
```


```kotlin
binding.btn.setOnClickListener {
    // 클릭 이벤트 발생시 처리 로직
}
```



#### 액티비티에서 인터페이스를 구현
```kotlin
class MainActivity : AppCompatActivity(), CompoundButton.OnCheckedChangeListener {
    override fun onCreate(savedInstanceState: Bundle?) {
        // 생략

        binding.checkbox.setOnCheckedChangeListener(this)
    }

    override fun onCheckedChanged(p0: CompoundButton?, p1: Boolean) {
        Log.d ("onCheckedChanged", "onCheckedChanged 호출")
    }
}
```

#### 이벤트 핸들러를 별도의 클래스로 구현
```kotlin
class MyEventHandler : CompoundButton.OnCheckdChangeListener {
    override fun onCheckedChanged(p0: CompoundButton?, p1: Boolean) {
        Log.d ("onCheckedChanged", "onCheckedChanged 호출")
    }
}

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        // 생략

        binding.checkbox.setOnCheckedChangeListener(MyEventHandler())
    }
}
```




## 키 이벤트
---
키를 입력했을 때 `onKeyDown()`, `onKeyUp()`, `onKeyLongPress()` 메소드가 자동으로 호출된다. 여기서 말하는 키는 소프트 키보드의 키를 입력할 때 호출되는 것이 아닌, 
안드로이드의 하드웨어 키보드를 말한다. 즉, 안드로이드 자체에서 제공하는 뒤로가기 버튼, 홈 버튼, 오버뷰 버튼, 전원 버튼, 볼륨 조절 버튼을 말하는데 
이 중에서도 `뒤로가기 버튼`과 `볼륨 조절 버튼`은 키 이벤트로 처리하게된다. 특히 뒤로가기 버튼은 `onBackPressed()` 함수를 이용하여 특정 이벤트를 발생시킨다.

```kotlin
override fun onBackPressed() {
    Log.d("onBackPressed", "Back Button 눌림")
}
```



## 참고 자료
---
- Do it! 깡쌤의 안드로이드 앱 프로그래밍 with 코틀린
<iframe src="https://coupa.ng/cbgCRw" width="120" height="240" frameborder="0" scrolling="no" referrerpolicy="unsafe-url"></iframe>
이 포스팅은 쿠팡 파트너스 활동의 일환으로, 이에 따른 일정액의 수수료를 제공받습니다.