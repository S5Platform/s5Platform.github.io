---
title: Parse Query
category: parse
order: 4
---

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

해당 필드가 `ref` 유형인 경우에는 찾으려 id로 새로운 객체를 생성하여 쿼리에 추가하는 방법으로 가능하다.

```
var player = Parse.Object.extend("Player");
player.id = 'aB15Tx';

query.equalTo("player", player );
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

    // results 는 array 형태
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

`ascending`과 `descending`을 사용하면 해당 필드로 정렬하여 검색할 수 있다.

```
// score 필드를 오름차순으로 정렬 
query.ascending("score");

// score 필드를 내림차순으로 정렬
query.descending("score");
```

`less`와 `greater`를 사용하면 숫자나 날짜 등 비교가 가능한 필드에 대한 조건 검색이 가능하다. 

```
// wins < 50
query.lessThan("wins", 50);

// wins <= 50
query.lessThanOrEqualTo("wins", 50);

// wins > 50
query.greaterThan("wins", 50);

// wins >= 50
query.greaterThanOrEqualTo("wins", 50);
```

`containedIn` 을 이용하면 주어진 조건에 포함되는 필드에 대한 조건 검색이 가능하다.
SQL에서 흔히 사용하는 in 절과 비슷하다고 볼수 있다.

```
// James 또는 John 이라는 이름을 가진 객체를 찾기
query.containedIn("name", ["James", "John"]);
```

`notContainedIn`을 이용하면 주어진 조건에 포함되지 않는 필드에 대한 조건 검색이 가능하다.

```
// James, John 둘 다 아닌 이름을 가진 객체를 찾기
query.notContainedIn("name", ["James", "Elly"]);
```

여러가지 조건을 동시에 사용해야 하는 경우 Compound Query를 이용해서 해결할 수 있다.

80점이상인 Player와 20점 이하인 Player를 함께 검색하려면 아래와 같이 할수 있다.

```
var ranked = new Parse.Query("Player");
ranked.greaterThan("score", 80);

var disqualifies = new Parse.Query("Player");
disqualifies.lessThan("score", 20);

var mainQuery = Parse.Query.or(ranked, disqualifies);
mainQuery.find({
  success: function(results) {
    // ranked, disqualifies
  },
  error: function(error) {
    // There was an error.
  }
});
```
