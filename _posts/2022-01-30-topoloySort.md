---
layout: post
title:  "Topology Sort, 위상 정렬"
date:   2022-01-30 22:15:28 +0800
categories: [Algorithm]
tags: [algorithm]
mainfont: GowunDodum-Regular
---

## 📕 Topology Sort(위상 정렬) 알고리즘이란?

위상정렬은 <span style="color:blue">DAG(Directed Acyclic Graph)에서 모든 vertex를 정렬하는 것</span>이다.

의미 그대로 <span style="color:red">방향성이 있고(Directed) 순환하지 않는(Acyclic) 그래프(Graph)</span>를 말한다. 

<span style="color:red">순서가 정해진 작업을 차례대로 수행할 때</span> 사용하는 알고리즘이다.


## 🎢 Topology Sort 알고리즘의 동작

<img src="https://user-images.githubusercontent.com/46019755/151703583-f613f4b3-3c62-445b-89c1-86c17325de4d.png">

<img src="https://user-images.githubusercontent.com/46019755/151703586-6e61d39b-2bf1-4e68-84bf-610dd72d29ca.png">

<img src="https://user-images.githubusercontent.com/46019755/151703588-6256c137-0060-4212-839c-2ca1a54892bd.png">

<img src="https://user-images.githubusercontent.com/46019755/151703593-b9d9787e-23a2-4485-ad6f-b2dc6c4b1c31.png">

<img src="https://user-images.githubusercontent.com/46019755/151703596-05b1cc11-1ff6-430a-83e3-9d54ac40040a.png">

<img src="https://user-images.githubusercontent.com/46019755/151703600-2e82c59a-efe9-4bd6-9504-5f998e3b4a5b.png">

<img src="https://user-images.githubusercontent.com/46019755/151703608-54502b81-64aa-486c-91ef-777b94121960.png">


## 🤯 로직

```
- 각 vertex에 indegree를 저장한다.
- indegree가 0인 vertex를 모두 큐에 넣는다.
- 큐가 빌때까지 다음을 반복한다.
  - 큐에서 하나 꺼낸다.
  - 큐에서 꺼낸 vertex와 연결된 vertex를 찾아 indegree를 1 감소한다.
  - indegree가 0인 vertex를 큐에 넣는다.
```

여기서 indegree란, 진입 차수로 나에게 들어오는 간선의 개수를 의미한다.

처음 시작할 때, indegree가 0인 vertex가 2개 이상일 수 있으므로, 여러 가지 답이 존재할 수 있다.

큐에서 나온 순서가 위상정렬의 결과이며 위상정렬은 순환하지 않는 그래프이지만, 

만약 모든 vertex를 방문하기 전에 큐가 비어버리면 <span style="color:red">사이클이 발생하는 경우</span>이다.


## ⏰ 시간 복잡도

모든 노드를 탐색하고 모든 간선을 차례로 제거하므로 `O(V+E)`가 된다.