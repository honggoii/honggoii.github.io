---
layout: post
title:  "Union Find (서로소 집합) 자료구조"
date:   2022-01-30 21:00:28 +0800
categories: [Algorithm]
tags: [algorithm]
mainfont: GowunDodum-Regular
---

## 📕 서로소 집합 자료구조란?

<span style="color:red; font-size:13pt">서로소란? </span>
공통 원소가 없는 두 집합

서로소 집합 자료구조는 2가지 연산을 가지고 있다.
### 1. Union 연산 : 같은 집합으로 묶는다.
### 2. Find 연산 : 특정 원소가 속한 집합의 부모(루트)를 찾으러간다.

## 🎢 Union연산과 Find연산의 동작
예를들어, {1, 2, 3, 4, 5, 6} 6개의 원소가 있다고 하자.

집합이 다음과 같다.

{1, 4}, {2, 3}, {2, 4}, {5, 6}


이제 Union-Find 자료구조를 이용하여 각 원소가 속한 집합을 찾는다.

1. parent 테이블 하나를 만든다.

2. 각 노드의 parent를 자기자신으로 초기화한다.

<img src="https://user-images.githubusercontent.com/46019755/151700028-c6b500cf-e370-4f72-be8b-d112a637106f.png">

3. 각 집합에 대해 union-find 연산을 수행한다.

{1, 4}

1의 부모와 4의 부모를 비교하여 더 작은 수가 부모가 되도록한다.

<img src="https://user-images.githubusercontent.com/46019755/151700034-0091f9c7-497e-4827-88f5-593db97a6b78.png">

{2, 3}

2의 부모와 3의 부모를 비교하여 더 작은 수가 부모가 되도록한다.

<img src="https://user-images.githubusercontent.com/46019755/151700039-992f4884-c9aa-49c9-900f-0fa80365d6f9.png">

{2, 4}

2의 부모와 4의 부모를 비교하여 더 작은 수가 부모가 되도록한다.

<img src="https://user-images.githubusercontent.com/46019755/151700043-42658f05-1368-4c0b-96b7-46d24d52435f.png">

{5, 6}

5의 부모와 6의 부모를 비교하여 더 작은 수가 부모가 되도록한다.

<img src="https://user-images.githubusercontent.com/46019755/151700052-236836d8-9e27-4e4c-ac40-74715648b3d6.png">

4. 결과적으로 {1, 2, 3, 4}는 1을 부모로 갖는 집합, {5, 6}은 5를 부모로 갖는 집합이 된다.

<img src="https://user-images.githubusercontent.com/46019755/151700062-900f92d3-e287-4673-a8a0-79ad3e9fbff3.png">


## 🤯 로직

### Find 연산
```
- 부모가 아니면
- 내 부모의 부모(조부모)를 찾는다. (Find 연산 재귀)
- 부모가 맞으면
  - 부모를 리턴한다.
```
```python
def find(parent, x):
    if parent[x] != x: # 루트 노드가 아니면
        parent[x] = find(parent, parent[x]) # 루트 찾을 때까지 재귀
    return parent[x] # 루트 노드 반환
```

### Union 연산
```
- a의 부모를 찾는다. (Find 연산)
- b의 부모를 찾는다. (Find 연산)
- a의 부모가 b의 부모보다 작으면
  - b의 부모를 a로한다.
- b의 부모가 a의 부모보다 작으면
  - a의 부모를 b로한다.
```
```python
def union(parent, a, b):
    a = find(parent, a)
    b = find(parent, b)
    if a < b: # 더 작은 원소가 부모가 되도록
        parent[b] = a
    else:
        parent[a] = b
```

## 🎡 Cycle 판별
무방향 그래프에서 Union-Find 연산을 사용하여 `Cycle 여부`를 판별할 수 있다.

```python
if find(parent, a) == find(parent, b): # 루트가 같으면 
    cycle = True # 사이클이 발생
    break
else: # 사이클이 발생하지 않으면
    union(parent, a, b) # 합집합 수행
```