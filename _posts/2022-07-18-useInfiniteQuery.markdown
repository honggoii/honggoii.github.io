---
layout: post
title:  "useInfiniteQuery"
date:   2022-07-18 22:59:43 +0900
categories: ReactNative
---

SNS 서비스의 댓글 개수만큼 댓글 컴포넌트를 만들때, `FlatList` 를 사용했다.

화면에는 약 10개정도의 댓글 컴포넌트가 그려지는데 만약 1만개의 댓글이 있다면, 1만개를 다 불러 오는 것 보다 처음 20개를 부르고 데이터의 마지막 부분에 갈 즈음에 다음 20개를 부르는 방식이 더 효율적이라고 생각했다.

`FlatList` 의 `onEndReachedThreshold` 속성을 사용하여 화면에 리스트의 어느 부분에 닿았을 때 다음 데이터를 요청할지 값을 정해주면 그 값에 따라 onEndReached 가 호출된다.

기존에는 이 `onEndReached` 에 **댓글 조회하는 동일한 api의 파라미터만 변경하며** 다음 리스트를 불러오도록 구현했다.

<span style="background-color:white; color:red">React Query</span>에는 이처럼 GET을 이용한 api 호출, 즉 <span style="background-color:white; color:blue">useQuery</span>의 파라미터만 변경하여 호출할 때 사용하는 <span style="background-color:white; color:blue">useInfiniteQuery</span>가 있다.


```javascript
const {
  fetchNextPage,
  fetchPreviousPage,
  hasNextPage,
  hasPreviousPage,
  isFetchingNextPage,
  isFetchingPreviousPage,
  ...result
} = useInfiniteQuery(queryKey, ({ pageParam = 1 }) => fetchPage(pageParam), {
  ...options,
  getNextPageParam: (lastPage, allPages) => lastPage.nextCursor,
  getPreviousPageParam: (firstPage, allPages) => firstPage.prevCursor,
})
```

#### Parameters
- **queryKey**: 고유 key 값
- **queryFn**: promise를 반환하는 함수
- **getNextPageParam: (lastPage, allPages) => unknown | undefined**
    - 호출된 페이지의 마지막 데이터를 담은 lastPage와 모든 페이지를 담은 allPages를 전달
    - 다음에 전달할 페이지를 리턴해주면 pageParam 에 들어가고, 더이상 불러올 페이지가 없으면 `undefined`를 반환한다.
- **getPreviousPageParam: (firstPage, allPages) => unknown | undefined**
    - 호출된 페이지의 처음 데이터를 담은 firstPage와 모든 페이지를 담은 allPages를 전달
    - 이전에 전달할 페이지를 리턴해주면 `pageParam` 에 들어가고, 더이상 불러올 페이지가 없으면 `undefined`를 반환한다.

#### Returns
- **data**
  - **pages**: 한 번 조회 시 가져온 데이터를 담은 리스트
  - **pageParams**: 한 번 조회 시 사용한 파라미터를 담은 리스트
- **fetchNextPage: (options?: FetchNextPageOptions) => Promise<UseInfiniteQueryResult>**
  - 다음 페이지를 가져오라는 함수
- **hasNextPage: boolean**
  - 가져올 다음 페이지가 있으면 `true` 반환

<span style="background-color:white; color:blue">useInfiniteQuery</span>를 사용하여 다음과 같이 코드를 변경


```javascript
const {data, fetchNextPage, hasNextPage} = useInfiniteQuery(
    'queryKey',
    async ({pageParam = ''}) => { 
        // 댓글 조회 api 호출
    },
    {
        getNextPageParam: (lastPage, allPages) => {
    	    return lastPage?.nextPage;
	},
    },
);

<FlatList
    data={리스트에 보여줄 데이터 배열}
    renderItem={({item, index}) => {
        return ( <Comment /> )
        }
    }
    onEndReachedThreshold={언제 불러올 지}
    onEndReached={() => {
        if (hasNextPage) fetchNextPage();
    }}
/>
```


---
#### 참고 자료
> https://tanstack.com/query/v4/docs/reference/useInfiniteQuery
> https://reactnative.dev/docs/flatlist
> https://jforj.tistory.com/243
> https://jforj.tistory.com/246