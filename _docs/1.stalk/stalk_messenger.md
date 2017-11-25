---
title: STALK MESSENGER
category: stalk
order: 2
---

### STALK MESSENGER

STALK-MESSENGER는 STALK-SERVER의 API를 사용하여 React Native 기반으로 화면을 개발한 오픈소스 메신저이다. 기본으로 제공하는 컴포넌트를 활용하여 비교적 쉽게 화면을 구성하거나 스타일을 변경할 수 있다. React Native를 활용했기 때문에 하나의 소스를 이용하여 Android나 IOS 앱을 제작할 수 있다는 장점이 있다. MIT 라이선스를 사용하며 모든 소스가 공개되어 있기 때문에 그대로 사용하거나, 소스를 수정하여 자체적인 메신저를 쉽게 개발할 수 있다. STALK MESSENGER에서 구현하고 있는 기능은 아래와 같다.

-	유저관리 : 회원가입, 로그인, 로그아웃, 프로필 수정, 프로필 이미지 등록
-	친구관리 : 사용자조회, 친구추가, 친구삭제
-	채널관리 : 채널조회, 채널삭제, 사용자초대, 채널 이미지 표시
-	메세지관리 : 이전 메시지 조회, 메시지 전송, 이미지 전송, 푸시 알림

## STALK MESSENGER의 설치와 실행

```
git clone https://github.com/S5Platform/stalk-messenger
cd stalk-messenger
npm install
```

ios에서 실행하기 위해서는 ios 기반의 시뮬레이터가 설치되어 있어야한다.

```
// ios에서 실행하기
react-native run-ios
```

android에서 실행하기 위해서는 android emulator가 설치되어 있어야한다.

```
// android에서 실행하기
react-native run-android
```

![stalk_im](/images/stalk_im.png)

#### STALK MESSENGER의 환경설정

STALK MESSENGER는 [env.js](https://github.com/S5Platform/stalk-messenger/blob/master/env.js)를 이용하여 환경설정 을 할수 있다.

`SERVER_URL`은 Stalk Sever와의 통신을 위한 URL 이기 때문에 정확한 URL을 입력해야 한다.

아래는 환경 설정 파일의 예시이다.

```
APP_NAME: 'STALK',
APP_ID: 'STALK',
SERVER_URL: 'http://127.0.0.1:8080',
TEST_MODE: true,
VERSION: 1,
APP_IDENTIFIER_IOS: 'io.stalk.s5messenger',
APP_IDENTIFIER_ANDROID: 'io.stalk.s5messenger',
ANDROID_GCM_SENDER_ID: 'xxxxxxxxxx'
```

STALK MESSENGER는 메시지를 발송하기 위해 socket io를 사용하고 있다. View에서 socket io를 아래와 같이 연결하면 채팅방에 속해있는 사용자들과 메시지를 주고 받을 Socket을 생성할 수 있게 된다.

```
var node = {
  url : 'http://127.0.0.1:8180',
  app: 'STALK' // 현재 사용중인 app의 이름,
  name: '10' //할당받은 server의 이름,
  channelId: '24b53f' //채팅을 위해 생성한 채널의 id
  currentUserId : this.props.user.id // 현재 로그인 한 사람의 id
}

this.socket = new SocketIO(node.url, {
  nsp: '/channel',
  forceWebsockets: true,
  forceNew: true,
  connectParams: {
    A: node.app,
    S: node.name,
    C: channelId,
    U: currentUserId
  }
});
```
