---
layout: post
title:  "순열과 조합"
date:   2021-12-20 21:33:00 +0800
categories: [Algorithm]
tags: [algorithm]
mainfont: GowunDodum-Regular
---

## 순열
(1,2,3) (1,3,2) (2,3,1) (2,1,3) (3,2,1) (3,1,2) => `모두 다른 것`으로 취급

### c++
```c++
void Permutation(int cnt) {
    if (cnt == 3) {
        return;
    }
    
    for(int i = 0 ; i < 5; i++) {
        if(visit[i]) continue;
        visit[i] = true;
        Permutation(cnt+1);
        visit[i] = false;
    }
}
```

### java
```java
static int n, m; // 1~n까지 m개를 뽑는다.
static int[] selected, used;
static StringBuilder sb = new StringBuilder();

static void permutation(int cnt) {
    if (cnt == m) { // m개를 골랐으면
        for (int i=0; i < m; i++) {
            sb.append(selected[i]).append(' '); // 출력
        }
        sb.append('\n');
    } 

    for (int i=1; i <= n; i++) {
        if (used[i] == 1) continue; // i는 이미 뽑았다.
        selected[cnt] = i; // cnt번에 방문한 값은 i
        used[i] = 1; // i는 뽑았습니다.

        permutation(cnt+1); // 다음꺼 고르러
        selected[cnt] = 0; // 뽑았던 건 초기화
        used[i] = 0; // i는 뽑지 않았습니다.
    }
}
```



## 중복 순열
순열 + (1,1,1) (2,2,2) (3,3,3)

### c++
```c++
void Permutation(int cnt) {
    if (cnt == 3) {
        return;
    }
    
    for(int i = 0 ; i < 5; i++) {
        visit[cnt] = arr[i];//cnt번에 방문한 값은 arr[i]
        Permutation(cnt+1);
    }
}
```

### java
```java
static int n, m; // 1~n까지 m개를 뽑는다.
static int[] selected;
static StringBuilder sb = new StringBuilder();

static void permutation(int cnt) {
    if (cnt == m) { // m개를 골랐으면
        for (int i=0; i < m; i++) {
            sb.append(selected[i]).append(' '); // 출력
        }
        sb.append('\n');
    }

    for (int i=1; i <= n; i++) {
        selected[cnt] = i; // cnt번에 방문한 값은 i

        permutation(cnt+1); // 다음꺼 고르러
        selected[cnt] = 0; // 뽑았던 건 초기화
    }
}
```

## 조합
(1,2,3) (1,3,2) (2,3,1) (2,1,3) (3,2,1) (3,1,2) => `모두 같은 것`으로 취급

### c++
```c++
void Combination(int start, int cnt) {
    if (cnt == 3) {
        return;
    }
    
    for(int i = start ; i < 5; i++) {
        if(visit[i]) continue;
        visit[i] = true;
        Combination(i, cnt+1);
        visit[i] = false;
    }
}
```

### java
```java
static void combination(int start, int k) {
    if (k == m) { // m개를 골랐다!
        for (int i=0; i < m; i++) {
            sb.append(selected[i]).append(' ');
        }
        sb.append('\n');
        return;
    } 

    for (int i=start+1; i <= n; i++) { // start부터 뽑겠다!
        selected[k] = i;
        combination(i, k+1);
        selected[k] = 0;
    }
}
```


## 중복 조합
조합 + (1,1,1) (2,2,2) (3,3,3) 

### c++
```c++
void Combination(int start, int cnt) {
    if (cnt == 3) {
        return;
    }
    
    for(int i = start ; i < 5; i++) {
        visit[cnt] = arr[i];//cnt번에 방문한 값은 arr[i]
        Combination(i, cnt+1);
    }
}
```

### java
```java
static void combination(int start, int k) {
    if (k == m) { // m개를 골랐다!
        for (int i=0; i < m; i++) {
            sb.append(selected[i]).append(' ');
        }
        sb.append('\n');
        return;
    } 

    for (int i=start; i <= n; i++) { // start부터 뽑겠다!
        selected[k] = i;
        combination(i, k+1);
        selected[k] = 0;
    }
}
```