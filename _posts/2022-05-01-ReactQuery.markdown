---
layout: post
title:  "React Query"
date:   2022-05-01 22:59:43 +0900
categories: ReactNative
---

데이터 Fetching, 캐싱, 동기화, 서버 쪽 데이터 업데이트 등을 쉽게 만들어주는 React 라이브러리

기존의 Redux와 같은 상태 관리 라이브러리는 클라이언트쪽 데이터를 관리하기에 적합

<span style="background-color:white; color:blue">React Query</span>는 서버쪽 상태를 관리하기에 가장 적합한 라이브러리 중 하나


#### React Query 장점
- 기존 Redux로 만든 구조에 비해 코드 분량 감소
- 빠르고 응답성 향상
- 메모리 성능 향상


#### useMutation
```javascript
import { useMutation } from 'react-query';
import { getApi } from '@apis/index';

const usetTodoCreator = () => {
	const mutation = useMutation((todo: TodoType) => 
		getApi.post('/todos', todo);
	);
	return mutation;
}
```



---
#### 참고 자료
> https://tech.kakao.com/2022/06/13/react-query/  
> https://fe-developers.kakaoent.com/2022/220224-data-fetching-libs/   
> https://tanstack.com/query/v4/docs/overview?from=reactQueryV3&original=https://react-query-v3.tanstack.com/overview    
> https://techblog.woowahan.com/6339/    
> https://tech.osci.kr/2022/07/13/react-query/    