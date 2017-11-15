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

### Redux

Redux는 자바스크립트 앱을 위한 예측 가능한 상태 컨테이너이다. [Flux 아키텍쳐]()의 사상을 발전시킨 개념인데, store , reducer, action 이라는 3가지의 개념이 존재한다.

- store : 앱의 상태 전부는 하나의 store라는 객체 트리에 저장된다.
- action : 상태를 변경하기 위해서는 action을 통해서만 가능하다.
- reducer : action이 상태 트리를 어떻게 변경할지 명시하기 위해서 reducer를 작성해야 한다.

![redux](/images/redux.png)

위와 같이, store에서 모든 데이터를 담고 있고, 컴포넌트끼리는 직접 교류하지 않고 store 를 통하여 교류를 한다. store에 있는 데이터가 업데이트 되면 해당 store에 connect (subcribe) 하고 있는 컴포넌트들에 결과를 반영하는 것이다. 

Redux의 3가지 원칙은 아래와 같다.

#### 진실은 하나의 소스로부터

애플리케이션의 모든 상태는 하나의 스토어 안에 하나의 객체 트리 구조로 저장되어야 한다.

#### 상태는 읽기 전용이다

상태를 변화시키는 유일한 방법은 무슨 일이 벌어지는 지를 묘사하는 액션 객체를 전달하는 방법뿐이다.

이를 통해서 뷰나 네트워크 콜백에서 결코 상태를 직접 바꾸지 못 한다는 것을 보장할 수 있다. 모든 상태 변화는 중앙에서 관리되며 모든 액션은 엄격한 순서에 의해 하나하나 실행되기 때문에, 경쟁 상태에 대한 고민을 할 필요가 없게 된다. 


#### 변화는 순수 함수로 작성되어야한다

액션에 의해 상태 트리가 어떻게 변화하는 지를 지정하기 위해 프로그래머는 순수 리듀서를 작성해야합니다.

리듀서는 그저 이전 상태와 액션을 받아 다음 상태를 반환하는 순수 함수이다. 이전 상태를 변경하는 대신 새로운 상태 객체를 생성해서 반환해야한다.

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

#### StackNavigator

default로 StackNavigator는 iOS 와 Android의 Look&Feel에 유사하도록 설정 되어 있다. 새로운 화면으로 전환될때 iOS의 경우는 화면의 오른쪽에서 슬라이딩 되면서 보여지게 되고, Android의 경우는 Modal과 비슷한 형태의 화면이 화면 하단에서 올라오도록 되어 있다.

```
const RootStack = StackNavigator(
  {
    // Router Options
    Home: {
      screen: HomeScreen,
    },
    Profile: {
      screen: ProfileScreen,
    },
  },
  {
    // Visual Options
    headerMode: 'none',
    mode: 'card'
  }

);
```

StacKNavigator에 설정할 수 있는 Visual 설정은 아래와 같은 것들이 있다.

- mode : 화면전환할 때의 옵션을 선택하는 것으로 *card*와 *modal*이 있다. *card* 의 경우 기본적인 화면 전환을 의미하며, *modal* 옵션은 iOS에서만 동작하는 option으로 화면 아래에서 올라오면서 화면이 전환된다.

- headerMode : 헤더 부분을 어떻게 표현할 것인가에 대한 옵션으로 *none*의 경우 헤더를 표현하지 않게 되고, *float*은 iOS에서의 기본 옵션, *screen*은 *android*에서의 기본 옵션이다.

#### TabNavigator

TabNavigator는 TabBar를 이용하여 화면을 구성할 때 사용할 수 있는 컴포넌트이다. navigationOption으로 Tab에서 사용할 Title과 Icon을 설정할 수 있다.


```
const RootStack = TabNavigator(
  {
    // Router Options
    Home: {
      screen: HomeScreen,

      // Navigation Options
      navigationOptions: {
        tabBarLabel: 'Home',
        tabBarIcon: ({ tintColor }) => <Icon name={'people'} color={tintColor} />
      },
    },
    Profile: {
      screen: ProfileScreen,
      navigationOptions: {
        tabBarLabel: 'Profile',
        tabBarIcon: ({ tintColor }) => <Icon name={'chatbubbles'} color={tintColor} />
      },
    },
  },
  {
    tabBarComponent: 'TabBarBottom',
    tabBarPosition: 'top',
    animationEnabled: true,
    tabBarOptions: {
      activeTintColor: '#e91e63',
      showLabel: true
    }
  }
);
```

TabNavigator에서 설정할 수 있는 Visual 설정은 아래와 같은 것들이 있다.

- tabBarPosition : *top* 이나 *bottom* 으로 설정이 가능하다.
- tabBarOptions : TabBar의 설정이 가능하다.

#### DrawerNavigator

DrawerNavigator는 왼쪽이나 오른쪽에서 슬라이드하면서 나오는 Drawer를 구현할때 사용할수 있는 Component이다.

```
const MyNavScreen = ({ navigation, banner }) => (
  <ScrollView style={styles.container}>
    <SampleText>{banner}</SampleText>
    <Button
      onPress={() => navigation.navigate('DrawerOpen')}
      title="Open drawer"
    />
    <Button onPress={() => navigation.goBack(null)} title="Go back" />
  </ScrollView>
);

const InboxScreen = ({ navigation }) => (
  <MyNavScreen banner={'Inbox Screen'} navigation={navigation} />
);

InboxScreen.navigationOptions = {
  drawerLabel: 'Inbox',
  drawerIcon: ({ tintColor }) => (
    <MaterialIcons
      name="move-to-inbox"
      size={24}
      style={{ color: tintColor }}
    />
  ),
};

const DraftsScreen = ({ navigation }) => (
  <MyNavScreen banner={'Drafts Screen'} navigation={navigation} />
);

DraftsScreen.navigationOptions = {
  drawerLabel: 'Drafts',
  drawerIcon: ({ tintColor }) => (
    <MaterialIcons name="drafts" size={24} style={{ color: tintColor }} />
  ),
};

const DrawerExample = DrawerNavigator(
  {
    Inbox: {
      path: '/',
      screen: InboxScreen,
    },
    Drafts: {
      path: '/sent',
      screen: DraftsScreen,
    },
  },
  {
    initialRouteName: 'Drafts',
    contentOptions: {
      activeTintColor: '#e91e63',
    },
  }
);

const styles = StyleSheet.create({
  container: {
    marginTop: Platform.OS === 'ios' ? 20 : 0,
  },
});

export default DrawerExample;
```

*'DrawerOpen'*이나 *'DrawerClose'* 으로 화면을 이동시켜서 Drawer를 열거나 닫을 수 있다.

```
this.props.navigation.navigate('DrawerOpen'); // open drawer
this.props.navigation.navigate('DrawerClose'); // close drawer
```

DrawerNavigatorConfig 로 설정할 수 있는 Option들은 아래와 같다.
 - drawerWidth : drawer의 width
 - drawerPosition : drawer의 위치를 설정할 수 있다. left or right로 설정할 수 있다.
