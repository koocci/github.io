---
layout: post
title:  "[AngularJS] AngularJS 블루프린트"
date:   2016-11-21 16:34:11 +0900
categories: AngularJS
tags: [Angularjs, 프로그래밍, MEAN stack, 기초, 블루프린트, IONIC]

---

# Angular JS

---

![tree](https://cdn.pixabay.com/photo/2016/11/01/18/19/trees-1789120_1280.jpg)

이전에 **AngularJS** 에 대해 한번 블로깅 한적이 있다. 당시에 프로젝트를 진행할 줄 알고 (정확히는 외주) 미리 배우는 차원에서 진행했었는데, 아쉽게도 엎어지는 바람에 흐지부지 되었었다. 그리고 이 후 AngularJS에 대해 프로젝트를 하지 않았던 것이 마음에 걸렸는 데 이번에 멘토링, 기타 프로젝트 두어가지를 진행하게 되면서 다시 AngularJS 를 접하게 되었다.

지난번 프로젝트 때 사용한 책은 상당히 간소화해서 MAEN 스택을 설명하던 책이라 아쉬운 부분이 많았고 이번에는 새로이 도서관에서 책을 빌리게 되었다. 책 이름은 `AngularJS 웹 애플리케이션 개발 블루프린트` 라는 책이고, **최소한의 코드로 완벽하게 동작하는 애플리케이션 만들기** 라는 소제목을 가지고 있는 책이다.

전체적으로 AngularJS를 이용해 원페이지 웹 애플리케이션을 만들어 나가는 커리큘럼이고 꽤나 설명이 좋다. (특히 node js도 같이 연동한다.) 그리고 웹 애플리케이션을 만들며 기초를 다지면 IONIC 관련 도서를 이용해 어플로 만들어갈 예정이다.

특히나 이 책의 좋은 점은 주변 개발 환경에 대해서도 좋은 툴들을 많이 설명하므로 주의깊게 알아두면 좋을 듯하다.
먼저, 이 도서는 AngularJS 1.2.17 버전을 기준으로 작성되었으니 참고 하도록 하자.

---

### AngularJS와 싱글 페이지 애플리케이션 소개

---

먼저 **싱글 페이지 애플리케이션** 이 무엇인지 알아보도록 하자.

AngularJS는 다른 무엇보다 싱글 페이지 애플리케이션에 주로 사용하는 데, 싱글 페이지 애플리케이션은 **하나의 페이지 안에 전체 사이트나 애플리케이션이 로드되는 앱이나 웹사이트** 라고 한다.

즉, 사이트가 한 번 로드되면 사용자가 링크를 타고 다른 곳을 갈 때 새로운 페이지가 로드되는 것이 아니라, 메인 페이지 내의 일정 영역을 갱신하는 것이다.

그럼 일반적인 웹사이트와 싱글 페이지 애플리케이션이 동작하는 방법에서 **차이점** 을 알아 보자.

자바, PHP, .NET 같은 서버 사이드 기술에 의해 구현된 전통적인 웹사이트는 **클라이언트 요청이 있을 때 마다 데이터베이스에 질의하고 결과를 처리한 후 템플릿에 로드하고 브라우저에 보내지는 웹페이지를 동적으로 생성** 한다.

여기서 흐름을 보듯, **서버에서 많은 부하가 발생** 하는 일을 모두 맡게 되고, 많은 트래픽이 발생이 되며 병목이 생긴다. 따라서 높은 트래픽을 자랑하는 유명사이트들이 많은 서버를 사용하는 이유다.

그러나 AngularJS같은 자바스크립트 프레임워크로 개발된 싱글 페이지 애플리케이션은 조금 다른 방식이다.

아키텍처를 보면 전체 템플릿이 HTML, 자바스크립트, CSS와 함께 사용자의 브라우저로 다운로드되어 요청이 발생했을 때 **템플릿에 채워질 내용은 웹 서버에서 전달** 하고 **페이지 구성은 사용자의 브라우저에서** 일어나게 된다. (틀은 모두 브라우저에서 일어나고 주요 데이터, 즉 내용은 웹 서버에서 전달한다.) 따라서 서버는 데이터를 주고받는 기능만 하고 페이지를 구성하는 일은 관여하지 않게 된다. 결론적으로, **페이지는 사용자의 브라우저에서 구성이 되므로 웹 서버의 트래픽이 늘어나더라도 일반 웹사이트보다 부하가 줄어들게 된다.**

이렇게 싱글 페이지 애플리케이션의 또다른 멋진 점중 하나는 **프레젠테이션 계층을 백엔드 계층과 완전히 분리할 수 있다** 는 것이다.

---

### 간단한 AngularJS 앱 구성

---

여기서 이제 간단히 AngularJS 구성을 해볼 것이다. js파일을 다운 받고, 프로젝트에 넣어서 해보도록 하자.

    <!DOCTYPE html>
    <html>
    <head>
      <title>AngularJS Basic</title>
    </head>
    <body ng-app ng-init=" myName = 'Jinhyun Koo'">
      {{myName}} is {{ 2016 - 1993 }} years old.
      <script src="../angular.min.js" type="text/javascript "></script>
    </body>
    </html>

가장 간단한 이름과 나이 출력이다.

이제 여기서 쓰인 문법적 요소들을 정리해 보자. ( 이전 포스팅에서 했던 내용이니 간단히 하고 넘어가도록 하자. )

`ng-app : AngularJS 자신을 로드하기 위해 정의한 엘리먼트. 대부분 <html> <body> 태그에 추가한다. 만약 일반적인 애플리케이션에서 AngularJS를 추가해서 구현할 때, div에 선언할 경우도 있다.`

`ng-init : 초기화를 수행하고 싶을 때 사용한다. 여기서는 myname이라는 모델에 나의 이름을 설정했다. 단, 상용환경에서는 사용하지 않도록 하자. 변수의 초기화는 뷰가 아니라 컨트롤러가 되어야 좋다.`

`{{ }} : 연속된 중괄호는 모델에 저장된 값을 출력할 때 사용한다. 또한, 예제에서 보듯 산술 식의 결과도 가능하다.`

`지시자(Directives) : 여기서 살펴본 ng-app과 ng-init 태그를 지시자라고 한다.`

여기서 지시자를 한 번더 보도록 하자. 지시자는 AngularJS 앱에서 중요한 역할을 하며 AngularJS는 이를 통해 애플리케이션의 DOM 엘리먼트를 수정할 수 있다. AngularJS는 미리 정의된 지시자를 가지고 있고, 특수한 요구 사항에 있어서 커스텀한 지시자를 만들 수도 있다.


---

### 모델과 뷰

---

AngularJS 모델에는 **원시 자료형, 해시 테이블, 자바스크립트 오브젝트** 가 될 수 있다.

모델의 데이터는 **{ {  } }** 표현식을 사용하면 뷰에서 출력할 수 있다. 모델은 여러 가지 방식으로 정의된다. 위 첫 예제에서 본 것처럼 ng-init 지시자 안에 모델을 정의 할 수 있다. 또한 다음 표현식과 같은 템플릿을 통해서도 생성된다.

    <button ng-click="firstName = 'JinHyun Koo'">click</button>

**scope** 를 통해 컨트롤러 안에서 생성할 수 있는데, 가장 이상적인 방법이라 할 수 있다.

다음 코드를 한 번 보도록 하자.

    <!DOCTYPE html>
    <html ng-app>
    	<head>
    		<title>Model in Scope </title>
    	</head>
    	<body ng-controller="PeopleController">
    		{{person.name}} lives in {{person.city}}
    	<script src= "../angular.min.js" type="text/javascript"></script>
    	<script type="text/javascript">
    		function PeopleController($scope){
    			$scope.person={name:"JinHyun Koo", city:"Pusan"}
    		}

    	</script>

    	</body>
    </html>


예제에서 PeoPleController라는 이름의 **컨트롤러** 를 생성하고 데이터를 **해시 테이블** 형태로 저장하고 있는 person 모델을 정의헀다 $scope는 AngularJS 객체로서 자바스크립트 객체 모델을 속성으로서 참조할 수 있다.

---

### 주소록 앱 개발하기

---

언제나 개발은 프로젝트 기반으로 해야 실력이 쑥쑥 는다. 이 책이 딱 그렇다. 이전 예제에서 모델을 만드는 다양한 방법을 알아봤다. 그래픽 기반의 **사용자 인터페이스를 포함하는 상용이나 애플리케이션** 의 경우는 MVC 모델을 사용해 개발하는 것이 필수적이다.

이제 이전 예제들을 기반으로 간단한 주소록 앱을 만들 예정이다.
PeopleController 컨트롤러 안에 전용 모델을 만드는 것으로 시작을 해보자. 그리고 script.js라는 파일(파일명은 개인적으로 달리 하겠다)을 만들어 자바스크립트 소스를 작성할 것이다.

해당 스크립트 소스는 다음과 같다.

    function PeopleController($scope){
      $scope.people = {
        {name : "John Doe", phone : "1234567", city: "New York"},
        {name : "Sarah Parker", phone : "3938402", city: "Boston"},
        {name : "Little John", phone : "13940234", city: "Los Angeles"},
        {name : "Adam Doe", phone : "4954345", city: "Las Vegas"}
      }
    }

여기서는 PeopleController를 정의하고 people 라 불리는 모델을 생성하였다. 이 모델은 name, phone, city라는 속성을 가진다.
이제 index.html을 만들어 보자.

    <!DOCTYPE html>
    <html ng-app>
      <head>
        <title>Address Book</title>
      </head>
      <body ng-controller="PeopleController">
        <h1>Address Book</h1>
        <div>
          <div ng-repeat="person in people">
            <div>
              {{person.name}} - {{person.phone}}
            </div>
            <span>{{person.city}}</span>
          </div>
        </div>
        <script src="angular.min.js" type="text/javascript"></script>
        <script src="addressBook.js" type="text/javascript"></script>
      </body>
    </html>

참고로 자바스크립트는 바디 태그 위쪽이나 헤드보다 페이지 하단에서 로드하는 것이 좋은 습관이다.

예제에서 보듯이 **HTML5 DOCTYPE** 을 정의하고 있다. 이후 ng-app 지시자를 이용해 AngularJS 애플리케이션을 초기화한다. ng-controller 지시자를 사용하는 것과 PeopleController에 이를 할당하는 것도 볼 수 있다. 이렇게 함으로써 **컨트롤러의 스코프 안에 들어가는 DOM의 한 영역을 정의** 한다.

`ng-repeat`도 볼 수 있는데, **컬렉션에서 항목의 리스트를 표시하는 빌트인 지시자** 다. ng-repeat 지시자는 **단순히 엘리먼트를 복제하고 미리 정의된 프로퍼티에 데이터를 연결** 해준다.

예제에서 보듯 ng-repeat 지시자를 이용하면 jQuery나 순수 자바스크립트만 사용한 것에 비해 **데이터를 쉽고 편하게 표시** 할 수 있다.

그럼 index.html을 한번 브라우저에 띄워보길 바란다. 모델을 설정한 데이터가 오류없이 보인다면 성공이다. 그럼 AngularJS가 어떻게 적용되고 있는지 더 알아보자.

여기서는 크롬의 **개발자 도구** 를 사용하였다.

코드를 한번 들여다보자. 아마 자신이 작성했던 코드와 많이 다를 것이다.
맨 처음 보이는 것은 AngularJS가 `ng-scope` 클래스를 스코프가 초기화되는 **모든 DOM 엘리먼트에 추가한 점** 이다. (나중에 스코프를 제대로 알아보기로 하자.)  ng-repeat 지시자 안에 존재하는 **전체 DOM을 복제** 했다. 또한 데이터가 연결된 **모든 엘리먼트마다 ng-binding이라는 클래스를 추가** 한다.

AngularJS는 사용된 지시자에 따라서 서로 다른 CSS를 적용할 것이다. 이런 점은 꾸미고 싶을 때 유용하게 사용될 수 있는데, 예를 들면 입력 양식에서 사용자에게 검증 메시지를 표시하기 위해 사용할 수 있다.

---

### AngularJS에서 스코프 이해하기

---

![wonder](https://cdn.pixabay.com/photo/2016/06/06/23/49/budapest-1440679_1280.jpg)

스코프라는 것을 이제 알아보도록 하자.
앞선 예제에서 people 컨트롤러를 $scope 인자와 함께 정의했다. 또한 people 모뎅를 이 스코프의 일부분으로 정의했다. 요소검사를 하면서 여러 개의 ng-scope가 정의된 것도 보았다. 그래서 이 스코프라는 것은 무엇일까?

AngularJS의 문서를 따르면, 스코프 객체는 `애플리케이션 모델을 지칭하고 뷰의 표현식에서 실행 컨텍스트를 제공하는 역할`을 한다.
표현식 `{{person.name}}` 이 출력 가능한 이유는 name이 스코프에 의해 접근할 수 있는 프로퍼티이기 때문이다.

알아둬야 할 사실 중 한 가지는 모든 AngularJS 앱은 ng-app 지시자에 생성되는 **루트 스코프** 를 가지게 된다는 점이다. 다른 많은 지시자들 역시 그들만의 스코프를 생성할 수 있다. 스코프는 **페이지의 DOM 구조에 따라서 게층구조** 를 가지도록 정렬된다. **자식 스코프들은 원형적으로 부모 스코프로부터 상속** 한다.

**지시자가 스코프 옵션을 사용한 경우** 는 에외인데, 이때는 **고립된 스코프** 를 생성한다. 지시자와 고립된 스코프에 대한 얘기는 나중에 알아보도록 할 것이다.

---

### 앱에 스타일 넣기

---

이제 index.html에 클래스를 추가하고 css파일을 만들어 스타일을 넣어보자.

    <!DOCTYPE html>
    <html ng-app>
      <head>
        <title>Address Book</title>
        <link rel="stylesheet" type="text/css" href="addressBook.css" />
      </head>
      <body ng-controller="PeopleController">
        <h1>Address Book</h1>
        <div class="wrapper">
          <div class="contact-item" ng-repeat="person in people">
            <div class="name">
              {{person.name}} - {{person.phone}}
            </div>
            <span class="city">{{person.city}}</span>
          </div>
        </div>
        <script src="angular.min.js" type="text/javascript"></script>
        <script src="addressBook.js" type="text/javascript"></script>
      </body>
    </html>


보면 알겠지만 title 밑에 스타일시트를 추가 했고, 내부적으로 wrapper 클래스와 contact-item 클래스를 선언했다. 또한 name과 city 클래스가 적용되었다.

그럼 css 파일을 보도록 하자.

    body{
      font-family: sans-serif;
      font-weight: 100;
      background: #ccc;
    }
    h1{
      text-align: center;
      color: #666;
      text-shadow: 0px 2px 0px #fff;
    }
    .name{
      font-size: 18px;
    }
    .city{
      font-style: italic;
      font-size: 13px;
    }
    .wrapper{
      width: 550px;
      margin: 0 auto;
      box-shadow: 5px 5px 5px #555;
      background: #fff;
      border-radius: 15px;
      padding: 10px;
    }
    .contact-item{
      border-bottom: thin solid #ccc;
      padding: 10px;
    }

기본적인 css 설명은 생략해도 된다고 생각된다.


---

### 연락처 정렬하기

---

이제 연락처를 알파벳순으로 정렬해 보도록 하자. 이를 위해서 AngularJS의 `orderBy` 빌트인 필터를 사용한다.

AngularJS에서 필터는 **데이터를 양식화** 하기 위해 사용한다. 미리 정의된 AngularJS의 필터를 사용하거나 새롭게 만들수도 있다. 필터들은 이후 나중에 다뤄볼 예정이다.

    <div class="contact-item" ng-repeat="person in people | orderBy: 'name'">
      <div class="name">
        {{person.name}} - {{person.phone}}
      </div>
      <span class="city">{{person.city}}</span>
    </div>

결과를 확인해 보면 정렬이 되어 있음을 볼 수 있다.

---

### 주소록에 연락처 추가하기

---

이제 연락처를 멋지게 보여주는 주소록이 완성되었고, 이제 추가하기를 해보도록 하자.

    <div class="wrapper">
      <h2>Add a Contact</h2>
      Name : <input type="text" ng-model="newPerson.name" />
      Phone : <input type="text" ng-model="newPerson.phone" />
      City : <input type="text" ng-model="newPerson.city" />
      <button ng-click="Save()">Save</button>
    </div>

이 예제는 상당히 직관적이다. 새로운 div를 생성하고 꾸며주기 위해 wrapper 를 클래스를 재사용했다.
name, phone, city 를 위한 세 개의 텍스트 박스를 추가하는데, **newPerson 이라는 모델 오브젝트에 이 텍스트 박스들을 연결** 했다.

`ng-click` 지시자를 이용해 마지막에 button과 연결하였다.
이제 이 클릭을 자바스크립트 파일에서 처리해 보자.

    $scope.Save = function(){
      $scope.people.push({name : $scope.newPerson.name, phone : $scope.newPerson.phone, city : $scope.newPerson.city});
    }

Save() 함수가 어디에 정의 되야하는지는 직관적으로 알 수 있다. scope가 어디에 해당하는지 생각해보자.

$scope.Save 함수에서는 단순히 입력 박스의 값을 수집해서 추가 되는 people 모델에 넣어주는 일을 수행한다.
그럼 결과를 확인하자. 이것을 **양방향 데이터 바인딩** 이라고 부르는 AngularJS의 멋진 기능중 하나이다.

---

### ng-show 와 ng-hide 지시자

---

지금까지 매우 간단하게 한가지 앱을 만들었다. 하지만 연락처 추가 버튼을 만들고 연락처 추가 양식을 버튼이 클릭되었을 때만 보여지도록 하면 더 좋을 것 같다.

따라서 이를 `ng-show`와 `ng-hide`를 통해 만들어 보자.

이 역시 매우 직관적으로 만들 수 있다. ng-show 속성이 **true** 면 보여지고 그렇지 않으면 감춰 진다. 여기서 중요한 점은 **ng-show 와 ng-hide 지시자가 단순히 DOM 엘리먼트의 표시 여부를 조정할 뿐** 이라는 것이다.

연락처 추가 버튼을 만들고 위 지시자들을 이용해 연락처 추가 버튼을 클릭했을 때 입력 양식이 보이고, 이 버튼은 사라지게 만들어보자. 그리고 저장 버튼을 누르면 그 반대로 진행해 보겠다.

    <center>
      <button ng-click="ShowForm()" ng-hide="formVisibility ">Add Contact</button>
    </center>
    <div ng-show="formVisibility" class="wrapper">
      <h2>Add a Contact</h2>
      Name : <input type="text" ng-model="newPerson.name" />
      Phone : <input type="text" ng-model="newPerson.phone" />
      City : <input type="text" ng-model="newPerson.city" />
      <button ng-click="Save()">Save</button>
    </div>

ng-hide에 `formVisibility`가 선언되어 있는 걸 볼 수 있고, 이를 **true, false** 로 조정하여 줄 것이다.

    $scope.Save = function(){
      $scope.people.push({name : $scope.newPerson.name, phone : $scope.newPerson.phone, city : $scope.newPerson.city});
      $scope.formVisibility = false;
    }

    $scope.ShowForm = function(){
      $scope.formVisibility = true;
    }

다음과 같이 자바스크립트 파일을 선언했다.
그럼 어떻게 되는 지 직관적으로 볼 수 있다.

버튼이 제대로 동작하는 지 확인해보고, 버튼 css를 조금만 바꿔보도록 하겠다.

    button{
      background : #080;
      color: #fff;
      padding: 5px 15px;
      border-radius: 5px;
      border: thin solid #060;
      margin: 5px auto;
    }

    button:hover{
      background: #0A0;
    }

이제 첫번째 앱을 완성하였다.

여기까지 1장을 완료했다. 한번 다시 퇴고하며 정리할 시간을 가져보자.

2장은 개발 환경에 대해 얘기하는데 얼마나 재밌을 지 기대가 된다.

제가 만든 소스는 [이곳](https://github.com/koocci/AngularJS-examples) 에서 보실 수 있습니다.
