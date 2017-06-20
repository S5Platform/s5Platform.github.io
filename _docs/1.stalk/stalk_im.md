---
title: STALK-IM
category: stalk
order: 1
---

## STALK-IM

STALK-IM은 XPush를 활용한 풀스택(FullStack) 오픈소스 메신저 플랫폼이다. STALK-IM를 활용하면 메신저 서비스를 쉽게 구현할 수 있으며, 디자인을 수정하거나 기능을 추가하여 새로운 메신저를 개발할 수 있다. STALK-IM은 메신저 개발에 필요한 유저관리, 데이터 관리, 메시지 전송, 이미지 전송 기능들을 API의 형태로 담당하는 STALK-SERVER와 메신저 화면을 실제로 구현한 STALK-MESSENGER로 구성되어 있다.

###	STALK Messenger Server
[STALK SERVER](https://github.com/S5Platform/stalk-messenger-server)는 메신저 개발에 필요한 사용자 관리, 데이터 관리, 메시지 전송 등의 기능을 제공하는 Node.js 기반의 백엔드 서버 BackEnd Server)이다. npm이나 docker를 이용하여 직접 설치하여 사용할 수 있다. 유저 관리, 데이터 관리 등은 Parse Server를 활용하여 API 형태로 제공하고, XPush를 활용하여 부하분산을 고려한 메시지 전송이 가능하도록 설계되었다. STALK-SERVER에서 제공하고 있는 주요 기능은 아래와 같다.

-	유저 관리 : 회원가입, 로그인, 로그아웃, 프로필 관리
-	친구 관리 : 사용자조회, 친구추가, 친구삭제
-	채널 관리 : 채널조회, 채널삭제, 사용자초대
-	메시지 관리 : 메세지조회, 메시지 전송, 이미지 전송

#### STALK-SERVER 의 설치

```
git clone https://github.com/S5Platform/stalk-messenger-server
npm install
```

#### STALK-SERVER 의 실행

세션서버는 Parse Server 의 클라우드 기능을 활용한 위한 API 서버이다. 
데이터 저장을 위해 Mongo DB 를 활용하기 때문에
실행을 위해서는 [Mongo DB](https://www.mongodb.com/) 가 사전에 설치되어 있어야 한다.

Mongo DB 설치 후, 아래 명령어를 통해 실행할 수 있다.

```
export VERBOSE=1  # logging verbose
./bin/start --session
```

채널서버는 XPush의 메시지 전송 기능을 활용한 채팅 서버이다.
접속 정보를 보관하기 위해 Redis와 Zookeeper를 활용하고 있기 때문에 redis의 설치가 필요하다.

Redis 설치 후, 아래 명령어를 통해 실행할 수 있다.

```
./bin/start --channel
```


### STALK-MESSENGER

STALK-MESSENGER는 STALK-SERVER의 API를 사용하여 React-Native 기반으로 화면을 개발한 오픈소스 메신저이다. 기본으로 제공하는 컴포넌트를 활용하여 비교적 쉽게 화면을 구성하거나 스타일을 변경할 수 있다. React-Native를 활용하면 하나의 소스를 이용하여 Android나 IOS 앱을 제작할 수 있다는 장점이 있다. MIT 라이선스를 사용하며 모든 소스가 공개되어 있기 때문에 그대로 사용하거나, 소스를 수정하여 자체적인 메신저를 쉽게 개발할 수 있다. STALK-MESSENGER에서 구현하고 있는 기능은 아래와 같다.

-	유저관리 : 회원가입, 로그인, 로그아웃, 프로필 수정, 프로필 이미지 등록
-	친구관리 : 사용자조회, 친구추가, 친구삭제
-	채널관리 : 채널조회, 채널삭제, 사용자초대, 채널 이미지 표시
-	메세지관리 : 이전 메시지 조회, 메시지 전송, 이미지 전송, 푸시 알림
