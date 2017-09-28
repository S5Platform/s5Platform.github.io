---
title: React Native
category: React Native
order: 1
---

# React Native

리액트 네이티브는 Facebook에서 공개한 오픈소스로 javascript를 사용해서 모바일 앱을 개발할 수 있게 해주는 플랫폼이다. Facebook에서 공개한 React를 사용하기 때문에 익숙하게 접근이 가능하며, 하이브리드 모바일 앱이 아닌 Native 앱을 만들 수 있다. 

### 


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

0.44 버젼 부터 Navigator가 deprecated 되었다. Navigation을 보다 쉽게 실행할 수 있게 reactnavigation.org 에서 Navigation을 [React Navigation](https://reactnavigation.org/)을 공개하였다. 아래와 같은 방법으로 설치할 수 있다.

```
yarn add react-navigation
```

```
npm install --save react-navigation
```