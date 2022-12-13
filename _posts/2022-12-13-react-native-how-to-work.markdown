---
layout: post
title:  "React Native 동작 방식"
date:   2022-12-13 21:49:43 +0900
categories: ReactNative
---

React Native App은 4개의 스레드가 있다.

1. <span style="background-color:white; color:blue">UI Thread</span> - 메인 스레드. 각 네이티브 UI 렌더링에 사용되는 스레드.
2. <span style="background-color:white; color:blue">JS Thread</span> - **비즈니스 로직**이 실행되는 스레드. 자바스크립트 코드 실행, API 호출, 터치 이벤트와 같은 것들이 처리되는 스레드.
3. <span style="background-color:white; color:blue">Native Modules Thread</span> - 플랫폼 API에 액세스해야 할 때 사용되는 스레드
4. <span style="background-color:white; color:blue">Render Thread</span> - Android L (5.0)에서만 UI를 그리는데 사용되는 OpenGL 명령어를 생성하는데 사용되는 스레드


#### **Bridge**

UI Thread와 JS Thread는 직접 상호작용하지 않고 bridge를 통해 상호작용한다.

birdge는 3가지 중요한 특징을 가진다.

- <span style="background-color:white; color:blue">Asynchronous</span> : 서로 block되지 않음
- <span style="background-color:white; color:blue">Batched</span> : 최적화된 방식으로 하나의 스레드에서 다른 스레드로 메세지 전달
- <span style="background-color:white; color:blue">Serializable</span> : 같은 데이터를 공유하지 않고 교환

일반적으로 React Native를 3 부분으로 분리할 수 있다.
- **Native side**
- **JS side**
- **Bridge**


#### **React Native 작업 프로세스**

1. **UI Thread**가 실행되고 JS 번들 로딩
2. JavaScript 코드가 성공적으로 로딩되면, UI Thread는 다른 **JS Thread**로 보냄 -> JS Thread가 계산을 많이할수록 UI Thread가 덜 고통받기 때문
3. React가 새로 렌더링을 시작하면, 새로운 가상 DOM을 생성되고 이때, 변경 사항을 다른 스레드(**Shadow Thread**, shadow node에 생성되기 때문에 생긴 이름)로 보냄
4. **Shadow Thread**는 레이아웃을 계산하고 **UI Thread**에 파라미터/객체를 보냄
5. **UI Thread**만 화면에 렌더링할 수 있기 때문에, Shadow Thread는 생성된 레이아웃을 UI Thread로 전송하고 이때만 UI가 렌더링


---
#### 참고 자료
> [https://www.codementor.io/@saketkumar95/how-react-native-works-mhjo4k6f3](https://www.codementor.io/@saketkumar95/how-react-native-works-mhjo4k6f3)  
> [https://reactnative.dev/docs/performance](https://reactnative.dev/docs/performance)  
> [https://medium.com/we-talk-it/react-native-what-it-is-and-how-it-works-e2182d008f5e](https://medium.com/we-talk-it/react-native-what-it-is-and-how-it-works-e2182d008f5e)  
> [https://medium.com/@sannanmalikofficial/how-the-react-native-bridge-works-86171d9a7585](https://medium.com/@sannanmalikofficial/how-the-react-native-bridge-works-86171d9a7585)