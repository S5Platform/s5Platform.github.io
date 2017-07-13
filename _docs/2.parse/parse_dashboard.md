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

실행이 완료되면, `http://localhost:4000` 를 이용하여 접근할 수 있다.

Parse Dashboard 에서는 Parse Server내의 Class와 Object 목록을 확인할 수 있으며, Object 를 수정하거나 삭제할 수 있다. 또한 Push 발송을 했던 이력을 확인할 수도 있으며, Push를 직접 발송할 수도 있다.