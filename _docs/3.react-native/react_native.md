---
title: React Native
category: React Native
order: 1
---

# React Native

React Native는 Facebook에서 공개한 오픈소스로 javascript를 사용해서 모바일 앱을 개발할 수 있게 해주는 플랫폼이다. Facebook에서 공개한 React를 사용하기 때문에 익숙하게 접근이 가능하며, 하이브리드 모바일 앱이 아닌 Native 앱을 만들 수 있다. 

### How React Native works

React Native는 *React를 모바일 환경에서 어떻게 사용할 수 있을까?* 라는 아이디어에서 시작되었다. 때문에 React Native를 이해하기 위해서는 React의 핵심 개념인 *Virtual DOM* 에 대한 이해가 요구된다.

React는 자바스크립트 내에 DOM Tree와 같은 구조체를 VIRTUAL DOM으로 갖고 있다. 다시 그릴 때는 그 구조체의 전후 상태를 비교하여 변경이 필요한 최소한의 요소만 실제 브라우져의 DOM에 반영된다. 따라서 무작위로 다시 그려도 변경에 필요한 최소한의 DOM만 갱신되기 때문에 빠르게 처리할 수 있는 것이다.

React Native에서는 browser의 DOM 그리는 대신에 IOS일때는 Object-C API를, Android일 때는 Java API를 사용하여 화면을 그린다. *Connector*가 React 와 Native UI 요소들 간의 인터페이스를 담당하고 있기 때문이다. 

### React Native Start

 React Native command line interface를 이용하면 쉽게 React Native App의 샘플 프로젝트을 생성할 수 있다. 아래 명령어를 이용하여 React Native 를 설치한다.

```
npm install -g react-native-cli
```

react-native-cli 가 설치가 완료되면 아래와 같은 명령어를 이용해서 *SampleApp* 이라는 이름의 프로젝트를 생성할 수 있다.
이때 프로젝트 이름은 alphanumeric으로 생성해야 한다. 

```
react-native init SampleApp
```

생성된 프로젝트 폴더에서 `run-ios`을 사용하여 생성된 어플리케이션을 실행할 수 있다.

```
cd SampleApp
react-native run-ios
```

### React Navigation

0.44 버젼 부터 Navigator가 deprecated 되었다. Navigation을 보다 쉽게 구현하기 위해 Reactnavigation.org 에서 Navigation을 [React Navigation](https://reactnavigation.org/)을 공개하였다. 아래와 같은 방법으로 설치할 수 있다.

```
yarn add react-navigation
```

```
npm install --save react-navigation
```

#### Using React Navigation

- StackNavigator : 한번에 하나의 화면을 표현할 수 있으며, 화면이 전환되면 스택의 최상단에 위치하게 된다.
 
- TabNavigator : TabBar를 이용하여 사용자가 여러개의 화면 중 하나를 선택할 수 있다.

- DrawerNavigator : Drawer 를 이용하며 화면 왼쪽이나 오른쪽애서 슬라이드 되면서 새로운 화면이 나타난다.
