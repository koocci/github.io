---
layout: post
title:  "[AngularJS] 시작하세요! AngularJS 6"
date:   2016-12-21 15:03:14 +0900
categories: AngularJS
tags: [Angularjs, 프로그래밍, MEAN stack, 기초, 블루프린트, IONIC]

---

# &를 이용한 독립 scope 설정

---

![shy](http://farm2.static.flickr.com/1145/637501307_862ef3d1a7_z.jpg)

학교 시험과 자격증 시험으로 인해 잠시 쉬었는데, 이전에 이어서 `&`를 이용해 독립 scope를 지정하는 법을 알아보겠다.

scope 설정에서 속성의 값으로 `&`나 `&연결된 DOM 속성명`을 주면 **부모 scope 환경에서 실행될 수 있는 표현식에 대한 레퍼런스** 를 가지고 올 수 있다.

앞서 사용했던 예제에서 지시자 기능을 조금 바꿔보려고 한다. 단순히 인사를 나타내는 구문이였지만, 이제는 대상자에게 메세지를 보내는 형태로 만들어 보겠다.

여기서 메세지를 보내는 로직은 **지시자 안에 있는 것이 아니고 컨트롤러와 같은 지시자 외부에 있게 된다고 가정하자.** 메세지를 보내기 전에 어떠한 일을 해야 하는데 그건 상황에 따라 다르므로 지시자를 수정하지 않고 하기란 불가능 하기 때문이다. 그럼 템플릿 코드부터 보도록 하자.

`<h1>hello <span>{{name}}</span> <button ng-click="send()">메세지 보내기</button></h1>`

그럼 지시자 쪽 코드를 보자.

    <!DOCTYPE html>
    <html ng-app = "sampleApp">
      <head>
        <meta charset="utf-8" />
        <title>example 2.29</title>
      </head>
      <body ng-controller = "demoCtrl">
        <div ng-repeat="helloSb in helloList" hello to="{{helloSb.name}}" send="sendMessage(helloSb.name, this)"></div>

        <!--angular file-->
        <script src="../angular.js" type="text/javascript"></script>
        <script type="text/javascript">

          angular.module('sampleApp', [])
            .controller('demoCtrl', ['$scope',function($scope){
              $scope.helloList = [{name:'google'},{name:'naver'},{name:'angular'}];

              $scope.sendMessage = function(toSb){
                console.log(toSb + "에게 메세지를 보낸다.");
              };
            }])
            .directive('hello', function(){
              return {
                templateUrl : "template/helloTmpl3.html",
                restrict : "AE",
                scope : {
                  name : "@to",
                  send : "&"
                }
              }
            });
        </script>
      </body>
    </html>

바뀐 템플릿을 먼저 보자.

`<button>` 이 환영 문구 오른쪽에 추가되고 해당 버튼을 클릭하면 `send()` 표현식을 계산하게 된다.

그러면 `$scope.send`의 값에 () 연산을 하여 결국 함수를 호출하게 되는데, 이 `send`는 지시자 설정 객체의 scope에서 `&`로 설정됐다. 그래서 호출할 함수의 레퍼런스는 이 지시자가 적용된 DOM의 send 속성 값을 함수의 내용으로 하는 함수의 레퍼런스를 지시자 내부의 send가 갖게 된다.

즉, 가상의 function(){sendMessage(hellSb;)}; 가 있고, 이 함수의 레퍼런스를 지시자 내부의 send가 갖게 된다. 그리고 가상의 함수는 부모 scope의 컨텍스트에서 실행된다. 여기서 부모 scope는 ng-controller에서 만들어지는 scope가 아니라 ng-repeat로 인해 만들어지는 scope다. 그래서 `{helloSb : "..."}`로 만들어진 scope를 컨텍스트로 하여 실행되어 console에 해당하는 값이 전달되고 보이는 것이다.

---

### = 을 이용한 독립 scope 설정

---

scope 설정에서 속성의 값으로 `=`이나 `=연결된DOM속성명`을 주면 **부모 scope의 특정 속성과 지시자 내부 scope의 속성과 양방향 바인딩** 을 한다. 여기서 주의할 점이 있다.

`scope : { name : "=to"}` 와 같이 설정되어 있으면 **부모 scope의 속성명이 아니라 연결된 DOM의 속성명** 이다. 이 연결된 DOM의 to라는 속성명에 대한 값이 바로 부모 scope의 속성명이 된다.

이제 한번 에제를 만들어 보자.

템플릿부터 수정한다.

`<h1>hello <span>{{name}}</span> <input type='text' ng-model="name"></h1>`

    <!DOCTYPE html>
    <html ng-app = "sampleApp">
      <head>
        <meta charset="utf-8" />
        <title>example 2.30</title>
      </head>
      <body ng-controller = "demoCtrl">
        <ul>
          <li ng-repeat="helloSb in helloList">
            <input type="text" ng-model="helloSb.name" />
          </li>
        </ul>
        <div ng-repeat="helloSb in helloList" hello to="helloSb.name"></div>
        <!--angular file-->
        <script src="../angular.js" type="text/javascript"></script>
        <script type="text/javascript">

          angular.module('sampleApp', [])
            .controller('demoCtrl', ['$scope',function($scope){
              $scope.helloList = [{name:'google'},{name:'naver'},{name:'angular'}];
            }])
            .directive('hello', function(){
              return {
                templateUrl : "template/helloTmpl4.html",
                restrict : "AE",
                scope : {
                  name : "=to"
                }
              }
            });
        </script>
      </body>
    </html>

내부 지시자에서 사용하는 scope의 name 속성을 변경하도록 `input`태그를 추가했다.

브라우저 화면이서 보면 여섯개의 `input`태그를 볼 수 있다. 이 태그는 위 리스트에 있는 `input`과 hello 지시자가 만드는 input 태그로 구분이 가능하다. 어느 하나의 태그를 수정하더라도 양쪽이 다 바뀔 것이다. 즉 `지시자 내부 scope의 name`과 `demoCtrl 컨트롤러의 helloList 배열`의 각 요소 객체의 name이 모두 연결되어 각 속성의 값을 바꾸면 서로 갱신이 된다.

---

### ngTransclude와 translude 설정

---

Angular에서는 지시자를 이용해 특정 DOM을 조절할 수 있다. (`ng-repeat`) 하지만 hello 지시자처럼 재사용할 수 있는 기능이 있는 컴포넌트도 만들수 있다. 트리 컴포넌트, 그래프 컴포넌트 같은 UI 컴포넌트도 그러하다. 그러나 다른 컴포넌트를 포함하거나 다른 DOM을 담고 있는 컨테이너를 만들 때에도 사용할 수 있다. 위젯이나 패널이 그러하다. `<widget>`, `<panel>`태그를 작성하면 만들 수 있는데, 태그로 만드려면 각각의 지시자를 만들면 된다. 그러나 `<panel>` 태그의 내용을 지시자 템플릿에서 사용해야 템플릿에서 `ng-transclude`라고 설정된 부분에 `<panel>` 태그의 내용이 복사된다. 간단히 만들어 보도록 하자.

템플릿 코드다.

    <div class="panel {{type}}">
      <div class="panel-title">
        {{title}}
      </div>
      <div class="panel-content">
        <div ng-transclude>

        </div>
      </div>
    </div>

지시자 코드는 다음과 같다.

    <!DOCTYPE html>
    <html ng-app = "sampleApp">
      <head>
        <meta charset="utf-8" />
        <title>example 2.31</title>
        <style type="text/css">
          .panel{
            margin: 10px;
            -moz-border-radius: 2px;
            -webkit-border-radius: 2px;
            border-radius: 2px;
            border: 1px solid black;
          }

          .info, .panel-title{
            background-color: gray;
            color: white;
          }

          .alert, .panel-title{
            background-color: red;
            color: white;
          }

          .panel .panel-content{
            padding: 10px;
          }
        </style>
      </head>
      <body ng-controller = "demoCtrl">
        <panel title="알림" type="alert">
          <p>
            AngularJS는 자바스크립트 웹 애플리케이션을 쉽게 개발하게 도와줍니다.
          </p>
        </panel>
        <panel title="공지사항 목록" type="info">
          <ul>
            <li ng-repeat="notice in noticeList">
              <a href="{{notice.url}}">{{notice.text}}</a>
            </li>
          </ul>
        </panel>


        <!--angular file-->
        <script src="../angular.js" type="text/javascript"></script>
        <script type="text/javascript">

          angular.module('sampleApp', [])
            .controller('demoCtrl', ['$scope',function($scope){
              $scope.noticeList = [{
                url: "notice/1",
                text: "공지사항 첫 번째 글입니다.",
              },{
                url: "notice/2",
                text: "공지사항 두 번째 글입니다.",
              },{
                url: "notice/3",
                text: "공지사항 세 번째 글입니다.",
              }];
            }])
            .directive('panel', function(){
              return {
                templateUrl : "template/panelTmpl.html",
                restrict : "AE",
                transclude: true,
                scope : {
                  true : "@",
                  type : "@"
                }
              }
            });
        </script>
      </body>
    </html>

예제를 한번 해석해 보겠다.

`transclude` 옵션을 true로 했을 때, 템플릿에서 `ng-transclude`를 사용한 것을 알 수 있다. 이렇게 `transclude` 를 사용하면 `<panel>` 태그의 내용이 탬플릿에서 `<div ng-transclude></div>`안으로 잘라서 붙여진 것과 같이 된다. 그리고 `<panel>` 태그에 title과 type 옵션을 통해 자연스럽게 변경할 수 있게 된다.

---

### 외부 라이브러리

---

앞서, `bootstrap`을 언급한 적이 있다. `ui-bootstrap`의 경우, 트위터 부트스트랩의 css를 이용하고, AngularJS를 이용해 자바스크립트 기능을 넣어 구현하는 모듈이다. 해당 모듈과 똑같이 트위터 부트스트랩의 기능을 제공하지만 다른 방식으로 구현한 모듈이 있다. `angular-strap`모듈이다. 해당 모듈은 **트위터 부트스트랩의 자바스크립트 라이브러리를 이용해 지시자를 개발한 모듈** 이다.

즉, 트위터 부트스트랩의 자바스크립트 라이브러리가 꼭 필요한 모듈은 `angular-strap` 모듈이고 필요가 없는 모듈은 `ui-bootstrap`모듈이다.

모두 장단점이 있는데, 다른 자바스크립트 라이브러리를 사용하지 않으면 의존성이 없으므로 다른 라이브러리 변경의 걱정이 없다. 그러나 그만큼 개발 기간이 오래 걸리고 책임에 따른 유지보수도 생각해야 한다. 다른 라이브러리를 사용하면 기본부터 만들 필요 없이 AngularJS 프레임워크와 잘 맞춰 돌아가게 지시자만 개발하면 된다.




앞서 적어둔 모든 소스는 [이곳](https://github.com/koocci/AngularJS-examples) 에서 보실 수 있습니다.
