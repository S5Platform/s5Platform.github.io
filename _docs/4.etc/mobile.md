---
title: Mobile App Development Trends
category: etc
order: 2
---

# Mobile App Development Trends

-----------
## 앞서가는 Swift

Swift가 IOS 앱을 개발하는 언어의 첫번째 주자로 등극하게 되었다. Swift는 Native iOS 앱을 만들기 위한 오픈소스 프로그래밍 언어이다. 자바스크립트와 유사한 syntax를 사용하기 때문에 Object-C에 비하여 사용하기 쉽고, 훌륭한 성능을 보장하기 때문에 널리 사용되고 있다.

[TOIBE Index](https://www.tiobe.com/tiobe-index/)에서도 16위까지 Swift 순위가 올라갔고, Objective-C는 17위까지 떨어져서 상당한 차이가 나고 있다

또한 GitHub에서 사용하는 언어를 봐도 현저히 Swift의 비중이 높다. 많이 사용되는 만큼 많은 정보가 만들어지고 있다.

## React Native 의 강세

Cross Platform을 지원하는 앱을 만드는데 있어, React Native가 해당 분야를 지배하고 있다. React Native가 해당 위치를 지키게 된 주요 특징은 아래와 같다.

- Native Framework를 적용하기 쉬우며 Native에 유사한 성능을 기대할 수 있다.
- React와 Redux에 익숙한 개발자들이 쉽게 개발이 가능하다.
- React Native Bridge를 이용하여 다양한 Third Party 모듈을 사용할 수 있다.

## AR(Augmented Reality Becomes)의 발전

포켓몬 고로 시작된 AR의 가능성이 2017년도에 점점 현실이 되어가고 있다. 2017년 8월 말 Apple과 Google이 AR을 개발하는데 도움을 주는 \개발툴을 각각 공개하면서 가속화되고 있다.

### Apple의 ARKit

Apple은 iOS11을 공개하면서 ARKit 을 공개하였고, 이를 사용한 앱들을 함께 공개하였다. 이케아, 푸드 네트워크, GIPHY World, Arise 등에서 만든 인테리어, 게임, 증강현실 동영상 앱 등이 공개 됐다. ARKit은 A9을 사용하는 아이폰6S 이상에서 작동이 가능하다.

아크잇에 사용된 'World Tracking'이라 말하는 기술은 아이폰과 아이패드를 일종의 동작 감지기로 사용하여 아크잇이 실제 환경에서 몇 가지 포인트를 잡아내고, 그 이후 기기가 움직이더라도 기존의 포인트를 계속 추적해낸다. 이후 가상 물체를 위치에 지정하여 출현시킨 뒤 핸드폰이 한 번 이동했다가 다시 그 자리를 비추면 정확히 그 자리에 물체가 남아있다. 그 외에도 아크잇은 평면을 감지해 잡아낼 수 있다는 특징이 있다.

ARKit이 개발자에게 좋은 점은 바로 하드웨어 걱정을 할 필요 없다는 것, 그리고 실제 사물을 추적하는 방법과 그래픽 처리에 대해 고민할 필요가 없다는 것이다.

### Google의 ARCore

2016년에 등장한 Google 탱고 AR 플랫폼은 소소한 성과를 올리는데에 그쳤다. 탱고 AR 플랫폼을 지원하는 스마트폰이 2개에 불과했기 때문이다. 
이를 개선하여 2017년 8월 경 Google은 ARCore라는 이름의 플랫폼을 발표했다. 이 플랫폼은 탱고 AR 플랫폼과는 달리 부가 하드웨어 없이 동작한다는 장점이 있다. 출시 초기에는 구글 픽셀과 갤럭시S8만 지원했지만, 2017년 10월 중순 갤럭시S8 플러스, 갤럭시노트8로 지원이 확대됐다.

## Cloud Computing과 Serverless Computing

Cloud 기반의 Mobile App의 비율이 점점 증가하였다. Google Drive나 Dropbox 등의 클라우드 컴퓨탕에 기반한 앱들이 많이 등장하고 있다. 이러한 앱들은 데이터를 앱이 직접 가지고 있지 않기 때문에 앱의 사이즈가 비교적 적다.

이와 비슷하게 serverless computing services를 이용한 모바일앱이 등장하고 있다. Serverless computing 또는 Function as a Service (FaaS) 라고 불리우는 서비스를 활용하는 것인데 개별적으로 동작하는 함수를 등록해놓고 해당되는 리퀘스트가 발생 시에 해당 함수를 사용하여 처리를 하는 방식으로 동작한다. 리퀘스트당 비용이 발생하기 때문에 초기 구축비용이 적게 들며 클라우드 서버를 관리하지 않아도 된다는 장점이 있다. 대표적으로 AWS의 Lambda가 있다.