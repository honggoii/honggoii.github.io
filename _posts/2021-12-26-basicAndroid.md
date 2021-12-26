---
layout: post
title:  "Android 컴포넌트와 운영체제 구조"
date:   2021-12-26 20:00:50 +0800
categories: [Android]
tags: [android]
mainfont: GowunDodum-Regular
---

## 컴포넌트
---
- 애플리케이션을 구성하는 단위
- 애플리케이션의 구성요소
- 애플리케이션 안에서 독립된 실행 단위 => 컴포넌트끼리 서로 종속되지 않아서 코드 결합이 발생하지 않는다.
- 안드로이드에서는 하나의 클래스가 하나의 컴포넌트이다. 개발자가 작성하는 클래스 모두 하나의 컴포넌트가 되는 것은 아니다. 런타임 때 생명주기를 누가 관리하느냐에 따라 컴포넌트 클래스가 될지 결정된다. 아래 그림과 같이 생명주기를 안드로이드 시스템이 관리하면 `컴포넌트 클래스`가 되고 개발자 스스로가 관리하면 `일반 클래스`가 된다.

<img width="50%" height="50%" alt="component image" src="https://user-images.githubusercontent.com/46019755/147406421-487032a7-40b5-4438-a561-797c4a1693a7.png">


## 안드로이드 4대 컴포넌트
---
각 컴포넌트는 앱이 실행되는 동안에 각각 다른 기능을 수행한다.
1. `Activity` : 화면을 구성하는 컴포넌트
2. `Service` : 백그라운드 작업을 하는 컴포넌트. 화면 출력이 없고, 화면과 상관없이 백그라운드에서 장시간 실행해야할 업무를 담당한다.
3. `Content Provider` : 앱의 데이터를 공유하는 컴포넌트. 하나의 앱이 자신의 데이터를 다른 앱에 공유하거나 공유받기 위해 사용한다. 카카오톡에서 사진을 보내기 위해 갤러리 앱에 접근하는 경우를 예로 들 수 있다.
4. `Broadcast Receiver` : 사용자 이벤트가 아닌, 부팅 완료, 배터리 방전과 같은 시스템 이벤트가 발생할 때 실행되는 컴포넌트.


## Resource
---
코드에서 정적인 값(항상 똑같은 값)을 분리한 것이다. 
res 폴더 아래에 리소스를 만들면 자동으로 `R.java` 파일에 상수 변수로 리소스가 등록되고 이 상수 변수를 코드에서 사용한다. 예를 들어 res/drawable/icon.png를 코드에서 사용하기 위해서는 `R.drawable.icon`과 같이 이용하면된다. 이처럼 res 폴더는 개발자가 건드릴 경우 시스템은 자동으로 `R.java` 파일에 상수 변수를 만들어주기때문에 규칙을 지켜줘야한다. 개발자 마음대로 폴더 혹은 하위 폴더를 만들 수 없다.


## 매니페스트 파일
---
안드로이드 앱의 메인 환경 파일이다. 시스템은 매니페스트 파일을 바탕으로 앱을 실행하므로 각 컴포넌트들을 매니페스트 파일에 등록해야 시스템이 인지할 수 있다. 매니페스트 파일에 들어가는 태그를 간략하게 소개하면 다음과 같다.
- `<manifest>` : 매니페스트 파일의 루트 태그
- `<application>` : 앱 전체를 대상으로 하는 설정 태그
- `<activity>`, `<service>`, `<provider>`, `<receiver>` : 각 컴포넌트를 등록하는 태그
- 앱 아이콘을 클릭했을 때 실행되는 액티비티를 설정하는 태그는 다음과 같다.  
  
```kotlin
<intent-filter>  
    <action android:name = "android.intent.action.MAIN" />
    <category android:name = "android.intent.category.LAUNCHER" /> 
<intet-filter>
```


## 안드로이드 운영체제 구조
---


출처: [https://en.wikipedia.org/wiki/Android_(operating_system)](https://en.wikipedia.org/wiki/Android_(operating_system))

- 하드웨어 추상화 레이어(`HAL`) : 자바 API 프레임워크가 하드웨어 기능을 이용할 수 있도록 표준 인터페이스 제공
- 안드로이드 런타임(`ART`) : 앱을 실행하는 역할.

<img width="50%" hegith="50%" alt="java compile" src="https://user-images.githubusercontent.com/46019755/147407319-b21e8fe2-1742-49ea-bd6d-47f7265c2062.png">


## 참고 자료
---
- Do it! 깡쌤의 안드로이드 앱 프로그래밍 with 코틀린
<iframe src="https://coupa.ng/cbgCRw" width="120" height="240" frameborder="0" scrolling="no" referrerpolicy="unsafe-url"></iframe>
이 포스팅은 쿠팡 파트너스 활동의 일환으로, 이에 따른 일정액의 수수료를 제공받습니다.