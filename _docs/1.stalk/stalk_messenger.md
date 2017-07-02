---
title: STALK MESSENGER
category: stalk
order: 2
---

### STALK MESSENGER

STALK-MESSENGER는 STALK-SERVER의 API를 사용하여 React Native 기반으로 화면을 개발한 오픈소스 메신저이다. 기본으로 제공하는 컴포넌트를 활용하여 비교적 쉽게 화면을 구성하거나 스타일을 변경할 수 있다. React Native를 활용했기 때문에 하나의 소스를 이용하여 Android나 IOS 앱을 제작할 수 있다는 장점이 있다. MIT 라이선스를 사용하며 모든 소스가 공개되어 있기 때문에 그대로 사용하거나, 소스를 수정하여 자체적인 메신저를 쉽게 개발할 수 있다. STALK MESSENGER에서 구현하고 있는 기능은 아래와 같다.

-	유저관리 : 회원가입, 로그인, 로그아웃, 프로필 수정, 프로필 이미지 등록
-	친구관리 : 사용자조회, 친구추가, 친구삭제
-	채널관리 : 채널조회, 채널삭제, 사용자초대, 채널 이미지 표시
-	메세지관리 : 이전 메시지 조회, 메시지 전송, 이미지 전송, 푸시 알림

## STALK-MESSENGER의 설치와 실행

```
git clone https://github.com/S5Platform/stalk-messenger
cd stalk-messenger
npm install
```


```
// ios에서 실행하기
react-native run-os
```