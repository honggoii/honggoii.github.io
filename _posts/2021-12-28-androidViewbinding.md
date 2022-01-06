---
layout: post
title:  "ViewBinding"
date:   2021-12-28 21:03:16 +0800
categories: [Android]
tags: [android]
mainfont: GowunDodum-Regular
---

## View Binding
---
xml에 선언한 View를 얻기 위해서는 `findViewById()` 함수로 얻어와야 한다. xml에 정의한 뷰들은 대부분이 사용되기 떄문에 뷰의 개수만큼 `findViewById()`를 사용할 수도 있다.
이렇게 불필요하다고 할 수 있는..? 코드를 줄이기 위해 `butterknife` 라이브러리가 등장했지만 View Binding을 이용하면 더 간결한 코드로 뷰 객체를 이용할 수 있다.
즉 `View Binding`은 XML 파일에 선언한 뷰 객체를 코드에서 쉽게 이용하는 방법이다. 


## 바인딩 클래스
---
먼저 `build.gradle` 파일에 View Binding을 사용하겠다고 선언해준다.  

```
android {
    //...
    buildFeatures {
        viewBinding = true
    }
    //...
}
```

이렇게 View Binding을 사용하겠다고 선언해주면 XML 파일에 등록된 뷰 객체를 포함하는 `바인딩 클래스`가 자동으로 생성되고 우리는 더이상 `findViewById()`를 호출하지 않고 
이 클래스를 이용해서 뷰 객체에 접근할 수 있다. 만약 어떤 xml 파일이 바인딩 클래스가 될 필요가 없다면, 해당 xml의 루트 태그에 `tools:viewBindingIgnore="true"` 속성을 사용하여 
`바인딩 클래스`가 자동으로 만들어지는 것을 막을 수 있다. 이렇게 자동으로 만들어진 클래스를 사용해야 하는데 이름을 알아야 사용할 것이 아닌가! 자동으로 만들어지는 이 클래스는 규칙을 가지고 생성되기 때문에 우리는 이 클래스를 사용할 수 있다. 대문자를 시작으로 xml파일의 _은 지우고 _다음에 등장하는 알파벳은 대문자로 바꾼 후, `Binding`을 붙여주면 된다.

- activity_main.xml ====> `ActivityMainBinding`

이렇게 만들어진 클래스를 사용해서 `layoutInflater`를 인자로한 `inflate()` 함수를 호출하면 바인딩 객체를 얻을 수 있다! 
이렇게 얻어진 바인딩 객체의 root 프로퍼티에 XML의 루트 태그 객체가 자동으로 등록되므로 기존에 액티비티와 레이아웃을 연결한 `setContentView()` 함수에 `binding.root`를 전달하면 된다.

```kotlin
val binding = ActivityMainBinding.inflate(layoutInflater) // activity_main.xml 파일에서 바인딩 객체 획득
setContentView(binding.root)
```

이렇게 바인딩 객체에 등록된 뷰를 사용하기 위해서는 xml 파일에 등록한 id값을 가져오면 된다. 예를들어 id가 text1인 TextView를 가져오려면 `binding.text1`과 같이 가져오면 된다.


## LayoutInflater
---
레이아웃 xml 파일을 뷰 객체로 생성해서 메모리에 할당해주는 클래스.

```kotlin
val inflater = getSystemService(Context.LAYOUT_INFLATER_SERVICE) as LayoutInflater
val rootView = inflater.inflate(R.layout.activity_main, null)
```

`inflater()`는 xml의 루트 태그의 객체를 반환한다. 




## 참고 자료
---
- Do it! 깡쌤의 안드로이드 앱 프로그래밍 with 코틀린
<iframe src="https://coupa.ng/cbgCRw" width="120" height="240" frameborder="0" scrolling="no" referrerpolicy="unsafe-url"></iframe>
이 포스팅은 쿠팡 파트너스 활동의 일환으로, 이에 따른 일정액의 수수료를 제공받습니다.