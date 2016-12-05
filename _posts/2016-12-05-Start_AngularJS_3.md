---
layout: post
title:  "[AngularJS] 시작하세요! AngularJS 3"
date:   2016-12-05 15:15:14 +0900
categories: AngularJS
tags: [Angularjs, 프로그래밍, MEAN stack, 기초, 블루프린트, IONIC]

---

# 템플릿 & 지시자

---

![universe](http://farm9.static.flickr.com/8211/8279854121_bb59717e19_z.jpg)

이전에 템플릿과 다양한 지시자들에 대해 알아 보았다.

이제 체크박스, 셀렉트, 이벤트, 클래스 및 스타일 까지 하고 넘어가도록 하자.

체크박스는 다음과 같다.

`<input type="checkbox" ng-model="문자열" name="문자열" ng-true-value="문자열" ng-false-value="문자열" ng-required="true/false" ng-change="문자열">`

여기서 새로이 보는 것이 두가지 있다.

* ng-true-value
  - 체크박스를 체크했을 때 바인딩된 모델에 대입할 값 (기본값은 true)
* ng-false-value
  - 체크박스의 체크를 해제했을 때 바인딩 된 모델에 대입할 값(기본값은 false)

예제를 보도록 하자.

    <!DOCTYPE html>
    <html ng-app = "myApp">
      <head>
        <meta charset="utf-8" />
        <title>example 2.12</title>
      </head>
      <body>
        <form name="sampleForm" ng-init="value1 = true; value2 = '좋다';">
          선택 1 : <input type="checkbox" name="check1" ng-model="value1" />
          <br/>
          선택 2 : <input type="checkbox" name="check2" ng-model="value2" ng-true-value = "'좋다'" ng-false-value = "'싫다'" />
          <br/>
          <p>
            선택1의 바인딩된 값 : { {value1} }
          </p>
          <p>
            선택2의 바인딩된 값 : { {value2} }
          </p>
        </form>
        <!--angular file-->
        <script src="../angular.js" type="text/javascript"></script>
        <script type="text/javascript">

          var myApp = angular.module('myApp', []);

        </script>
      </body>
    </html>

실수하기 쉬운 것은 `ng-true-value`, `ng-false-value`  에 값을 넣을 때 따옴표를 넣어주어야 한다.(도서상으론 없지만 아무래도 구글링한 결과 해야 하는 것으로 보인다.)

그럼 `select`를 보도록 하자.

`<select ng-model="문자열" name="문자열" ng-options="별도의 표현식" ng-required="true/false">`

처음 보는 것은 `options` 일 것이다.

이는 옵션을 나타내기 위한 별도의 표현식이며, 다음과 같다.

* 배열이 데이터 일때
  - label for value in array
  - select as label for value in array
  - label group by for value in array
  - select as label group by group for value in array

* 객체 데이터 일때
  - label for (key, value) in object
  - select as label for (key, value) in object
  - label group by group for (key, value) in object
  - select as label group by group for (key, value) in object

`ng-options`는 위와 같이 `ng-repeat`처럼 반복적인 데이터를 위한 별도의 표현식을 제공한다.
`~for ~in`이 기본 구조이고 `as` 또는 `group by` 를 같이 사용한다. 그럼 해당 구성요소 설명을 보자.

* array/object
  - $scope에 있는 배열 또는 객체에 접근하는 표현식
* value
  - 배열 요소를 가리키는 내부변수 생성 표현식
* label
  - `option` 요소의 라벨이 될 표현식
* select
  - 부모인 `select` 요소에 모델로 바인딩되는 표현식
  - `select` 가 없을 때에는 value의 값이 기본적으로 select 값이 된다.
* group
  - `optgroup` 요소가 되는 표현식

잘 이해가 안될 수 있다 그럴땐 예제를 보자.

    <!DOCTYPE html>
    <html ng-app = "myApp">
      <head>
        <meta charset="utf-8" />
        <title>example 2.15</title>
      </head>
      <body>
        <div ng-init="countryList = [{name : '한국', code : 'ko', continent : '아시아'},{name : '일본', code : 'jr', continent : '아시아'},{name : '미국', code : 'en', continent : '북미'}]">
          <form name="sampleForm">
            <div>
              출발 국가 :
              <select ng-model="depCountry" ng-options="country.name for country in countryList" ng-required= "true">
                <option value="">
                  선택해 주세요.
                </option>
              </select>
            </div>
            <div>
              경유 국가 :
              <select ng-model="viaCountry" ng-options="country.name for country in countryList">
                <option value="">
                  선택해 주세요.
                </option>
              </select>
            </div>
            <div>
              도착 국가 :
              <select ng-model="arrCountry" ng-options="country.name group by country.continent for country in countryList" ng-required= "true">
                <option value="">
                  선택해 주세요.
                </option>
              </select>
            </div>
          </form>
          <div>
            <p>
              출발 국가 : { {depCountry.name} }
            </p>
            <p>
              경유 국가 : { {viaCountry.name} }
            </p>
            <p>
              도착 국가 : { {arrCountry.name} }
            </p>
          </div>
          <div ng-show="sampleForm.$invalid">
            출발 국가와 도착 국가는 필히 선택해 주세요
          </div>
        </div>

        <!--angular file-->
        <script src="../angular.js" type="text/javascript"></script>
        <script type="text/javascript">

          var myApp = angular.module('myApp', []);

        </script>
      </body>
    </html>

마치 데이터베이스 쿼리같은 느낌이다.

---

### css 연동

---

이번엔 css 클래스로 유효성 검증 결과를 표현해 보려 한다.

AngularJS는 **컨트롤 요소의 유효성 검증 결과를 요소의 css 클래스로 알아서 추가해준다.**

만약 텍스트 타입 입력 요소에 값이 주어지지 않으면 `ng-invalid` css 클래스를 해당 입력 요소에 추가한다.

그런데 값이 입력된다면 `ng-valid` 클래스를 추가한다.

이렇게 `ng-required`, `ng-pattern` 등은 유효성 검사를 위한 속성에 따라 css 클래스가 추가가 된다.

그럼 에시로 한번 보도록 하자.

    <!DOCTYPE html>
    <html ng-app = "myApp">
      <head>
        <meta charset="utf-8" />
        <title>example 2.16</title>
        <style type="text/css">
          .ng-invalid{
            border : 3px solid red;
          }
          .ng-valid{
            border : 3px solid green;
          }
          .ng-pristin{
            border-style: solid;
          }
          .ng-dirty{
            border-style: dashed;
          }
        </style>
      </head>
      <body>
        <form name="sampleForm" ng-init="name = '철수'">
          이름 : <input type="text" name="name" ng-model="name" ng-maxlength="3" ng-required="true" />
          핸드폰 번호 : <input type="text" name="tel" ng-model="tel" ng-pattern="/^\d{3}-|d{3,4}-|d{4}$/" />
        </form>

        <!--angular file-->
        <script src="../angular.js" type="text/javascript"></script>
        <script type="text/javascript">

          var myApp = angular.module('myApp', []);

        </script>
      </body>
    </html>

해당 사항에 대한 설명은 이전에 다 되었고 어떻게 변하는지 확인을 해보면 된다.

---

### 이벤트 템플릿

---

아마 ToDo 를 만들며 click을 다뤄본 것이 기억 날 것이다.

Angular는 그와 같이 자바스크립트를 사용하지 않고 이벤트 처리를 할 수 있게 도와준다.

일반적으로, `ng-click`이외에 `마우스 오버`, `마우스 엔터`, `키프레스`등 다양하게 지원한다.

* ng-click
* ng-dbclick
* ng-keydown
* ng-keypress
* ng-keyup
* ng-mousedown
* ng-mouseenter
* ng-mouseleave
* ng-mousemove
* ng-mouseover
* ng-mouseup
* ng-change
  - `input`, `textarea` 요소에서 사용한다. 값이 변경됬을 때 표현식이 계산된다.
* ng-blur
  - `input`, `textarea`, `a` 요소에서 사용한다. 개체가 포커스를 잃었을 때 표현식이 계산된다.

따로 설명이 적혀있지 않은 지시자는 모든 태그에 사용 가능하다.

사용법은 간단하다

    <any ng-이벤트명="표현식">
    ...
    </any>

예제를 한번 보자.

    <!DOCTYPE html>
    <html ng-app = "myApp">
      <head>
        <meta charset="utf-8" />
        <title>example 2.17</title>
        <style type="text/css">
          .box{
            width: 100px;
            height: 60px;
            margin: 10px;
            background-color: black;
            color: white;
            text-align: center;
            padding-top: 40px;
          }
        </style>
      </head>
      <body ng-controller="mainCtrl">
        <div>
          <div class='box' ng-click="handleEvt('박스가 클릭됬다.')">
            click
          </div>
          <div class='box' ng-mousedown="handleEvt('박스 마우스 다운')">
            mousedown
          </div>
          <div class='box' ng-mouseenter="handleEvt('박스 마우스 엔터')">
            mouseenter
          </div>
          <div class='box' ng-mousemove="handleEvt('박스 마우스 무브')">
            mousemove
          </div>
          change : <input type="text" ng-model="inputText" ng-change="handleEvt('입력값 변경')" />
          keydown : <input type="text" ng-model="inputText2" ng-keydown="handleEvt($event.keyCode+'키보드 눌러짐')" />
        </div>
        <div>
          <p>
            { {message} } { {eventCnt} }
          </p>
        </div>

        <!--angular file-->
        <script src="../angular.js" type="text/javascript"></script>
        <script type="text/javascript">

          var myApp = angular.module('myApp', []);

          myApp.controller("mainCtrl", ['$scope', function($scope){
            $scope.message="";
            $scope.eventCnt = 0;
            $scope.handleEvt = function(message){
              $scope.message = message;
              $scope.eventCnt++;
            }
          }]);
        </script>
      </body>
    </html>

---

### 클래스/ 스타일 동적 처리

---

이제 마지막으로 볼 차례다.

개발을 하다보면, 큳번 간롼네거 css클래스를 동적으로 처리해야 할 때가 있다.
그럴 때 `jquery`라면 `addclass`나 `removeclass`를 사용헀을 것이지만, Angular는 지시자가 따로 있다.

    <any ng-class="표현식">
    </any>

    혹은

    <any class="ng-class: '표현식';">
    </any>

아마 예제를 보면 직관적으로 유추가 가능할 것이다.

    <!DOCTYPE html>
    <html ng-app = "myApp">
      <head>
        <meta charset="utf-8" />
        <title>example 2.17</title>
        <style type="text/css">
          .apple{
            background-color: red;
          }
          .lemon{
            background-color: yellow;
          }
          .even{
            background-color: blue;
          }
        </style>
      </head>
      <body>
        <div ng-init="fruitList = ['apple','banana','lemon','grape']">
          <ul>
            <li ng-repeat="fruit in fruitList" ng-class="'{ {fruit} }'">
              { {fruit} }
            </li>
          </ul>
          <ul>
            <li ng-repeat="fruit in fruitList" ng-class="{'even': { {$index % 2 != 0} } }">
              { {fruit} }
            </li>
          </ul>
        </div>
        <!--angular file-->
        <script src="../angular.js" type="text/javascript"></script>
        <script type="text/javascript">

          var myApp = angular.module('myApp', []);

        </script>
      </body>
    </html>

여기서 틀릴 수 있는 것은 밑의 `ng-class`의 경우는 따옴표를 붙이지 않지만 위에는 붙여야만 한다는 것이다.

그럼 `ng-style`을 보도록 하자.

사용법 자체는 위와 똑같으므로 생략하겠다.

    <!DOCTYPE html>
    <html ng-app = "myApp">
      <head>
        <meta charset="utf-8" />
        <title>example 2.17</title>
      </head>
      <body ng-controller="myCtrl">
        <div>
          <div ng-style="bgStyle">
            { {bgStyle.backgroundColor} }
            <button ng-click="changeColor('yellow')">색 변경</button>
          </div>
        </div>
        <!--angular file-->
        <script src="../angular.js" type="text/javascript"></script>
        <script type="text/javascript">

          var myApp = angular.module('myApp', []);
          myApp.controller('myCtrl',['$scope', function($scope){
            $scope.bgStyle = {
              backgroundColor: 'red'
            }
            $scope.changeColor = function(color){
              $scope.bgStyle.backgroundColor = color;
            }
          }]);
        </script>
      </body>
    </html>

이제 대부분의 템플릿을 동적으로 컨트롤 하는 법을 알아보았다. 이외의 것들은 문서를 참고하거나 개인적으로 사용할 떄 찾아보며 사용하면 될 듯하다.

---

### MVC - 모델, 뷰, 컨트롤러

---

![universe](http://farm9.static.flickr.com/8106/8523093518_d11af25fa6_z.jpg)

jQuery로 웹, 어플을 만들어 보면서 가장 힘들었던 것은 적용하기 힘든 재사용성과 뷰인지 데이터인지 뒤죽박죽 섞이게 만들어지는 스파게티 코드였다.

마음에 드는 코드를 짜는 건 너무 힘든 과정이였고 그에 따라 유지보수 비용이 발생하는 건 당연했다.

`이거 고치려면 거의 처음부터 다시 짜다 싶이 해야하는데요` 라는 가장 해선 안되는 변명이 나오게 된다.

이런 코드들을 풀어버리기 위해 많은 프레임워크들이 나왔었는데 그중 MVC 패턴을 지원하는 것들이 바로 그러하다.

Angular 역시 그러하지만 이전의 **MVC** 와는 조금 다르고 **MVVM(Model-View-View-Model)** 와 비슷하지만 독자적인 방식으로 MVC를 구현했다.

사실 처음엔 MVC 패턴에 가까웠지만 버젼이 올라가면서 MVVM에 가까워졌고, 의견이 다분하지만 어느 패턴으로 정하지 않고 사람 마음대로 정하라는 뜻에서 **MVW(Model-View-Whatever)** 이라고 칭하였다.

그렇다고 너무 어려워 할 것은 아니고 MVC 패턴을 알고 있다면 인터페이스나 데이터, 애플리케이션 로직을 분리하는 개념은 같으므로 비슷하게 이해하고 있으면 될 듯 하다.

* 모델(Model)
  - 도메인에 해당하는 정보를 나타내는 오브젝트
  - 대체로 애플리케이션의 데이터와 행위를 포함
* 뷰(View)
  - 모델의 정보를 UI에서 보여주는 역할
  - 하나의 모델을 다양한 뷰에서 사용할 수 있고, 여러 모델을 하나의 뷰에서 사용할 수 있다.
* 컨트롤러(Controller)
  - 애플리케이션에서 사용자의 입력을 받아 모델에 변경된 상태를 반영
  - 모델이 변하게 하여 결국 뷰를 갱신
  - 직접 뷰를 변경하는 것이 아니라 주요 로직이 모델을 변경하고 그 결과가 뷰로 나타나는 것

이렇게 MVC로 하면 개발과 유지보수에 몇가지 이점이 생긴다.

1.  사용자 인터페이스와 비즈니스 데이터 분리
  - 비즈니스 데이터에 해당하는 모델을 다른 뷰에서도 사용하여 모델을 재사용할 수 있게 한다.
2.  MVC 패턴으로 개발함으로써 팀 사이에 표준화된 개발 방식을 제공
  - 제각기 개발하기 쉬운 자바스크립트 개발 환경에서 표준화된 개발 환경을 제시하는 이점

그럼 하나하나 보도록 하자.

---

### 모델

---

하나의 엔터티나 여러 개의 엔터티는 모델이 된다. 그러나 angular 에서는 모델 정의에 있어서의 차이점이 있다. 보통은 기본 모델 클래스가 있고 개별 모델 클래스가 상속을 받지만, angular는 별다른 상속없이 순수 **자바스크립트 객체** 가 모델이 된다.

그러나 중요한 것은 모델 객체는 `$scope` 객체로부터 접근할 수 있어야 한다는 점이다.

우리는 이미 많은 경우에 있어서 모델을 선언해왔다. 컨트롤러 내부에 선언하기도 하고 템플릿에 선언하기도 했다.

우리가 `ng-init` 이 후에 적은 내용들은 모두 템플릿에서 선언한 모델이고, 컨트롤러 내부에 `$scope.something`같은 경우, 모두 모델을 선언한 예시 이다.

또한 간접적으로 `ng-repeat`의 경우, `book in bookList`과 같이 만들어지기도 한다.

`<input type='text' ng-model='search'>`

의 경우에서는 `ng-model`속성에 search 값을 대입한다.

Angular에서는 `ng-model` 지시자를 사용하면 해당 모델이 `$scope`에 없을 경우 암묵적으로 `$scope`에 search 속성을 만들고, `input` 태그 값을 search 속성의 값으로 대입한다.

즉, **모델을 만들고 데이터를 연결한다.**

아까 설명 했지만 `ng-repeat`의 경우도 재각각의 배열 요소만큼의 `DOM`을 생성하고 $scope가 연결되어 만들어 진다.

---

### 뷰

---

뷰는 문서 객체 모델이다. 브라우저에서 HTML 문서를 읽고 DOM을 생성하는데, Angular에서는 이 **DOM** 이 뷰가 된다.

템플릿과 뷰를 혼동할 경우가 있다. Angular는 HTML문서가 템플릿이고 이 템플릿을 Angular가 읽어서 뷰를 생성한다. 과정을 보도록 하자.

1.  HTML로 작성한 템플릿을 브라우저가 읽는다.
2.  브라우저는 문서 객체 모델을 생성한다.
3.  angular.js 파일이 실행되어 angular 소스가 실행된다.
4.  DOM 생성 시 DOM Content Loaded 이벤트가 발생하는데 AngularJS가 이 때 생성된 정적 DOM을 읽고 뷰를 컴파일 한다. 컴파일 시 확장 태그나 속성을 읽고 처리한 후 데이터를 바인딩한다.
5.  컴파일이 완료하면 동적 DOM, 즉 뷰가 생성된다.

---

### 컨트롤러

---

사실 컨트롤러는 그리 많은 일을 하는 것은 아니다. 단지 하나의 역할 이라고도 볼 수 있는데, **애플리케이션의 로직** 을 담당한다.

즉, **모델의 상태를 정의, 변경** 한다.

결국 쉽게 말해 `$scope`객체에 데이터나 행위를 선언하는 것이다. 그리고 <del>컨트롤러는 인자로 `$scope`를 전달받는 단순한 자바스크립트 함수다.</del>

여기서 사실, 이전의 Angular의 경우라면 위 말이 맞다. 함수를 선언하듯 컨트롤러를 선언해서 사용해 왔다. 그러나 지금은 모듈을 선언하고 컨트롤러를 해당모듈에 연결지어 다르게 선언하는 것이 보통이므로 개인적인 생각으론 딱 맞는 설명은 아니라고 생각한다.

다만 주의해야 할 점이 있다. 컨트롤러는 **단 하나의 뷰에 해당하는 애플리케이션의 로직만을 담당** 해야 한다. 화면상의 로직이 아니라 **애플리케이션의 비즈니스 로직** 이다.

이 말은 DOM을 조작하는 행우와 같은 화면 상의 로직은 지시자에서 구현을 하고, 컨트롤러는 단순히 비즈니스 로직을 해야 한다는 말이다.

예시를 들면 `$("ul").add("<li .... ")` 와 같이 DOM을 조작해서는 안된다.

그러나 하나의 화면에 여러 컨트롤러를 작성할 수 있다. 하나의 화면은 사실 여러 뷰의 조합이기 때문이다.(Ajax와 비슷한 개념이라고 생각된다.)

또한 하나의 컨트롤러에 하나의 $scope만을 가지게 된다. 또한 $rootScope가 있다.

그러나 한 화면에 여러 컨트롤러가 있게 되면 각자 독립된 scope이므로 서로간의 연결을 하기가 힘들다. 이러한 점은 추후에 배울 서비스로 해결이 가능하다.

이제 다음 포스팅 부터는 `rootScope`에 대한 얘기부터 진행해 보도록 하자.

앞서 적어둔 모든 소스는 [이곳](https://github.com/koocci/AngularJS-examples) 에서 보실 수 있습니다.
