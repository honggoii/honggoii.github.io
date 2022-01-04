---
layout: post
title:  "API 호환성과 퍼미션"
date:   2022-01-04 21:34:54 +0800
categories: [Android]
tags: [android]
mainfont: GowunDodum-Regular
---


## API 레벨
---
`build.gradle` 파일에서는 다음과 같이 SDK 버전을 설정한다.

```
minSdkVersion 16
targetSdkVersion 30
```

여기서 말하는 `minSdkVersion`은 해당 API부터 설치가 가능하다는 의미이고 `targetSdkVersion`은 현재 이 앱을 개발할 API 레벨을 말한다. 
API 레벨 16까지 등장한 함수들은 문제가 없지만 16이후로 등장한 함수들은 호환성에 문제가 생긴다. 
만약 API 레벨 30에서 새로 등장한 함수가 있다고 했을 때, 해당 앱은 API 레벨 16부터 설치가 가능하므로 레벨이 16인 앱을 생각해서 개발을 해야한다는 것이다. 

이러한 문제를 해결하기 위해서 `@RequireApi`/`@TargetApi` 애너테이션을 사용하여 안드로이드 스튜디오 상에서의 오류를 해결할 수는 있다. 
하지만 실제 앱에서는 문제가 발생하므로 `Build.VERSION.SDK_INT`를 사용하여 현재 앱을 사용하는 기기의 API 레벨을 확인하여 특정 API 레벨 이상에서만 함수가 실행되도록 할 수 있다.

```kotlin
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.R) {
    // R 버전 이상인 기기에서만 실행하는 블럭
}
```


## 퍼미션
---
앱의 특정 기능에 대한 접근 권한을 말한다. 다른 앱이나 안드로이드 시스템이 보호하는 기능을 사용하거나 내가 만든 기능의 권한을 얻어야만 다른 앱에서 사용하도록 할 때 사용한다. 

- `<permission>` : 보호하고자 하는 앱의 매니페스트 파일에 설정
- `<uses-permission>` : 보호된 기능을 사용하고자 하는 앱의 매니페스트 파일에 설정





## 참고 자료
---
- Do it! 깡쌤의 안드로이드 앱 프로그래밍 with 코틀린
<iframe src="https://coupa.ng/cbgCRw" width="120" height="240" frameborder="0" scrolling="no" referrerpolicy="unsafe-url"></iframe>
이 포스팅은 쿠팡 파트너스 활동의 일환으로, 이에 따른 일정액의 수수료를 제공받습니다.