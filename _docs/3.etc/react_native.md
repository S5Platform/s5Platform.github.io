---
title: React Native
category: etc
order: 1
---

# React Native Trend

-----------
## 1달 주기의 릴리즈 정책 시작

react native 가 발표된 이후, 새로운 기능을 추가하기 위해 2주에 한번씩 새로운 버젼을 릴리즈하는 정책을 유지해왔다. 이는 2주에 한번씩 릴리즈되는
Facebook 의 ios 앱과 동일한 릴리즈 페이스를 유지하기 위함이었다.

이러한 릴리즈 정책은 2016년 12월 0.40 버젼부터 이후부터 1달 주기로 릴리즈되도록 정책이 변경되었다. 2주 단위의 릴리즈가 버젼을 유지하기에 힘들다는 의견이 반영된 점도 있다.
`react-native-git-upgrade` 명령어를 이용하면 보다 쉽게 새로운 버젼을 적용할 수 있게 지원하고 있다.

## Using Native Driver for Animated

개발자들이 lag을 유발할 수도 있는 코드들에 대한 걱정을 하지 않으면서 성능이 뛰어난 애니메이션 효과를 사용할 수 있게 하기 위해 약 1년간 노력을 해왔다.
Animated Api는 serializable 을 이용하도록 설계되어 있었다. 애니메이션이 시작하기 직전에 애니메이션에 대한 모든 정보를 Native 에게 전송하게 되는데, 이러한 방법을 이용하여 Animation이 동작하는 동안 JS Thread를 block할 수 있게 되었다.

## Better List Views in React Native

기존의 ListView 에 있던 메모리 이슈나 버그들이 해결된 ListView가 등장했다. Use Case에 따라 FlatList, SectionList, VirtualizedList 등 다양한 ListView를 사용할 수 있게 되었다
VirtualizedList 는 Pull to refresh 나 Scroll loading 등의 기능을 지원하기 때문에  가변적인 데이터를 다루는 데 유용하다. scrollToIndex 와 같은 기능을 사용하면 렌더링 없이 원하는 위치로 이동할 수도 있다.

## idx: The Existential Function

복합한 형태의 JSON Data에서 null 일 수도 있는 데이터에 접근하기 위해서는 아래와 같이 지루한 코드를 사용하게 된다.

```
props.user &&
props.user.friends &&
props.user.friends[0] &&
props.user.friends[0].friends
```

이를 보다 쉽게 접근하기 위해 *idx* 라고 불리는 함수를 제공하고 있다. 이 함수는 내부에서 null or  undefined 여부를 체크해서 해당 값이 없을 경우 null or undefined를 return 하도록 구현되어 있다.

```
idx(props, _ => _.user.friends[0].friends)
```

## Introducing Create React Native App

React Native Project 를 쉽게 시작할 수 있도록 도움을 주는 [Create React App](https://github.com/react-community/create-react-native-app) 프로젝트가 공개되었다. Create React Native App 을 이용하면 개발장비에 Xcode 나 Android Studio 를 설치하지 않아도 Windows나 Linux 에서 React Native App을 개발할 수 있다. 

```bash
npm i -g create-react-native-app
create-react-native-app my-project
cd my-project
npm start
```

`create-react-native-app`으로 생성된 프로젝트를 실행하면 아래와 같이 QR Code 가 나오는데,

![qr](/images/qr.png)

[Expo App](https://expo.io/tools)을 통해 해당 QR Code 를 인식시키면 해당 디바이스에서 테스트가 가능하다.

*이때 동일 네트워크 안에 있어야 한다.*

`Expo app`은 Camera나 Video, 연락처와 Facebook 인증과 같은 유명한 네이티브 모듈을 포함하고 있으며, Expo에 기본적으로 포함되어 있지 않은 모듈의 경우는 `npm run eject`를 이용하면 사용이 가능하다.



