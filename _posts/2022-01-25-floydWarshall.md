---
layout: post
title:  "Floyd-Warshall, 플로이드 워셜"
date:   2022-01-25 00:10:28 +0800
categories: [Algorithm]
tags: [algorithm]
mainfont: GowunDodum-Regular
---

## 📕 Floyd-Warshall(플로이드 워셜) 알고리즘이란?
모든지점에서 다른 모든 지점까지의 최단 경로를 모두 구해야 하는 경우 사용한다.

`다이나믹 프로그래밍`으로 분류된다.

A에서 B로가는 비용 vs A에서 K번 노드를거쳐 B로가는 비용중에서 최소값을 갱신해나간다.


## 🎢 Floyd-Warshall의 동작

<img src="https://user-images.githubusercontent.com/46019755/150815640-273ce51e-ee9b-4930-83fe-85c5f495f10b.png">

<img src="https://user-images.githubusercontent.com/46019755/150815688-faf60cab-262e-4a46-8440-2482d48aa049.png">

<img src="https://user-images.githubusercontent.com/46019755/150815725-634bc099-7d63-4c01-9428-38e1608d01fa.png">

<img src="https://user-images.githubusercontent.com/46019755/150815752-c4082007-924a-4f37-9238-af623f7f22fb.png">

<img src="https://user-images.githubusercontent.com/46019755/150815793-af278f15-4c5f-40b6-9979-c545a4f3e17f.png">


## 🤯 로직
- `2차원` 최단 거리 테이블 무한으로 초기화
- 자기 자신 -> 자기 자신은 거리 0으로 초기화
- 1번~n번까지 (`k`)
   - 1번~n번까지 (`a`)
      - 1번~n번까지 (`b`)
         - a->b 거리 테이블을 바로 가는 거리(`a->b`)와 k를 거쳐가는 거리(`a->k->b`) 중 최소값으로 갱신 

## ⏰ 시간 복잡도

`O(n^3)`