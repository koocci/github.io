---
layout: post
title:  "[AngularJS] 시작하세요! AngularJS 3"
date:   2016-12-05 15:15:14 +0900
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
          <h1>부모 이름 : {{parent.name}}</h1>
          <div ng-controller="childCtrl">
            <h2>부모 이름 : {{parent.name}}</h2>
            <h2>자식 이름 : {{child.name}}</h2>
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



앞서 적어둔 모든 소스는 [이곳](https://github.com/koocci/AngularJS-examples) 에서 보실 수 있습니다.
