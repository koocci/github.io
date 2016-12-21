---
layout: post
title:  "[AngularJS] 시작하세요! AngularJS 5"
date:   2016-12-07 20:53:14 +0900
categories: AngularJS
tags: [Angularjs, 프로그래밍, MEAN stack, 기초, 블루프린트, IONIC]

---

# HTML에서 지시자를 사용하는 방법

---

![wind](http://farm4.static.flickr.com/3447/5738508334_88d9c68203_z.jpg)

지시자 이름은 **카멜표기법** 으로 작성한다. 이런 지시자의 이름을 HTML 즉, 템플릿에서는 `-` 또는 `_`문자를 넣고 소문자로 바꾸어 사용할 수 있다. 그러나, 사실 여러 방법이 있다는 것은 아주 예전 처음 Angular에 대한 포스팅을 할 때 언급한 적이 있다.

여기서 호출법이 4가지정도 있는데 알아보도록 하자.

1.  요소의 속성을 이용한 호출
  * `<span my-directive="expression"></span>`
2.  요소의 클래스를 이용한 호출
  * `<span class="my-directive: expression;"></span>`
3.  요소 이름을 이용한 호출
  * `<my-directive></my-directive>`
4.  코멘트를 이용한 호출
  * `<!-- directive: my=directive expression -->`

그럼 이 지시자 호출들을 한번 연습해보자.

    <!DOCTYPE html>
    <html ng-app = "sampleApp">
      <head>
        <meta charset="utf-8" />
        <title>example 2.24</title>
      </head>
      <body ng-controller="mainCtrl">
        <p ng:style="getStyle()">
          hello
        </p>
        <p class="ng_style: getStyle()">
          hello
        </p>
        <ng-form name="groupForm">
          <form name="formA">
            <input type="text" />
          </form>
          <form name="formB">
            <input type="text" />
          </form>
        </ng-form>
        <!--angular file-->
        <script src="../angular.js" type="text/javascript"></script>
        <script type="text/javascript">

          angular.module('sampleApp', [])
            .controller("mainCtrl",['$scope',function($scope){
              $scope.getStyle = function(){
                return {'color' : 'red'};
              }
            }]);

        </script>
      </body>
    </html>

위 예제를 보면, `ng-style` 지시자를 속성으로 사용하는데, 하나는 XML의 네임스페이스 방식으로 사용하고 있고, `ng-form` 지시자는 요소이름으로 사용하고 있다.

---

### 웹 표준 준수 대비

---

웹 표준은 준수하려는 많은 시도가 있다. 그래서 최근 지침도 나오고 준수 여부를 알려주는 서비스도 있다. 여기서 Angular를 사용하면 웹 표준을 지키지 않았다고 나오는데, 이에 따라 별도의 방법이 있다. `x-`, `data-`를 사용하는 지시자 앞에 붙이는 것이다. 이렇게 하면 웹 표준을 잘 맞춰서 준수할 수 있다.

---

### 옛날 인터넷 익스플로러 지원

---

IE7, IE8과 같은 오래된 브라우저는 요소명으로 호출하려면 Angular가 템플릿을 컴파일하기 이전에 DOM이 생성되어야 한다.

다음 코드를 보도록 하자.

<head>
  <script>
  document.createElement('my-directive');

  //css에서 사용할 때 필요하다.
  document.createElement('my:directieve');
  </script>
</head>

---

### Angular 제공 지시자

---

**내장 지시자** 라고 한다. Angular 버전마다 다른데 지시자 목록은 Angular 홈페이지 API 문서를 보면 확인할 수 있다.

[https://docs.angularjs.org/api](https://docs.angularjs.org/api) 해당 페이지에서 확인해 볼 수 있다.

---

### 사용자 정의 지시자

---

**웹 UI 컴포넌트를 만들 수 있는 메커니즘** 이 있는데 아마 Angular의 가장 큰 매력 중 하나가 아닐까 한다.
심지어 이것이 양방향 바인딩이 되고 도메인 특화된 HTML 태그를 구성할 수도 있다.

    <tabs>
      <pane title="패널 1">
        <title>패널 1</title>
        <p>hello 패널 1</p>
      </pane>
      <pane title="패널 2">
        <title>패널 2</title>
        <p>hello 패널 2</p>
      </pane>
    </tabs>

---

### 간단한 지시자 정의

---

지시자를 한번 만들어 보도록 하자.

정말 간단히 출력하는 예제다.

    <!DOCTYPE html>
    <html ng-app = "sampleApp">
      <head>
        <meta charset="utf-8" />
        <title>example 2.25</title>
      </head>
      <body>
        <div hello name = 'angularJS'></div>
        <!--angular file-->
        <script src="../angular.js" type="text/javascript"></script>
        <script type="text/javascript">

          angular.module('sampleApp', [])
            .directive('hello', function(){
              return function(scope, iElement, iAttrs, controller){
                  iElement.html("<h1>hello " + iAttrs.name + "</h1>")
              };
            });
        </script>
      </body>
    </html>

한번 분석을 해보자.

directive 메서드를 사용한 코드를 보면, 첫번째 인자로 지시자의 이름을 요구한다. 이는 카멜표기법으로 작성해야 한다고 앞서 이야기 했다.
그 다음 지시자 설정 함수를 줄 수 있는데, 이 함수에서 다른 서비스의 주입을 받고 싶을 때는 서비스 이름으로 파라미터에 넣어주도록 하자. 그럼 `$log` 를 한번 넣어 보도록 하겠다.

    angular.module('sampleApp', [])
      .directive('hello', function($log){
        return function(scope, iElement, iAttrs, controller, transcludeFn){
            $log.log("<h1>hello " + iAttrs.name + "</h1>");
            iElement.html("<h1>hello " + iAttrs.name + "</h1>")
        };
      });

서비스의 주입이나 `$log` 서비스와 같은 부분은 다음에 **의존관계 주입과 서비스** 부분에서 자세히 보도록 하고, 지시자에 대해서 알아보자.

directive 메서드에서 두 번째 인자인 지시자 설정 함수는 함수나 객체를 반환해야 한다. 위 예제 코드에서는 함수를 반환했는데, 이 함수는 **링크 함수**다.

**링크 함수** 는 해당 지시자가 적용된 `DOM`에 연결된 함수를 의미한다. 이 연결 함수는 순서대로 scope 객체, 연결된 요소 객체, 속성 객체, 컨트롤러 객체가 주어진다.

1.  scope 객체
  * scope 객체를 이용해 데이터 변경을 감지하거나 외부 컨트롤러와 데이터 바인딩할 때 사용한다.
2.  연결된 요소 객체
  * AngularJS는 제이쿼리와 뛰어난 호환성을 제공하지만 제이쿼리 없어도 사용할 수 있게 제이쿼리 라이트 버전을 제공한다. 제이쿼리를 해당 페이지에서 사용하면 연결된 DOM을 감싸고 있는 제이쿼리 객체가 반환되고 그렇지 않으면 AngularJS가 구현한 제이쿼리 라이트 객체가 반환된다. 해당 객체에는 html(), append(), css() 등 제이쿼리에서 제공하는 DOM을 제어할 수 있는 다양한 메서드가 있다.
3.  속성 객체
  * 연결된 요소에서 속성명과 속성값을 가지는 속성 객체다. 예를 들어, `<tap title="hello" > </tap>` 이라는 요소가 있을 때 해당 요소에 대한 속성 객체로서 title 이라는 속성을 이용해 hello를 가지고 올 수 있다. 여기서는 `iAttrs.name`을 보도록 하자.
4.  컨트롤러 객체
  * 지시자에서는 해당 지시자가 사용하는 여러 요소가 공통으로 공유하는 컨트롤러를 정의 할 수 있다. 여기서는 따로 컨트롤러를 등록하지 않았다. 이 부분의 컨트롤러는 `ng-controller`로 등록하는 컨트롤러가 아니라. 지시자에서 등록하는 컨트롤러다. 이것은 잠시 후 더 알아보자.
5.  transclude 함수
  * transclude 옵션을 사용할 경우, 포함되는 페이지 영역에 전달할 scope에 대한 링크 함수를 정의한다. 삽입되는 페이지 영역에 적절한 scope를 미리 연결하기 위해 사용한다.

다시 정리하면, directive 메서드의 첫 번째 인자로는 지시자 이름을 주고 그 다음에는 지시자 설정 함수를 준다. 이 설정 함수가 함수를 반환하면 링크 함수를 반환하는 것이고 객체를 반환하면 설정 객체를 반환한다.

이제 설정 객체를 알아보자.

---

### 지시자 설정 객체

---

지시자 설정 함수에서 반환되는 객체를 **지시자 설정 객체** 라고 한다고 했다. 이 설정 객체로 AngularJS가 지시자를 만들게 된다. 앞에서 본 에제의 hello 지시자에 설정 객체를 만들어 보겠다.

    <!DOCTYPE html>
    <html ng-app = "sampleApp">
      <head>
        <meta charset="utf-8" />
        <title>example 2.26</title>
      </head>
      <body>
        <div hello name = 'angularJS'></div>
        <!--angular file-->
        <script src="../angular.js" type="text/javascript"></script>
        <script type="text/javascript">

          angular.module('sampleApp', [])
            .directive('hello', function($log){
              return {
                name : 0,
                priority : 0,
                template : '<div></div>',
                // templateUrl : 'directive.html',
                replace : false,
                transclude : false,
                restrict : 'A',
                scope : false,
                // require : 'ngModel',
                controller : function($scope, $element, $attrs, $transclude){},
                compile : function compile(tElement, tAttrs){
                  return {
                    pre : function preLink(scope, iElement, iAttrs, controller){

                    },
                    post : function postLink(scope, iElement, iAttrs, controller){
                      $log.log("<h1>hello " + iAttrs.name + "</h1>");
                      iElement.html("<h1>hello " + iAttrs.name + "</h1>");
                    }
                  }
                  // 또는
                // return function postLink(scope, iElement, iAttrs, controlle) { }
                },
                // 또는
                // link: {
                //  pre: function preLink(scope, iElement, iAttrs, controller) { },
                //  post: function postLink(scope, iElement, iAttrs, controller){ }
                // }
                // 또는
                // link: function postLink(scope, iElement, iAttrs, controller) {}
              };
            });
        </script>
      </body>
    </html>

이전 예제의 지시자보다 훨씬 많은 정보가 들어갔다. 하나씩 알아 보자.

* name (문자열)
  - 지시자에서 사용하는 scope의 이름. 기본으로 지시자의 이름이 scope의 이름이 된다.
* priority (숫자)
  - 지시자가 적용된 DOM에 여러 지시자가 적용될 수가 있다. 이 때 우선순위를 줄 수 있는데, 숫자로 주며 큰 숫자가 먼저 호출된다.
* terminal (true/false)
  - 값이 true면 마지막에 호출 된다. 기본 false
* scope (true/false/객체)
  - 지시자에서 사용하는 scope 객체에 대한 설정 정보를 준다. 여기서 줄수 있는 값은 true/false/객체 인데 이 의미는 다음과 같다.
    + true : 해당 지시자 필요로 하는 새로운 scope가 생성
    + false : 해당 지시자가 적용된 DOM은 별도의 scope를 생성하지 않는다. 해당 지시자를 감싸고 있는 부모 DOM에서 사용하는 scope를 사용하게 된다. 대부분 `ng-controller`에서 생성한 scope를 사용한다.
    + 객체 : 객체를 선언하면 새로운 scope를 생성한다. 하지만 부모 scope와의 상속은 없다. 완전 독립된 scope 객체가 생성된다. 이 객체는 지시자 내부에서 사용하지만 부모 scope와의 관계가 있는 속성들을 정의한다. 범하기 쉬운 실수로 해당 객체가 지시자와 연결된 모델이라고 생각하여 컨트롤러에서 하는 것과 비슷하게 모델을 정의하는데 이 객체는 부모 scope와의 관계를 정의하는 설정 정보를 넣는 곳이다. 다음은 객체 속성에 줄 수 있는 값이다. 예를 들어 `{name : "@"}`또는 `{name : "@title"}`과 같은 형태로 줄 수 있다. 그러면 name은 해당 지시자에서 사용하는 scope에 대한 속성명이다. 다음은 속성 값으로 줄 수 있는 기호들이다.
      - "@" 또는 "@속성명" -> 연결된 DOM의 속성값을 내부 scope의 속성과 연결한다. DOM 속성값은 항상 문자열이므로 scope속성의 값도 문자열이 된다. "@"만 사용하게 되면 DOM 속성의 이름과 내부 속성의 이름이 같다고 판단한다.
      - "&" 또는 "&속성명" -> 부모 scope를 기준으로 주어진 표현식을 계산한다. 주어진 DOM의 속성값은 표현식이 되고 해당 표현식을 감싸는 함수의 레퍼런스가 scope 속성의 값으로 주어진다. 표현식을 감싸는 함수에 인자를 전달 하고 싶을 경우 인자명을 속성명으로 하고 속성값을 인자에 전달할 값으로 한 객체를 전달할 수 있다. 예를 들어, DOM의 속성값이 `call(number)`이면 지시자에서 `call({number : "000-000"})` 으로 인자를 전달할 수 있다.
      - "=" 또는 "=속성명" -> 부모 scope의 속성과 지시자 내부 scope의 속성 사이에 양방향 연결을 설정한다. 부모 scope의 속성은 DOM 속성의 값을 이용해 가져온다. 예를 들어, 부모 scope가 `{parentscopeName : 'parent'}`이고 지시자 내부 scope가 `{dirscope : "myAttr"}`로 설정되어 있을 때, `<my-dir my-attr="parentscopeName" > </my-dir>`로 DOM을 작성했다면 myDir 지시자 내부 scope의 dirscope에 "parent" 값이 바인딩된다. 부모 scope의 parentscopeName 값이 바뀔 때마다 myDir 내부지시자의 scope의 dirscope의 값도 같이 바뀌게 된다. 또한 반대로도 바뀌게 된다. 부모 scope에 연결된 속성이 없다면 `NON_ASSIGNABLE_MODEL_EXPRESSION` 에러가 발생하는데 없을 경우 에러가 나지 않으려면 "=?" 또는 "=?속성명"으로 설정해야 한다.
    + controller (함수) : 지시자에서 사용할 컨트롤러 함수. 다음과 같은 인자가 있다.
      - $scope -> 지시자에서 사용되는 scope 객체
      - $element -> 지시자의 요소객체(제이쿼리나 제이쿼리 라이트로 DOM 객체를 감싸고 있다)
      - $attrs -> 지시자의 속성 객체(AngularJS의 속성 타입)
      - $transclude -> transclude 옵션을 사용할 경우 포함되는 페이지 영역에 전달할 scope에 대한 링크함수를 정의한다. 삽입되는 페이지 영역에 적절한 scope를 미리 연결하기 위해 사용한다.
    + restrict ("EACM" 문자조합) : 지시자가 호출되는 방식을 결정한다. "EACM" 문자 조합으로 문자열을 줄 수 있다. 각 문자의 의미는 다음과 같다.
      - E -> 요소명을 이용한 호출 (`<my-directive></my-directive>`)
      - A -> 요소의 속성을 이용한 호출 (`<span my-directive= "expression" ></span>`)
      - C -> 요소의 클래스를 이용한 호출 (`<span class="my-directive: expression;"></span>`)
      - M -> 코멘트를 이용한 호출 (`<!-- directive: my-directive expression -->`)
    + template (문자열/ 함수) : 지시자의 템플릿을 설정한다. 지시자를 적용한 DOM은 해당 템플릿으로 대체된다. 대신 DOM의 속성과 css 클래스는 모두 복사된다. 함수로 작성하게 되면 tElement와 tAttrs를 인자로 받을 수 있다. tElement는 적용된 DOM의 제이쿼리 라이트나 제이쿼리 객체이고 tAttrs는 속성 객체다. 해당 함수는 템플릿을 문자열로 반환해야 한다.
    + templateUrl (문자열/함수) : template와 똑같은 역할을 한다. 단, 템플릿을 주어진 url을 통해 읽어드린다. 함수반환은 url문자열이다.
    + replace(true/flase) : 적용된 HTML 요소를 교체할지 여부를 결정한다. true로 값을 주면 적용된 요소 자체가 템플릿으로 교체되고 false로 값을 주면 요소 자체는 바뀌지 않고 내부 내용만 바뀐다.
    + transclude (true/ 'element') : 적용된 HTML 요소의 내부 내용을 컴파일하여 지시자에서 사용할 수 있게 한다. 컴파일한다는 의미는 내부 내용에 표현식이 작성됬거나 다른 지시자가 사용됬으면 해당 표현식의 계산이 되고 다른 지시자와 연결된 지시자 함수가 실행되어 그 결과가 내부 내용에 반영된다는 것이다. 템플릿에서 `ng-transclude`지시자를 이용해 적용된 HTML 요소의 내부 내용에 접근할 수 있다. true로 값을 주면 적용한다는 것이고 "element"라고 문자열을 주게되면 요소의 내부 내용뿐만 아니라 요소 전체를 지시자에서 사용한다는 의미다. 요소에 적용된 다른 지시자까지 모두 컴파일된다.
    + compile (함수) : 컴파일 함수를 정의한다. 해당 함수에서는 적용된 DOM을 변경하는 데 사용한다. compile 함수는 반드시 link 함수나 pre와 post를 속성으로 가지는 객체를 반환해야 한다. pre 속성에는 pre link 함수가 정의되고 post는 post link 함수가 정의되야 한다. 그러므로 다음 link 설정과 같이 사용할 수 없다. compile 함수에서 link 함수 또한 정의하기 때문이다. compile 함수에서 사용할 수 있는 인자는 다음과 같다.
      - tElement -> 연결된 DOM을 감싸고 있는 jqLite 또는 제이쿼리 인스턴스다. Link 함수와 같다.
      - tAttrs -> 속성객체다
      - Link(함수) -> 링크함수를 정의한다 DOM의 이벤트 리스너를 등록하거나 DOM을 변경하는 행위를 한다. 링크 함수는 템플릿이 컴파일 된 뒤에 실행 된다. 대부분 지시자의 로직을 여기서 구현하게 된다. 해당 함수 위의 compile 함수 설정과 같이 사용할 수 없다. 링크 함수의 인자는 위의 간단한 지시자 정의에서 설명했다.

---

### 자체 템플릿을 가지는 지시자

---

앞에서 만든 Hello 지시자를 좀더 업그레이드 해볼 예정이다. 앞서 설명 했던 template를 사용해서 시도해 보겠다.

    <!DOCTYPE html>
    <html ng-app = "sampleApp">
      <head>
        <meta charset="utf-8" />
        <title>example 2.26</title>
      </head>
      <body>
        <div hello name = 'angularJS'></div>
        <!--angular file-->
        <script src="../angular.js" type="text/javascript"></script>
        <script type="text/javascript">

          angular.module('sampleApp', [])
            .directive('hello', function(){
              return {
                template : "<h1>hello <span>name</span></h1>",
                restrict : "AE",
                link : function link (scope, iEl, iAt, ctrl){
                  iEl.find("span").text(iAt.name);
                }
              }
            });
        </script>
      </body>
    </html>

이전에는 링크 함수에서 DOM을 생성했지만, 지금은 template 설정으로 해당 지시자의 템플릿을 변경했다. 그러나 여기서 아쉬운 점이 있는데, 하나는 **템플릿을 변경하려면 지시자 함수가 정의된 자바스크립트 소스를 직접 수정** 해야 한다는 것이고, 두번째는 **링크 함수에서 템플릿의 마크업 구조를 정확하게 알아야만 데이터를 제대로 표현할 수 있다** 는 것이다. 그럼 이 두가지를 개선해보자. `templateUrl`을 사용할 것이고, 지시자 함수를 변경하기 앞서, 템플릿 파일을 만들어 볼 것이다. 먼저 `template/helloTpl.html`을 만들고 다음을 넣어두자.

`<h1>hello <span>name</span></h1>`

템플릿 파일은 위와 같이 HTML 태그로 시작하지 않는다 필요한 부분만 잘라 만든다.

그럼 설정을 바꿔 보자

    <!DOCTYPE html>
    <html ng-app = "sampleApp">
      <head>
        <meta charset="utf-8" />
        <title>example 2.26-1</title>
      </head>
      <body>
        <div hello name = 'angularJS'></div>
        <!--angular file-->
        <script src="../angular.js" type="text/javascript"></script>
        <script type="text/javascript">

          angular.module('sampleApp', [])
            .directive('hello', function(){
              return {
                templateUrl : "template/helloTmpl.html",
                restrict : "AE",
                link : function link (scope, iEl, iAt, ctrl){
                  iEl.find("span").text(iAt.name);
                }
              }
            });
        </script>
      </body>
    </html>

다음과 같이 바꿀 수 있다. 참고로 크롬에서는 `file:` 형태가 지원이 안될 수 있으므로, 설정을 바꾸던지 다른 브라우저로 확인하면 된다. 만약 서버를 올린 이후로 해당 설정을 한다면 고려할 필요 없다.

이렇게 템플릿을 외부 파일로 바꾸면 지시자 정의 코드와 템플릿 코드를 깔끔히 분리할 수 있다. 즉, **디자인 변경이나 템플릿 문서 구조의 변경과 자바스크립트 로직 사이를 분리할 수 있는 것** 이다. 그럼 이제 링크 함수에서 템플릿 문서 구조를 잘 알고 있는 이 아쉬운 점을 바꿔보자.

우리는 앞서 표현식을 배웠는데, 이 표현식으로 scope의 데이터를 템플릿에서 표현한 적이 있다. 그럼 지시자의 템플릿에서도 접근이 가능하다.

helloTmpl.html 파일은

`<h1> hello <span>{ {name} }</span></h1>`

으로 변경하고, 지시자 파일은

    <!DOCTYPE html>
    <html ng-app = "sampleApp">
      <head>
        <meta charset="utf-8" />
        <title>example 2.26-2</title>
      </head>
      <body>
        <div hello name = 'angularJS'></div>
        <!--angular file-->
        <script src="../angular.js" type="text/javascript"></script>
        <script type="text/javascript">

          angular.module('sampleApp', [])
            .directive('hello', function(){
              return {
                templateUrl : "template/helloTmpl2.html",
                restrict : "AE",
                link : function link (scope, iEl, iAt, ctrl){
                  scope.name = iAt.name;
                }
              }
            });
        </script>
      </body>
    </html>

다음과 같다.

이제 명확한 분리가 되며 문서 구조를 정확히 알 필요가 없어졌다. 그러나 한가지 더 해주어야 하는데, 이렇게 간단히 scope에서 데이터를 연결하는 일은 사실 지시자 컨트롤러에서도 할 수 있다. 다음을 보자.

    <!DOCTYPE html>
    <html ng-app = "sampleApp">
      <head>
        <meta charset="utf-8" />
        <title>example 2.26-3</title>
      </head>
      <body>
        <div hello name = 'angularJS'></div>
        <!--angular file-->
        <script src="../angular.js" type="text/javascript"></script>
        <script type="text/javascript">

          angular.module('sampleApp', [])
            .directive('hello', function(){
              return {
                templateUrl : "template/helloTmpl2.html",
                restrict : "AE",
                controller : function($scope, $element, $attrs, $transclude){
                  $scope.name = $attrs.name;
                }
              }
            });
        </script>
      </body>
    </html>

이렇게 링크 함수를 정의하지 않고 지시자 컨트롤러를 정의하 게 되었다. 그런데 여기는 좀 문제가 있다 scope 설정인다. 하나의 같은 문서에 다음과 같이 작성해보자.

    <div hello name="angularJS"></div>
    <div hello name="google"></div>
    <div hello name="naver"></div>

결과는 우리가 생각한 것과 다르게 모두 naver 가 나온다. 이유는 모두 같은 scope를 사용하기 때문에 마지막 호출된 지시자가 이전의 scope.name을 바꾸어 버렸기 때문이다.

---

### scope 완전 정복

---

지시자를 만들 때 가장 중요한 부분이 바로 **scope를 어떻게 설정할 것인가?** 이다. scope를 잘못 설정하면 의도하지 않은 결과가 발생하므로 분명한 의도에 맞는 scope를 설정해야 한다. 가령 지시자를 재사용할 수 있는 컴포넌트라 생각하고 만들려면 지시자가 사용하는 scope는 다른 지시자와 독립적인 공간이어야 하고, 같은 지시자가 하나의 페이지에서 여러번 사용되어도 서로 영향을 주지 않아야 한다. 하지만 특정 DOM을 간단히 조작하는 경우라면 별도로 만들 필요가 없다.

여기서 scope라는 속성을 이용하게 되고, 위 예제의 경우는 **별도의 새로운 scope를 만들지 않았으므로** false로 설정되어 있는 경우다. 즉, hello 지시자 템플릿에 사용한 표현식은 부모 scope를 이용해 계산된다. 따라서 모든 지시자에 영향이 간다.

그럼 **부모 scope를 상속받는 scope 설정** 을 보자.

scope 속성을 true로 하면, 부모 scope를 상속받는 새로운 scope가 생성된다.

    <!DOCTYPE html>
    <html ng-app = "sampleApp">
      <head>
        <meta charset="utf-8" />
        <title>example 2.27</title>
      </head>
      <body ng-controller = "demoCtrl">
        <div hello name='google'></div>
        <div hello name='naver'></div>
        <div hello></div>
        <!--angular file-->
        <script src="../angular.js" type="text/javascript"></script>
        <script type="text/javascript">

          angular.module('sampleApp', [])
            .controller('demoCtrl', ['$scope',function($scope){
              $scope.name = "Ctrl 에서 사용된 name 모델";
            }])
            .directive('hello', function(){
              return {
                templateUrl : "template/helloTmpl2.html",
                restrict : "AE",
                scope : true,
                controller : function($scope, $element, $attrs, $transclude){
                  if($attrs.name) $scope.name = $attrs.name;
                }
              }
            });
        </script>
      </body>
    </html>

scope 설정은 true로 해주었고, 그러면 별도의 scope가 설정이 되어 태그별 name값이 이전 지시자의 scope를 덮어 씌우지 않는다. 한가지 확인해 볼 것이 있는데, 마지막 hello 지시자가 적용된 `<div hello></div>` 에서 부모의 값인 `Ctrl 에서 사용된 name 모델`가 설정되었다는 점이다. 이는 hello 지시자의 내부 scope가 부모 scope로부터 상속받았으므로 `demoCtrl`컨트롤러 함수의 `$scope.name`의 값을 참조한 것이다. 이건 그런데 원하는 값이 아닐 수 있다. 부모의 `$scope`에 영향을 받으므로 지시자를 만들 때 이를 신경 써야 한다는 것이다.

---

### @ 를 이용한 독립 scope 설정

---

먼저 독립 scope를 만드려면 지시자 설정 객체의 **scope 속성에 객체 리터럴을 이용해 객체를 선언** 해야 한다. 그리고 **해당 객체에서 부모 객체와의 연관성을 정의** 한다.

`scope : {}`

이제 부모 객체와 연관된 지시자 내부 scope에서 사용할 scope 객체 송성명에 `@` 혹은 `@연결된 DOM속성명`을 값으로 줄 수 있다.

`scope : {name : "@"}` 또는 `scope : {name : "@to"}`

그럼 좀더 발전 시켜 보자.

    <!DOCTYPE html>
    <html ng-app = "sampleApp">
      <head>
        <meta charset="utf-8" />
        <title>example 2.28</title>
      </head>
      <body ng-controller = "demoCtrl">
        <div hello to='google'></div>
        <div hello to='naver'></div>
        <div hello></div>
        <!--angular file-->
        <script src="../angular.js" type="text/javascript"></script>
        <script type="text/javascript">

          angular.module('sampleApp', [])
            .controller('demoCtrl', ['$scope',function($scope){
              $scope.name = "Ctrl 에서 사용된 name 모델";
            }])
            .directive('hello', function(){
              return {
                templateUrl : "template/helloTmpl2.html",
                restrict : "AE",
                scope : {name : "@to"}
              }
            });
        </script>
      </body>
    </html>

다음과 같이 독립이 되었으므로, 부모 scope의 name 속성을 상속받지 않는다. `@to` 를 주어 지시자가 적용된 `<div>` 태그의 to 속성에 대한 값이 지시자 내부 scope의 name 속성에 연결되었다.

이제 이전의 컨트롤러 코드도 필요 없어 졌다. 한가지 더 응용을 해보고자 한다.

`$scope.helloList = [{name : "google"}, {name : 'naver'}, {name : 'angularJS'}];`

그리고 템플릿을 다음과 같이 하자

`<div ng-repeat="helloSb in helloList" hello to="{ {helloSb.name} }"></div>`

아마 원하는 결과가 나올 것이다. 이렇게 `@`를 통해 연결된 DOM의 속성값에 표현식을 사용하여 부모 scope의 값을 전달할 수 있는 것을 보았다.

이후 `&`를 이용한 독립 지시자 부터는 다음 포스팅에서 이어 하겠다.


앞서 적어둔 모든 소스는 [이곳](https://github.com/koocci/AngularJS-examples) 에서 보실 수 있습니다.
