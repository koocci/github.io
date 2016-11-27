---
layout: post
title:  "[AngularJS] AngularJS 블루프린트 4"
date:   2016-11-25 10:40:11 +0900
categories: AngularJS
tags: [Angularjs, 프로그래밍, MEAN stack, 기초, 블루프린트, IONIC]

---

# AngularJS로 빠르게 프로토타입 만들기

---

![computer](http://farm6.static.flickr.com/5081/5347580266_f1bd0f238d_z.jpg)

이전에 우리는 개발을 도와줄 다양한 도구를 알아보았다. 이제 AngularJS가 프로토타입을 만들기에 얼마나 훌륭한 도구인지 알아보자.

빠른 프로토타입은 개발하려고 계획 중인 웹 어플리케이션의 목표를 검증하는 데 좋은 방법이다.

`프로토타입을 이용하면 사용자의 클릭 흐름과 사용성 이슈를 파악하거나 초기에 나왔던 요구 사항이 정말로 유용한 것인지 등 애플리케이션의 여러 측면에 걸쳐서 사용자나 다른 이해관계로부터의 유용하고 영향력 있는 피드백을 받을 수 있다.`

과거의 프로토타입은 와이어 프레임을 이용하거나 개발자가 서로 연결되어 있는 HTML 페이지로 웹 애플리케이션의 기능을 흉내 내는 사이트를 만들어 사용했다.

전자는 애플리케이션이 완성됬을 때 어떻게 보이고 동작할지 정확하게 예측할 수 없고 후자는 개발에 시간이 더 걸리는 특징이 있는데, 대형 애플리케이션일 경우에는 더욱 그렇다.

이제는 AngularJS 덕분에 프로토타입 개발이 한층 쉬워졌으며, 짧은 시간 안에 더 적은 코드로 유사하게 동작하는 프로토타입을 개발할 수 있다.

그럼 다음과 같이 진행하겠다.

1. 프로토타입으로 만들 애플리케이션의 다양한 구성 요소들을 알아본다.
2. 그리드 레이아웃에 대해 이해하고 어떻게 부트스트랩이 동작하는지 알아본다.
3. AngularUI를 이용해 캐로설, 아코디언, 모달 창과 같은 UI dythemfdmf cnrkgksek.
4. 파셜(partials)을 이용해 이식 가능한 페이지를 작성하는 법을 배운다.
5. 동적인 데이터를 흉내내는 더미 데이터 모델을 생성한다.
6. 컨트롤러와 뷰를 연결하는 라우트(Routes)를 사용한다.

---

### 프로토타입으로 만들 애플리케이션의 이해

---

이제 우리는 `건강한삶(Healthy Living)` 이라는 가상 웹사이트를 위한 상호작용하는 프로토타입을 생성한다. 다음과 같이 네 개의 화면으로 구성된다.

1. 홈페이지: 캐로설(carousel), 히어로 유닛(hero unit1), 세 개의 주요 내용을 담은 블록으로 구성된다.
2. 기사 목록: 아코디언 뷰로 기사 목록을 보여준다.
3. 갤러리: 사진과 제목, 짧은 설명, 별 평점을 포함하는 갤러리
4. 구독자들: 열(column)로 그룹핑해주고, 엑셀 같은 인라인 편집 기능을 제공하는 데이터 그리드를 이용해 구독자의 리스트를 보여준다.

---

### 그리드 레이아웃과 부트스트랩 소개

---

HTML 페이지를 작성하는 일은 언제나 웹 디자이너의 몫이었고, 개발자들은 HTML 페이지의 작성을 요청받으면 도망가기 일쑤였다.

HTML 페이지 디자인과 관련해 또 다른 문제는 모든 디자이너들이 HTML 페이지를 만드는 데 DOM 엘리먼트와 선호하는 CSS 클래스를 이용해 레이아웃을 구성하는 그들의 방법이 있다는 것이다.

이렇게 생성된 HTML 페이지는 동적 페이지 생성을 위해 개발자가 해당 페이지를 전달받거나 같은 프로젝트에 두 디자이너가 참여할 경우 스트레스의 원인이 된다.

**그리드 레이아웃** 은 **이름을 짓는 규정과 DOM 구조에 대해 모두 동일하게 이해** 할 수 있도록 도와준다. 더 핵심적인 특징은 **HTML 페이지를 작성하는 시간을 줄여주면서 브라우저 호환성도 확보** 하게 해준다.

960 그리드 시스템이나 블루프린트가 초기에 사용했던 그리드 시스템이었는데, 최근에는 부트스트랩, 파운데이션, 시맨틱 UI가 프론트엔드 페이지를 작성하는 매우 대중적인 도구가 되었다.

여기서 호환 버전은 **부트스트랩 3.1.x** 다.

---

### 그리드 시스템 이해하기

---

최근에 그리드 시스템이 웹 개발 프로세스에서 폭넓게 사용되고 있다. **그리드 시스템** 은 **표준화된 치수들과 주로 사용되는 UI 구성 요소들의 표시 방식등을 표준화해 HTML 제작 과정을 간소화** 하는 것이 목표다.

부트스트랩은 반응형, 플루이드, 고정 레이아웃에서 사용 가능한 12열로 구성된 그리드 시스템이다. 거의 모든 UI 스타일에 대한 요구 사항을 만족시키는 사전 정의된 클래스의 전체 세트를 제공한다.

다음은 자주쓰는 클래스들 이다.

* `.col-md-*`
  - 992px이나 더 큰 해상도를 가지는 중간 크기의 장치(예를 들면, 데스크톱)에 적용되는 내용의 블록의 폭 크기다.
* `.col-xs-*`
  - 768px이나 더 작은 크기를 가지는 장치를 위해 사용한다.
* `.col-sm-*`
  - 768px이나 더 큰 크기를 가지는 태블릿 장치를 위해 사용한다.
* `.col-lg-*`
  - 1200px보다 더 큰 크기를 가지는 대형 장비를 위해 사용한다.
* `.col-md-offset-*`
  - 왼쪽부터 공간을 비워 놓기 위해 사용하는 오프셋 값이다.
* `.row`, `.row-fluid`
  - 공간을 행으로 나누기 위해 사용한다. 플루이드 레이아웃의 경우 .row-fluid를 사용한다.
* `.container`, `.container-fluid`
  - 엘리먼트의 너비를 940px로 설정하고 페이지의 수평 중앙에 위치시킨다. 플루이드 레이아웃의 경우 .container-fluid를 사용한다.
* `.lead`
  - 단락을 강조하고 싶을 때 사용한다. 주로 히어로 유닛이나 페이지 제목 밑에 요약을 표시할 때 사용한다.
* `.text-left`, `.text-center`, `.text-right`
  - 텍스트를 왼쪽, 중간, 오른쪽으로 정렬할 때 사용한다.
* `<blockquote></blockquote>`, `<cite></cite>`
  -  blockquote 태그는 인용한 문구에 사용하고 cite 태그는 출처를 감싸줄 때 사용한다.
* `.pull-left`, `.pull-right`
  - 엘리먼트가 속해 있는 컨테이너의 오른쪽이나 왼쪽으로 보내는 역할을 한다.
* `.btn primary`, `.btn-success`, `.btn-info`, `.btn-warning`, `.btn-danger`, `.btn-inverse`
  - 버튼이나 앵커 엘리먼트를 꾸미는 역할을 한다. 각 클래스에 따라 파란색 부터 검은색까지 다른 색상을 적용한다.

부트스트랩 패키지는 CSS, 자바스크립트 파일과 그리프아이콘(glyphicons)이 들어있는 이미지(/img) 폴더를 포함한다. CSS 파일은 그리드 시스템을 위한 모든 스타일을 포함하고 사전에 정의된 UI 구성요소들을 포함하고 있다. 자바스크립트 파일은 아코디언(accordion), 탭, 모달 창이나 프로그레스 바, 데이트 피커(date picker) 같은 UI 위젯을 생성하는 라이브러리를 포함한다.

---

### Angular UI 소개

---

Angular UI는 **Angular 앱 개발을 더욱 생산적으로 만들어주는 미니 프로젝트들의 묶음** 이다. 한번 무엇이 있는지 알아보자(이 책을 쓸 당시를 기준이므로 현재와 조금 다를 수 있다)

**UI-Utils**

UI-Utils 은 유틸리티 패키지로 다양한 종류의 유틸리티들을 애플리케이션에서 사용할 수 있게 해준다.

* IE Shiv : 익스플로러 8이나 그 이하 버전에서 커스텀 태그를 사용하도록 한다.
* jQuery Passthrough : uiJq 지시자를 이용하면 jQuery를 사용하기 위해 새로운 지시자를 만드는 대신 직접 사용할 수 있다.
* Event Binder : AngularJS 에서 지원하지 않는 이벤트의 콜백도 연결할 수 있게 한다.
* Keypress : 키보드 입력에 이벤트를 연결시켜준다.
* Mask : 조건으로 데이터를 걸러낼 수 있게 한다.
* Validate : 커스텀 검증자와 표현식을 만들어준다.
* Reset : 모델을 초기화시켜주는 아이콘이나 링크를 생성한다.
* Scrollfix : ui-scrollfix 클래스를 엘리먼트에 추가한다.
* Show / Hide / Toggle : ng-show와 ng-hide를 사용하는 대신, ui-toggle 지시자 하나만을 사용한다.
* Route Matching : 현재 페이지의 경로를 매칭시켜준다.
* Highlight : 스코프 모델에 존재하는 문자열을 강조할 때 사용한다.
* Inflector : 공백을 밑줄로 바꾸거나 문자열을 카멜케이스(camelCase)로 만들어주는 것과 같이 문자열을 다른 포맷으로 바꾸고 싶을 때 사용한다.
* Unique : 배열 안에 중복된 아이템을 제거한다
* Format : 이 필터는 어떤 종류의 문자열 치환도 가능하게 해준다.

**UI-Modules**

UI-Modules 프로젝트는 달력이나 구글 지도, TinyMCE나 CodeMirrorAce 같은 에디터들을 손쉽게 추가하도록 해준다.

**UI-Bootstrap**

UI-Bootstrap은 부트스트랩의 AngularJS 네이티브 구현이다. 앞으로 알아보겠지만 캐로설이나 아코디언, 탭같은 UI 컨트롤을 추가하는 작업이 한층 쉬워진다. UI-Bootstrap은 원본 CSS와 글리프아이콘들을 있는 그대로 사용한다는 것을 알아두자. AngularJS 지시자를 사용하기 위해 자바스크립트 파일만 수정되었다.

**NG-Grid**

NG-Grid는 AngularJS에 데이터 그리드를 추가할 때 사용한다. NG-Grid 는 상당수의 설정 가능한 옵션이 있는데, 정렬 가능한 열을 그리드에 추가하거나 엑셀과 유사한 편집 옵션등을 포함한다.

**UI-Router**

UI-Router는 중첩 라우팅을 제공하는 새로운 방식의 라우팅이다.

**IDE 플러그인**

다양한 문서 편집기에서 AngularJS의 지원을 받을수 있는 플러그인이나 확장 프로그램을 말한다.
이번에는 UI-Bootstrap과 NG-Grid 프로젝트를 써볼 생각이다.

---

### '건강한 삶' 사이트의 프로토타입 제작

---

![phone](http://farm6.static.flickr.com/5229/5684252431_078b33e0b9_z.jpg)

지금부터는 실습을 위해 가상 웹사이트인 `건강한 삶`의 상호작용하는 네 개의 페이지로 구성된 프로토타입을 만들 것이다.
사이트의 홈 영역은 완전히 동작하는 캐로설과 히어로 유닛, 각각의 기능을 제공하는 세 개의 섹션으로 구성된다.

그럼 애플리케이션 생성부터 시작해 보자.

1. `건강한 삶(Health Living)`의 줄임말을 이용해 hl 폴더를 생성한다.
2. 요맨을 설치했다고 가정하고 터미널 프로그램을 실행하자. 다음과 같은 코드로 스캐폴딩 앱을 생성한다.
  - mkdir hl
  - cd hl
  - yo angular

3. 프롬프트 창에서 '부트스트랩을 설치하겠습니까?' 라고 물으면 y를 입력해야한다.
4. Sass와 캠퍼스에 관해서는 N으로 한다.
5. 이 후 기본 설정을 사용한다.
  노드 패키지 매니져가 여러 파일들을 불러와서 앱의 스캐폴딩을 생성하는 것을 볼 수 있다. 모든 절차가 성공적으로 종료되고 명령 프롬프트로 동라올 떄까지 기다리자.
  이 후 완료 되면 구조를 볼 수 있고, 보어(bower)를 이용해서 UI-bootstrap을 설치하자.

6. 터미널에 다음과 같이 입력한다. `bower install angular-bootstrap`
  그럼 app/bower-components 아래에 angular-bootstrap 폴더를 생성한다.
  작성 중인 애플리케이션에서 Angular 부트스트랩을 사용하기 위해 자바스크립트 파일을 포함시키자.

7. app/index.html 파일을 열고 다음 라인을 추가하자. `<script src="bower_components/angular-bootstrap/UI-bootstrap-tpls.js"></script>`

`bower_components/angular-bootstrap` 폴더를 살펴보면 각각 압축된 버젼을 포함해 두 종류의 파일을 볼 수 있다.

  - ui-bootstrap.js: 모든 지시자를 포함하고 있지만 템플릿은 아니다. 기본 템플릿을 사용하지 않고 처음부터 개인화한 템플릿을 작성하고 싶다면 해당 파일을 사용하라.
  - ui-bootstrap-tpls.js: 모든 지시자와 기본 부트스트랩 템플릿 코드를 포함한다. 템플릿에 어떤 수정도 가하지 않을 계획이라면 해당 파일을 프로젝트에 포함시키자.

---

### ui.bootstrap 의존성 추가

---

다음은 Angular 부트스트랩의 의존성을 프로젝트에 추가할 것이다. 이를 위해선 `app/scripts/app.js` 파일의 다음 라인을 수정하자.

`angular.module('hlApp', ['ui.bootstrap'])`

그럼 애플리케이션 내에서 Angular 부트스트랩이 사용가능해진다.

---

### 내비게이션 바 만들기

---

내비게이션 바를 만들려면 `app/index.html` 파일을 열고 다음과 같이 <nav> 태그를 코드에 추가한다.

책은 이전버전이라 nav 태그를 만드는데, 실제로 현재는 이미 기본 bootstrap 형태가 완성되어 있고, 간단히 brand와 li 태그 쪽만 고쳐주자.

    <a class="navbar-brand" href="#/">Healthy Living</a>
    </div>

    <div class="collapse navbar-collapse" id="js-navbar-collapse">

    <ul class="nav navbar-nav">
      <li class="active"><a href="/#/articles">Articles</a></li>
      <li><a ng-href="/#/gallery">Gallery</a></li>
      <li><a ng-href="/#/subscribers">Subscribers</a></li>
    </ul>

한가지 더 하자면 `<div class="navbar navbar-default navbar-fixed-top" role="navigation">` 와 같이 선언하여 상단에 고정이 되도록 하자.

즉 자세히 설명하면,

`navbar-fixed-top` 은 상단에 내비게이션 바를 고정시켜 스크롤이 되더라도 움직이지 않게 한다. 하단이라면 top을 bottom으로 바꾼다.

다음으로 `container` 라는 속성을 적용했는데, 이는 앨리먼트의 너비를 940px로 설정하고 페이지 내에서 수평으로 중앙 정렬한다.

다음으로 brand 안에 이름을 적음으로서 마무리한다.

서버를 실행해보자.

`grunt serve`

이 명령은 gruntfile.js에 정의된 서버 태스크를 실행한다.

---

### 캐로설 추가

---

Angular 부트스트랩을 이용해 어떻게 캐로설을 추가하는지 알아보자. 대부분 프로젝트에 캐로설 뷰를 사용해본 경험이 있으리라 생각한다. 아마 많은 jQuery 플러그인 중 하나를 택했을텐데 대부분은 제대로 동작시키려면 많은 시행착오를 거치게 된다.

Angular 부트스트랩은 캐로설을 위한 커스텀 지시자를 가지고 있으며, 이를 사용하면 홈페이지에 캐로설을 추가하는 일은 엄청나게 쉬워진다.

`MainCtrl 컨트롤러` 와 `views/main.html` 파셜을 이용해 홈페이지를 그리기 때문에 캐로설 코드를 해당 파일들에 추가할 것이다.

과거에 HTML로 사용자의 상호작용을 구성하는 방식에서는 데이터와 디자인이 서로 섞이는 큰 단점이 있었다. 대부분의 디자이너는 서로 연결된 정적인 마크업으로 일반 HTML 페이지를 생성한다. 같은 코드를 반복한다는 것 외에 또다른 문제는 실제 앱을 만들면서 사용자와 상호작용하는 부분을 완성하기 위해 상당히 많은 양의 재작업이 필요하다.

그러나 AngularJS 를 이용하면 프레젠테이션 레이어를 실제 데이터와 분리해내는 것이 엄청나게 쉬워진다. 작성하는 데 효율적이고 정적인 데이터 모델을 동적인 데이터로 변경하기만 하면 된다.

마크업에서 데이터를 분리한다는 개념을 다시 한 번 떠올리며 첫 데이터 모델을 `app/scripts/controller/main.js` 파일에 추가하자.
awesomeThings 모델은 삭제하고 다음 코드로 대체하자.

    var baseURL = 'http://lorempixel.com/960/450/';
    $scope.setInterval = 5000;

지금부터는 어떤 종류의 웹사이트나 목업(mockup)을 만들 때 플레이스홀더(placeholder) 이미지나 스탁(stock) 이미지를 사용해야 한다. 특정 카테고리나 원하는 치수의 이미지를 제공해주는 [www.lorempixel.com](http://lorempixel.com/) 이라는 사이트가 존재한다.

이번부터는 이미지를 사용해야 하므로 baseURL 변수를 생성해서 우리가 원하는 이미지의 너비와 높이를 인자로 같이 넘겨주었다.

다음은 setInterval을 5000으로 지정했다. 이 값은 캐로섬의 오토슬라이더 값을 5초로 설정하는 데 사용한다.
이제 다음 코드로 slides 모델을 생성한다.

    $scope.slides = [
      {
        title : "7 Ways to stay Fit",
        image : baseURL + 'sports/',
        text  : "Play a sport for 30 minutes a day!"
      },
      {
        title : "Healthly Food",
        image : baseURL + 'food/',
        text  : "Food that you should be eating!"
      },
      {
        title : "Relaxing Holidays",
        image : baseURL + 'nature/',
        text  : '10 Locations for Nature Lovers!'
      }
    ];

이 모델은 기본적으로 title, image, text를 가지는 자바스크립트 오브젝트다. image 속성은 각 슬라이드의 카테고리명에 baseURL을 접두사로 사용했다. 이제 모델을 위한 작업은 끝났다.

이어서 views/main.html 파일을 열고 다음에 보이는 마크업을 점보트론 (jumbotron) 엘리먼트 상단에 추가하자.

    <carousel interval="setInterval">
      <slide ng-repeat="slide in slides" active="slide.active">
      </slide>
    </carousel>

위 코드가 Angular 부트스트랩으로 작성된 커스텀 지시자(<carousel>) 이다.
interval 속성은 다음과 같이 각 슬라이드 사이의 시간 지연을 설정하는 데 사용된다.

`interval = setInterval`

다음은 ng-repeat를 사용해 슬라이드를 반복한다.

이제 이미지와 제목, 텍스트를 표시할 엘리먼트를 넣어보겠다. `<slides>` 태그 안에 다음을 넣어보자.

    <img class="carousel-image" ng-src="{{slide.image}}"  />
    <div class="carousel-caption">
      <h2>{{slide.title}}</h2>
      <p>{{slide.text}}</p>
    </div>

파일을 저장하고 브라우저가 자동으로 갱신이 되는 것을 보자.

내비게이션 바가 혹시 캐로설을 덮어 씌운다면 다음과 같이 css를 바꿔주자

    body{
      padding-top: 50px;
    }

    .carousel-image{
      width: 100%;
    }

**참고** 개인적으로 만들어볼 때, 캐로설이 만들어지지 않고 이미지가 단순히 repeat만 되었다. 찾아보니 현재의 버젼과 맞지 않았고(3.2.x) 도서의 내용은 3.1.x에 맞추어져 있기 때문에 위 사항을 실제로 구동됨을 보기위해서는 버젼을 낮추어 활용을 하거나, 새로운 carousel 내용에 따라 새로 만들어야 한다. 나의 경우 버젼을 낮추었다.

---

### 히어로 유닛 수정

---

그럼 이제 히어로 유닛을 정리하고 근사한 문구를 넣어보자. `app/views/main.html` 파일을 열어서 히어로 유닛 엘리먼트의 내용을 변경하자.

    <div class="hero-unit">
      <h1>Welcome to Healthy Living</h1>
      <p>This is a Rapid Prototype demo on how you can use AngularJS with Angular UI and Bootstrap to quickly build a clickable prototype that can be shown to clients</p>
    </div>

css로 조금 조절을 하자.

---

### 내용 블록 세 개 추가

---

이제 조금씩 모양이 나온다. 히어로 유닛 아래에 내용 블록 세 개를 추가해보자.

데이터는 모델에, 마크업은 파셜 안에 분리하는 방법을 계속 이용한다.

`app/scripts/comtroller/main.js` 파일을 열고 lorempixel에서 동일하게 이미지를 추가하길 원하므로 content라는 이름을 가지는 모델을 새로 만들자.

코드는 다음과 같다.

    var baseURL = "http://lorempixel.com/200/200/";
    $scope.content = [
      {
        title    : "About us",
        img      : baseURL + '/people',
        summery  : "We are good, we are the best there"
      },
      {
        title    : "Our Services",
        img      : baseURL + '/business',
        summery  : "Food that you should be eating!"
      },
      {
        title    : "Contact Us",
        img      : baseURL + '/transport',
        summery  : '#111, Good Health Blvd, Happy Place, Antartica, Zip-432167'
      }
    ];

이제 `app/views/main.html`에 마크업을 추가하자.

히어로 유닛 마크업 다음에 <div>태그와 같이 세 개 블록을 포함할 row 컨테이너를 생성하자.

    <div class="row-fluid">

    </div>

세 개의 블록을 생성하기 위해서는 세 개의 컨테이너가 필요하고 각각은 4열의 너비를 가진다.

row-fluid 클래스 안에 ng-repeat를 이용해서 반복시킬 하나의 블록을 위한 마크업을 만들어보자.

    <div class="col-md-4" ng-repeat="block in content">
      <img ng-src="{{block.img}}" />
      <h3>{{block.title}}</h3>
      <p>{{block.summery}}</p>
    </div>

동작은 잘되지만 이미지가 보기 안좋다. 좀더 보기좋게 부트스트랩을 쓸 것이다.

`class="img-circle"`

둥근 이미지가 되었다. 혹시 다른 효과라면 `img-rounded`, `img-polaroid` 등으로 바꿀 수 있다.

---

### 새로운 뷰 생성

---

페이지가 완성되었지만 우리는 싱글페이지 애플리케이션을 만들고 있으므로 기술적으로 다른 페이지에 가지지는 않는다. 우리가 갖고 있는 것은 뷰인데, 그 안에는 유일한 URL이나 컨트롤러까지의 경로와 그에 상응하는 파셜에 대한 정보만 존재한다.

요맨을 사용해서 새로운 기사에 대한 뷰나 페이지를 만들기 위해 다음과 같이 부생성자(subgenerator) 명령어를 실행한다.

`yo angular:route articles`

요맨이 다음에서 설명하는 테스트 스위트를 자동으로 실행한다.

* 파일명 article.js 컨트롤러를 `app/scripts/controllers` 밑에 새로 생성한다.
* 새로운 파셜 `article.html`을 `app/views` 아래에 생성한다.
* `test.controllers/articles.js` 파일안에 단위 테스트를 생성한다.
* `app/scripts/app.js` 파일을 수정하고 해당 파일을 기사 뷰를 위해 경로에 추가한다.

많은 수작업을 해결했다.

시스템에서 사용 가능한 생성자와 부생성자를 더 알고 싶다면 다음 명령어를 실행하자.

`yo -help`

---

### 경로 이해하기

---

우리가 하는 프로젝트는 모두 경로가 관리되고 있다. 특히 경로는 어떤 뷰와 컨트롤러를 사용해야 하는지 알려준다.

`app/scripts/app.js` 파일을 보면 `$routeProvider` 가 있다. 해당 부분을 보면 어떻게 연결되는지 감이 올것이다.

여기서 중요한 것은, **뷰와 컨트롤러가 느슨하게 연결되어있다는 점** 이다. 즉, **서로서로 독립적이며 본질적으로 서로 다른 두 개의 뷰를 하나의 컨트롤러에 연결 가능** 하다. 따라서 **코드의 재사용성** 을 향상시킨다.

---

### 기사 목록을 위한 뷰 작성

---

먼저 `app/scripts/controllers/article.js`를 만져보자.

    angular.module('hlApp')
      .controller('ArticlesCtrl', function ($scope) {
        $scope.posts = [
        {
          title  : "Almonds are good for Health",
          content: "Almonds contain high amounts of HDL which helps reduce chalostrol.Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus rhoncus quam leo, id tristique sapien viverra eu. Maecenas ipsum lectus, suscipit auctor tristique in, venenatis ut nisl. Quisque eget bibendum libero. Nam nec mi augue."
        },
        {
          title  : "Sugar is bad for health",
          content: "Sugar besides being bad for diabeties, it also causes overweight and obesity problems.Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus rhoncus quam leo, id tristique sapien viverra eu. Maecenas ipsum lectus, suscipit auctor tristique in. "
        },
        {
          title  : "Cut down your carbs!!!",
          content: "Sugar besides being bad for diabeties, it also causes overweight and obesity problems.Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus rhoncus quam leo, id tristique sapien viverra eu. Maecenas ipsum lectus, suscipit auctor tristique in, venenatis ut nisl. Quisque eget bibendum libero. Nam nec mi augue. "
        }
       ];
    });

아마 이제는 조금 익숙해 졌지 않을까 생각한다.

혹시나 내용을 하나하나 치고있다면 그냥 [로렘입숨](www.lipsum.com)에서 긁어오길 바란다.

---

### Angular 부트스트랩을 사용한 아코디언 뷰

---

이제 파셜을 살펴보자. 아고디언을 만들것인데, `views/articles.html`을 한번 다루어 보자.

    <h1>Articles</h1>
    <accordion>
      <accordion-group heading = "{{post.title}}" ng-repeat="post in posts">
        {{post.content}}
      </accordion-group>
    </accordion>

코드는 따로 설명하지 않겠다.

---

### 이미지 갤러리 구축

---

이제 이미지 갤러리를 구축해볼 것이다 또다시 새로운 경로 파일을 만들어보자.

`yo angular:route gallery`

그럼 하던대로 모델부터 만든다.

    angular.module('hlApp')
      .controller('GalleryCtrl', function ($scope) {
        $scope.pictures=[];

        var baseURL = "http://lorempixel.com/300/180/";

        var titles = ["Healthy Food","Healthy @ Work","City Life ","Staying Fit","Looking Good","Nightlife !!"] ;

        var keywords=["food", "business","city","sports","fashion", "nightlife"];

        var dummyText="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed sed erat turpis. Integer eget consectetur quam. Sed at quam ut dolor varius condimentum et sit amet odio. ";

      });

약간의 설명을 하자면 title은 각각의 이미지 이름이고 keyword 는 baseURL 뒤에 붙여줄 용어다.

이제 pictures에 이미지를 넣는 함수를 정의하자.

    $scope.addPics=function(i){
      $scope.pictures.push({
          url:baseURL+keywords[i],
          title:titles[i],
          summary:dummyText
        })
    }

i를 파라미터로 받는 addPics 함수는 배열을 순회하며 각 속성을 업데이트한다.

i를 증가시키며 반복문안에서 위 함수를 실행시키자.

    for (var i=0;i<5;i++){
        $scope.addPics(i);
    }

지금은 6개정도의 이미지므로 5까지만 돌린다.

---

### 부트스트랩 섬네일을 이용한 갤러리 뷰

---

Angular 부트스트랩은 따로 갤러리 뷰에서 사용할 섬네일을 생성하거나 보여줄 특별한 지시자가 없다.
따라서 뷰에서는 일반 부트스트랩 클래스를 사용할 것이다.

`view/gallery.html` 파일을 다음과 같이 작성하자.

    <h1>Gallery</h1>
    <div class="thumbnails ">
    	<div class="col-md-4" ng-repeat="pic in pictures">
    		<img ng-src="{{pic.url}}">
    		<h3>{{pic.title}}</h3>
    		<p> {{pic.summary}}</p>
    	</div>
    </div>
    </div>

그리고 css를 바꿔보자.

---

### 별점 평가 추가

---

이제 별점 평가기능을 추가해 볼 것이다.
Angular 부트스트랩 덕분에 파셜에 코드한 줄을 추가하는 만큼 별점기능이 쉬워졌다.

`app/views/gallery.html`을 열고 다음과 같이 해보자.

`<rating ng-model="rate" max="max" readonly="isReadonly" ></rating>`

그리고 컨트롤러에 다음을 추가한다.

    $scope.rate = 0;
    $scope.max = 10;
    $scope.isReadonly = false;

그럼 한번 결과물을 보자.

---

### NG-Grid를 이용한 데이터 그리드 작성

---

![cat](http://farm6.static.flickr.com/5043/5270760203_a00656e91d_z.jpg)

테이블과 데이터 그리드는 굉장히 자주 쓰인다. 예전에는 <table> 태그로 이리저리 붙였지만 갈수록 복잡해 질것이다.

따라서 열을 가지고 정리하거나 여러 행을 페이지형식으로 구성하는 것을 포함해 때로는 엑셀형식까지 만들어내야 할 때가 있다.

`NG-Grid` 덕분에 AngularJS에서 데이터 그리드의 다양한 기능이 매우 쉬워졌다.

---

### NG-Grid 컴포넌트 추가

---

NG-Grid는 Angular 부트스트랩이 아니라 따로 추가해야 한다. 보어를 통해 다운로드 받아보자.

<del> `bower install ng-grid` </del>

<del>그럼 ng-grid 폴더와 bower_components 안에 새로 생겼을 것이다.</del>

<del>그럼 ng-grid 관련 자바스크립트 파일과 css를 `app/index.html`에 추가시키자</del>

업그레이드 되면서 ng-grid가 angular-ui-grid가 되었다.

`bower install angular-ui-grid`

    <link rel="stylesheet" type="text/css" href="bower_components/angular-ui-grid/ui-grid.min.css">
    <script src="bower_components/angular-ui-grid/ui-grid.min.js">

다음을 추가한다.

그럼 이제 새로이 의존성을 추가하자.

    angular</del>
      .module('hlApp',
        'ui.bootstrap',
        'ui.grid'
     ])</del>

위 사항도 할 필요가 없어졌다.

그럼 또 새로운 페이지를 만들자.

`yo angular:route subscribers`

그럼, 현실적으로는 구독자 목록을 불러주는 웹 서비스를 호출하는 것이다. 따라서 정적인 JSON 파일을 만들고 더미 데이터를 입력해서 웹 서비스의 응답을 흉내 내보겠다.

앱 폴더 내에 `subscribers.json` 파일을 만들고 다음처럼 만들자.

    [
      {"no":"1","name":"Betty", "loyalty": 3,"joinDate":"3/5/10", "userType":"Free"},
      {"no":"2","name":"John", "loyalty": 5,"joinDate":"3/5/05", "userType":"Premium"},
      {"no":"3","name":"Peter", "loyalty": 6,"joinDate":"3/5/10", "userType":"Free"},
      {"no":"4","name":"Jaden", "loyalty": 7,"joinDate":"10/12/12", "userType":"Premium"},
      {"no":"5","name":"Shannon", "loyalty": 9,"joinDate":"22/01/08", "userType":"Premium"}
    ]

그럼 이걸 어떻게 컨트롤러에서 로드하는지 보자.

    angular.module('hlApp')
      .controller('SubscribersCtrl', function ($scope, $http, $modal) {
        $http.get("http://localhost:9000/subscribers.json").
          success(function(data){
            $scope.subscribers = data;
          })
    });

먼저 $http 서비스를 컨트롤러에 넣어주었고, get으로 해당 파일을 받아왔다. 이 후 success 응답을 받아 data를 모델에 붙이고 있다.

$http 서비스는 프라미스(promise)를 반환하는 두 개의 메소드, success와 error를 가지고 있다.

해당 부분은 후에 더 자세히 다룬다.

이제 모델이 준비되었고 NG-Grid를 다음과 같이 초기화 하자.

    $scope.gridOptions = {
      data: 'subscribers'
    }

이제 컨트롤러는 마무리 되었다.

그럼 그리드를 만들러 가보자.

`app/views/subscribers.html`에 다음과 같이 만든다.

    <h1>Subscribers</h1>
    <div class="gridStyles" ui-grid="gridOptions">

    </div>


css 역시 바꾸어 준다.

    .gridStyles{
      width: 940px;
      height: 300px;
    }

여기서 적어도 **height 만큼은 꼭 지정해서 NG-Grid가 어떤 영역안에 그려져야 하는지 알 수 있는게 좋다.** 높이 속성이 없으면 자동으로 부모 컨테이너의 높이를 사용하는데, 이 때문에 한번 스크롤 할 수 있는 크기에 하나의 데이터 행만 출력되기도 한다.

결과적으로는 알맞게 나왔지만 이렇게 사용하는 건 좋은 모습이 아니다. column Definitions 가 필요한데 다음처럼 바꾸도록 하자.

    columnDefs: [{
        field: 'no',
        displayName: 'No.'
    }, {
        field: 'name',
        displayName: 'Name'
    }, {
        field: 'loyalty',
        displayName: 'Loyalty Score'
    }, {
        field: 'userType',
        displayName: 'Subscription Type'
    }, {
        field: 'joinDate',
        displayName: 'Date of Joining'
    }]

아마 열의 제목이 변했을 것이다.

그럼 색상도 약간 변화를 주자.

    .ui-grid-row:nth-child(odd) .ui-grid-cell{
      background: AliceBlue
    }
    .ui-grid-row:nth-child(even) .ui-grid-cell{
      background:YellowGreen
    }

이제 번갈아 가면서 색이 출력된다.

---

### 그리드의 엑셀화

---

사실 엑셀화는 3.0 버전 이전에 지원이 됬다. 현재는 책에 나오는 형태로 불가능한 상태다.

[https://github.com/angular-ui/ui-grid/wiki/Configuration-Options](https://github.com/angular-ui/ui-grid/wiki/Configuration-Options) 참고하자.

---

### 구독자 추가를 위한 모달 창 구현

---

이제 구독자를 출력하는 건 가능하니 새로 추가기능을 넣어보자.

아마 지금까지 한 것 보단 복잡할 듯 하다.

먼저 버튼을 추가하자.

    <h1>Subscribers</h1>
    <button class="btn btn-success" ng-click="showModal()"> Add New User</button>
    <div class="gridStyles" ng-grid="gridOptions">
    </div>

그다음 add-user.html 파일을 views 에 새로 생성하고 다음과 같이 만든다.

    <div class="modal-header">
    	<button type="button" class="close" ng-click="cancel()" data-dismiss="modal" aria-hidden="true">&times;</button>
    	<h1>Add a Subscriber</h1>
    </div>
    <div class="modal-body">
    <label>Name</label><input type="text" ng-model="newUser.name"/>
    <label>Subscription Type</label><input type="text" ng-model="newUser.userType"/>
    <label>Loyalty Score</label><input type="number" ng-model="newUser.loyalty"/>
    <label>Date of Joining</label><input type="date"ng-model="newUser.joinDate"/>
    <br/>
    <button class="btn btn-success" ng-click="saveNewUser()"> Save User</button>

    </div>

코드가 직관적이므로 따로 설명은 하지 않겠다.

다음은 컨트롤러로 가서 코드를 추가하자.

    $scope.showModal = function() {
        $scope.newUser = {};
        var modalInstance = $modal.open({
            templateUrl: 'views/add-user.html'})}

$model 서비스는 몇가지 옵션을 갖춘 open 메소드를 가지고 있는데 templateUrl은 그중 하나다.

newUser이라는 이름의 빈 모델 객체도 생성한다. 이게 모달창에서 받은 데이터를 저장하는 용도가 될 것이다.

저장하고 한번 확인해보면, 상당히 투박하게 만들어 졌다. 게다가 함수도 적용이 안되 취소나 저장이 되지 않는다.

$model은 부모 스코프 내에 자신의 스코프를 새로 생성한다는 점을 기억하자. $modal.open 함수가 지원하는 다른 것은 **controller** 다.

새롭게 컨트롤러를 할당할 수 있는데 한번 보자.

`controller: 'AddNewUserCtrl',`

다음이 선언되었고 그 밑에 해당 컨트롤러를 적어보자.

    .controller('AddNewUserCtrl', function($scope, $modalInstance, newUser) {
        $scope.newUser = newUser;
        $scope.saveNewUser = function() {
            $modalInstance.close(newUser);
        };

        $scope.cancel = function() {
            $modalInstance.dismiss('cancel');
        };
    });

선언하면서 두가지 함수도 같이 선언하였다.

그리고 마지막 resolve 옵션도 넣어주자

    resolve: {
        newUser: function() {
            return $scope.newUser;
        }
    }

그럼 $modal도 요청받는 객체나 변수를 반환하기위해 프라미스를 이용한다.

여기서 resolve 부분은 newUser 모델 오브젝트를 반환한다.

이제 프라미스로 newUser 모델을 반환하므로 해당 데이터를 subscribers 모델로 푸시하자.

    modalInstance.result.then(function(selectedItem) {
        $scope.subscribers.push({
            no: $scope.subscribers.length + 1,
            name: $scope.newUser.name,
            userType: $scope.newUser.userType,
            loyalty: $scope.newUser.loyalty,
            joinDate: $scope.newUser.joinDate

        });
    });

그 의미는 잘 알수 있을 것이다.

---

### 실시간 입력 양식 검사

---

input 필드에 정의된 type 속성에 의해 AngularJS는 ng-valid와 ng-invalid 클래스를 실시간으로 추가한다. 사용자에게 유용한 피드백을 돌려주기 위해 해당 기능을 사용할 것이다.

앱에서 제공하려는 것은 사용자 입력 데이터가 유효하면 녹색 테두리, 아니면 적색을 띌 것이다.

그럼 main.css 에 다음을 추가하자.

    .modal-body .ng-valid{
        border: thin solid #090;
    }
    .modal-body .ng-invalid{
        border: thin solid #990000;
    }

이제 상호작용하는 프로토타입을 만드는 것은 모두 끝났다.

마지막 정리로 프로토타입의 장점을 적어보겠다.

* 애플리케이션이 어떻게 보이고 동작하는지 이해관계자들이 확실히 알 수 있다.
* 값진 사용성 피드백을 얻을 수 있고, 프로토타입을 다뤄봄으로써 사용성 관련 이슈들을 손쉽게 파악한다.
* 프레젠테이션 레이어 코드는 사용에서 바로 사용하고, 실제 개발 환경에서는 웹 서비스에서 반환하는 동적인 데이터를 정적인 데이터로 바꿔주기만 하면 된다. 따라서 시간이 줄어든다.
* AngularJS로 사용자의 클릭흐름을 구축하는 것은 일반 HTML, CSS, jQuery를 사용하는 것보다 훨씬 적은 시간이 든다. 또한 재활용코드가 많아진다.

---

### 요약

---

이번에는 매우 길게 어떻게 데이터와 프레젠테이션 레이어를 분리하는지 보았다. 적은양의 코드도 보았을 것이다.

뼈대를 구축하고 우리가 원하는 새로운 페이지를 생성하는데 요맨을 사용했다. 앱 전체에 걸쳐 사용할 다양한 구성요소를 위해 Angular 부트스트랩의 커스텀 지시자를 사용했다.

routeProvider도 알아봤으며, 그리드시스템을 사용해보았다. 이제 다음에는 REST 서비스에 대해 다뤄보도록 하자.

앞서 적어둔 모든 소스는 [이곳](https://github.com/koocci/AngularJS-examples) 에서 보실 수 있습니다.
