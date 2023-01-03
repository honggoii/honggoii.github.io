---
layout: post
title:  "React Native Load Local HTML File"
date:   2023-01-03 22:49:43 +0900
categories: ReactNative
---

### 문제

- 웹뷰에 로컬 html 파일을 실행해야 하는 상황
- Android, iOS 모두 debug 모드에서 테스트 완료했으나, iOS가 release만 하면 로컬 html 파일을 열지 못하는 문제가 발생

### 문제 해결

- OS별로 로컬 파일을 불러오는 경로가 다르다.
- `<WebView>` 속성에 `originWhitelist={['*']}` 를 추가해야 **release 모드에서도** 로컬 파일 경로를 찾아 갈수가 있다.
- `originWhitelist` 속성의 default 값은 `"http://"` 와 `"https://` 인데, 불러올 파일은 로컬에 있는 경로이니 `"http://"` 가 아닐 것이므로 찾아갈 수 없을거라는 **나의 뇌피셜**
- debug에서는 왜 찾아가는지 이유는 찾지 못함

### Android

`android > app > src > main > assets` 경로에 로컬 파일을 넣어주고 다음과 같이 경로를 지정해준다.

`'file:///android_asset/test.html'`

### iOS

`'require('로컬 파일 경로')'`

```jsx
<WebView
  originWhitelist={['*']}
  source={
    Platform.OS === 'android'
      ? {uri: 'file:///android_asset/test.html'}
      : require('./test.html')
  }
/>
```

### originWhitelist={[’*’]}

- **static HTML 파일**을 Load하기 위해서 설정해 주어야 하는 속성
- 탐색을 허용할 원본 문자열 목록
- default값은 `"http://"` 와 `"https://` 이다.

### 삽질

iOS에서 release 모드로 빌드하려면 bundle을 말아줘야 하는데, bundle을 말기만 하면 웹뷰를 불러오지 못해서 로컬 html 경로를 불러오는 방식 자체가 틀렸다고만 생각했다.

[https://skyksit.com/programming/react/react-native-local-html-webview/](https://skyksit.com/programming/react/react-native-local-html-webview/)

해당 블로그를 참고해서 시도해봤으나 문제는 해결되지 않았다.

### iOS

`'Web.bundle/test.html'`

```
<WebView
  source={{uri: Platform.OS === 'android' ? 'file:///android_asset/test.html' : 'Web.bundle/test.html'}}
/>
```

안드로이드는 로컬 파일을 불러오기 위해 정해진 경로, `file:///android_asset/` 가 있는 것은 맞지만, iOS는 `Web.bundle` 자체가 로컬 파일을 불러오는 정해진 경로가 아니라고 생각한다.

#### bundle

의존성 관계가 있는 파일을 묶는 역할

#### 참고 자료

- [https://skyksit.com/programming/react/react-native-local-html-webview/](https://skyksit.com/programming/react/react-native-local-html-webview/)
- [https://github.com/facebook/react-native/issues/505](https://github.com/facebook/react-native/issues/505)
- [https://github.com/react-native-webview/react-native-webview/issues/656](https://github.com/react-native-webview/react-native-webview/issues/656)
- [https://github.com/react-native-webview/react-native-webview/blob/master/docs/Reference.md](https://github.com/react-native-webview/react-native-webview/blob/master/docs/Reference.md)
- [https://stackoverflow.com/questions/57994130/how-to-load-the-local-file-in-react-native-ios-webview](https://stackoverflow.com/questions/57994130/how-to-load-the-local-file-in-react-native-ios-webview)
- [https://stackoverflow.com/questions/47661941/react-native-webview-does-not-render-local-html-when-building-release-apk](https://stackoverflow.com/questions/47661941/react-native-webview-does-not-render-local-html-when-building-release-apk)
- [https://aboutreact.com/load-local-html-file-url-using-react-native-webview/#IOS](https://aboutreact.com/load-local-html-file-url-using-react-native-webview/#IOS)
- [https://stackoverflow.com/questions/47808746/create-groups-vs-create-folder-reference-in-xcode](https://stackoverflow.com/questions/47808746/create-groups-vs-create-folder-reference-in-xcode)
- [https://nazan9.tistory.com/7](https://nazan9.tistory.com/7)
- [http://vocaro.com/trevor/blog/2012/10/21/xcode-groups-vs-folder-references/](http://vocaro.com/trevor/blog/2012/10/21/xcode-groups-vs-folder-references/)
- [https://velog.io/@young_pallete/Bundle이란](https://velog.io/@young_pallete/Bundle%EC%9D%B4%EB%9E%80)
- [https://sihyungyou.github.io/iOS-app-bundle/](https://sihyungyou.github.io/iOS-app-bundle/)