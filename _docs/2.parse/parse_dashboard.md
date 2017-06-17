---
title: Parse Dashboard
category: parse
order: 2
---

## Parse Dashboard

Parse Server를 사용할때, [Parse Dashboard](https://github.com/parse-community/parse-dashboard) 를 이용하면 어플리케이션을 효율적으로 관리할 수 있다. Parse Dashboard는 오픈소스 기반의 nodejs 어플리케이션이다. 아래 명령어를 이용하여 쉽게 설치가 가능하다.

```
git clone git@github.com:ParsePlatform/parse-dashboard.git
cd parse-dashboard
npm install

```

설치가 완료된 후에는 `parse-dashboard-config.json` 파일 내용을 수정하면 된다.

```
{
  "apps": [
    {
      "serverURL": "http://localhost:1337/parse",
      "appId": "myAppId",
      "masterKey": "myMasterKey",
      "appName": "MyApp"
    }
  ]
}
```

아래 명령어를 사용하여 실행이 가능하다.

```
npm run dashboard 
```

실행이 완료되면 , `http://localhost:4000` 를 이용하여 접근할 수 있다.