## Parse Query

`Parse Query`를 이용하면 보다 정교하게 원하는 데이터를 검색할 수 있다.

쿼리는 아래와 같이 생성할 수 있다.

```
var Score = Parse.Object.extend("Score");
var query = new Parse.Query(Score);
```


### Query Constraints

`equalTo` 를 사용하면 해당 필드의 값이 일치하는 객체를 검색할 수 있다.

```
query.equalTo("playerName", "James");
```

`notEqualTo` 를 사용하면 해당 필드의 값이 일치하지 않는 객체를 검색할 수 있다.

```
query.notEqualTo("playerName", "James");

```

`greaterThan` 를 사용하면 해당 필드의 값보다 큰 객체를 검색할 수 있다.

````
query.greaterThan("score", 100);
```

여러 조건들을 설정한 후 `find`를 호출하면 선택한 결과와 일치하는 객체들을 검색할 수 있다.

```
query.find({
  success: function(results) {

    // results 는 array gㅕㅇ태
    for (var i = 0; i < results.length; i++) {
      var object = results[i];
      console.log(object.id + ' - ' + object.get('playerName'));
    }
  },
  error: function(error) {
    console.log("Error: " + error.code + " " + error.message);
  }
});
````