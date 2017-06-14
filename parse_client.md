## Parse Client

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

## Parse Users

`Parse.User`라는 이름의 특별한 클래스를 사용하면 유저관리를 쉽게 사용할 수 있다.
`Parse.Object`를 확장한 클래스이기 때문에 Parse.Object의 모든 기능을 지원하고 있으며, 특별한 3개의 필드가 추가되어 있다.

- username: The username for the user (required).
- password: The password for the user (required on signup).
- email: The email address for the user (optional).

### Signing Up
신규유저를 생성하기 위해서는 `signUp`을 사용하면 된다.
신규 유저생성 시에 username과 password는 필수값이므로 반드시 입력해주어야 하는데, username은 동일한 APP내에 유니크해야 한다.
`set`을 이용하여 다른 정보를 추가할수 있다. 

```
var user = new Parse.User();
user.set("username", "james");
user.set("password", "james1234");
user.set("email", "james@google.com");

```
// 다른 정보 추가
user.set("age", "42");
user.set("gender", "male")

user.signUp(null, {
  success: function(user) {
    console.log( user.id )
  },
  error: function(user, error) {
    // 가입 실패시 로그를 확인
    console.log( error );
  }
});
```

### Logging In
생성된 유저를 이용해서 로그인하기 위해서는 `logIn`을 사용하면 된다.

```
Parse.User.logIn("james", "james1234", {
  success: function(user) {
    // 로그인 성공시 이벤트를 수행한다.
  },
  error: function(user, error) {
    // 로그인 실패시, 로그를 확인
  }
});
```

### Current User
로그인된 현재 사용자의 정보를 가져오려고 할때는 `current()`를 사용하면 된다.

```
var currentUser = Parse.User.current();
```

### Resetting Passwords

Parse Server 에는 Password 초기화 기능이 내장되어 있다. 이메일 주소를 인자로 이용하여 `requestPasswordReset` 함수를 호출하면 아래 순서에 의거하여 패스워드를 초기화할수 있는 기능을 제공한다.

*이때 Parse Server 에 이메일 발송을 위한 설정이 완료되어 있어야한다.*

- 전달받은 이메일 주소를 이용하여 임시 Password로 변경한다. 
- 전달받은 이메일 주소로 패스워드를 초기화할 수 있는 링크를 포함한 이메일을 전송한다.
- 해당 링크를 클릭하면 패스워드를 초기화할 수 있는 화면이 열린다.
- 사용자가 신규 패스워드를 입력하면 패스워드를 변경할 수 있다.

```
Parse.User.requestPasswordReset("email@example.com", {
  success: function() {
  // Password reset request was sent successfully
  },
  error: function(error) {
    // Show the error message somewhere
    alert("Error: " + error.code + " " + error.message);
  }
});
```

### Quering User

원하는 유저를 검색할때는 query를 사용하면 된다. 유저 패스워드 등의 중요 정보가 자동으로 제거된 상태로 결과를 받을 수 있다.

```
var query = new Parse.Query(Parse.User);
query.equalTo("gender", "male");
query.find({
  success: function(men) {
    // 
  }
});
```

## Files

### Creating a Parse.File
`Parse.File` 를 이용하면 쉽게 파일 객체를 생성할 수 있다. base64를 사용하는 방법과 byte Array를 사용하는 방법이 있다.
첫번째 인자로를 파일이름을 주도록 되어 있는데,
파일 업로드시에 유니크한 식별자를 생성하기 때문에 파일 이름이 충돌날 것에 대한 고려를 할 필요는 없다.

파일이름을 세팅할 때는, 확장자를 함께 주는 것이 업로드 완료된 파일에 접근하기 용이하다.

```
var base64 = "V29ya2luZyBhdCBQYXJzZSBpcyBncmVhdCE=";
var parseFile = new Parse.File("profile.png", { base64: base64 }); 
```

```
var bytes = [ 0xBE, 0xEF, 0xCA, 0xFE ];
var parseFile = new Parse.File("profile.png", bytes);
```

생성한 파일객체를 save 하면 파일을 저장할 수 있다.
Parse Server의 DB로 MongoDB를 사용하고 있다면, GridFS에 저장이 되며,
PostgreSQL을 사용하고 있다면, Amazon S3 등의 별도 파일저장소를 사용해야 저장이 가능하다.

```
parseFile.save().then(function() {
  // The file has been saved to Parse.
}, function(error) {
  // The file either could not be read, or could not be saved to Parse.
});
```

파일 객체를 `Parse.Object`에 추가하면 해당 객체를 save할 경우 자동으로 파일이 업로드되면서 파일 객체가 생성된다.

```
var score = Parse.Object.extend("Score");
score.set("score", 10);
score.set("dataFile", parseFile);
score.save();
```

### Retrieving File Contents

생성된 파일 객체는 `url` 함수를 사용하면 컨텐츠를 가져올 수 있다.
이미지 형태의 파일인 경우 아래와 같이 src에 세팅하면 이미지를 바로 표시할 수 있다.

```html
<img id="profileImg" src="" />
```

```javascript
var imageUrl = profilePhoto.url();
$("profileImg")[0].src = imageUrl;
```
