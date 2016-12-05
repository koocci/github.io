---
layout: post
title:  "[AngularJS] 시작하세요! AngularJS"
date:   2016-12-03 23:23:14 +0900
categories: AngularJS
tags: [Angularjs, 프로그래밍, MEAN stack, 기초, 블루프린트, IONIC]

---

# 시작하세요! AngularJS

---

![angular](http://farm8.static.flickr.com/7225/7399778412_0de724ac40_z.jpg)

이전과 내용이 바뀔 것이다.

이전 책을 도서관에서 빌려서 보았으나 버젼이 많이 바뀌어 더이상 진행하기가 힘들었다. 따라서 차라리 바이블 같은 책을 하나 빌려보자는 의미로 한가지 책을 빌렸다. **시작하세요! AngularJS 프로그래밍** -고재도 저- 라는 책인데 나온지는 꾀 되었지만 많이 보는 것 같았다. 그리고 현재 내가 재학중인 학교에 Angular 관련 도서를 찾아보았을 때, 나의 상황과 가장 알맞는 도서라는 생각이 들어 선택하게 되었다. (이전 책도 그렇게 골랐던 거지만, 단순히 실전위주라는 게 아직 나에게 무리한 요구 였구나 라는 생각이 든다.)

그래도 참 많은 걸 배웠다. Angular 만의 사이클이라던지, 어떤 방식으로 연결이 되는가에 대해 어느정도 감을 잡은 상태다. 이제 기초적인 내용으로 기반을 쌓고 진행해 가며, 프로젝트를 진행해 볼 생각이다.

그리고 블로그의 목적이 나의 배움의 장이자, 내가 아는 지식을 공유하는 형태였는 데 최근 공부만 하다보니, 이렇다할 결과물을 올린게 오래되었다. 따라서 이번 앵귤러 관련 공부가 끝나면 몇가지 프로젝트들을 올려볼 생각이다.

---

### 환경설정

---

이번 도서에는 내가 필요한 부분만 가져올 예정이다.

먼저, 해당 도서 역시 `yeoman` 을 이용한 스캐폴딩 으로 진행한다. 또한 `grunt` 와 `bower`를 이용해 진행한다. 해당 설치법은 따로 설명하지 않겠다.

혹시, 위에 들어둔 것들의 역할을 아직 모르겠다면 다음과 같이 생각하자.

`yeoman` : 스케폴딩. 즉 기반을 다져주는 것. 임시 가설물

`grunt` : Task Runner

`bower` : Package manager

그럼 프로젝트 구성으로 넘어가 보도록 하자.

---

### 프로젝트 구성

---

보통 프로젝트 구성을 Angular 샘플코드를 다운 받거나 직접 구성해볼 수 있다.

간단히 Angular 홈페이지에서도 다운 받을 수 있는데, (물론 bower로 다운받는 게 더 쉽다.) 그 내부를 한번 보려고 한다.

해당 다운 파일( (https://www.angularjs.org/)[https://www.angularjs.org/] 여기서 보면, ZIP 버젼) 을 열어 보면, 많은 파일이 있다. 여기서 \*.map 이라고 끝나는 파일을 압축된 파일을 크롬 인스펙터와 같은 **디버거** 에서 확인 할 수 있게 해주는 파일이다.

그 이외에 자바스크립트 파일은 다음과 같다.

* angular-animate
  - ngAnimate 모듈 사용에 필요. 애니메이션 관련 기능 제공
* angular-cookies
  - ngCookies 모듈 사용에 필요. $cookies, $cookeStore를 사용 할 수 있다.
* angular-loader
  - 비동기로 자바스크립트를 로드할 때 필요
* angular-mocks
  - 단위 테스트를 위한 가짜 코드(Mock)를 만들 때 필요
* angular-resource
  - ngResource 모듈 사용에 필요. $source 서비스 제공
* angular-route
  - ngRoute 모듈 사용에 필요. 라우팅과 관련된 기능을 제공
* angular-sanitize
  - ngSanitize 모듈 사용에 필요. HTML 코드에 불필요한 문자열 등을 제거할 때 사용
* angular-scenario
  - Scenario 테스트에 필요
* angular-touch
  - ngTouch 모듈 사용에 필요. 모바일에서 터치 이벤트를 감지하는 데 사용
* angular
  - ng 모듈 사용에 필요. 실제 AngularJS의 코어. 반드시 필요!

다음과 같다. 그런데 위 같은 사항이 지난 책에는 자세히 나오지 않았기에, 이 책을 통해 정리해 볼 기회가 생겼다.

사실, 아무 생각없이 만든다면 위 사항을 모른 채 다 집어넣고 만들기도 하지만, 이제 그럴 정도의 단계는 지났다고 생각이 된다.

---

### ToDo

---

간단히 ToDo 를 구현해 보자.

이미 많은 시행착오를 겪었으니, 간단히 만드는 것은 할 수 있을 것이다.

먼저 html 파일을 만들자.

    <!DOCTYPE html>
    <html>
      <head>
        <meta charset="utf-8" />
        <title>ToDo App Demo</title>
      </head>
      <body>
        <h1>AngularJS TODO App</h1>
      </body>
    </html>

간단히 만들었다. 이제 `트위터부트스트랩` 을 사용해 볼 것이다.

    <link rel="stylesheet" href="http://netdna.bootstrapcdn.com/bootstrap/3.1.1/css/bootstrap.min.css">
    <script src="http://netdna.bootstrapcdn.com/bootstrap/3.1.1/js/bootstrap.min.js">

위 소스를 넣어 준다.

이 후, `<body class="well">` 를 적용하면 배경이 약간 달라졌음이 느껴질 것이다.

아직 바로 Angular로 들어갈 것은 아니니 일단 한 번 정적인 페이지로 만들어 보자.

    <!DOCTYPE html>
    <html>
      <head>
        <meta charset="utf-8" />
        <title>ToDo App Demo</title>
      </head>
      <body class="well">
        <h1>AngularJS TODO App</h1>

        <p>
          전체 할 일 <string>2</string>개 / 남은 할일은 <string>1</string>개
          <a href="">보관하기</a>
        </p>

        <ul class="list-unstyled">
          <li class="checkbox">
            <input type="checkbox" />Angular 독서
          </li>
          <li class="checkbox">
            <input type="checkbox" />개인 프로젝트 구성
          </li>
        </ul>

        <form name="newItemForm" class="form-inline" action="">
          <div class="form-group">
            <label class="sr-only" for="newItemText">새로운 할 일</label>
            <input type="text" class="form-control" name="newItemText" placeholder="새로운 할 일" />
          </div>
          <button type="submit" class="btn btn-default">추가</button>
        </form>


        <!--twitter bootstrap-->
        <link rel="stylesheet" href="http://netdna.bootstrapcdn.com/bootstrap/3.1.1/css/bootstrap.min.css" />
        <script src="http://netdna.bootstrapcdn.com/bootstrap/3.1.1/js/bootstrap.min.js" ></script>
      </body>
    </html>

간단히 뷰가 보인다.

여기서 AngularJS를 한번 적용시켜 보자.
Angular 파일은 자기가 원하는 대로 지원하자.

      ...
      <body class="well" ng-controller="todoCtrl">
        <h1>{ {appName} }</h1>

        ...

        <ul class="list-unstyled">
          <li class="checkbox" ng-repeat="todo in todoList">
            <input type="checkbox" ng-model= "todo.done" />{ {todo.title} }
          </li>
        </ul>

        <form name="newItemForm" class="form-inline" action="">
          <div class="form-group">
            <label class="sr-only" for="newItemText">새로운 할 일</label>
            <input type="text" class="form-control" name="newItemText" placeholder="새로운 할 일" />
          </div>
          <button type="submit" class="btn btn-default">추가</button>
        </form>

        ...

        <script type="text/javascript">
          var todoList = [
            {
              done : true,
              title : "AngularJS 공부하기"
            },
            {
              done : false,
              title : "개인 프로젝트 구성"
            }
          ];
          var myApp = angular.module('myApp', []);

          myApp.controller('todoCtrl', ['$scope', function($scope) {
            $scope.appName = "AngularJS TODO APP";
            $scope.todoList = todoList;
          }]);

        </script>
      </body>
    </html>

조심해야 할 것이 하나 있다. Angular 버젼이 높아지면서 이전에는 되었던 단순히 컨트롤러 함수를 만들어서 넣어주는 것은 **더이상 되지 않는다.** 따라서 myApp으로 **모듈** 을 만들어 위와 같이 진행해야 한다.

그럼 계속 진행하려고 한다. 원래 위 스크립트 파일은 나눠주는 게 좋다. 그러나 기본적인 앱이니 간단히 가겠다.

여기서 이제 실제로 쓸 수 있게(DB는 붙이지 않았지만,) 입력도 할 수 있게 해보자.

    ...

      전체 할 일 <string>{ {todoList.length} }</string>개 / 남은 할일은 <string>{ {remain()} }</string>개
      <a href="" ng-click="archive()">보관하기</a>
    </p>

    ...

    <form name="newItemForm" class="form-inline" action="">
      <div class="form-group">
        <label class="sr-only" for="newItemText">새로운 할 일</label>
        <input type="text" class="form-control" name="newItemText" placeholder="새로운 할 일" ng-model = "newTodo"/>
      </div>
      <button type="button" class="btn btn-default" ng-click="save(newTodo)">추가</button>
    </form>

    ...

    <script type="text/javascript">
      var todoList = [
        {
          done : true,
          title : "AngularJS 공부하기"
        },
        {
          done : false,
          title : "개인 프로젝트 구성"
        }
      ];

      var myApp = angular.module('myApp', []);

      myApp.controller('todoCtrl', ['$scope', function($scope) {
        $scope.appName = "AngularJS TODO APP";
        $scope.todoList = todoList;

         $scope.save = function(newTodo){
          todoList.push({
            done : false,
            title : newTodo
          });

          $scope.newTodo = '';
        };

        $scope.archive = function(){
          for(var i = $scope.todoList.length - 1; i >= 0; i--){
            if($scope.todoList[i].done){
              $scope.todoList.splice(i, 1);
            }
          };
        };

        $scope.remain = function(){
          var remainCnt = 0;
          angular.forEach($scope.todoList, function(value, key){
            if(value.done == false){
              remainCnt++;
            }
          });
          return remainCnt;
        }

      }]);

      ...

여기까지 무난히 작성이 가능하다. 다만 조금 바뀐 게 있다면 `submit` 으로 버튼을 만들지 않고 `button` 으로 바꿨다는 것이다. submit으로 했을 때 아마 리프레시가 되면서 제대로 작동하지 않을 것이다. 이는 `event.preventDefault();` 로 막아줄 수 있지만, 지금은 해당사항을 구현하지 않았다.

굳이 한다면,

`<button type="submit" class="btn btn-default" ng-click="save($event,newTodo)">추가</button>`

    $scope.save = function($event,newTodo){
      event.preventDefault();
     todoList.push({
       done : false,
       title : newTodo
     });

     $scope.newTodo = '';
    };

위와 같이 될 것이다.

자 여기까지 ToDo 앱이 완료 되었다.

간단했다. 이미 이전에 작성해본 주소록 어플과 매우 유사했다. 이제 좀더 기초로 넘어가서 다져보도록 하자.

---

### 부트스트랩

---

**부트스트랩** 이라할 때 흔히 UI 라이브러리를 생각한다. 그러나 지금은 조금 다른 얘기를 해볼 것이다.(실상, 그 정의가 달라지진 않는다.)

보통 **그 자체의 동작에 의해서 어떤 소정의 상태로 이행하도록 설정된 방법** 이라는 의미다.

Angular에 적용해 본다면, **단순한 HTML 페이지를 웹 애플리케이션으로 동작하게 하기위한 프로세스** 가 존재하는데 이를 **AngularJS 부트스트랩** 이라 할 수 있다.

크게 2가지가 있다. `ng-app`, 그리고 `angular.bootstrap`

`ng-app`의 경우는 많이 접해 보았다. AngularJS 웹 애플리케이션의 **범위를 제한** 한다. 또한 **해당 노드가 루트노드가 되어 하위 노드들이 Angular 를 사용할 수 있게 한다.** 주의 할 점은 해당 페이지에 딱 **1번** 사용해야 하는 것이다.

위에 설명했지만 `ng-app` Angular 가 웹 애플리케이션을 부트스트랩 하게 한다. 그 순서도를 한 번 보도록 하자.

1.  AngularJS 스크립트가 실행된다.
2.  DOMContentLoaded 이벤트 발생
3.  document.readyState가 `complete`상태로 전환
4.  DOMContentLoaded 이벤트 발생
5.  HTML 페이지 읽으며 `ng-app` 속성을 찾음

위와 같다 그럼 `ng-app`을 찾은 이 후는 어떻게 될까?

1.  ng-app에 값으로 주어진 모듈을 로드한다.
2.  애플리케이션에 유일한 injector를 생성한다.
3.  ng-app 지시자가 적용된 정적 DOM을 루트로 하여 컴파일한다. 컴파일 시 $rootScope를 전달하고 이 후 정적 DOM에 Angular가 적용되어 동적 DOM이 되면 이를 브라우저가 렌더링하여 뷰가 만들어진다.

이제 순서도가 조금 눈에 들어올 것이다. 이 후 배울 (이미 예습이 되어 있는) 모듈 혹은 injector에 대해서도 전혀 모르고 들어갔던 지난번보다 배경지식이 쌓여 있는 상태다. 따라서 해당 순서도는 아마 몸으로도 느낄 수 있을 것이다.

그럼, 한가지가 더 남았다.

자바스크립트 API를 이용한 부트스트랩이다. `ng-app`의 경우 자동으로 부트스트랩이 됨을 알 수 있다. Angular 에선 이를 수동으로 할 수 있는 API를 제공해 주는데, 다음과 같다.

`angular.bootstrap(DOM 객체)`

예시를 보며 이해해 보도록 하자.

    <div id="app1">
      { { 1 + 2 } }
    </div>
    <div id="app2">
      { { 1 + 2 } }
    </div>

여기서 자바스크립트 파일을 다음과 같이 추가해 보자.

    <script>
      angular.element(document).ready(function(){
          angular.bootstrap(document.getElementById('app1'));
      });
    </script>

아마 `ng-app` 과 비슷한 효과가 `app1`에 일어남이 보일 것이다.

여기서 `ng-app`과 다른 점은 똑같이 app2에도 적용하면 둘다 적용이 된다는 점이다. `ng-app`은 한번 밖에 설정을 못하지만 bootstrap은 여러번 설정이 가능하다.

이 후 포스팅에서 템플릿과 데이터 바인딩 기초를 계속 진행해 가도록 하겠다.

앞서 적어둔 모든 소스는 [이곳](https://github.com/koocci/AngularJS-examples) 에서 보실 수 있습니다.
