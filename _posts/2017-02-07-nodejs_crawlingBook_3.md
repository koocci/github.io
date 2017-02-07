---
layout: post
title:  "[node js] Node js로 크롤링하기(reTry) 3"
date:   2017-02-08 00:04:23 +0900
categories: Nodejs
tags: [node js, node, crawling, 크롤링, 노드]

---

# 로그인

---

![beautiful](http://farm5.static.flickr.com/4089/5061528905_13d8d546b8_z.jpg)

아마 크롤링에 있어서는 마지막 호스팅이 되지 않을까 한다.

그 이유는 이후의 단계를 봤을 때, `electron`(atom 에디터가 electron으로 만들어졌다.) 한글 형태소 분석 등 머신러닝 혹은 딥러닝 부분까지 진행되지만 사실 이 이후단계는 파이썬이 아직까지 훨씬 효율적이라고 생각한다. 따라서 파이썬을 이용해 `Django`나 `Flask`쪽을 공부해볼 생각이고, 크롤링은 여기까지 완료한다면 아마 대부분의 내용을 긁어올 수 있을 것이기 때문에 따로 더이상 적지 않으려고 한다.(phantom, casper, cron 만 잘써도 충분히 엄청난 일들을 할 수 있다.)

그럼 진행해 보도록 하자.

먼저 로그인 기능은 상당히 까다롭다. 회원전용, admin 등등 웹사이트 대부분은 로그인을 필요로 하게 만든다. 덕분에 로그인을 해야 볼 수 있는 정보들이 굉장히 많아졌다. 따라서 `phantomJS`와 `CasperJS`를 이용해 이를 로그인하고 진행해 보도록 하자.

도서상으론 티스토리를 예시로 들었지만 난 티스토리를 쓰지 않으므로, 쉽게 할 수 있는 사이트를 아무곳이나 찾아서 진행해 보길 바란다.

사용법만 제대로 알아간다는 개념으로 다음 코드를 보자.

``` javascript

var casper = require('casper').create({verbose: true, logLevel: "debug"});

//URL 및 로그인 정보 변수
var url = "http://YOUR_CRAWLING_SITE.com/";
var id = "YOUR_ID";
var password = "YOUR_PASSWORD";

casper.start();

casper.open(url);

// Form.Submit
casper.then(function(){
  casper.fill("#form",{
    id: id,
    pw: password
  }, true);
});

// 로그인 후 수행
casper.then(function(){
  var getName = function(){
    return document.querySelector("#user_name").innerText;
  };
  console.log("이름 : " + this.evaluate(getName));

});

casper.run();

```

상당히 간단해 보이는데, 조금 정리를 해보자.

`casper.fill(CSS 선택자, 값 객체, [, Submit 여부])`

* css 선택자
  - 개발자도구로 볼수 있는 css 선택자.
* 값 객체
  - name, value 속성을 지정
* Submit 여부
  - true일 경우, 전송까지 수행

또한 `evaluate` 라는 메소드를 사용하는데, 이는 `웹 페이지 내에서 임의의 자바스크립트 코드 수행`할 수 있게 한다.

`casper.ivaluate(함수, [, 파라미터[, 파라미터2[, ...]]])`

* 함수
  - 페이지 내에서 수행하고 싶은 자바스크립트 함수 객체
* 파라미터
  - 함수에 넘기고 싶은 파라미터

그럼 위 예시에서는 document 객체를 사용하는데, 이 것은 html내의 document객체를 사용할 수 있는 것이다. 즉, DOM 요소로 접근을 할 수가 있다. 여기서는 `document.querySelector`로 가져오고 있다.

---

### 마우스 클릭

---

바로 예제부터 보는게 나을 것이라 생각한다.

``` javascript

var casper = require('casper').create({verbose: true, logLevel: "debug"});

//URL 및 로그인 정보 변수
var url = "http://YOUR_CRAWLING_SITE.com/";
var id = "YOUR_ID";
var password = "YOUR_PASSWORD";

casper.start();

casper.open(url);

// Form.Submit
casper.then(function(){
  casper.fill("#form",{
    id: id,
    pw: password
  }, true);
});

// 로그인 후 수행
casper.then(function(){
  var getName = function(){
    return document.querySelector("#user_name").innerText;
  };
  console.log("이름 : " + this.evaluate(getName));
});

// 버튼 클릭
casper.then(function(){
  if(casper.exists('#button')){
      casper.click('#button');
      console.log("CLICK");
  }
});

casper.then(function(){
  casper.capture("capture.png", {
    top:0, left:0, width:1400, height: 800
  });
});

casper.run();

```

직관적으로 느껴지는 것이 있을 것이다. 추가로 이전에 했던 캡쳐 역시 넣어두었다.

이외에도 casper에 대해 찾아보면, `querySelectorAll`이라던지, `url.changed`같은 많은 메소드들을 볼 수 있다.

생각보다 빠르게 포스팅이 마무리 되었다. CSS 선택자나 DOM 파싱에 대한 것은 따로 다루지 않겠다. (웹 프로젝트 하나만 제대로 완성해도 충분히 깨우치는 부분이다.)

추가로, 해당 crawling 코드는 [이곳]()에 공유하겠다.












-
