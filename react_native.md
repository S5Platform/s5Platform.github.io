# React Native Trend

-----------
## 1달 주기의 릴리즈 정책 시작

react native 가 발표된 이후, 새로운 기능을 추가하기 위해 2주에 한번씩 새로운 버젼을 릴리즈하는 정책을 유지해왔다. 이는 2주에 한번씩 릴리즈되는
Facebook 의 ios 앱과 같은 페이즈를 유지하기 위함이었다.

이러한 정책은 2016년 12월 릴리즈된 0.40 버젼 이후부터 1달 주기로 릴리즈 하도록 정책이 변경되었다.
`react-native-git-upgrade` 명령어를 이용하면 보다 쉽게 새로운 릴리즈 버젼을 적용할 수 있게 지원하고 있다.

## Using Native Driver for Animated

개발자들이 lag을 유발할 수도 있는 코드들에 대한 걱정을 하지 않으면서 성능이 뛰어난 애니메이션 효과를 사용할 수 있게 하기 위해 약 1년간 노력을 해왔다.
Animated Api는 serializable 을 이용하도록 설계되어 있었다. 애니메이션이 시작하기 직전에 애니메이션에 대한 모든 정보를 Native 에게 전송하게 되는데, 이러한 방법을 이용하여 Animation이 동작하는 동안 JS Thread를 block할 수 있게 되었다.

## Better List Views in React Native

기존의 ListView 에 있던 메모리 이슈나 버그들이 해결된 ListView가 등장했다. Use Case에 따라 FlatList, SectionList, VirtualizedList 등 다양한 ListView를 사용할 수 있게 되었다
VirtualizedList 는 Pull to refresh 나 Scroll loading 등의 기능을 지원하기 때문에  가변적인 데이터를 다루는 데 유용하다. scrollToIndex 와 같은 기능을 사용하면 렌더링 없이 원하는 위치로 이동할 수도 있다.
