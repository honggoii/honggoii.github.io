---
layout: post
title:  "Android의 View"
date:   2021-12-26 19:58:26 +0800
categories: [Android]
tags: [android]
mainfont: GowunDodum-Regular
---

## 뷰 클래스의 계층 구조
---

<img width="100%" height="100%" alt="view hierarchy" src="https://user-images.githubusercontent.com/46019755/147468717-c1c9121c-8c90-4eca-bf35-574dc70ff4d9.png">

Layout이 속하는 ViewGroup은 특정 UI를 출력하기 보다는 여러 View들을 묶어서 관리할 목적으로 사용하고 이 외에 TextView, ImageView와 같은 View들은 특정한 UI를 출력할 
목적으로 사용한다.


## 컴포지트 패턴 (Composite Pattern)
---
문서 객체 모델(Document Object Model)이라고도 하며, 객체를 계층 구조로 만들어 이용하는 패턴이다.


## layout_width와 layout_height
---
view들의 가로와 세로의 크기를 지정할 때 사용하는 속성이다. 이 속성을 지정하는 방법에는 3가지가 있다.
1. px, dp 단위로 직접적인 수치
2. `match_parent` : 부모(자신의 상위 계층) 크기 전체
3. `wrap_content` : 자신이 출력될 정도의 크기

보통 크기를 직접적으로 정하는게 깔끔(?)하다고 생각할 수 있지만, 하나의 애플리케이션으로 다양한 기기에 사용되는 안드로이드는 기기 호환성을 생각해야한다. 
이를 위해서 직접적인 수치보다 `match_parent`, `wrap_content`와 같이 상대적인 크기를 지정하는 것이 좋다.


## margin과 padding
---

- `margin` : View와 View의 거리
- `padding` : 나를 감싸는 View와 내용물과의 거리

<img width="100%" height="100%" alt="margin and padding" src="https://user-images.githubusercontent.com/46019755/147469245-c3ebb81e-19c0-4ee2-9504-2b4e7aedd99b.png">


## android:visibility의 속성
---
View를 보여줄지 말지 정하는 `android:visibility`의 속성에는 다음과 같이 3가지가 있다.
1. `visible` : 뷰 출력
2. `invisible` : 뷰 출력 X + 자리 차지
3. `gone` : 뷰 출력 X

여기서 `invisible`과 `gone`은 뷰를 출력하지 않는다는 공통점이 있지만, 자리를 차지하느냐에 따라 차이가 발생한다.
`invisible`은 화면에 보이지는 않지만 자신의 자리는 다른 View가 오지 못하도록 자리를 차지하고 `gone`은 화면에 보이지 않고 자신의 자리에 다른 View가 올 수 있도록 자리를 차지하지 않는다.

<img width="100%" height="100%" alt="visibility" src="https://user-images.githubusercontent.com/46019755/147469518-358419c2-50a6-4dea-9089-922d62dcc3cd.png">


## TextView 속성
---

- `android:autoLink` : 특정 형태(web, phone, email 등) 문자열에 자동 링크 추가
- `android:maxLines` : 특정 줄까지만 출력
- `android:ellipsize` : maxLines를 이용해서 출력을 줄일 때, 줄임표(...) 출력
  - `start` : 문자열 앞에 줄임표
  - `middle` : 문자열 중간에 줄임표
  - `end` : 문자열 뒤에 줄임표
  - `start` 와 `middle` 속성을 사용하기 위해서는 `android:singleLine="true"` 속성일 때만 적용 가능하다. 


## 참고 자료
---
- Do it! 깡쌤의 안드로이드 앱 프로그래밍 with 코틀린
<iframe src="https://coupa.ng/cbgCRw" width="120" height="240" frameborder="0" scrolling="no" referrerpolicy="unsafe-url"></iframe>
이 포스팅은 쿠팡 파트너스 활동의 일환으로, 이에 따른 일정액의 수수료를 제공받습니다.