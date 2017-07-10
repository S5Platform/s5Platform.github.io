---
title: Parse Server
category: parse
order: 1
---


### Parse, as Backend Service

Parse는 모바일 앱을 쉽게 만들 수 있게 도움을 주는 클라우드 기반의 백엔드 플랫폼 서비스(Backend as a service)로 2011년 등장했다. 모바일앱을 만들기 위해 반복적으로 사용되는 기능들을 API로 제공하기 때문에, 모바일앱을 만드는 개발자가 최대한 앱에 집중할 수 있도록 하는 도움을 준다. 푸시 알림, 소셜 통합, 데이터 보관, 클라우드 보관 등의 기능을 제공하고 있다. 2013년 Facebook에 인수되면서 안정성에 대한 신뢰가 커졌고, 상당한 수준의 서비스를 거의 무료로 사용할 수 있다는 점에서 큰 호응을 얻었다. 2014년의 Facebook의 발표에 의하면 전세계에서 약 50만개 이상의 앱이 Parse를 사용하고 있다고 조사되었다.  Parse 서비스의 무료 사용 조건은 아래와 같은데, 초기 스타트업이 클라우드 서비스 비용에 대한 부담없이 사용할 수 있는 수준이었다.

- 1초당 30번의 request 가 무료
- 20 GB 의 파일 저장 용량
- 20 GB 의 DB 용량
- 2 TB 의 파일 전송량


### Parse Service 의 종료와 오픈소스화

Facebook은 2016년 1월 Parse 서비스를 1년 내에 서비스를 종료한다고 발표했다. 그 이후 더 이상 회원가입을 받지 않고 있으며, 이미 사용중인 회원들에 한해 1년간 서비스를 이전할 수 있는 기간을 부여했다. 이와 동시에 Parse에서 사용할 수 있었던 주요 기능들을 직접 설치해서 사용할 수 있도록 Parse Server 라는 이름의 오픈소스를 공개했다. 공개된 Parse Server와 MongoDB를 자체적으로 설치하고, Parse에서 제공한 데이터 이관툴을 이용하면 기존의 Parse 서비스와 비슷하게 운영을 할 수 있다.

[Parse Server](https://github.com/parse-community/parse-server)

### Parse Server 의 설치와 실행

Parse Server를 설치하기 위해서는 아래 명령어를 활용하여 쉽게 설치할 수 있다.

```
npm install -g parse-server
```

Parse Server 에서 제공하는 DB 종류로는 MongoDB와 PostgreSQL이 있다. 둘 증 하나를 설치한 후에 Parse Server를 아래와 같이 시작할 수 있다.

- appId : 고유의 키
- masterKey :고유의 키
- databaseURI : 사용하려는 DB의 접속정보
- filesAdapter : 업로드되는 파일을 저장하기 위한 어탭터 설정으로 S3Adapter 등이 있다.
- push : push notification 설정을 한다.

```
parse-server --appId APPLICATION_ID --masterKey MASTER_KEY --databaseURI mongodb://localhost/test
```

> 이때, MongoDB를 사용하지 않는 경우에는 파일 저장을 위해 filesAdapter 설정을 반드시 추가해야한다.

### Parse Server의 활용

Parser Server는 `Express`에 마운트가 가능하다.

아래 코드와 같이 ParseServer를 생성하면 Express에서 Parse Server의 API를 추가할 수 있다.

```
var app = express();

var api = new ParseServer({
  databaseURI: 'mongodb://your.mongo.uri',
  cloud: './cloud/main.js',
  appId: 'myAppId',
  fileKey: 'myFileKey',
  masterKey: 'mySecretMasterKey',
  push: { ... }, // See the Push wiki page
  filesAdapter: ...,
});

app.use( '/parse', api);
```