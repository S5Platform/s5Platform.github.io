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

### Saving Object

object에 `set`을 이용하면 프로퍼티를 추가할 수 있으며
`save`를 이용하면 해당 객체를 손 쉽게 저장할 수 있다. 저장에 성공하면 유니크한 `objectId`가 자동으로 생성된다.

```
var Score = Parse.Object.extend("Score");
var score = new Parse.Query(Score);

score.save(null, {
  success: function(score) {
    // 성공한 경우 objectId가 자동으로 생성됨
    console.log(score.id);
  },
  error: function(score, error) {
    //
  }
});
```

### Retrieving Object

`Parse.Query`를 이용하면 원하는 Data에 접근할 수 있다.
`query.get`을 이용하면 해당 `objectId`로 데이터를 조회할 수 있다.

```
var GameScore = Parse.Object.extend("Score");
var query = new Parse.Query(Score);
query.get("xWMyZ4YEGZ", {
  success: function(score) {
   console.log( score );
  },
  error: function(object, error) {
    console.log( object );
  }
});
```

### Updating Objects

object 를 업데이트 하는 방법도 매우 간단하다. 업데이트를 하려고 하는 객체의 objectId를 지정한 후에 업데이트를 하려는 필드에 `set` 을 이용하여 값을 저장한 후 `save`를 하면 된다.

```
var Score = Parse.Object.extend("Score");
var score = new Score();

score.id = "xWMyZ4YEGZ";
score.set( "score", 1337);

score.save(null, {
  success: function(score) {
  },
  error: function(object, error) {
    console.log( object );
  }
});
```

숫자로 되어있는 필드의 경우, `increment`를 사용하먄 증가시킬 수 있다.

```
score.increment("score");
score.save();
```

Array로 되어 있는 필드의 경우 `addUnique`를 사용하면 새로운 필드를 추가할 수 있다.

```
score.addUnique("skills", "flying");
score.addUnique("skills", "kungfu");
score.save();
```

### Destroying Objects

`unset`을 이용하면 파일 내의 필드를 삭제할 수 있다.

```
score.unset("score");
score.save();
```

`destroy`를 이용하면 object 자체를 삭제할 수 있다. destory를 이용할 떄는 query를 이용하여 객체를 선택 후에 삭제해야 정상적으로 동작한다.

```
score.destroy({
  success: function(score) {
    // delete success
    console.log( score );
  },
  error: function(score, error) {
    // delete failed.
  }
});
````

`destroyAll`을 이용하면 여러개의 객체를 삭제할 수 있다.

```
Parse.Object.destroyAll([object1, object2, object3]).then(function(success) {
  // All the objects were deleted
}, function(error) {
  console.error(error.message)
});
```