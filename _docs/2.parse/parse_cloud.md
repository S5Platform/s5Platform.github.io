---
title: Parse Cloud
category: parse
order: 5
---

### Parse Cloud Code

`Parse Cloud`는 Client에서 처리할 수 없는 복잡한 로직을 서버에서 처리할 수 있도록 제공하는 기능이다.
Parse JavaScript SDK를 사용하기 로직을 구현할 수 있기 때문에 비교적 손쉽게 작성할 수 있다. Client의 로직을 Server 쪽에서 사용할 수 있기 때문에, 앱을 업데이트하지 않아도 서버 배포를 통해 로직을 적용할 수 있다는 장점이 있다.


#### Config

Cloud Code 를 구현하기 위해서는 Parse Server를 실행할 때 아래와 같이 cloud 코드가 포함된 파일에 대한 Path 설정을 추가해야 한다.

```
{	
	"app": "AppName",
	"cloud": "./cloud/index.js"
}
```

#### Cloud Functions

Parse Cloude 모듈을 관리할 `index.js` 는 아래와 같이 작성한다. 모듈은 아래에 추가로 작성할 수 있다.

```
require('./hello.js');
.
.
.

```

`define` 을 통해 Function을 구현하면 Parse Client 를 통해 호출할 수 있는 Code 를 작성할 수 있다.

아래는 간단한 `hello` 코드를 구현한 예제이다.

```
Parse.Cloud.define("hello", function(request, response) {
	response.success({'msg':'Hello World'});
});
```

작성된 Cloud Code 는 Parse Client 에서 아래와 같이 호출할 수 있다.

```
Parse.Cloud.run('hello', {}).then(function(result) {
	console.log( result.msg );
});

```

Parse Cloud 함수 내에서는 Parse Client와 동일한 방법으로 데이터에 접근할 수 있다.

Parse Object 에서 자체적으로 제공하지 않는 데이터를 가공해야 할 경우에 유용하다.

아래 코드는 게임이 완료된 점수들으 최대값과 최저값, 총합과 평균을 계산하는 Cloud function 이다. 

```
Parse.Cloud.define("analyseScore", function(request, response) {
  var query = new Parse.Query("GameScore");
  query.equalTo("status", "ended");
  query.find({
    success: function(results) {
      var sum = 0;
      var max = 0;
      var min = 0;

      for (var i = 0; i < results.length; ++i) {
      	var point = results[i].get("point");
        sum += point;

        if( max < point ){
        	max = point;
        }

        if( min > point ){
        	min = point;
        }
      }

      response.success({sum:sum, min:min, max:max, avg: (sum / results.length ) });
    },
    error: function() {
      response.error("tour lookup failed");
    }
  });
});
```