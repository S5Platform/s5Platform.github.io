---
title: Javascript Development Trends
category: etc
order: 3
---

# Javascript Development Trends

-----------

2017년, 개발자들이 사용하는 가장 핫한 언어는 자바스크립트(JavaScript)였다. JavaScript는 개인 개발자가 주도한 오픈소스 라이브러리 프레임워크에 의해 발전되어 왔는데다. 수많은 개발자들이 서로 한번도 만나지 않은채 개발을 진행하기도 했다.

## AngularJS
AngularJS는 Google의 개발문서를 통해 알려지게 되었고, Google이 개발과 마케팅에 참여하면서 성장하게 되었다. 실제로 Google의 전담 인력이 AngularJS의 개발과 마케팅에 참여하고 있다.

초창기 AngularJS는 생산성으로 많은 개발자들의 호응을 얻었다. 반면, Two-way binding과 client rendering 구조로 성능에 문제가 있다라는 지탄을 받아왔다. 이러한 문제점을 개선하고자 2016년에 Angular 2.0이 출시되었는데, 기존 버젼과 호환성이 유지되지 않은채 완전히 새로운 프레임워크로 바뀌게 된 것이다. Angular 2.0 출시로 기존의 이름인 'AngularJS'는 1.x 버전을 지칭하고, 'Angular'는 2.0 이후 버전을 지칭하게 됐다.

Angular는 아래와 같은 릴리즈 정책을 가지고 업데이트를 해왔다. 여기서 중요한 점은 하위 버젼과의 호환성을 지원한다는 것이다.

- 매주 패치 릴리즈
- 각 주요 릴리즈 매월 3 회 마이너 릴리즈
- 마이너 릴리즈가 6 개월마다 변경된다.

2017년 3월 업데이트된 Angular 4.0.0 정식버전의 주요 변경사항은 아래와 같다.

- Angular 4.0.0 은 2.x 버전과 대부분 호환되며 크기가 더 작고 빠르게 되었다. 
- 템플릿 바인딩 구문에서 if / else 구문을 사용할 수 있다.
- 템플릿 바인딩 구문에서 로컬 변수를 할당 할 수 있다.
- TypeScript 2.1 과 2.2 지원하게 되었다.
- 템플릿 중 하나에서 오류가 발생하면 컨텍스트를 제공하는 소스 맵을 생성한다.

## React

React는 Facebook이 참여해 마케팅과 개발을 주도하고 있는 오픈 소스이다. Facebook에 의해 시작되었고 Facebook에 의해 강하게 지원을 받고 있다. Facebook의 전담인력이 참여하여 React를 활용한 개발툴과 Framework(React Native)가 개발하고 있다.

2017년 9월 업데이트된 react 16.0.0 버젼의 주요 변경사항은 아래와 같다.

- New render return types : render 함수로 Array 형태를 리턴할 수 있게 되었다. 기존에는 Array 형태를 return 하기 위해 필요했던 Wrapper Component 가 더이상 필요하지 않게 되었다.

```
render() {
  return [
    <li key="A">First item</li>,
    <li key="B">Second item</li>,
    <li key="C">Third item</li>,
  ];
}
```
- 에러 메시지의 표시가 방식이 사용자가 좀더 이해할 수 있도록 개선되었다.

- custom DOM Attribute 의 사용이 가능해졌다.


```
// React 15 output:
<div />
```

```
// React 16 output:
<div mycustomattribute="something" />
```