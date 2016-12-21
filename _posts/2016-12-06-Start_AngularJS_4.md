---
layout: post
title:  "[AngularJS] 시작하세요! AngularJS 4"
date:   2016-12-06 20:50:14 +0900
categories: AngularJS
tags: [Angularjs, 프로그래밍, MEAN stack, 기초, 블루프린트, IONIC]

---

# $scope

---

![flower](http://farm4.static.flickr.com/3754/13559623353_1c90743bab_z.jpg)

이전까지 MVC를 다루다가 `$rootScope`를 잠깐 언급만 하고 끝이 났다.

이제 이것에 대해 알아보려 한다.

`$scope`가 얼마나 중요한 역할을 하는지는 이미 몸으로 겪어왔다. **양방향 바인딩** 의 핵심이자 뷰와 컨트롤러를 이어주는 **징검다리** 이기도 하다. `$scope`는 단순히 자바스크립트 객체이다.. 그렇지만 **연결된 DOM 요소에서 표현식이 계산되는 실행환경이고 뷰와 컨트롤러에서 사용되는 데이터와 기능이 살아 숨쉬는 공간이다.** 게다가 `$rootScope`의 존재를 보듯, 계층적 구조를 가진다.

`$scope`의 특징을 다시 정리해보면 다음과 같다.

* 뷰와 컨트롤러를 이어주는 징검다리
* 연결된 DOM에서의 실행환경
* 양방향 데이터 바인딩 처리
* 이벤트 전파 처리
* 계층적 구조

---

### 계층 구조

---

이제 `$rootScope`에 대해 알아보자. 이것은 `ng-app`을 생성하며 `ng-app`이 선언된 DOM 요소가 최상위 노드가 되어 여러 자식 `$scope`를 가지게 된다.

즉, DOM과 같은 계층적 구조에서 최상위 계층에 `$rootScope`가 존재하는 것이다.
어쩌면 `window`와 같은 글로벌 변수 영역이라고 볼 수도 있겠다.

그럼 예제를 보도록 하자.

    <!DOCTYPE html>
    <html ng-app = "myApp">
      <head>
        <meta charset="utf-8" />
        <title>example 2.20</title>
      </head>
      <body>
        <div ng-controller="parentCtrl">
          <h1>부모 이름 : { { parent.name } }</h1>
          <div ng-controller="childCtrl">
            <h2>부모 이름 : { { parent.name } }</h2>
            <h2>자식 이름 : { { child.name } }</h2>
            <button ng-click="changeParentName()">부모이름변경</button>
          </div>
        </div>

        <!--angular file-->
        <script src="../angular.js" type="text/javascript"></script>
        <script type="text/javascript">

          var myApp = angular.module('myApp', []);
          myApp.controller('parentCtrl',['$scope', function($scope){
            $scope.parent = {name : "parent Kim"};
          }]);

          myApp.controller('childCtrl',['$scope', function($scope){
            $scope.child = {name : "child Ko"};
            $scope.changeParentName = function(){
              $scope.parent.name = "another Kim";
            };
          }]);
        </script>
      </body>
    </html>


결과를 보자.

먼저, `ng-app` 지시자에 `$rootScope`가 하나 만들어진다.

그리고 `parentCtrl` ,`childCtrl` 까지 3개의 `scope`가 생겼다.

그리고 해당사항들이 어떻게 변화가 일어나는지 연구해 보자.

parent의 변화가 똑같이 일어난다. 변경버튼을 누르더라도 두가지가 똑같이 변경된다.

이는 부모 `$scope`로 부터 프로토타입을 상속받았기 때문이다.

만약 자식에 없는 모델이라면 속성의 부모에서 찾는다는 것을 눈으로 확인해 보았다.

---

### scope type

---

`$scope`나 `$rootScope`객체는 Angular 내부에서 정의하는 Scope 타입의 인스턴스다. 따라서 별도의 생성자 함수가 Angular 내부에 정의돼 있다.

    function Scope(){ ... }
    Scope.prototype.$apply = function(){};
    Scope.prototype.$digest = function(){ ... }
    Scope.prototype.$watch = function(){ ... }
    Scope.prototype.$new = function(){ ... }
    // ...

Angular는 초기 부트스트랩 시 프레임워크 내부에서 `$rootScope`을 `new Scope()` 와 같이 생성한 후 해당 `$rootScope`을 서비스로 제공한다. 그리고 `ng-controller`나 웹 애플리케이션에서는 다음과 같이 `$rootScope`을 이용해 자식 `$scope` 객체들을 만들 수 있다.

`var $scope = $rootScope.$new();`

서비스는 이후에 배워볼 것이고, scope 타입의 프로토타입 메서드들을 알아보도록 하자.

* $apply(표현식 혹은 함수)
  - 주로 외부 환경에서 Angular 표현식을 실행할 때 사용
  - 외부 라이브러리로 이벤트를 처리할 때나 setTimeout 메서드를 사용할 때 사용
  - 인자로는 표현식이나 함수를 전달할 수 있다.
  - 표현식을 전달하면 해당 표현식을 계산
  - 함수를 전달하면 함수 실행
  - 내부적으로 `$rootScope`의 `$digest`를 실행해 등록된 모든 `$watch`를 실행

* $broadcast(이벤트 이름, 인자들 ...)
  - 첫번째 인자인 이벤트 이름으로 하는 이벤트를 모든 하위 `$scope` 에게 발생시킴
  - 가령 $scope.$broadcast(popup.open,{ title : 'hello'});를 호출하면 `$on` 메서드를 이용해 해당 이벤트(popup.open)를 듣고 있는 $scope들에게 { title : 'hello'}의 데이터를 전달
  - `$scope`들 사이의 참조관계를 매우 느슨하게 만들어 재활용 할 수 있는 UI 컴포넌트 개발에 용이

* $destroy()
  - 현재 `$scope`를 제거할 수 있다.
  - 모든 자식 `$scope`까지 파괴된다.

* $digest()
  - `$scope`와 그 자식에 등록된 모든 `$watch` 리스너 함수를 실행
  - `$watch` 리스너 함수가 보는 표현식에 대해 변화가 없다면 리스너 함수는 실행시키지 않는다.

* $emit(이벤트명, 인자들 ... )
  - 해당 `$scope`를 기준으로 상위 계층 `$scope`에게 이벤트 명으로 인자를 전달
  - `$on`으로 이벤트 명을 듣고 있는 상위 계층에 한해 전파

* $eval(표현식, 로케일)
  - 주어진 표현식을 계산하고 그 결과를 반환
  - 현재 `$scope`를 기준으로 표현식이 계산
  - `$scope`의 b라는 속성에 3이라는 값이 있으면 `$scope.$eval('b+3');` 결과는 6

* $evalAsync(표현식)
  - `$eval`과 마찬가지나, 표현식의 결과값이 바로 반환되지 않고 나중에 어떠한 시점에서 그 결과를 반환
  - 적어도 한번의 `$digest`호출

* $new(독립여부)
  - 새로운 자식 `$scope`를 생성
  - 독립여부를 true, false 로 전달
  - true일 경우 프로토타입을 기반으로 상속하지 않게 됨

* $on(이벤트 이름, 리스너 함수)
  - 주어진 이벤트 이름으로 이벤트를 감지하다가 해당 이벤트가 발생하면 리스너 함수 실행
  - 이벤트 리스너 함수는 첫 번째 인자로 이벤트 객체를 받고 다음으로 `$emit`이나 `$broadcast`에서 전달한 값을 인자로 받음
  - 자세한건 추후에...

* $watch(표현식, 리스너 함수, 동등성여부)
  - 대상 `$scope`에 특정 표현식을 감지하는 리스너 함수를 등록
  - `$scope`의 data 속성에 특정 객체가 할당되어 있다고 할 때 `$scope.$watch("data".function(){ ... })`로 함수를 호출하면 `$scope.data`의 레퍼런스가 변경 될 때 리스너 함수가 호출
  - 리스너 함수는 인자로 새로운 값과 이전 값이 주어짐
  - 동등성 여부는 변경을 레퍼런스로 감지할 것인지 동등한 여부로 감지할 것인지 정할 떄 사용
  - 기본값은 false, 레퍼런스 변경시만 리스너 함수가 호출
  - 자세한건 추후에...

* $watchCollection(표현식, 리스너 함수)
  - 기본적으로 `$watch`와 같은 기능을 하며 대신 배열이나 객체에 대한 변경을 감지 할 때 사용.
  - 배열일 경우 새로운 배열 요소가 추가되거나 배열 요소들 사이의 순서가 변경되거나 배열 요소가 삭제될 때마다 리스너 함수가 호출
  - 객체일 경우 속성의 변경이 있을 때 마다 리스너 함수 호출

사실 사용을 안해보았으므로 이해하는 것이 한계가 좀 있다.

먼저 사용 시점 별로 묶어 보면

데이터 바인딩 처리 시 `$apply`, `$digest`, `$watch`, `$watchCollection`를 사용

사용자 정의 이벤트 처리 시 `$broadcast`, `$emit`, `$on`를 사용

`$eval`, `$evalAsync`는 표현식을 `$scope` 객체의 컨텍스트에서 계산할 때 사용

`$scope` 객체는 scope 타입의 인스턴스이므로 프로토타입 상속에 의해 위 메서드를 사용할 수 있다.

---

### $scope에서 사용자 정의 이벤트 처리

---

Angular 에서는 웹 애플리케이션에 애플리케이션 이벤트를 정의하고 이런 이벤트 처리를 할 수 있게 해준다.
이 과정들은 `$scope`를 이용해서 처리할 수 있고, 이 scope 객체에서 이벤트가 발생하길 듣고 있다가 처리한다.

이벤트를 발생시키는 API는 `$scope` 객체의 `$broadcast`와 `$emit` 메서드가 있다.

`$broadcast`는 자식 `$scope`에게 특정 이벤트의 이름으로 주어진 데이터와 함께 이벤트를 발생시킨다.

그리고 `$emit`은 반대로 부모 `$scope`에게 특정 이벤트의 이름으로 주어진 데이터와 함께 이벤트를 발생시킨다.

이렇게 `$broadcast`나 `$emit`으로 발생하는 이벤트는 `$on` 메서드로 해당 이벤트 리스너 함수를 등록한다.

첫번째 인자는 이벤트 객체고 두번째 인자는 전달되는 데이터다. 그럼 예제를 보도록 하자.

    <!DOCTYPE html>
    <html ng-app = "myApp">
      <head>
        <meta charset="utf-8" />
        <title>example 2.20</title>
        <style>
          .ng-scope { border: 1px solid red; padding: 5px; }
          .msg-list-area{ margin: 10px; height: 400px; border: 1px solid black;}
        </style>
      </head>
      <body ng-controller="mainCtrl">
        <input type="text" ng-model="noticeMsg" />
        <input type="button" value="공지 전송" ng-click="broadcast(noticeMsg)" />
        <div class="msg-list-area" ng-controller="chatMsgListCtrl">
          <ul>
            <li ng-repeat="msg in msgList track by $index">
              { {msg} }
            </li>
          </ul>
        </div>
        <div ng-controller="chatMsgInputCtrl">
          <input type='text' ng-model="newMsg" />
          <input type='button' value="전송" ng-click="submit(newMsg)" />
        </div>

        <!--angular file-->
        <script src="../angular.js" type="text/javascript"></script>
        <script type="text/javascript">

          var myApp = angular.module('myApp', []);

          myApp.controller('mainCtrl',['$scope', function($scope){
            $scope.broadcast = function(noticeMsg){
              console.log("broadcast")
              $scope.$broadcast("chat:noticeMsg", noticeMsg);
              $scope.noticeMsg = "";
            };
          }]);

          myApp.controller('chatMsgListCtrl',['$scope', '$rootScope', function($scope, $rootScope){
            $scope.msgList = [];

            $rootScope.$on("chat:newMsg", function(e, newMsg){
              console.log("on1")
              $scope.msgList.push(newMsg);
            });

            $scope.$on("chat:noticeMsg", function(e, noticeMsg){
              console.log("on2")
              $scope.msgList.push("[공지] " + noticeMsg);
            });

          }]);

          myApp.controller('chatMsgInputCtrl',['$scope', function($scope){
            $scope.submit = function(newMsg){
              console.log("submit")
              $scope.$emit("chat:newMsg", newMsg);
              $scope.newMsg = "";
            }
          }]);

        </script>
      </body>
    </html>

직접 작성을 하면서 비교를 해보는 것이 제일 좋다. `$rootScope`와 `$scope`의 연결에 있어서 차이를 한번 잘 보도록 하자.

`$broadcast`와 `$emit`의 차이와 각각이 `$on`으로 받을 때 어떤 스코프와 연결되는 지를 주의깊게 보면 좋을 듯하다.

또한 여기서 중요한 점은 각 컨트롤러가 서로 강력히 엮여있지 않다는 점이다.

이렇게 이벤트 기반으로 작성하였을 때, **각 영역의 기능을 수정하고 컨트롤러의 메서드를 수정해도 다른 영역에 영향을 주지 않는다.** 만약 공지 전송 컨트롤러 함수가 중앙 메시지 목록을 보여주는 화면에 해당하는 컨트롤러 함수의 특정 메서드를 직접 사용하다가 해당 메서드의 이름이 바뀌면 에러가 발생할 것이다. 하지만 이를 막을 수 있고 심지어 **새로운 화면 영역과 해당 컨트롤러 함수가 추가되더라도 이벤트만 적절히 처리하면 얼마든지 기존 영역을 수정하지 않고 웹 애플리케이션을 확장할 수 있다.**

---

### 모듈

---

모듈은 대체로 **관련된 기능을 하나로 묶어 다른 코드와 결합도를 줄이고 재사용성을 높이기 위해 사용** 한다.

모듈을 선언하는 것부터 보도록 하자.

`angular.module("모듈이름",["사용할 모듈, ... "])`

우리가 지금껏 써오던 선언을 한 번 보자.

`var myApp = angular.module('myApp', []);`

아마 똑같음을 느낄 것이다. 즉, 우리는 계속해서 모듈을 써왔고 예전에는 단순히 함수처럼 연결만 해서 컨트롤러를 썼지만(도서에도 그렇다.) 지금은 모듈을 선언해야만 연결할 수 있게 되었다.

`angular.module`함수를 사용해 모듈을 만들면 모듈 **인스턴스** 가 반환되는데 해당 모듈 인스턴스는 `컨트롤러`, `서비스`, `지시자`, `필터`들을 담는다.

모듈 인스턴스가 사용할 수 있는 메서드를 정리해 보자.

* Module.config(configFunction)
  - 모듈이 로딩될 때 호출되면 config 함수에 해당 익명 함수로 서비스를 설정할 수 있다.
* Module.contstant(name, object)
  - 모듈에서 사용되는 상수를 등록한다.
* Module.controller(name, constructor)
  - 모듈에서 사용되는 컨트롤러를 등록한다.
* Module.directive(name, directiveFactory)
  - 모듈에서 사용되는 지시자를 등록한다.
* Module.factory(name, providerFunction)
  - 모듈에서 사용되는 서비스를 팩토리 형태로 등록한다.
* Module.filter(name, filterFactory)
  - 모듈에서 사용되는 필터를 등록한다.
* Module.provider(name, providerType)
  - 모듈에서 사용되는 서비스를 제공하는 프로바이더를 등록한다.
* Module.run(initializationFn)
  - 애플리케이션 초기화 함수를 등록한다. 모든 모듈의 등록을 완료했을 때 초기화 함수가 실행된다.
* Module.service(name, construnctor)
  - 모듈에서 사용되는 서비스를 등록한다.
* Module.value(name, object)
  - 모듈에서 사용되는 객체를 등록한다.

모듈의 API를 보면 Angular에서 모듈의 의미를 어느정도 알 수 있다. 간단히 말하면 `컨트롤러`,`서비스`,`필터`,`지시자`를 담는 그릇정도라 생각된다.

하나의 AngularJS 웹 애플리케이션은 하나의 모듈을 지정할 수 있다.

자바의 메인 메서드처럼 `run` 함수를 이용해 애플리케이션 시작에 대한 로직을 작성 할 수 있다.

그리고 위에서 적어둔 것들을 애플리케이션에 등록할 수 있다.

---

### 모듈의 사용

---

우리는 이전부터 계속해서 모듈을 이용해 컨트롤러를 등록해 왔다. 따라서 여기서 예제를 딱히 보일 필요는 없어 보인다.

그 외에 다른 모듈들에 대해 알아보도록 하자.

먼저 모듈의 이름을 배열로 선언하는 것을 보도록 하자.(사실 예제에서 이미 해보았다.)

`angular.module("ngExam",['moduleA','moduleB'])`

위와 같이 `ngExam`을 선언 하면, 해당 모듈이 참조하는 `moduleA`, 와 `moduleB`를 선언하는 것이다.

사실 `ng-repeat`, `ng-select`와 같은 지시자와 곧 배워볼 `$http`, `$log`와 같은 서비스 모두 기본 모듈인 `ng`모듈에서 제공하는 것들이다. 그러나 기본 모듈 외에도 별도의 모듈을 제공한다. `ngMock`, `ngCookies`, `ngResource`,`ngSanitize`가 그러하다.

하나씩 써보도록 해보자.

    <!DOCTYPE html>
    <html ng-app = "cookieDemo">
      <head>
        <meta charset="utf-8" />
        <title>example 2.23</title>
      </head>
      <body ng-controller="mainCtrl">
        <h1>Cookie 서비스 사용</h1>
        <p>
          test 키로 저장된 값 : { {value} }
        </p>
        <button ng-click="getValue()">쿠키가져오기</button>
        <br />
        <input type='text' ng-model="iValue" /><button ng-click="putValue(iValue)">쿠키저장</button>
        <!--angular file-->
        <script src="../angular.js" type="text/javascript"></script>
        <script src="../angular-cookies.js" type="text/javascript"></script>
        <script type="text/javascript">

          angular.module('cookieDemo', ['ngCookies'])
            .controller("mainCtrl",['$scope','$cookies',function($scope, $cookies){

              $scope.value = ($cookies.test || "없음");
              $scope.getValue = function(){
                $scope.value = $cookies.test;
              };
              $scope.putValue = function(iV){
                $cookies.test = iV;
              }
            }]);

        </script>
      </body>
    </html>

위 예제는 도서에 있는 예제를 조금 고치게 되었다. 원래 `$cookieStore`이라는 모듈을 써서 구현했지만, 이 모듈은 버젼업에 따라 사라졌다. 따라서 비슷하게 쓸 수 있는 `$cookies`를 쓰게 되었고, 그에따라 문법을 조금 수정해서 쓰게 되었다.

여기서 `$cookies` 서비스를 사용하기 위해 컨트롤러 함수에 인자로 추가해주었는데, 이렇게 하면 AngularJS가 해당 모듈이 제공하는 서비스를 사용할 수 있게 해준다. **의존관계 주입** 이라고 하는데 지난번 도서에서 한번 다룬적은 있지만 이는 좀더 자세하게 나중에 배워보도록 하겠다.

모듈은 Angular에서 제공해주는 것 외에도 커스텀하게 만든 것들을 사용할 수 있다. 보통 `bootstrap` 을 많이 쓴다.

이는 부트스트랩을 angularJS 지시자로 만들어 제공한다.

---

### 파일 구조

---

Angular seed 파일을 받아서 한번 보면 구조가 다음과 같다.

    app/                    --> all of the source files for the application
      app.css               --> default stylesheet
      components/           --> all app specific modules
        version/              --> version related components
          version.js                 --> version module declaration and basic "version" value service
          version_test.js            --> "version" value service tests
          version-directive.js       --> custom directive that returns the current app version
          version-directive_test.js  --> version directive tests
          interpolate-filter.js      --> custom interpolation filter
          interpolate-filter_test.js --> interpolate filter tests
      view1/                --> the view1 view template and logic
        view1.html            --> the partial template
        view1.js              --> the controller logic
        view1_test.js         --> tests of the controller
      view2/                --> the view2 view template and logic
        view2.html            --> the partial template
        view2.js              --> the controller logic
        view2_test.js         --> tests of the controller
      app.js                --> main application module
      index.html            --> app layout file (the main html template file of the app)
      index-async.html      --> just like index.html, but loads js files asynchronously
    karma.conf.js         --> config file for running unit tests with Karma
    e2e-tests/            --> end-to-end tests
      protractor-conf.js    --> Protractor config file
      scenarios.js          --> end-to-end scenarios to be run by Protractor

이전과는 좀 많이 달라졌다고 볼수도 있다 도서를 기준으로 하면 `partial`과 같은 폴더도 있고, `lib` 폴더도 따로 만든다.

또한 `app.js` 파일 내부도 달라졌는데,

    angular.module('myApp', [
      'ngRoute',
      'myApp.view1',
      'myApp.view2',
      'myApp.version'
    ]).

와 같이 선언된 지금과 달리, 예전엔 다음과 같았다.

`angular.module("myApp",['myApp.filters', 'myApp.services', 'myApp.directives', 'myApp.controllers']).`

크게 달라진 것은 아니고 파일별로 모듈이 선언되어 있는 것이다.

달라졌다라고 느끼는 점이 드는 부분이 있는데, 완전히 기능적으로 분류했던 예전과 지금은 약간의 뷰 별로 나눈 느낌이 있다.

이전에 레이어별 분류를 보면,

`controllers`, `directives`, `filters`, `services` 와 같이 폴더를 나누어 각각에 알맞는 파일을 넣어둔다. 이렇게 레이어별로 관리하는 것에 대한 이점은 굳이 설명하지 않아도 될 것이라고 생각한다.

또한 기능별 분류가 있다.

하나의 웹 어플리케이션을 정의하는 방법은 다양하다. 상당히 많은 기능이 있고, 그것을 유지보수, 기능 확장과 같은 측면에서 크기가 클 수록 취약하다는 것은 자명하다. 여기서 Angular의 모듈을 이용해 논리적으로 기능별로 묶고 폴더를 이용해 물리적으로 기능을 분류하면 상당히 편리하게 변할 수 있다.

예를 들어 보자.

`angular.module('myApp', ['myApp.user', 'myApp.bookmark']);`

`angular.module('myApp.bookmark', ['myApp.bookmark.controller', 'myApp.bookmark.service', 'myApp.bookmark.filter', 'myApp.bookmark.directive']);`

`angular.module('myApp.user', ['myApp.user.controller', 'myApp.user.service', 'myApp.user.filter', 'myApp.user.directive']);`

가장 최 상위 모듈은 각각의 하위 모듈 2개를 참조하고, 각 기능별 모듈은 레이어별로 모듈을 참조한다.

위와 같이 기능별로 만든다면 폴더는 다음과 같을 것이다.

* bookmark
  - controllers
  - directives
  - filters
  - services
* user
  - controllers
  - directives
  - filters
  - services

이렇게 재사용 코드를 작성하는 건 상당히 까다롭다. 잦은 연습으로 할 수 있도록 해보자.

---

### 지시자의 모든 것

---

기존에 **DOM에 id 속성을 부여하거나 어느 DOM 아래에 있는 특정 class를 찾거나 하는 방식** 으로 자바스크립트에서 원하는 바를 선택해서 행동하는 방법을 취했다. 반면에 Angular에서는 **해당 DOM과 연결된 하나의 함수를 만들고 이 함수가 DOM을 조작하여 새로운 기능을 추가하는 행위** 를 할 수 있다.

바로 이 함수가 DOM 과 연결되는 **지시자 함수** 다. 지시자 함수는 연결된 특정 DOM에 `$scope`를 연결, 조작해서 특정 행위를 할 수 있다. 즉, 이걸 활용해서 HTML을 확장한다.

예제를 보면 쉽다.

`jQuery`에서 아코디언을 사용할 경우 다음과 같다.

`<div id='accordion'></div>`

`jQuery("#accordion").accordion({...});`

그러나 Angular에서는 부트스트랩시 템플릿을 읽을 때 accordion태그를 발견하면 해당 지시자 함수를 호출 해 DOM 기능을 추가한다

이 지시자 함수에서 이벤트 바인딩이나 데이터 바인딩을 처리하는데 아코디언 컴포넌트에 대한 속성이나 이벤트 처리에 대한 인터페이스로 HTML 태그를 이용한다.

`<accordion data="accordionItem">` 이라고 작성하면 컨트롤러의 scope에 있는 accordionItem이 해당 컴포넌트의 데이터로 주입되는 것이다.

이 후 지시자를 사용하는 방법은 다음 포스팅에서 알아보도록 하자.





앞서 적어둔 모든 소스는 [이곳](https://github.com/koocci/AngularJS-examples) 에서 보실 수 있습니다.
