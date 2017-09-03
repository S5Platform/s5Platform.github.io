---
title: STALK SERVER
category: stalk
order: 1
---

###	STALK SERVER
[STALK SERVER](https://github.com/S5Platform/stalk-messenger-server)는 메신저 개발에 필요한 사용자 관리, 데이터 관리, 메시지 전송 등의 기능을 제공하는 Node.js 기반의 백엔드 서버 BackEnd Server)이다. npm이나 docker를 이용하여 직접 설치하여 사용할 수 있다. 유저 관리, 데이터 관리 등은 Parse Server를 활용하여 API 형태로 제공하고, [XPush](https://github.com/xpush/node-xpush)를 활용하여 부하분산을 고려한 메시지 전송이 가능하도록 설계되었다. STALK-SERVER에서 제공하고 있는 주요 기능은 아래와 같다.

-	유저 관리 : 회원가입, 로그인, 로그아웃, 프로필 관리
-	친구 관리 : 사용자조회, 친구추가, 친구삭제
-	채널 관리 : 채널조회, 채널삭제, 사용자초대
-	메시지 관리 : 메세지조회, 메시지 전송, 이미지 전송


![stalk_im](/images/stalk_im.png)

#### STALK SERVER 의 설치

```
git clone https://github.com/S5Platform/stalk-messenger-server
npm install
```

#### STALK-SERVER 의 실행

세션서버는 Parse Server 의 클라우드 기능을 활용한 위한 API 서버이다. 
데이터 저장을 위해 Mongo DB나 PostgreSQL을 활용할 수 있다.
기본적으로는 MongoDB를 활용하도록 되어 있기 때문에
STALK SERVER의 실행을 위해서는 [Mongo DB](https://www.mongodb.com/) 가 사전에 설치되어 있어야 한다.

*mongoDB 실행 시 bindIp 를 0.0.0.0 으로 세팅을 해야 localhost 이외의 다른 IP에서도 접근이 가능하다.*

Mongo DB 설치 후, 아래 명령어를 통해 실행할 수 있다.

```
export VERBOSE=1  # logging verbose
./bin/start --session
```

채널서버는 XPush의 메시지 전송 기능을 활용한 채팅 서버이다.
채널 서버의 정보를 동적으로 관리하기 위해 Redis와 Zookeeper를 활용하고 있기 때문에 redis와 zookeeper의 설치가 필요하다.

Redis와 Zookeeper 설치 후, 아래 명령어를 통해 실행할 수 있다.

```
./bin/start --channel
```

`--config` 옵션을 이용하여 config file을 이용하여 서버를 실행할 수 있다.

config 파일에 포함될 수 있는 주요 설정으로는 아래를 참고한다.

#### STALK SERVER의 환경설정

- zookeeper : 부하분산을 위해 사용할 zookeeper의 주소를 설정한다.
- redis : 캐싱을 위해 사용할 redis의 접속 정보를 설정한다.
- serverName : channelServer가 실행될 때의 서버 네임을 지정한다.
- channelProtocol : 채널 서버가 https를 사용하는 경우 true로 설정한다.
