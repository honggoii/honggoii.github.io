---
layout: post
title:  "RecyclerVew"
date:   2022-01-06 21:26:28 +0800
categories: [Android]
tags: [android]
mainfont: GowunDodum-Regular
---


## RecyclerVew
---
목록 화면을 만들 때 사용하는 뷰. `RecyclerView`를 만들기 위해서는 아래의 4가지가 필수❗로 구현되어야 한다.

1. `ViewHolder` : `RecyclerView`의 각 항목을 구성하는 뷰 객체. `RecyclerView.ViewHolder`를 상속받아서 구현한다.
2. `Adapter` : `VieHolder`에 있는 각 뷰 객체에 데이터 대입. `Recyclerveiw.Adapter`를 상속받아서 구현한다. `Adapter`에서 재정의해야 함수는 다음과 같다.
   - `getItemCount()` : `RecyclerView`에 나타나야할 항목의 개수. 항목의 개수를 반환하면 해당 개수만큼 `onBindViewHodler()`가 호출되어 데이터를 입힌다.
   - `onCreateViewHolder()` : `ViewHolder` 생성. 반환한 객체는 `onBindViewHolder()`에 자동으로 전달한다.
   - `onBindViewHolder()` : `ViewHolder`의 각 뷰 객체에 알맞은 데이터 대입  
3. `LayoutManager` : `Adapter`가 만든 데이터가 들어간 항목을 배치하여 출력
4. `2개의 xml 파일` : `RecyclerView`를 등록할 xml파일 + 각 항목을 구현할 레이아웃 xml


## notifyDataSetChanged()
---
동적으로 `RecyclerView`의 항목을 추가하거나 제거한 후 호출.

```kotlin
adapter.notifyDataSetChanged()
```



## 참고 자료
---
- Do it! 깡쌤의 안드로이드 앱 프로그래밍 with 코틀린
<iframe src="https://coupa.ng/cbgCRw" width="120" height="240" frameborder="0" scrolling="no" referrerpolicy="unsafe-url"></iframe>
이 포스팅은 쿠팡 파트너스 활동의 일환으로, 이에 따른 일정액의 수수료를 제공받습니다.