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


```java
void Permutation(int cnt) {
    if (cnt == 3) {
        return;
    }
    
    for(int i = 0; i < 5; i++) {
        if(visit[i]) continue;
        visit[i] = true;
        Permutation(cnt+1);
        visit[i] = false;
    }
}
```



## 중복 순열
순열 + (1,1,1) (2,2,2) (3,3,3)



## 조합
(1,2,3) (1,3,2) (2,3,1) (2,1,3) (3,2,1) (3,1,2) => `모두 같은 것`으로 취급



## 중복 조합
조합 + (1,1,1) (2,2,2) (3,3,3) 

