---
layout: post
title:  "다양한 Layout"
date:   2021-12-28 21:03:16 +0800
categories: [Android]
tags: [android]
mainfont: GowunDodum-Regular
---

## Linear Layout
---
`orientation`이라는 속성을 통해 뷰를 가로(`horizontal`) / 세로(`vertical`) 로 배치하는 레이아웃 클래스이다. 
주로 중첩해서 사용하여 복잡한 뷰를 구성해낼 수 있다.

- `layout_weight` : 여백을 각각 나눠갖는다. 예를들어 버튼 2개가 있고 버튼1에는 `layout_weight`을 1, 버튼2에는 `layout_weight`을 3을 주게되면, 남은 여백을 각각 1/4, 3/4씩 나눠 차지한다.
- `gravity` : 자신이 가지고 있는 자식(`콘텐츠`) 정렬
- `layout_gravity` : 뷰 자체 정렬. Linear Layout에서는 가로/세로 방향으로 뷰를 배치하기 때문에 `orientation`과 같은 방향으로는 `layout_gravity` 속성이 적용되지 않는다.


## Relative Layout
--- 
상대 뷰의 위치로 자신의 위치를 정렬하는 레이아웃 클래스이다.

다음과 같은 속성의 값에는 기존 뷰의 id를 입력한다.

#### 기존 뷰를 기준으로 배치
- `layout_above` : 기존 뷰 위에 배치
- `layout_below` : 기존 뷰 아래에 배치
- `layout_toLeftOf` : 기존 뷰 왼쪽에 배치
- `layout_toRightOf` : 기존 뷰 오른쪽에 배치

#### 기존 뷰를 기준으로 정렬
- `layout_alignTop` : 기존 뷰와 위쪽을 맞춤
- `layout_alignBottom` : 기존 뷰와 아래쪽을 맞춤
- `layout_alignLeft` : 기존 뷰와 왼쪽을 맞춤
- `layout_alignRight` : 기존 뷰와 오른쪽을 맞춤
- `layout_alignBaseline` : 기존 뷰와 텍스트 기준선 맞춤


## Frame Layout
---
뷰를 추가한 순서대로 겹쳐 만드는 레이아웃 클래스이다. 겹쳐서 만들기때문에 주로 `visibility` 속성을 이용해서 액티비티 코드를 통해 각 이벤트에 맞게 필요한 뷰를 보여줄 때 주로 사용한다. 



## 참고 자료
---
- Do it! 깡쌤의 안드로이드 앱 프로그래밍 with 코틀린
<iframe src="https://coupa.ng/cbgCRw" width="120" height="240" frameborder="0" scrolling="no" referrerpolicy="unsafe-url"></iframe>
이 포스팅은 쿠팡 파트너스 활동의 일환으로, 이에 따른 일정액의 수수료를 제공받습니다.