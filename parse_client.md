### Parse Client

Parse JavaScript SDK를 사용하면 Parse Server 안의 데이터에 쉽게 접근할 수 있다.
아래 문서를 확인하면, [Parse JS Client](http://docs.parseplatform.org/js/guide/) 보다 자세한 내용을 확인 할 수 있으며, JavaScript SDK의 주요 사용법은 아래와 같다.

### 초기화

브라우져 환경에서 사용할 경우에는 아래와 같이 사용할 수 있다.

```
var Parse = require('parse');
```

Nodejs 환경에서 사용할 경우는 아래와 같이 사용할 수 있다.

```
var Parse = require('parse/node');
```

React Native 환경에서 사용할 경우는 아래와 같이 사용할 수 있다.

```
var Parse = require('parse/react-native');
```

아래와 같이 초기화하여 사용할 수 있다.

```
Parse.initialize("YOUR_APP_ID");
Parse.serverURL = 'http://YOUR_PARSE_SERVER:1337/parse'
```