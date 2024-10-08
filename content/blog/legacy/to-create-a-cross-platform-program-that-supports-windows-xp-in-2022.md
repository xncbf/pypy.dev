---
title: 2022년에 windows xp 를 지원하는 크로스 플랫폼 프로그램 개발기
date: 2022-04-24 21:04:54
category: legacy
thumbnail: { thumbnailSrc }
draft: false
---


- [개요](#개요)
- [우리의 상황에 맞는 대처](#우리의-상황에-맞는-대처)
  - [electron](#electron)
  - [nw.js](#nwjs)
- [브라우저를 품은 프레임워크](#브라우저를-품은-프레임워크)
- [자동 업데이터](#자동-업데이터)
- [결론](#결론)

## 개요

우리는 매장에서 사용되는 POS 용 프로그램을 제작했다.

항상 그랬지만 우리는 스타트업에서 처음 시장의 반응을 확인하기 위해 빠르게 만들 필요가 있었다.

요구사항은 간단했다.

- windows xp 부터 windows 10 까지 모든 운영체제를 지원할 것.
- 시리얼 포트를 통해 영수증 출력이 가능할 것.
- 새로운 기능이 출시되면 각 영업점에서 알아서 업데이트가 가능하도록 할 것.

## 우리의 상황에 맞는 대처

요구사항을 충족하면서 가장 잘 만드는 방법은 각 OS 버전별로 네이티브 앱을 만드는 것이었다.

하지만 알다시피 처음부터 완벽하게 만들 수는 없었다. 항상 그랬듯이 인원이 부족하고 시간이 부족했다.

가장 효율적으로 빠르게 만들기 위해 windows xp 를 지원하는 크로스플랫폼 데스크톱 프레임워크를 찾기 시작했다.

### electron

처음 확인했던 것은 요즘 핫한 크로스 플랫폼 프레임워크 `electron` 이었다.

하지만 windows xp 를 지원하지 않아서 패스...

### nw.js

그 다음 찾았던것은 electron 과 비슷한 경쟁자 `nw.js` (node-webkit) 였다.

최근 버전은 windows xp 를 지원하지 않았지만 과거 버전 0.14.7 버전에서 windows xp 를 마지막으로 지원하는것을 확인했다!

## 브라우저를 품은 프레임워크

`nw.js` 가 크로스 플랫폼을 지원할 수 있는건 크로미움을 내장하고 있기 때문이다.

크로미움을 내장하고 있기 때문에 html, js 로 코드 작성이 가능하다. 웹사이트를 만드는것처럼 만들고나면 데스크탑 앱이 만들어지는 방식이다.

하지만 그렇기 때문에 발생하는 단점도 있는데, windows xp 를 지원하는 nw.js 0.14.7 버전은 크로미움 50이 탑재되어있어서 요즘 많이 사용되는 es6 이상 문법은 사용이 불가능한 문제가 있었다.

그리고 크로미움은 기본적으로 메모리를 많이 잡아먹기 때문에 기본적으로 저사양 컴퓨터가 대부분인 POS 에서는 버벅이는 모습을 자주 볼 수 있었다.

## 자동 업데이터

다행히 누군가 구현해놓은 구현체가 있었다. `node-webkit-updater` 를 통해 package.json 버전을 읽어와서 새로운 버전이 존재할 시 자동으로 업데이트 하도록 만들었다.

## 결론

결국 요구사항을 충족하는 크로스 플랫폼 데스크탑 앱을 만들수 있었다.

장점은 웹 사이트로도 쉽게 띄울 수 있고 필요하면 영수증 출력을 제외하고 똑같이 사용이 가능했다. (최신 브라우저에서는 영수증 출력도 가능하다.) 내가 개발하는 맥북에서도 쉽게 디버깅이 가능했다.

오랜만에 레거시 환경에서 개발을 하게 되었는데 내가 겪은 상황처럼 항상 최신 기술만 사용해서 개발할 수 없는 상황이 올 수도 있다.

나도 한때 어느 프로그램이 옛날 버전을 왜 이렇게 계속 지원해 주는 걸까 생각해 본 적도 있지만 개발과 전혀 관계가 없는 업계에서는 10년전 컴퓨터를 사용하고 있을 수도 있다.

그리고 그 컴퓨터로 windows xp 를 사용하면서 `다른 프로그램들은 잘 되던데 이건 왜 안돼요?` 를 시전할 수도 있다.

레거시를 오래 지원해주는 오픈소스를 감사하게 생각하자.
