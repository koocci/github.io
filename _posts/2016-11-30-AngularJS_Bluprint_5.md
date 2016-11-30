---
layout: post
title:  "[AngularJS] AngularJS 블루프린트 5"
date:   2016-11-30 19:17:11 +0900
categories: AngularJS
tags: [Angularjs, 프로그래밍, MEAN stack, 기초, 블루프린트, IONIC]

---

# AngularJS 앱에 REST 적용하기

---

![wind](http://farm9.static.flickr.com/8152/7176953741_b996bb4e8c_z.jpg)

이전에 프로토 타입을 구축해보았다.

실제로 개발은 동적 데이터를 사용할 것이고 백앤드는 연결되어야 하므로 이제 **JSON** 포맷과 **REST** 웹 서비스를 적용해 보도록하자.

원래 도서상으로 서비스를 직접 만들어 보지만 소개하는 페이지가 조금 바뀌기도 했고, 한국에 맞춰서 개인적으로 만드는 걸 추천하지만 이론적인 것들만 정리해서 적어 보기로 했다.

여기서 우리는 다음을 배워볼 것이다.

* AngularJS의 팩토리, 서비스, 프로바이더가 무엇인지 알아본다.
* $http 서비스를 이용해 어떻게 웹 서비스를 호출하는지 알아본다.
* 의존성 주입(DI, Dependency Injection)을 알아본다.
* 프라미스의 개념과 비동기 호출에 대해 이해한다.

---

### REST API의 응답 이해하기

---

먼저 **RESTful** 웹 서비스가 어떻게 되는지 알아보자.

대부분의 REST 웹 서비스는 URL에 쿼리스트링 형태로 간단히 호출할 수 있다.

`http://tempdomain.com/api/.../temp.json?limit=5&country=ko&apikey=YOURAPIKEY`

와 같은 형태 일 것이다.

간단히 테스트를 해볼 수 있는데, 그냥 해당 주소에 자신이 할당 받은 API 키를 넣고 검색해보면 된다. 혹은 chrome의 postman과 같은 서비스를 이용해 보기도 한다.

그럼 아마 출력이 나올 것이다.

---

### Angular 시드

---

이전에는 요맨을 이용해서 뼈대를 만들어 보았다. 이번에는 **Angular 시드** 프로젝트를 뼈대 프로젝트로 정하고 그 위에 개발을 하는 방식을 알아보도록 하겠다.

Angular 시드 프로젝트는 github에 공개되어 있고 핵심 AngularJS 개발자 팀이 계속 유지시키므로 가장 최신 버젼이라고 봐도 된다.

[https://github.com/areai51/angular-seed.git](https://github.com/areai51/angular-seed.git) 해당 주소이다.

간단히 git clone으로 가져오면 된다.

다운을 받고 바로 `npm install` 명령어로 의존성 라이브러리들을 설치하도록 하자.

---

### node 웹 서버 구동

---

여기까지 하면 index.html 파일을 클릭했을 때 애플리케이션을 브라우저에서 볼 수 있지만 웹 서버 내에서 실행을 시켜보자.

그럼 다음 명령어를 실행해보자

`npm start`

**현재 버젼으로 다운받으면 원하는 도서에서 원하는 작업은 진행하기 힘드므로 해당 프로그램을 따로 받아두었다**

따로 API 키를 받아서 보고 싶지만 딱히 회원가입을 하고 싶진 않기도 하고 코드만 분석해 보도록 하겠다.

`app/js/app.js`를 보도록 하자.

    config(['$routeProvider', function($routeProvider) {
      $routeProvider.when('/', {templateUrl: 'partials/movie-list.html', controller: 'MovieListCtrl'});
      $routeProvider.otherwise({redirectTo: '/'});
    }])

다음과 같은 코드가 들어있다. 여기서는 한개의 파셜만 필요하기 때문에 `/` 경로를 바로 지정해 주었다.

---

### 서비스에 대한 이해

---

특정한 기능들이 **여러 페이지나 섹션에 걸쳐 공통적으로 사용** 될 때 매번 컨트롤러안에 반복해서 쓰는 것보다 **서비스 안에 코드를 작성** 하고 다양한 구성 요소에서 호출하는 게 더 좋다.

간단한 예를 들어보자.

상품 목록을 가져오는 일이 있다 할 때, **인증 토큰이나 API 키를 넘겨주고 응답을 받아서 파싱하는 코드** 는 서비스에 둘 수 있다.

서비스에 있어서 이런 건 꼭 기억해 두자.

* 서비스는 한 번만 초기화되는 싱글톤 인스턴스며 앱의 생에 전체에 걸쳐 영속한다.
* 서비스는 지연 로딩되는데, 이것은 애플리케이션의 구성 요소가 서비스를 필요로 할 때에 초기화된다는 의미다.
* 이런 서비스들은 의존성 주입을 통해 구성 요소들에 주입되거나 맵핑된다.

AngularJS는 **$animate, $log, $http, $sanitize** 등과 같은 내장 서비스들이 있다.

물론 기본 지원 외에 직접 제작도 가능하다.

**$provide** 서비스는 자신만의 서비스를 등록하고 생성하는 데 사용되는 많은 메소드를 가지고 있고 그 메소드 목록은 다음과 같다.

* provider()
  + $injector 함수와 함께 프로바이더 함수를 등록하는데 사용.
  + 프로바이더 함수는 생성자 함수이며 프로바이더 설정을 위한 추가적인 메소드를 포함.
* service()
  + 생성자를 이용해 서비스 인스턴스를 등록하는 데 사용.
  + 생성자는 new 문구를 이용해 새로운 서비스의 인스턴스를 생성할 때 호출한다.
* factory()
  + 서비스 팩토리를 등록하기 위해 사용한다. 서비스를 사용하기 위해 가장 많이 사용되고 가장 쉬운 메소드 중 하나
  + 기본형 타입과 함수, 객체를 반환할 수 있다.
* value()
  + 반환 값이 문자열, 숫자, 배열, 함수, 객체인 서비스를 등록할 때 사용
  + 값들은 서비스를 통해서만 접근 가능하다.
* constant()
  + value 서비스와 유사하게 상수 서비스를 등록할 때 사용
  + 차이점은 상수는 서비스와 프로바이더를 통해 접근이 가능하다는 것.

---

### 팩토리 서비스 작성

---

**팩토리** 는 전체 애플리케이션에 걸쳐서 다른 함수나 컨트롤러에 인자로 넘겨질 수 있는 단일 객체, 배열 또는 함수를 반환하는 데 사용한다.

여기서는 국가 목록을 저장하고 컨트롤러를 통해 모델에 넘겨주는 팩토리 함수를 생성하였다.
`app/js/services.js` 를 보도록 하자.

    'use strict';
    angular.module('myApp.services', []).
    value('version', '0.1')
    .constant('API_KEY','<enter your api key >')


    .factory('rtmFactory', ['$http','API_KEY',function($http,API_KEY) {
        var countries = [
        {name: 'USA',code: 'us'},
        {name: 'UK',code: 'uk'},
        {name: 'France',code: 'fr'}
        ];
        return {
            getCountries: function() {
                return countries;
            },
                getMovies:function(countryCode){

            return $http.jsonp('http://api.rottentomatoes.com/api/public/v1.0/lists/movies/box_office.json?limit=10&country='+countryCode+'&callback=JSON_CALLBACK&apikey='+API_KEY)


        }

        }
    }])


여기서 `rtmFactory` 라는 이름의 펙토리를 지정해 주었고 `myApp` 모듈에 연결하였다.

팩토리 내부에서 어떻게 흐름이 이어지고 있는지 잘 보도록하자.

---

### 의존성 주입

---

**의존성 주입** 은 하나 혹은 그 이상의 의존성이 참조로서 주입되거나 넘겨지는 소프트웨어 디자인 패턴이다.
이를 이용하면 코드를 필요할 때에만 로드되게 할 수 있다.

여기서는 데이터 객체를 들고 있는 팩토리를 의존성 주입을 이용해 컨트롤러에 넘겨준다.

AngularJS에 **다른 서비스를 탐색하고 함수를 주입** 해주는 `$injector` 서비스가 있다.

함수에 의존성을 주입하는 방법은 다양한데 가장 쉬운건 **필요한 의존성을 함수의 인자로서 넘기는 것** 이다.

그럼 rtmFactory 서비스를 MovieListCtrl 컨트롤러에 인자로 넘겨보자.

`app/js/controller.js` 를 보도록 하자.

    'use strict';
    angular.module('myApp.controllers', []).
    controller('MovieListCtrl', ['$scope', 'rtmFactory',
        function($scope, rtmFactory) {
            $scope.countries = rtmFactory.getCountries();

먼저 여기까지만 보자.

어떻게 넘겨주었는지 직관적으로 알 수 있다.

---

### $http 사용한 REST 웹 서비스 호출

---

$http는 Angular 내장 서비스고 백 앤드 시스템이나 서드파티 시스템과 통신할 때 사용한다.

기본적으로 브라우저에서 제공하는 `XMLHttpRequest`를 감싸고 있는 객체고, 개발자에게 저수준 API에 대한 고민없이 쉽게 작업할 수 있는 환경을 제공한다.

환경 객체를 인자로 받고 두가지 메소드를 통해 프라미스를 반환하는데 `success`, `error` 가 그것이다. 그 외에도 `.then()` 메소드를 사용해 결과적으로 **응답을 단일 객체로 반환하는 콜백 함수** 를 등록한다.

사용법은 다음과 같다.

    $http(
      method : 'GET',
      url : 'api/api-endpoint'
    ).success(function(data, status, headers, config){
      // 성공
    }).error(function(data, status, headers, config){
      // 에러
    })

이걸 조금 단축해서 표현할 수 있는데,

`$http.get('api/api-endpoint').success(successCallback).error(errorCallback)`

이다.

여기서 .get() 메소드와 유사하게 단축 메소드들을 $http 서비스의 일부로 사용가능하다.

* $http.head
* $http.post
* $http.jsonp
* $http.put
* $http.delete

이제 아까 만들어 둔 팩토리 함수와 연결 지었던 `getMovies` 부분이 잘 이해됬으리라 생각한다.

다만 웹서비스 호출을 위해 일반적인 `$http.get` 이 아닌 `$http.jsonp`를 사용했다는 것에 유의하자. 이 메소드는 **JSON with padding** 의 줄임말로 script 태그 속성을 활용해 콘텐츠를 다른 도메인에 속해 있는 사이트로부터 가져오는 방법 중 하나다.
