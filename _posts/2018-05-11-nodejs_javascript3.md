---
layout: post
title:  "[Node js] Nodejs & javascript"
date:   2018-05-10 16:26:00 +0900
categories: Nodejs
tags: [Nodejs, javascript, 면접]

---

## Nodejs & Javascript 면접 질문 3
---


![node](http://farm5.static.flickr.com/4006/4492637329_1b127bdff5_z.jpg)

이번엔 앞서 쌓은 javascript와 기타 지식들을 가지고, Node js에 적용해 보려고 한다.

먼저 Node js가 무엇인지 알아보도록 하자.

---

### Node js 란?

---

`Node.js®는 Chrome V8 JavaScript 엔진으로 빌드된 JavaScript 런타임입니다. Node.js는 이벤트 기반, 논 블로킹 I/O 모델을 사용해 가볍고 효율적입니다. Node.js의 패키지 생태계인 npm은 세계에서 가장 큰 오픈 소스 라이브러리 생태계이기도 합니다`

[출처 : https://engineering.huiseoul.com/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EB%8A%94-%EC%96%B4%EB%96%BB%EA%B2%8C-%EC%9E%91%EB%8F%99%ED%95%98%EB%8A%94%EA%B0%80-v8-%EC%97%94%EC%A7%84%EC%9D%98-%EB%82%B4%EB%B6%80-%EC%B5%9C%EC%A0%81%ED%99%94%EB%90%9C-%EC%BD%94%EB%93%9C%EB%A5%BC-%EC%9E%91%EC%84%B1%EC%9D%84-%EC%9C%84%ED%95%9C-%EB%8B%A4%EC%84%AF-%EA%B0%80%EC%A7%80-%ED%8C%81-6c6f9832c1d9](https://engineering.huiseoul.com/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EB%8A%94-%EC%96%B4%EB%96%BB%EA%B2%8C-%EC%9E%91%EB%8F%99%ED%95%98%EB%8A%94%EA%B0%80-v8-%EC%97%94%EC%A7%84%EC%9D%98-%EB%82%B4%EB%B6%80-%EC%B5%9C%EC%A0%81%ED%99%94%EB%90%9C-%EC%BD%94%EB%93%9C%EB%A5%BC-%EC%9E%91%EC%84%B1%EC%9D%84-%EC%9C%84%ED%95%9C-%EB%8B%A4%EC%84%AF-%EA%B0%80%EC%A7%80-%ED%8C%81-6c6f9832c1d9)

먼저 **Javascript 엔진** 은 자바스크립트 엔진은 자바스크립트 코드를 실행하는 프로그램 혹은 인터프리터를 말한다.

자바스크립트 엔진은 표준적인 인터프리터로 구현될 수도 있고 혹은 자바스크립트 코드를 바이트코드로 컴파일하는 저스트인타임(just-in-time) 컴파일러로 구현할 수도 있다.

Chrome **V8** Javascript 엔진은 C++ 로 만들어 졌으며, 오픈소스이다.

V8 은 **저스트인타임 컴파일러** 로 구현되어 있고, 중간 바이트코드로 변환하는 것이 아니라 머신코드로 변환시켜 속도의 향상을 이루었다.

**이벤트 기반** **논 블로킹 I/O 모델** 은 상당히 중요한 개념이라, 하나씩 집고 가겠다.

---

#### 이벤트 기반 (Event Driven)

---

[출처 : http://www.nextree.co.kr/p7292/](http://www.nextree.co.kr/p7292/)

[출처 : https://plus4070.github.io/nhn%20entertainment%20devdays/Node.js_EventHandling.html](https://plus4070.github.io/nhn%20entertainment%20devdays/Node.js_EventHandling.html)

Node js는 **단일 Thread 이벤트 기반 모델** 이다.

앞선 포스트에서 Javascript의 이벤트 루프나 콜 스택, 태스크 큐에 대해선 설명을 했기 때문에, 아마 이해가 좀더 쉽게 될 것이다.

Node js는 백그라운드에서 Thread 풀을 가지긴 하지만, 애플리케이션 자체에는 Multi-Thread 개념이 없다.

그럼 어떻게 많은 처리를 하는가하면, **Event Callback** 방식이다.

Thread 기반 방식과 Event Callback 방식의 차이가 어떻게 다른지를 알려면 Thread 기반 방식을 먼저 알아야 한다.

![Thread 기반](http://www.nextree.co.kr/content/images/2016/09/syhan_140320_node1_021-1024x518.png)

**Thread 기반** 웹 모델은 요청이 웹 서버로 도착하면 현재 Thread 풀에 가용한 Thread에게 그 작업을 할당한다(Multi-Thread).

그리고 해당 요청에 대한 처리는 동일한 Thread에서 지속된다.

예를 들어, File을 받아오는 작업과 Data를 받아오는 작업이 있다고 하면 2개의 작업을 처리하기 위해 2개의 Thread가 생성이 되고 각각의 Thread에서 File을 받아오는 작업과 Data를 받아오는 작업을 처리하게 된다.

즉, Multi-Thread 방식은 서버의 요청 처리를 쓰레드에서 처리하도록 하여 병렬처리를 가능하도록 하는 방식이다.

쓰레드는 서버 CPU 자원을 시분할 형태로 나누어 가짐으로써 독립실행이 가능하며 다른 요청을 동시에 받을 수 있게 한다.

이러한 방식은 IO Blocking을 해결하는 이상적인 모델로 보일 수 있다.

그러나 한계점이 있는데,

일반적으로 클라이언트의 요청마다 Thread를 발생시키다보니, 이 말은 동시 접속자 수가 많을 수록 Thread가 많이 발생한다는 의미이며 그만큼 메모리 자원도 많이 소모한다는 의미이다.

그러나 서버의 자원은 제한되어 있으므로 일정 수 이상의 Thread는 발생시킬 수 없다.

또한, 하나의 Thread에서 CPU를 사용하고 있다고 하면, 다른 Thread는 해당 작업이 끝날 때까지 기다려야 한다는 것이다.

즉, 동기적으로 일을 처리하게 된다.

![동기처리](http://www.nextree.co.kr/content/images/2016/09/syhan_140320_node1_031-1024x369.png)

하나의 요청이 처리되는 동안 다른 요청이 처리되지 못하며 요청이 완료되어야만 다음 처리가 가능한 방식이므로, 동기 방식은 IO 처리를 Blocking 하는데 지금까지는 이 문제를 Thread로 처리했다.

이런 문제를 비동기처리로 처리하는게 Node js의 원리이다.

제어권을 다음 요청으로 바로 넘기기 때문에, IO 처리인 경우 Blocking 되지 않으며 다음 요청을 처리할 수 있다.

다시 정리해서, 단일 Thread를 사용하여 이벤트 루프를 도는데, 이벤트 큐에 추가되어 있는 작업들을 순서대로 Thread에 할당해서 처리하는 방식이다.

여기서 다음 그림을 보면 이해가 쉽다.

![이벤트 루프](http://www.nextree.co.kr/content/images/2016/09/syhan_140320_node1_041.png)

클라이언트에서 요청이 들어오면 비동기 처리를 위해, 이벤트가 발생하고 서버의 이벤트 루프에 메시지 형태로 전달된다.

그러면, 이벤트 루프가 이를 처리할 동안, 제어권을 넘겨주고 다음 요청을 진행한다.

**그럼 그 처리가 끝났다는 것을 어떻게 아는 것일까??** 이 부분이 면접 질문으로 받은 적이 있다.

그 부분이 **CallBack** 이다. 해당 요청이 완료되면 CallBack을 이용해, 완료 되었음을 알려준다.

여기서 싱글 쓰레드다 보니, 요청 처리가 하나의 Thread 안에서 처리된다는 의미가 되므로, 해당 처리가 오래 걸릴 수록 전체 서버 처리에 영향을 주게 된다. 이게 치명적인 **약점** 이다.

`다시 정리를 해보자.`

Node js은 **Event 기반** 이다. 따라서 **Event Callback** 방식으로 동작하고 **Event Loop** 가 **Single Thread** 를 사용한다.

이 때 **비동기 방식** 을 사용해, 병렬처리를 해결하여 효율을 증대시켰다. (`non-blocking I/O`라고 하는데 이는 잠시 후에 알아보자.)

요청이 들어오면, 해당 요청을 **Event Loop** 에 메세지형태의 Event로써 전달한다.

그럼 **Event Loop** 는 해당 요청을 처리할 것이고, 처리 도중 제어권을 다음 요청에 넘겨준다.

그렇게 요청들은 **Event Loop** 에서 처리되기 위해 대기할 것이고(Task Queue), **Event Loop** 는 하나의 event가 처리가 되면 **Callback** 으로 처리완료를 알려준다.

---

#### non blocking I/O

---

흔히, **Async NonBlocking I/O** 라고 많이 말한다. 이 역시 질문을 받은 적이 있다. 매우 중요하니 알아두는 것이 좋다.

앞서, 병렬 처리에 대해 설명하며 비동기처리, 혹은 blocking I/O와 같은 단어를 사용했는데 과연 이게 무엇일까?

[출처 : https://homoefficio.github.io/2017/02/19/Blocking-NonBlocking-Synchronous-Asynchronous/](https://homoefficio.github.io/2017/02/19/Blocking-NonBlocking-Synchronous-Asynchronous/)

Blocking과 Sync, non-blocking Async는 비슷하다고 생각하여 차이점을 알기 힘든데, 이는 관심사에 따라 나누어진다고 본다.

**Blocking/non-blocking** 은 `제어권을 넘겨주는가 마는가`의 문제이다.

**Async/Sync** 는 `작업이 완료되었다는 것을 신경 쓰는지 안쓰는지`의 차이이다.

A에서 B를 호출했다고 하자, 그럴때 `B가 바로 제어권을 다시 A에게 넘겨준다면 non-blocking 이다`.

그러나, `B가 끝나고 나서 A에게 제어권을 다시 넘겨준다면 Blocking`이다.

즉 Node js는 요청이 왔을 때, 이벤트 루프에 이벤트를 주고난 후, 이벤트 루프가 바로 다음 요청에게 제어권을 넘겨주고 이벤트 루프는 해당 이벤트를 처리한다. 따라서 non-blocking 이라고 볼 수 있다.

또한, A에서 B를 호출할 때, A에서 callback을 넘겨주고 B가 작업을 완료한 후, callback을 실행하게 되고, A는 해당 완료를 신경쓰지 않는다면 Async 이다.

반면에, B가 모두 처리한 후 리턴하거나 만약 바로 제어권을 넘겨주었다하더라도 해당 처리가 끝났는지 계속해서 확인한다면 Sync이다.

즉, Node js의 경우 요청에 대한 처리를 이벤트루프가 완료하고 callback으로 처리한다음 끝이나기 때문에, Async라고 볼 수 있다.

---

### 콜 스택, 태스크 큐, 이벤트 루프 등 전체 정리

---

먼저, 이렇게 앞선 내용을 조사하면서 Task Queue가 단순히 콜백 함수만을 저장하는 것이고, 이벤트 루프에 들어가는 큐가 따로 있는 것인지, 헤깔렸었다.

이에 대한 해답은 다음과 같다.

[출처 : https://www.quora.com/Does-Node-js-have-more-than-1-event-loop-task-queue](https://www.quora.com/Does-Node-js-have-more-than-1-event-loop-task-queue)

`Beware, to be clear, that a task queue is only a component in an event loops and that engine can implement tasks queues without event “loops”.`

주의해야 할 점은 Task Queue는 Event Loop의 구성 요소일 뿐이고, Engine은 Event Loop없이 Task Queue를 만들 수 있다.

`The event loop, on is side, is a never ending loop that executes the “jobs” which are in its own queue`

이벤트 루프는 이 자체의 큐에있는 작업을 실행하는 끝나지 않는 루프이다.

그럼 전체적으로 정리를 해보겠다. 이번엔 Javascript의 콜 스택과 테스크 큐, 이벤트 루프 전반적으로 모두 첨가해 설명을 하려고 한다.

1. 흔히, URL을 이용해 우리는 서버에 원하는 **요청** 을 하게 된다.
2. 그러면 Node js에서는 최우선 실행 파일(흔히, app.js)부터 실행을 시작해 **콜 스택** 에 넣기 시작한다. (Express를 사용할 때, Error가 나면 오류가 난 부분을 log로 출력하는데, (바로 Express를 사용하면, 보통 Morgan이라는 미들웨어가 로깅처리를 하게 된다.) 이 때, 나오는 로깅들이 Stack상의 정보다.)
3. **REST API** 라는 네트워크 아키텍쳐를 사용했다고 할 때, 원하는 **행위(Verb)** 즉, HTTP Method에 따라, URI에 **표현(Representations)** 된 **자원(Resource)** 를 이용해, 만들어 둔 Routing이 시작되고, 담당하는 함수를 찾아 실행이 되기 시작한다.
4. 이때, 하나의 요청이 아니라 여러 요청이 들어올 수 있다. 그렇게 되면, 요청이 들어올 때 하나씩 **Task Queue** 에 쌓이기 시작한다. 그러면 **이벤트 루프** 가 큐에서 이벤트를 하나씩 받아, **제어권** 은 다시 다음 요청에 넘기고 처리를 하기 시작한다.
5. 여기서 **파일 읽기**, **데이터베이스 질의**, **소켓 요청**, **원격 서비스 접속** 과 같은 경우, **Blocking I/O** 로 되는데, 이럴 때는 **백그라운드의 Thread pool** 에 CallBack과 함께 보내고, 완료 되었을 때 Task Queue가 CallBack을 가지게 되며, 해당 CallBack을 더이상 진행하는 Task가 없을 때, 흔히 이벤트 루프가 비었을 때 받아 처리하는 형태로 진행한다.
6. 처리가 끝나면 **CallBack** 으로 완료를 요청에 보낸다.

조심해야 할 건 콜 스택은 Javascript 파일 자체의 실행할 때 쌓이는 실행 순서이고, 요청 자체의 흐름과는 다른 내용이다.

위 내용을 설명해 달라는 면접 질문을 받은 적 있다. 상당히 난이도가 있는 내용이니, 정확히 알아두어야 한다.

---

### Nodejs에서 Garbage Collector의 동작은?

---

마지막으로, Nodejs에서의 GC에 대해 알아보자. 이 역시 면접 질문을 받았다. 전혀 생각을 못하던 부분이라 많이 당황했던 경험이 있다.

일단, Garbage Collector가 무엇인지 부터 알고 넘어가자.

---

#### Garbage Collector 란?

---

아마 다들 알고 있을 것이라 생각한다. **Garbage Collector** 란, ` 메모리 관리 기법 중의 하나로, 프로그램이 동적으로 할당했던 메모리 영역 중에서 필요없게 된 영역을 해제하는 기능`을 한다.

흔히, GC는 **포인터 형식** 으로 진행된다.

해당 객체를 참조하는 게 더이상 없을 때 해당하는 객체를 쓰레기 값이라 보고, 그 객체에 할당된 메모리를 해제한다.

보통 해제할 때는 포인터 추적 기법을 쓰고, 가끔 참조 카운팅 기법을 쓴다.

[출처 : http://blog.sonim1.com/136](http://blog.sonim1.com/136)

1. 표시하기 지우기
**mark-and-sweep** 라 불리는 방식이다.

포인터 추적 기법의 대표적인 예다.

변수가 특정 컨텍스트에서 사용할 것으로 정의되면 그 변수는 컨텍스트 안에 있는 것으로 표시 되며, 변수가 컨텍스트 밖으로 나가면 밖에 있다고 표시된다.

표시라는게 구현 방법이 다양하기 때문에 브라우저마다 조금씩 다르긴하지만 일반적으로 특정 비트를 on상태로 표시하거나 컨텍스트 내부, 외부를 나타내는 변수 목록을 따로 두거나 하는 방식으로 구현하고 있다.

표시가 됐다면 메모리 청소가 실행될 때마다 표시를 체크하여 메모리 정리를 한다.

2. 참조 카운팅
참조 카운팅은 널리 쓰이지는 않는 방식이다.

각 값이 참조 되었는지 추적하여 카운트를 기록한다.

값의 참조 카운트가 0이되면 사용할 일이 없으니 메모리를 회수한다.

이 방식의 경우 순환참조 문제가 발생하면 메모리가 회수되지 않아서 문제가 된다.

순환 참조란 A와 B객체가 있을 때, A 객체가 B를 참조하고, B 객체가 A를 참조할 경우 서로 참조카운트가 줄어들지 않아 발생하는 오류이다.

이에 대한 해결 방법으로는 순환참조한 변수에 null을 대입해줘서 참조를 끊어주는 방법이 있다.

---

#### Node JS에서는?

---

JavaScript는 JAVA와 같이 GC 소프트웨어를 실행해 자동적으로 해당하는 메모리를 해제한다.

Node js에서도 똑같은 지 보도록 하자.

[출처 : https://medium.com/@Dongmin_Jang/node-js-memory-leak-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%88%84%EC%88%98-ac32234cb9e0](https://medium.com/@Dongmin_Jang/node-js-memory-leak-%EB%A9%94%EB%AA%A8%EB%A6%AC-%EB%88%84%EC%88%98-ac32234cb9e0)

이전에 Node js가 V8엔진을 사용한다는 것을 알고 있고, V8엔진은 C++로 만들어 졌다는 것을 알고 있다.

node.js에서는 V8을 이용해서 자바스크립트를 native code로 컴파일한다. (앞서 말했듯이 저스트인타임 컴파일러로 동작한다.)

즉, Native code는 JavaScript가 아니라는 소리다. 따라서, 실제로 자바스크립트로 메모리가 할당, 회수 되지 않는다는 것이다.

그러므로, V8 엔진은  garbage collection 메카니즘을 이용한다.

이 매커니즘은 만약 메모리 세그먼트가 어디로부터 참조되지 않는다면 그것은 더 이상 사용되지 않을 것이라고 추측하여 해제한다. (포인터 추적 기법)

다음 포스팅에는 DB, 보안 등에 대한 내용을 정리해 보도록 하겠다.
