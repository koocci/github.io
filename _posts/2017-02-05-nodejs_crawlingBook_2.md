---
layout: post
title:  "[node js] Node js로 크롤링하기(reTry) 2"
date:   2017-02-05 21:58:23 +0900
categories: Nodejs
tags: [node js, node, crawling, 크롤링, 노드]

---

# PhantomJS, CasperJS

---

![smile](https://gongu.copyright.or.kr/gongu/wrt/cmmn/wrtFileImageView.do?wrtSn=965017&filePath=L2Rpc2sxL25ld2RhdGEvMjAxMy8yNS9DTFM0L0FSVF9BNTYzXzE2MV8xNDhfbnVyaW1lZGlhXzIwMTMxMjIw&thumbAt=Y&thumbSe=b_tbumb&wrtTy=4)

지금부터는 로그인 기능이 필요한 웹사이트를 크롤링해보려고 한다. 상당히 궁금했던 부분이고, PhantomJS를 언젠가 해보겠다고 했지만 Angular를 사용하면 잠시 써본게 전부라, 이번에 한번 제대로 입문을 해보려 한다.

PhantomJS나 CasperJS는 **폼에 값을 설정하거나, 특정 버튼을 클릭하는 것처럼 웹 브라우저의 UI 자동화작업을 지원** 한다. 따라서 여러 페이지 이동이나 로그인 기능을 하는 것에 있어서 상당히 편리하고, 그런 이후의 데이터를 취득함에 있어서 가장 좋을 것이다.

역할을 한번 설명해 보자.

+ PhantomJS
  - 커맨드 라인으로 사용할 수 있는 브라우저 (화면이 없는 브라우저)
+ CasperJS
  - PhantomJS 를 쉽게 사용하기 위한 라이브러리

PhantomJS를 조금 자세히 설명하면 렌더링 엔진으로 웹킷(WebKit)이 채용되었다. 웹킷은 애플의 웹 브라우저인 사파리에서 사용하는 렌더링 엔진이다. 또한 구글 크롬이 블링크(Blink)라는 렌더링 엔진을 사용하지만 원래 사용했던 엔진이기도 하다.
이렇게 PhantomJS를 이용하면 커맨드 라인으로 브라우저 조작, 데이터 취득, 스크린샷등이 가능해진다. 웹사이트에서 데이터를 스크래핑하거나 UI 테스트 자동화 등에 활용이 가능하다.

CasperJS는 아까 말한대로 PhantomJS 를 쉽게 사용하기 위한 라이브러리다. 그래서 CasperJS를 사용하려면 PhantomJS가 설치되어 있어야 한다.
이외에 다루진 않겠지만, 파이어폭스의 렌더링 엔진인 게코(Gecko)를 기반으로 한 SlimerJS를 사용하는 것도 좋다.

설치는 그냥 개별적으로 진행하고, 간단히 하나씩 해보자.

    // 웹사이트 타이틀을 표시하는 프로그램

    var TARGET_URL = 'http://jpub.tistory.com';

    // CasperJS 객체 생성
    var casper = require('casper').create();

    //웹 사이트 열기
    casper.start(TARGET_URL, function(){ // 실제 실행은 아님. 방문할 URL 지정 페이지 로드시 수행할 콜백함수 지정
    //타이틀 출력
    this.echo(casper.getTitle()); //페이지 로드 후, 실행 접속한 사이트 제목을 취득 후 출력
    });

    casper.run(); //실제 실행


위 프로그램은 웹사이트 타이틀을 가져오는 것이다. 실행은 node로 하는 것이 아니라, casperjs 파일이름 으로 실행한다.

참고로, fs 모듈이 설치되어 있다면, [다음](http://stackoverflow.com/questions/39641513/cant-find-module-fs-when-running-casperjs-on-js-file)
과 같이 연동이 안될 수 있으니 지워주자.

그럼 콘솔에 해당 타이틀이 출력된다.

만약 CasperJS의 런타임 정보를 좀더 알고싶으면 실행 시 `-verbose`나 `-log-level=debug`라고 하면 색상과 함께 정보가 표시 된다.

간단히 해봤으니 이번엔 캡처 프로그램을 만들어보자.

    // 스크린샷

    var TARGET_URL = 'http://jpub.tistory.com';

    // CasperJS 객체 생성
    var casper = require('casper').create();

    // 개시
    casper.start();

    casper.open(TARGET_URL);

    // 스크린샷 수행
    casper.then(function(){
    casper.capture("screenshot.png");
    });

    //실행
    casper.run(); //실제 실행

아마 실행을 하면, 이미지 파일이 만들어 질 것이다.

위 타이틀을 가져오는 프로그램과 코드차이를 보자. open을 쓰고 then이라는 메소드로 연결해 주었다는 점을 보면 어떤 처리로 이어지는지 이해하면 될 것이다.

그럼 이어서 이미지 공유 사이트인 플리커(Flickr)에서 고양이 사진을 한번 스크린샷으로 저장해보자.

    // 스크린샷 (Flickr)

    // CasperJS 객체 생성
    var casper = require('casper').create();

    // 개시
    casper.start(); // 빈 페이지 준비

    // 화면 사이트 설정
    casper.viewport(1400, 800); //브라우저 화면 크기

    //UserAgent 설정
    casper.userAgent('User-Agent: Mozilla/5,0 (Windows NT 6.1; WOW64) AppleWebKit/537.36(KHTML, like Gecko) Chrome/37.0.2062.120 Safari/537.36');

    // 플리커에서 고양이로 검색

    var text = encodeURIComponent("고양이");
    casper.open('https://www.flickr.com/search/?text=' + text);


    // 스크린샷 수행
    casper.then(function(){
      casper.capture("flickr-cat.png", {
        top:0, left:0, width:1400, height: 800
      });
    });

    //실행
    casper.run(); //실제 실행

다음과 같다. `UserAgent`는 잠시 후에 다시 설명하도록 하고, **CasperJS 의 흐름** 을 한번 정리해보자.

CasperJS는 `start()` `run()` 메소드 사이에 순서대로 실행하고자 하는 처리를 `then()` 메소드를 사용하여 지정하는 식으로 작성하면 된다. 물론 비동기 처리가 기본이다. 그러나 `then()` 메소드를 사용하면 다음 메소드로 넘어가지 않으니, 동기 수행이 쉽게 이루어진다.

그럼 아까전 UserAgent에 대해 다시 말해보자.

**사용자 에이전트** 란 웹사이트에 접속할 때 사용하는 프로그램을 말하는데, 어떤 웹 브라우저를 사용하는가를 뜻한다.

혹시 `UserAgent`에 대해 좀더 궁금하다면 [이곳](http://ohgyun.com/292)에 들어가서 한번 보도록 하자.

그럼 이 `UserAgent`를 조절해서 모바일용 화면도 볼수 있지 않을까?

그럼 바로 모바일 버전에 대해 여는 것을 만들어 보자.

    // 스크린샷 (iPhone 모드)

    var TARGET_URL = "http://jpub.tistory.com";

    // CasperJS 객체 생성
    var casper = require('casper').create();

    // 개시
    casper.start(); // 빈 페이지 준비

    // UserAgent 설정
    casper.userAgent('Mozilla/5.0 (iPhone; CPU iPhone OS 7_0 like Mac OS X)' +
      'AppleWebKit/537.51.1 (KHTML, like Gecko) Version/7.0 Mobile/11A465 Safari/9537.53');

    // 화면 사이즈 설정
    casper.viewport(750, 1334);

    casper.open(TARGET_URL);

    // 스크린샷 수행
    casper.then(function(){
      casper.capture("screenshot.png");
    });

    //실행
    casper.run(); //실제 실행

아마 스크린샷 이미지를 보면, UI가 좀 달라졌다는 것을 알 수 있을 것이다.

그럼 이제 한가지만 더 해보도록 하자.

지금까지 한걸 보면 CasperJS 로 쉽게 웹사이트를 캡쳐할 수가 있다. 그럼 커맨드 라인에서 인자로 넘겨준 URL의 스크린샷을 찍는 프로그램을 만들어보자.

CasperJS 에서는 실행 했을 때, 지정한 인자가 `casper.cli.args` 에 배열로 들어가게 된다.

이를 토대로 작성해보자.

    // 스크린샷 (커맨드 입력)

    // CasperJS 객체 생성
    var casper = require('casper').create();
    var utils = require('utils');

    var args = casper.cli.args;
    if(args.length < 1){
      //사용법 표시
      casper.echo("USES:");
      casper.echo("shot-tool URL [savepath]");
      casper.exit();
    }

    var savepath = "screenshot.png";
    var url = args[0];
    if(args.length >= 2){
      savepath = args[1];
    }

    //CasperJS 처리 개시
    casper.start(); // 빈 페이지 준비
    casper.viewport(1024, 768);
    casper.open(url);
    casper.then(function(){
      this.capture(savepath, {
        top:0, left:0, width:1024, height:768
      });
    });

    //실행
    casper.run(); //실제 실행


`casperjs yourFile.js http://www.naver.com screen_exam.png`

실행은 다음과 같다.

여기서 `http://` 부분을 적지않고 주소만 적으면 나오지 않으니 주의하고, 저장하고자하는 파일 이름 설정에도 확장자를 적어두도록 한다.

그러면 조금 더 나아가서, 리눅스(CentOS)나 MAC OS X에서는 다음과 같이 셸 스크립트를 만들어 더 쉽게 사용할 수가 있다.

    #!/bin/sh
    SCRIPT_DIR="$(dirname "$0")"
    /usr/local/bin/casperjs $SCRIPT_DIR/yourFile.js $*



와 같이 하고 실행은 `sh shot-tool.sh http://google.com` 정도가 될 것이다.

다음 포스팅에선 로그인을 제대로 해보도록 하자.
