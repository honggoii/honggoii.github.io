---
layout: post
title:  "React Query"
date:   2022-05-01 22:59:43 +0900
categories: ReactNative
---

데이터 Fetching, 캐싱, 동기화, 서버 쪽 데이터 업데이트 등을 쉽게 만들어주는 React 라이브러리

기존의 Redux와 같은 상태 관리 라이브러리는 클라이언트쪽 데이터를 관리하기에 적합

<span style="background-color:white; color:blue">React Query</span>는 서버쪽 상태를 관리하기에 가장 적합한 라이브러리 중 하나

#### Server state
제어하거나 소유하지 않는 위치에서 원격으로 지속

fetching과 updating에 비동기 API 필요

공유한 소유권을 의미하며 다른 사용자가 알지 못하는 사이에 변경할 수 있다.

주의를 기울이지 않으면 응용 프로그램에서 구식이 될 수 있다.

#### React Query 장점
복잡하고 잘못 이해된 많은 코드를 제거하고 몇 줄의 React Query 로직으로 대체

새 서버상태 데이터 소스를 연결할 걱정없이 애플리케이션을 보다 쉽게 유지보수하고 새 기능을 구축

더 빠르고 응답성이 향상되어 최종 사용자에게 직접적인 영향
대역폭을 절약하고 메모리 성능 향상


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