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
- filesAdapter : 업로드되는 파일을 저장하기 위한 어탭터 설정
- push : push notification 설정을 한다.
```
parse-server --appId APPLICATION_ID --masterKey MASTER_KEY --databaseURI mongodb://localhost/test
```

> 이때, MongoDB를 사용하지 않는 경우에는 파일 저장을 위해 filesAdapter 설정을 반드시 추가해야한다.

#### FileAdapter의 종류로는 아래와 같은 것들이 있다.

- GridStoreAdapter : MongoDB의 GridFS를 사용하는 것으로 databaseURI 로 MongoDB를 이용할 경우 default로 사용된다.
- S3Adapter : Amazon S3를 이용하여 파일을 저장할 경우 설정한다.
- GCSAdapter : Google Cloud Storage를 이용하여 파일을 저장할 경우 설정한다.


### S3Adapter의 설정

S3Adapter를 사용하기 위해서는 [S3Adapter](https://github.com/parse-server-modules/parse-server-s3-adapter)모듈을 추가로 설치해야 한다.

설치가 완료되면 아래와 같이 *S3_ACCESS_KEY* 와 *S3_SECRET_KEY*를 환경변수로 추가해주어야 한다.

```
export S3_ACCESS_KEY=YOUR_S3_ACCESS_KEY
export S3_SECRET_KEY=YOUR_S3_SCREET_JEY
```

parse server를 실행할때 config는 아래와 같다.

```
  "filesAdapter": {
    "module": "parse-server-s3-adapter",
    "options": {
      "bucket": "my_bucket",
      // optional:
      "region": 'us-east-1', // default value
      "bucketPrefix": '', //
      "directAccess": false, // default value
      "baseUrl": null, // default value
      "baseUrlDirect": false, // default value
      "signatureVersion": 'v4', // default value
      "globalCacheControl": null, // default value. Or 'public, max-age=86400' for 24 hrs Cache-Control
      "ServerSideEncryption": 'AES256|aws:kms' //AES256 or aws:kms, or if you do not pass this, encryption won't be done
    }
  }
```

- bucket : s3에 설정한 bucket 명
- region : s3에 설정된 region 명
- directAccess : s3의 url에 직접 접속할때 사용한다. 해당 설정이 true면 s3 URL을 이용해서 직접 접속하게 된다.
- bucketPrefix : 업로드 할때 사용되는 default 폴더
- baseUrl : 업로드 완료 후 결과가 되는 url

### Email Adapter의 설정

Parse Server에서는 `email 인증`과 `패스워드 초기화` 등의 메일링 기능을 제공하고 있다. 해당 기능을 사용하기 위해서는 
parse server의 옵션 중에 *verifyUserEmails* 설정과 *emailAdapter* 설정이 되어 있어야 한다.

사용할 수 있는 email adapter의 종류로는 아래와 같은 것들이 있다.

- [parse-server-postmark-adapter](https://www.npmjs.com/package/parse-server-postmark-adapter)
- [parse-server-sendgrid-adapter](https://www.npmjs.com/package/parse-server-sendgrid-adapter)
- [parse-server-mandrill-adapter](https://www.npmjs.com/package/parse-server-mandrill-adapter)
- [parse-server-simple-ses-adapter](https://www.npmjs.com/package/parse-server-simple-ses-adapter)
- [parse-server-mailgun-adapter-template](https://www.npmjs.com/package/parse-server-mailgun-adapter-template)
- [parse-server-mailjet-adapter](https://www.npmjs.com/package/parse-server-mailjet-adapter)
- [simple-parse-smtp-adapter](https://www.npmjs.com/package/simple-parse-smtp-adapter)


```
"emailAdapter": {
  "module": "parse-server-mailgun-adapter-template",
  "options": {
    "displayName": "YourAppName",
    "fromAddress": "no-reply@yourdomain.com",
    "domain": "yourdomain.com",
    "apiKey": "mail-gun-api-key"
  }
}
```

### PushAdapter 설정

Parse Server를 이용하면 GCM(Google Cloud Messaging)과 APNS(Apple Push Notification Service)를 이용하여 Push Notification 메시지를 발송할 수 있다.

Android 와 ios 일 경우, 각각 발송을 위한 key 값을 설정해주어야 한다.


Android의 경우 google console 에서 GCM 사용 설정 시에 생성되는 senderId와 apiKey를 입력해준다.
```
// android senderId와 apiKey 설정 ( server 용 )
android: {
  senderId: '...',
  apiKey: '...'
}
```

ios의 경우 Apple Push Services를 위한 인증서를 생성한 후에 저장한 인증서의 위치와, 생성시 설정한 `passphrase`, Push를 받을 app의 bundleId를 입력해주면 된다. 인증서의 type에 따라 `production`을 true or false로 설정하면 된다. production 일 경우 실제 운영환경의 APNS를 사용하게 된다.

```
ios: {
  pfx: '/file/path/to/XXX.p12',
  passphrase: '', // optional password to your p12/PFX
  topic: '',
  production: false
}
```

### Parse Server의 활용

Parser Server는 `Express`에 마운트가 가능하다.

아래 코드와 같이 ParseServer를 생성하면 생성된 객체를 express에 인자로 넘겨서 Express에서 Parse Server의 API를 추가할 수 있다.

```
var app = express();

var api = new ParseServer({
  databaseURI: 'mongodb://your.mongo.uri',
  cloud: './cloud/main.js',
  appId: 'myAppId',
  fileKey: 'myFileKey',
  masterKey: 'mySecretMasterKey',
  push: { ... }, // 위 PushAdapter 설정 참고
  filesAdapter: ...,
});

app.use( '/parse', api);
```