---
layout: post
title:  "리소스"
date:   2022-01-03 21:57:56 +0800
categories: [Android]
tags: [android]
mainfont: GowunDodum-Regular
---


## 리소스
---
리소스란 정적인 자원을 이야기한다. 앱에서 사용하는 리소스는 크게 다음과 같이 두가지가 있다.
1. 앱 리소스
2. 플랫폼 리소스


## 앱 리소스
---
안드로이드 스튜디오에서 모듈을 생성하면 자동으로 `res` 폴더가 생기고 하위에 `drawable`, `layout`, `mipmap`, `values`와 같이 4개의 폴더가 기본으로 생긴다. 
이 외에도 `animator`, `anim`, `color`, `menu`, `raw`, `xml`, `font` 가 있으며 개발자는 이 외의 폴더를 만들수 없고 앞에서 설명한 폴더의 하위에도 개발자가 임의로 폴더를 만들 수 없다. 왜냐하면 우리가 layout을 만들거나 이미지를 불러올 때, `R` 파일을 이용한다. `R` 파일을 이용해서 가져올 수 이유는 우리가 `res` 폴더 아래에 정해진 규칙에 맞게 파일을 생서하면 시스템은 `R.java` 파일에 리소스들을 상수로 저장하기 때문이다.


## 특별한 values 폴더
---
앞서 말했듯이 `res` 폴더 하위의 폴더들은 이미 정해져있고 개발자가 해당 폴더에 맞는 파일을 추가하면 시스템은 `R.java` 파일에 규칙에 맞게 상수를 등록한다. 
여기서 `values` 폴더는 다른 폴더와 다른 특징이 있다. 그것은 바로 `R.java` 파일에 상수로 등록하지 않는 다는 것!😮 그럼 `values` 폴더 안에 있는 리소스는 어떻게 사용할 수 있을까? 안드로이드에 프로젝트를 하나 시작하면 기본적으로 `res/values` 아래에 `colors.xml`과 `strings.xml`이 생긴다. 해당 xml 파일안에는 다음과 같은 코드들이 들어있다. 

<img src="https://user-images.githubusercontent.com/46019755/147934332-be4441fd-8c40-480d-b4a8-3b57387cf238.png">

<img src="https://user-images.githubusercontent.com/46019755/147934552-fd9a94c0-b8aa-40b8-9150-be6dbf9047fd.png">

`strings.xml`에 있는 리소스나 `colors.xml`에 있는 리소스를 사용하기 위해서는 `name` 속성값을 사용한다. 예를 들어 `strings.xml`에 있는 "Sample App"이라는 문자열을 사용하고 싶다면 `@string/app_name`과 같이 사용하면 된다. 이처럼 `colors.xml`에 있는 색상을 사용하고 싶으면 `@color/teal_200`과 같이 사용해주면된다! 


## color 폴더와 values 하위의 colors.xml
---
색을 지정하는 리소스는 두 가지가 있는 것 같다. 하나는 `res` 하위 폴더인 `color` 폴더가 있고 `res` 하위 폴더의 `values`에도 색상을 지정해서 사용할 수 있다. 두 개다 색상을 지정하는 리소스라는 점에서는 같지만 살짝 차이가 있다. 
흔히 버튼이 눌렸는지 사용자가 확인할 수 있도록 눌렀을 때와 누르지 않았을 때의 색상을 다르게 하는 경우가 있는데 이때 차이가 발생한다. 
먼저 `res` 하위 폴더의 `values`에서 `color` 태그로 지정한 색상들은 각각 리소스로 등록되어 개별적으로 사용할 수 있다. 눌렸을 때 `blue`라는 이름을 안 눌렸을 때 `gray`라는 이름을 사용한다고 했을 때, 개발자는 activity에 가서 버튼이 누르면 `R.color.blue`를 사용하고 버튼이 눌리지 않았으면 `R.color.gray`를 사용하게 된다. 
이와 다르게 `color` 폴더에는 `<selector>`라는 태그가 있어서 그 안에 `<item>` 태그를 이용해 뷰의 상태와 그때의 색상을 지정해 놓을 수 있다. 이를 이용하면 xml 파일에서 button의 색상 속성에 `@color/해당 파일명`을 넣으면 상태에 맞는 색상이 버튼에 적용이된다.


## 플랫폼 리소스
---
개발자가 직접 만드는 리소스와 달리 안드로이드 플랫폼에서 제공하는 리소스를 말한다. 앱 리소스를 사용할 때는 `R`을 뜻하는 `@` 기호를 사용한 것처럼 플랫폼 리소스를 사용할 때도 `@` 기호를 사용하는 것은 같지만, `@android:`와 같이 android를 붙여서 사용해야 한다.


## 참고 자료
---
- Do it! 깡쌤의 안드로이드 앱 프로그래밍 with 코틀린
<iframe src="https://coupa.ng/cbgCRw" width="120" height="240" frameborder="0" scrolling="no" referrerpolicy="unsafe-url"></iframe>
이 포스팅은 쿠팡 파트너스 활동의 일환으로, 이에 따른 일정액의 수수료를 제공받습니다.