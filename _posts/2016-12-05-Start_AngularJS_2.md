---
layout: post
title:  "[AngularJS] 시작하세요! AngularJS 2"
date:   2016-12-05 09:12:14 +0900
categories: AngularJS
tags: [Angularjs, 프로그래밍, MEAN stack, 기초, 블루프린트, IONIC]

---

# 템플릿과 데이터 바인딩

---

![angular](http://farm4.static.flickr.com/3250/3044217300_aacac393d7_z.jpg)

우리는 다시 Angular에 대한 기초부터 다져보고 있다.

좋은 코드는 **재사용성** 이 높아야 한다. 앵귤러는 **바인딩** 을 통해 프론트앤드와 백앤드를 나누어 재사용성을 늘려줄 수 있다. 즉, 데이터와 화면을 분리하는 것이 필수적이다. 그리고 유기적인 Sync가 필요한데 이 부분이 이전에는 상당히 힘들었다.(스파게티 소스가 되기 쉬웠다.)

Angular는 여기서 템플릿 시스템과 데이터 바인딩을 이용해 해결해준다.

먼저 템플릿을 이해해보도록 하자. **JSP** 를 생각해보면 서버측 언어를 이용해 화면의 변화를 이루게 해준다. 그러나 브라우저 호환성이나 DOM API가 다른 문제점이 많았다. 이것을 해결해 주던 것이 **jQuery** 였다.

그러나 jQuery에도 문제점이 있었는데, **유지보수** 와 **확장성** 이다.

애플리케이션의 크기가 커질수록 DOM에 적용사항은 많아지고 코드는 길어진다.

여기서 템플릿이 사용되며 해당사항을 해결해 주었다. 그럼 Angular는 템플릿을 어떻게 사용하고 있는지 보자.

먼저, Angular는 **템플릿이 HTML 그 자체다.** DOM 자체를 템플릿으로 사용하게 된다.

이전 ToDo 어플에서도 만들어 보았지만 `ng-init`을 이용해 데이터를 주면 자바스크립트 코드가 하나도 없더라도 템플릿 적용이 가능하다.

jQUery를 사용할 때에는 해당 DOM을 다시 body에 삽입하는 등의 적용이 필요했지만, Angular는 DOM 자체가 템플릿이므로 따로 함수호출할 필요도 없고 특정 DOM을 삽입하지 않아도 된다.

그럼 HTML이 템플릿 그 자체인데 무엇을 추가해야 Angular 템플릿이 되는 것일까?

그럼 템플릿 작성시의 Angular 기능을 알아보자.

* 지시자
  - 기본 HTML을 확장 혹은 새로 추가한 요소나 속성이다. 우리는 `ng-app`, `ng-repeat`등을 이미 사용해 보았고 사용자가 만든 재사용할 수 있는 위젯과 같은 지시자도 여기에 해당한다.
* 마크업
  - 기본 HTML 마크업과 이중 중괄호
* 필터
  - 사용자에게 보여주는 데이터의 형식을 필터 처리한다.
* 폼 컨트롤
  - 입력 상자의 유효성 검사를 위해 Angular가 폼 태그를 확장했다. 폼 태그를 사용하면 자동으로 폼 컨트롤을 사용한다.

이런 기능을 사용하면 HTML의 선언적 언어의 중요함을 간직한 채 웹 애플리케이션 제작을 도와준다.

---

### 이중 중괄호

---

기본부터 보자. 이중 중괄호를 아마 꾸준히 써왔던 것을 알 수 있다. 크게 자바스크립트와 차이점은 크게 없지만 한번 정리해보면

* 객체의 접근
  - 자바스크립트는 기본적으로 `window`객체 안에서 찾지만 Angular는 `scope`안에서 찾는다.
* undefined, null 무시
  - 자바스크립트에서는 선언이 없을시 undefined 가 뜨고 에러가 나오지만 Angular는 무시해버린다.
* 제어문이 작성 안됨
  - if문, Loop, throw 문이 되지 않는다.
* 필터
  - Angular는 필터를 표현식에서 사용할 수 있다. 예를 들어 금액을 표시하고 싶을 때 필터를 써서 앞에 달러 표시를 붙여줄 수 있다.

예제를 하나 보도록 하자.

    <!DOCTYPE html>
    <html ng-app = "myApp">
      <head>
        <meta charset="utf-8" />
        <title>example 2.5</title>
      </head>
      <body ng-init="person = {name : '재도', favorite : ['사과', '딸기', '포도']}">
        <h1>Hello { {person.name} }</h1>
        <p>
          좋아하는 과일의 갯수 :
          { {numOfFavorite = person.favorite.length} }
        </p>
        <p>
          과일 갯수 * $100 = { {numOfFavorite * 100 | currency} }
        </p>
        <p>
          이름이 재도 인가요? { {person.name == "재도"} }
        </p>
        <p>
          좋아하는 과일 수가 4개보다 많나요? { {numOfFavorite > 4} }
        </p>
        <p>
          scope에 없는 객체에 접근하면? { {car.type.name} }
        </p>
        <!--angular file-->
        <script src="../angular.js" type="text/javascript"></script>
        <script type="text/javascript">

          var myApp = angular.module('myApp', []);

        </script>
      </body>
    </html>

간단히 설명한 사항들을 한번 정리해 보았다.

직관적으로 알 수 있을 것이다.

---

### 데이터 바인딩

---

많은 프레임워크들이 데이터 바인딩을 지원하지만 Angular는 **양방향 데이터 바인딩** 을 지원한다.

단방향은 데이터와 템플릿을 결합해서 화면을 생성한다면, 양방향은 **데이터의 변화를 감지** 해 템플릿과 결합하여 화면을 갱신하고 **화면에서의 입력에 따라 데이터를 갱신** 한다.

이는 ToDo 어플을 만들면서 알 수 있었다.

그럼 제작시 썼던 지시자들을 떠올려보자

* ng-controller
* ng-repeat
* ng-model
* ng-click

위 4개를 썼던 기억이 있을 것이다.

아마 간단한 활용정도는 할 수 있을 것이다.

---

### 지시자 정리

---

지시자의 종류는 다양하다. 항상 느끼지만 이런 부분에 있어서는 나 개인적으로는 외우지 않는다. 무엇이 있는지만 알면 찾아보고 사용할 수 있으면 된다.

먼저 반복 지시자를 보자.

위 예시에도 있듯이 `ng-repeat` 이다.

여기서 우리는 `<any ng-repeat "variable in expression">` 과 같이 사용했다.

몇가지 방법이 더 있는데,

`<any ng-repeat="(key 변수명, value 변수명) in 표현식">`

`<any ng-repeat="변수명 in 표현식 track by 표현식">`

이 있다.

아마 위의 방법은 직관적으로 알 수 있는데 밑은 조금 애매할 수 있다. 이는 책에 나오는 내용을 그대로 적어 두겠다.

     배열요소와 생성되는 DOM 요소를 연결할 때 사용하는 고유한 값을 지정하는 것이다. Track by를 별도로 작성하지 않으면 AngularJS는 동일하지 않은 값에 $$hashKey 속성을 추가하여 DOM 요소와 연결 할 떄 사용한다. 그리고 var items = [1,1]; 과 같은 동일한 값을 ng-repeat으로 표현하려고 하면 item in item track by $index로 $index에 의해 DOM 요소돠 연결되게 해야 한다. Track by를 이용해 고유한 속성값을 지정하면 무의미한 DOM 렌더링을 막을 수 있다. 그렇지 않으면 매번 다른 $$hashKey를 생성해서 그때마다 매번 DOM을 변경하기 때문이다.

`ng-repeat`를 적용한 html 요소는 배열 요소의 갯수만큼 HTML 요소를 생성한다. 여기서 각 요소는 별도의 `scope`가 생기게 된다. 여기서 특별한 속성이 제공되는데 후에 자세히 다룰 것이지만 `ng-repeat`에 대해서 한번 정리해보면

* $index
  -  배열 요소의 인덱스.(0 ~ length - 1)
* $first
  - 배열 요소의 첫번째 값이면 true, 아니면 false
* $middle
  - 첫번째와 마지막이 아니면 true
* $last
  - 배열 요소의 마지막이면 true
* $even
  - 인덱스가 짝수면 true
* $odd
  - 인덱스가 홀수면 true

사용은 간단히 `{ { $index } }` 와 같이 적어준다면 사용이 가능하다.

다음 예제를 참고하길 바란다.

    <!DOCTYPE html>
    <html ng-app = "myApp">
      <head>
        <meta charset="utf-8" />
        <title>example 2.8</title>
      </head>
      <body>
        <div  ng-init="customerList = [{name : '영희', age : 25}, {name : '순희', age : 28}]">
          <ul>
            <li ng-repeat="customer in customerList">
              [{ {$index + 1} }] 고객 이름 : { {customer.name} }, 고객 나이 : { {customer.age} }
            </li>
          </ul>
        </div>
        <div ng-init="myFriend = {name : '철수', age : 25, hobby : '축구'}">
          내 친구 소개
          <ul>
            <li ng-repeat="(attr, value) in myFriend">
              <p>
                { {attr} } : { {value} }
              </p>
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

지금까지 배운 것들이 잘 정리되어 있음을 알 수 있다.

---

### 조건 지시자

---

조건문은 코딩에 있어서 필수적으로 사용하게 된다. 조건에 따라 템플릿 작성을 달리하고 싶을 때가 있는데, 그럴때 보통 자바스크립트의 if문 혹은 switch 문과 비슷하게 쓸 수 있는 것이 있다.

`ng-switch`, `ng-if`가 그렇고 비슷한 지시자로 `ng-show`, `ng-hide` 지시자가 있다. 이 둘응 display를 제한하는 지시자다.

먼저 사용법부터 보도록 하자.

    <any ng-switch="표현식">
      <any ng-switch-when="조건 일치 값1"> ... </any>
      <any ng-switch-when="조건 일치 값2"> ... </any>
      ...
      <any ng-switch-default> ... </any>
    </any>

여기서 `ng-swith`는 `ng-switch on`으로 써도 같은 구문이다.

역시 예제를 보며 이해해보도록 하자.

    <!DOCTYPE html>
    <html ng-app = "myApp">
      <head>
        <meta charset="utf-8" />
        <title>example 2.9</title>
        <style type="text/css">
          .box{
            width: 100px;
            height: 100px;
          }
          .red{
            background-color: red;
          }
          .green{
            background-color: green;
          }
          .blue{
            background-color: blue;
          }
          .black{
            background-color: black;
          }
        </style>
      </head>
      <body>
        <div>
          <input type="radio" ng-model="color" value="red" > 빨강 </input>
          <input type="radio" ng-model="color" value="green" > 초록 </input>
          <input type="radio" ng-model="color" value="blue" > 파랑 </input>

          <div ng-switch on="color">
            <div ng-switch-when="red" class="box red"></div>
            <div ng-switch-when="green" class="box green"></div>
            <div ng-switch-when="blue" class="box blue"></div>
            <div ng-switch-default class="box black"></div>
          </div>

        </div>

        <!--angular file-->
        <script src="../angular.js" type="text/javascript"></script>
        <script type="text/javascript">

          var myApp = angular.module('myApp', []);

        </script>
      </body>
    </html>

같은 문장을 3번 반복해서 하되, 각각의 클래스를 달리하며 색을 바꾸어 준다. 직관적으로 알 수 있다.

그럼 `ng-if`에 대해 알아보자

    <any ng-if="표현식">
    ...
    </any>

위와 같이 사용할 수 있으며, 참과 거짓 여부에 따라 해당 요소를 없애거나 생성한다.

이보다 더 자주 쓰는 것이 있는데 바로 `ng-show`, `ng-hide` 지시자 이다.

차이점이라면 `ng-show`, `ng-hide`는 css의 display 속성을 조절해서 화면을 컨트롤 한다면, `ng-if`는 아예 없애버리는 것이다.

이 역시 예제를 보도록 하자.

    <!DOCTYPE html>
    <html ng-app = "myApp">
      <head>
        <meta charset="utf-8" />
        <title>example 2.10</title>
      </head>
      <body>
        약관의 동의 : <input type="checkbox" ng-model="checked" ng-init="checked=false" />
        <br />
        동의하면 다음으로 진행됩니다.

        <button ng-if="checked">다음</button>

        <!--angular file-->
        <script src="../angular.js" type="text/javascript"></script>
        <script type="text/javascript">

          var myApp = angular.module('myApp', []);

        </script>
      </body>
    </html>

그럼 `ng-show`, `ng-hide` 를 보도록 하자.

    <any ng-show="표현식">
    ...
    </any>
    <any ng-hide="표현식">
    ...
    </any>

이는 숨기거나 보이게 하는 용도이므로, 예제를 잘 보도록 하자.

    <!DOCTYPE html>
    <html ng-app = "myApp">
      <head>
        <meta charset="utf-8" />
        <title>example 2.11</title>
      </head>
      <body>
        약관의 동의 여부 : <input type="checkbox" ng-model="checked" ng-init="checked=false" />
        <br />
        <div>
          <span ng-show="checked">
            다음으로 진행됩니다.
            <button>다음</button>
          </span>
        </div>
        <div>
          <span ng-hide="checked">
            다음으로 진행할 수 없습니다.
          </span>
        </div>

        <!--angular file-->
        <script src="../angular.js" type="text/javascript"></script>
        <script type="text/javascript">

          var myApp = angular.module('myApp', []);

        </script>
      </body>
    </html>


헤깔릴 수도 있는 부분은 둘다 참일 때 해당사항이 진행이 된다는 것이므로, 같은 값을 넣어주면 된다.

---

### 컨트롤러 지시자

---

![angular](http://farm3.static.flickr.com/2839/11648639246_3ff8e48a7a_z.jpg)

아마 가장 많이 쓰고 중요한 **컨트롤러 지시자** 를 해볼 차례다.

controller는 템플릿의 특정 부분을 처리하는 자바스크립트 함수를 선언할 수 있게 한다.

단순히 데이터를 보여주는 것은 템플릿을 쓰면 되지만, **데이터를 가공하거나 서버에 데이터를 저장하고 불러오는 애플리케이션 로직 코드는 자바스크립트로 작성해야 한다.**

    <any ng-controller="표현식">
    ...
    </any>

작성법은 매우 간단하다. 여기서 표현식은 전역적으로 접근 할 수 있는 자바스크립트 함수의 이름이거나 모듈로 등록된 컨트롤러 함수 이름(추후에 모듈에 대해 더 알아볼 것이다)이거나 현재 scope에서 접근할 수 있는 함수의 이름이다.

이 역시 예제로 알아보자.

    <!DOCTYPE html>
    <html ng-app = "myApp">
      <head>
        <meta charset="utf-8" />
        <title>example 2.12</title>
      </head>
      <body ng-controller="myCtrl">
        <div>
          고객 목록
            <ul>
              <li ng-repeat="customer in customerList">
                [{ {$index + 1} }] 고객 이름 : { {customer.name} }, 고객 나이 : { {customer.age} }
              </li>
            </ul>
        </div>
        <div>
          고객 목록
            <ul>
              <li ng-repeat="youngCustomer in youngCustomerList">
                [{ {$index + 1} }] 고객 이름 : { {youngCustomer.name} }, 고객 나이 : { {youngCustomer.age} }
              </li>
            </ul>
        </div>


        <!--angular file-->
        <script src="../angular.js" type="text/javascript"></script>
        <script type="text/javascript">

          var myApp = angular.module('myApp', []);
          myApp.controller('myCtrl', ['$scope', function($scope) {
            var customerList = [{name : '영희', age : 10}, {name : '순희', age : 28}];
            var youngCustomerList = [];

            angular.forEach(customerList, function(value, key){
              if(value.age < 25){
                youngCustomerList.push(value);
              }
            });
            $scope.customerList = customerList;
            $scope.youngCustomerList = youngCustomerList;
          }]);
        </script>
      </body>
    </html>


이전에도 말했지만 예전 버전은 controller에 해당하는 함수만 만들어 넣어줄 수 있었지만 지금은 위와 같이 구현을 해야 진행이 된다.

좀더 자세한 컨트롤러 애기는 나중에 하도록 하자.

---

### 폼/입력 지시자

---

이제 데이터를 주고받기 위해 필요한 html의 `form` 태그를 알아보도록 하자.

자식요소가 다양한데 간단히 기억나는 것만 적어보아도 `input`, `select`, `textarea`등이 있다. 그 중에 폼 양식을 서버로 제출하기 전에 사용자가 값을 검증해야 할 때가 있다.

이런 유효한 값이 채워졌는지 검사하는 걸 `폼 양식 유호성 검증(Form Validation)` 이라고 하는데, 이런 지시자를 Angular는 제공한다.

먼저 텍스트 부터 알아보자.

`<input type="text" ng-model="문자열" name="문자열" ng-required="문자열" ng-minlength="숫자" ng-maxlength="숫자" ng-pattern="문자열" ng-change="문자열">`

설명을 하지 않아도 될 듯 하지만 그래도 적어보겠다.

* ng-model
  - 바인딩 대상
* name
  - 폼에서 사용될 이름
* ng-required
  - 필수 입력 여부
* ng-minlength
  - 입력박스에 입력되는 값의 최소 글자수
* ng-maxlength
  - 입력박스에 입력되는 값의 최대 글자수
* ng-pattern
  - 입력된 값과 비교될 정규표현식
* ng-change
  - 사용자의 입력이 발생할 때 실행될 표현식

그럼 이 역시 예제로 보자

    <!DOCTYPE html>
    <html ng-app = "myApp">
      <head>
        <meta charset="utf-8" />
        <title>example 2.12</title>
      </head>
      <body>
        <form name="sampleForm" ng-init="name = '철수'">
          이름 : <input type="text" name= "name" ng-model="name" ng-minlength="3" ng-required="true" />
          <span class='error' ng-show="sampleForm.name.$error.required">필수입력</span>
          </br>
          핸드폰 번호 : <input type="text" name= "tel" ng-model="tel" ng-pattern="/^\d[3]|d[3,4]-\d[4]$/"/>
          <span class='error' ng-show="sampleForm.tel.$error.pattern">000-000-0000</span>
          </br>
          <p>
            사용자 정보 : { {name} }/{ {tel} }
          </p>
          <p>
            sampleForm.name.$valid = { {sampleForm.name.$valid} }
          </p>
          <p>
            sampleForm.name.$error = { {sampleForm.name.$error} }
          </p>
          <p>
            sampleForm.tel.$valid = { {sampleForm.tel.$valid} }
          </p>
          <p>
            sampleForm.tel.$error = { {sampleForm.tel.$error} }
          </p>
          <p>
            sampleForm.$valid = { {sampleForm.$valid} }
          </p>
          <p>
            sampleForm.$error.required = { {sampleForm.$error.required} }
          </p>
        </form>
        <!--angular file-->
        <script src="../angular.js" type="text/javascript"></script>
        <script type="text/javascript">

          var myApp = angular.module('myApp', []);

        </script>
      </body>
    </html>

여기서 아마 처음보는 것들이 많을 것이다. 이것을 이해하려면 `FormController`, 와 `ngModelController`를 알아야 한다.

AngularJS 는 표준 HTML 태그 또한 **Angular 지시자** 로 만들 수 있다. 즉, `from` 태그 역시 지시자로 간주하고 확장 할 수 있다. 그래서 AngularJS 는 폼 상태관리를 위해 `FormController`를 만들었다. 나중에 설명하겠지만 지시자에 별도의 컨트롤러를 지정할 수 있다. 아무튼 Angular 기반의 웹 애플리케이션에서 각 `Form`은 `FormController`의 인스턴스이고 `form` 의 `name` 속성에 준 값을 이용해 `$scope`에서 접근할 수 있다.

즉, 위 예시와 같은 경우, `sampleForm`에 대한 scope가 설정되었고, `$scope.sampleForm`로 접근이 가능하다.

여기서 **인스턴스** 란 말을 했는데, 이는 객체가 된다는 것이다. 여기서 이 객체의 속성을 보도록 하자.

속성

* $pristine
  - 사용자의 입력이 없었으면 true
* $dirty
  - 사용자의 입력이 있었으면 true
* $valid  
  - `form`에 있는 컨트롤 요소(`input`)가 모두 유효성 검증을 통과하면 true
* $invalid
  - `form`에 있는 컨트롤 요소(`input`)가 모두 유효성 검증을 통과하면 false
* $error
  - 유효성 검증의 이름(`required`, `email`, `minlength` ...)을 키로 하고 각 컨트롤 요소의 name을 값으로 가진 객체

메서드

* $addControl()
  - 컨트롤 요소를 추가
* $removeControl()
  - 컨트롤 요소 제거
* $selDirty()
  - `$dirty` 값을 바꾼다. 즉, 강제로 폼이 수정된 상태를 변경
* $setValidity()
  - `form` 요소의 유효성 상태를 바꾼다.
* $setPristine()
  - `form` 요소의 `$pristine`을 false로 변경

이제 앞의 예제에 몇몇 부분은 이해가 가게 되었다.

그러나 아직 `NgModelController`를 모르고 있다.

`NgModelController`는 `form` 내부의 요소들, `input`, `select`, `textarea` 요소 개개의 유효성 상태나 사용자 입력 상태를 컨트롤 한다.

이 역시 다음을 참고한다.

속성

* $viewValue
  - 화면에서 보이는 값
* $modelValue
  - 컨트롤 요소가 바인딩된 모델 값
* $parsers
  - 함수들의 배열
  - 각 함수는 순서대로 `DOM` 으로부터 값을 읽을 때마다 호출 즉, `$viewValue`의 값이 바뀔 때 호출
  - 호출된 함수가 반환한 값은 다음 함수로 전달, 최종적으로 `$modelValue`에 전달
* $formatters
  - 함수의 배열
  - 각 함수는 순서대로 바인딩된 데이터(`$modelValue`)가 바뀔 때마다 호출
  - 호출된 함수가 반환한 값은 다음 함수로 전달, 최종적으로 `$modelValue`에 전달
* $viewChangeListeners
  - 화면 요소의 값이 변경될 때마다 호출되는 함수의 배열
  - 해당 함수들은 어떤 인자도 없이 호출되고 반환된 값은 무시
* $error
  - 유효성 검증의 이름(`required`, `email`, `minlength` ...)을 키로 하고 각 컨트롤 요소의 name을 값으로 가진 객체
* $pristine
  - 사용자의 입력이 없었으면 true
* $dirty
  - 사용자의 입력이 있었으면 true
* $valid  
  - `form`에 있는 컨트롤 요소(`input`)가 모두 유효성 검증을 통과하면 true
* $invalid
  - `form`에 있는 컨트롤 요소(`input`)가 모두 유효성 검증을 통과하면 false

메서드

* $render()
  - 화면이 업데이트될 때 마다 호출. 지시자를 만들어 `ngModelController` 의 `$render`에 함수를 대입해 놓으면 화면이 업데이트 될 때 마다 호출
* $setValidity(validationErrorKey, isValid)
  - 유효성 상태를 설정하고 컨트롤 요소의 유효성 상태가 변경될 때 `FormController`에게 알려준다.
  - `validationErrorKey` 값이 `$error[validationErrorKey] = isValid` 형태로 된다.
  - `validationErrorKey`는 카멜케이스 형태로 기술하면 css로 `ng-valid-my-err/ng-invalid-my-err`와 같은 형태로 삽입된다.
* $isEmpty
  - 입력 요소의 값이 빈 값인지 확인.
  - 여기서 빈 값이란 `undefined`, `''`, `null` 또는 `NaN`에 해당한다.
  - 해당 메서드를 오버라이드하면 빈 값에 대한 정의를 다시 할 수 있다.
* $setPristine()
  - `form` 요소의 `$pristine`을 false로 변경
* $setViewValue(value)
  - 화면에 값을 추가

  이제 예제를 보고 한번 분석해 보길 바란다.

이 후 아직 많은 지시자가 남았다. 다음 포스팅에선 예제를 기준으로 빠르게 해결한 뒤에 Angular 기본 구성으로 넘어가도록 하자.


앞서 적어둔 모든 소스는 [이곳](https://github.com/koocci/AngularJS-examples) 에서 보실 수 있습니다.
