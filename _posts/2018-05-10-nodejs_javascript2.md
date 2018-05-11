---
layout: post
title:  "[Node js] Nodejs & javascript"
date:   2018-05-10 16:26:00 +0900
categories: Nodejs
tags: [Nodejs, javascript, 면접]

---

## Nodejs & Javascript 면접 질문 2
---


![node](http://farm5.static.flickr.com/4422/36853132821_4f0185514f_z.jpg)

이번엔 좀 전반적인 부분부터 알아보도록 하자.

**Javascript** 파일을 실행했을 때 어떻게 진행되는지 알아보려고 한다.

 그전에 우리가 URL을 브라우져에 쳐서 어떻게 진행되는지 알아보자.

 ---

### HTML, CSS, Javascript 실행과정

 ---

 [출처 : https://d2.naver.com/helloworld/59361](https://d2.naver.com/helloworld/59361)

브라우저는 일단 `사용자가 선택한 자원을 서버에 요청하고 브라우저에 표시하는 것`을 한다.

사용자가 URL을 입력하고 들어가게 되면 브라우저의 렌더링 엔진이 `요청 받은 내용을 브라우저 화면에 표시하는 일`을 한다.

1. 기본적으로 **HTML** 이라고 생각한다면, HTML문서를 파싱하고 난 후, DOM을 렌더링한다.

**DOM** 은 `Document Object Model`이고, HTML이나 XML 문서의 프로그래밍 Interface이다.

렌더링 과정은 다음과 같다.

    1. HTML을 파싱해 DOM 트리를 구성한다.
    2. 렌더 트리를 구성한다.
    3. 렌더 트리를 레이아웃한다.
    4. 렌더 트리를 그린다.



[출처 : https://code.i-harness.com/ko/q/1b656e](https://code.i-harness.com/ko/q/1b656e)

2. CSS의 경우, 병렬적으로 DOM 렌더링과 같이 렌더링된다.

문서의 Header에서 가능한 한 높게 요청 된 외부 CSS 파일에 모든 CSS 코드를 넣는 것이 좋다.

그렇지 않으면, DOM에서 CSS 요청 위치의 발생까지 렌더링 된 다음 렌더링이 처음부터 다시 시작하게 된다.

3. DOM이 완전히 렌더링되고 페이지의 모든 에셋에 대한 요청이 해결되거나 타임 아웃되면 JavaScript가 onload 이벤트에서 실행된다.

Javascript가 헤더에 선언이 된 경우, 브라우저의 렌더링에 방해가 되므로, 무거울 경우 실행에 오래걸릴 수 있기 때문에 가벼운 것만 Header에 선언하고, DOM구조가 필요한 경우엔 `onLoad`함수 내에서 사용한다.

그러나 Body태그에 선언이 된다면,(일반적으로 쓰는 방법이다) 렌더링 이후에 실행된다.
따라서, 별다른 설정이 필요없다.

---

#### Javascript 실행 과정

---

[출처 : http://multifrontgarden.tistory.com/62?category=471264](http://multifrontgarden.tistory.com/62?category=471264)

javascript는 소스를 한번 `파싱`한 후 한줄씩 런타임으로 진행하게되는데 파싱단계에서 소스가 재정렬이 되게된다.

**파싱** 은 일련의 문자열을 의미있는 토큰(token)으로 분해하고 이들로 이루어진 파스 트리(parse tree)를 만드는 과정이다.

**런타임** 이라 함은, 컴퓨터 프로그램이 실행되고 있는 동안의 동작을 말한다.

이때, 파싱과 런타임은 `실행컨텍스트` 단위로 실행된다.

실행컨텍스트는 지난 블로그를 참고하면 된다.

재정렬 될 때는 두가지가 최상위로 올라가게 된다.

1. var 변수선언
2. 함수선언

단순히 전역 변수로 선언되거나 const, let으로 선언된 변수는 오류가 나오겠지만, 위 두가지는 선언이 위로 올라간다면 출력에 undefined가 뜬다는 것을 알고 있자.
단, 함수를 실행하면 오류가 난다.


---

### HTTP의 통신 과정

---

이제 통신에 대해 알아보자.

HTTP 통신은 어떻게 이루어 질까.

먼저 **HTTP(HyperText Transfer Protocol)** 이란, `HyperText인 HTML을 전송하기 위한 통신 규약`이다.

HTTPs 는 뒤에 Secure을 붙이 보안이 강화된 규약이 된다.

HTTP에서 요청은 4가지 형식이 있는데 다음과 같다.
[출처 : https://joshua1988.github.io/web-development/web-protocols/](https://joshua1988.github.io/web-development/web-protocols/)

1. GET : 문서를 요청. 서버가 클라이언트에 상태 정보와 복제된 문서를 보냄으로써 응답을 함. (조회)
2. HEAD : 상태 정보를 요청. GET 과 동일한 형태로 응답을 하지만, 문서를 복제하지는 않는다.
3. POST : 데이터를 서버로 송신. 서버는 해당 데이터를 특정 아이템에 덧붙인다. (생성)
4. PUT : 데이터를 서버로 송신. 서버가 특정 아이템을 완전히 대체한다. (수정)

여기서 `REST API`와 헤깔릴 수 있다. REST API는 면접시, 자주 물어보는 질문이므로 알아두도록 하자.

먼저 **REST** 는 `Representational State Transfer` 을 말하고, 웹의 장점을 활용하는 네트워크 기반의 아키텍쳐이다.

그리고, 다음과 같은 구성을 가진다.

1. 자원(RESOURCE) - URI
2. 행위(Verb) - HTTP METHOD
3. 표현(Representations)

REST API의 특징은 다음을 참고하자.

[출처 : http://meetup.toast.com/posts/92](http://meetup.toast.com/posts/92)

REST API를 사용할 때는 다음 두가지가 매우 중요하다.

1. URI는 정보의 자원을 표현해야 한다.(동사보다는 명사 사용)
2. 자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE)로 표현한다.

여기서 행위는 HTTP 메서드를 그대로 사용하는데, HTTP 에는 여러가지 메서드가 있지만 REST에서는 CRUD(Create Read Update Delete)에 해당 하는 4가지의 메서드만 사용한다.

참고로, URL 과 URI를 헤깔려할 수 있는데, 다음과 같다.

**URL** 은 `Uniform Resource Locator`

**URI** 는 `Uniform Resource Identifier`

이다.

URI가 더 상위의 개념이다. URL이 `정형화된 리소스 위치표시` 라면, URI는 `정형화된 리소스 식별자` 이다.

하여튼, HTTP 통신을 **브라우저 환경** 을 기준으로 설명하자면, 다음과 같다.

1. 브라우저에 사이트를 입력하면, GET 요청에 의해 서버에서 호출이 된다.
2. DNS에 실제 IP 주소를 조회 한다.
3. 서버에 도착한 후, 요청과정을 수행하고, 응답한다.
4. 클라이언트에 도착하여 뷰에 보인다.

이 것을 좀더 세부적으로 통신과정을 보도록 하자.

HTTP 통신 과정은 **TCP 계층** 에 대한 설명이 필요하다.

`3-Way HandShaking`을 통해, TCP/IP프로토콜을 이용해서 통신을 하는 응용프로그램이 데이터를 전송하기 전에 먼저 정확한 전송을 보장하기 위해 상대방 컴퓨터와 사전에 세션을 수립한다.

그 과정은 다음과 같다.

[출처 : http://mindnet.tistory.com/entry/네트워크-쉽게-이해하기-22편-TCP-3-WayHandshake-4-WayHandshake](http://mindnet.tistory.com/entry/네트워크-쉽게-이해하기-22편-TCP-3-WayHandshake-4-WayHandshake)

![3-Way Handshaking](http://cfile9.uf.tistory.com/image/225A964D52F1BB69177202)

1. Client > Server : TCP SYN

A클라이언트는 B서버에 접속을 요청하는 SYN 패킷을 보낸다. 이때 A클라이언트는 SYN 을 보내고 SYN/ACK 응답을 기다리는 SYN_SENT 상태가 되는 것이다.

2. Server > Client : TCP SYN/ACK

B서버는 SYN요청을 받고 A클라이언트에게 요청을 수락한다는 ACK 와 SYN flag 가 설정된 패킷을 발송하고 A가 다시 ACK으로 응답하기를 기다린다. 이때 B서버는 SYN_RECEIVED 상태가 된다.

3. Client > Server : TCP ACK

A클라이언트는 B서버에게 ACK을 보내고 이후로부터는 연결이 이루어지고 데이터가 오가게 되는것이다. 이때의 B서버 상태가 ESTABLISHED 이다.

**SYN** 은 `synchronize sequence numbers`을 말하고, **ACK** 는 `Acknowlegement`를 말한다.

이 후 통신이 끝난다음 마무리 될 때는 `4-Way Handshaking`과정을 거친다.

이는 다음과 같다.

![4-Way Handshaking](http://cfile21.uf.tistory.com/image/2678E035537EEE9126A109)

[출처 : http://hyeonstorage.tistory.com/287](http://hyeonstorage.tistory.com/287)

최초에는 서로 통신 상태이기 때문에 양쪽이 ESTABLISHED 상태이다.

1. 통신을 종료하고자 하는 Client가 서버에게 FIN 패킷을 보내고 자신은 FIN_WAIT_1 상태로 대기한다.
2. FIN 패킷을 받은 서버는 해당 포트를 CLOSE_WAIT으로 바꾸고 잘 받았다는 ACK 를 Client에게 전하고 ACK를 받은 Client는 상태를 FIN_WAIT_2로 변경한다.
그와 동시에 Server에서는 해당 포트에 연결되어 있는 Application에게 Close()를 요청한다.
3. Close() 요청을 받은 Application은 종료 프로세스를 진행시켜 최종적으로 close()가 되고 server는 FIN 패킷을 Client에게 전송 후 자신은 LAST_ACK 로 상태를 바꾼다.
4. FIN_WAIT_2 에서 Server가 연결을 종료했다는 신호를 기다리다가 FIN 을 받으면 받았다는 ACK를 Server에 전송하고 자신은 TIME_WAIT 으로 상태를 바꾼다. (TIME_WAIT 에서 일정 시간이 지나면 CLOSED 되게 된다.)

최종 ACK를 받은 서버는 자신의 포트도 CLOSED로 닫게 된다.

이 부분 역시 면접에 자주 나오니 꼭 알아두도록 하자.

다음 포스팅은 Nodejs 에 대해 좀더 잘 알아보는 과정을 가지도록 하자.
