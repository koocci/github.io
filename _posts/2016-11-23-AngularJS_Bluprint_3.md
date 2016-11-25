---
layout: post
title:  "[AngularJS] AngularJS 블루프린트 3"
date:   2016-11-23 21:12:11 +0900
categories: AngularJS
tags: [Angularjs, 프로그래밍, MEAN stack, 기초, 블루프린트, IONIC]

---

# 개발 환경 점검2

---

![code](http://www.freedigitalphotos.net/images/previews/matrix-tech-means-coding-digital-and-hi-tech-100276987.jpg)

이전 포스팅에선 Node.js 와 grunt에 대해 알아보았다.

이제 이전에 말했듯이 요맨에 대해 알아보도록 하겠다.

---

### 요맨: 워크플로우 도구

---

요맨은 단순한 도구로 알려지기보다 **워크플로우** 로 알려지길 원한다. 실제로 세가지 도구를 모아놓고 있어 워크플로우를 효율적으로 관리하게 해준다. 도구들은 다음과 같다.

* 요(Yo):  수많은 생성기를 제공하는 **스캐폴딩** 도구로서 프로젝트의 **뼈대** 를 신속히 만들 수 있게 해준다. 요는 AngularJS 앱을 위한 생성기를 가지고 있고 이번에 사용할 것이다.
  -  **스캐폴딩** : 데이터베이스의 각 테이블에 대한 웹 페이지를 자동으로 생성하는 Dynamic Data 요소
* 그런트(Grunt): 앱을 **미리보기** 하거나 **테스트, 빌드** 등의 태스크를 실행하는데 사용된다.
* 보어(Bower): **의존성** 을 관리하는 데 최적의 도구다. 요맨은 보어를 사용해 필요한 스크립트를 검색하거나 다운로드한다.

---

### 요맨 설치

---

`sudo npm install -g yo`

`sudo npm install -g generator-angular`

위의 명령어는 요를 설치하는 것이고 밑은 AngularJS를 위한 생성기 설치이다.

<del>그런데 내 설정환경의 문제인지, 제대로 설치가 되지 않는 문제가 있어 다음과 같이 설치 했다.(해당 github을 참조했다.)</del>

<del>`npm install -g grunt-cli bower yo generator-karma generator-angular` </del>

위 사항은 이 후에 설명할 grunt를 해결하면서 필요 없어졌다.

설치가 되면 폴더를 만든다.

`mkdir yoho`

`cd yoho`

`yo angular`

위 처럼 새로운 파일을 만들어서 작업을 해도 되고, 개인적으로는 이미 만들어진 파일이 있어, 새로 만들지는 않았다.

그러면 몇가지 질문이 나오는데, Sass와 컴퍼스를 사용하곘냐는 질문에 <del>대한 말만 제외하고 모두 Y를 택하자.</del> 그 이유는 우린 CSS를 사용할 것이기 때문이다. 물론 규모가 좀 커진다면 Sass와 컴퍼스(Compass)를 사용하는게 좋다.

`여기서 요류가 있는데, 책에서는 grunt가 Y 로 답하게 나오지만, 지금은 gulf가 default인듯 하다 따라서 grunt에 대해서도 N을 선택 해주자.`

최근 동향 상으론 grunt보다 gulf가 더 활발하므로 gulf를 배우는 것도 좋을 듯하다.

그럼 yo 폴더로 가보자.

상당히 많은 프로젝트가 만들어 졌다.

<del>여기서 karma에 대해 조금 애를 먹었다. 설치가 제대로 되지 않는 문제가 있었는데 딱히 해결법들을 보고 해도 잘 고쳐지지가 않아서 dependenceis 에</del>

<del>`"gulp-karma": "~0.0.5",`</del>
<del>`"karma": "~0.13.19"`</del>

<del>이렇게 넣어주었다.</del>

위 사항은 grunt를 해결해주면서 더이상 필요 없어졌다.

여기서 `node_modules` 파일을 보면 비어있다. 이는 요맨이 모든 의존성을 나열한 package.json 파일을 생성했지만 다운로드하진 않은 것이다. 따라서 다음을 실행한다.

`npm install`

그럼 하위폴더가 구현되었다는 것을 알게 될 것이다.

이 후에 다운된 파일들 중심으로 설명이 있는데, 한번 정리해 보겠다.

* app/404.html
  - 404 에러 페이지      
* app/favicon
  - 브라우저 탭 이미지       
* app/index.html
  - 앱 홈페이지. ng-view를 제외하면 대부분 브라우저 확인과 여러 자바스크립트 파일이다. 실질적으로 ng-view 이외에는 AngularJS 코드는 없고 파일 자체도 그와 같이 유지외어야 한다.
* robots.txt
  - 검색엔진의 로봇이나 크롤러를 위한 룰을 정의하는 곳으로, 그들에게 어떤 페이지를 인덱스해야하고 어떤 영역은 인덱스를 할 필요 없는지 알려준다.
* scripts/app.js
  - 경로들을 정의하는 파일로, 주어진 URL에 대해 로드해야 하는 탬플릿 뷰와 컨트롤러를 정의한다.
  - AngularJS에서 컨트롤러와 뷰는 느슨하게 연결되어 있다. 이 말은 **하나의 컨트롤러가 여러 개의 뷰와 통신할 수 있으며** app.js에 있는 **경로들을 변경하는 것으로 컨트롤러를 위한 템플릿을 교체하는 게 가능** 하다는 의미다.
* scripts/controllers/main.js
  - 앱을 위해 **컨트롤러를 작성하는 곳** 이다. 스캐폴딩의 일부분으로 요맨이 미리 기본 컨트롤러 MainCtrl과 AboutCtrl을 모델과 함께 생성했다. 파일을 수정하거나 다른 컨트롤러들을 추가해도 된다.
* style/main.css
  -  **모든 css 코드는 여기에 있어야 한다.** Style 폴더는 bootstrap.css 파일도 포함할 수 있다. 이 파일은 부트스트랩의 모든 클래스를 포함한다. 파일을 수정하거나 추가적인 코드를 넣지 않도록 주의하자.
* views/about.html, views/main.html
  - views 폴더는 **전체 템플릿 뷰나 일부 뷰를 index.html의 ng-views에 지정해 포함** 할 수 있다. scripts/app.js에 지정된 경로가 주어진 URL에 대해 어떤 뷰를 보여줄지 조정한다.
* Bower.json
  - 이 파일은 앱을 위한 다양한 모듈 및 플러그인의 의존성과 개발 의존성을 **추적** 하는 데 사용한다.
  - 개발 의존성이란 devDependencies로 단위 테스트, 스크립트 파일 패키징, 문서화 같은 개발과 관련된 의존성을 말한다.
* Gruntfile.js
  - 이 파일이 무엇을 위한 것인지는 이미 안다. 아마 약 300줄이 넘는 코드들이 이미 들어있다.
  - 여러 개의 사전에 정의된 테스크를 볼 수 있고, 기본 테스크 묶음 외에도 **test와 build 묶음** 을 볼 수 있다. 이를 이용하면 **앱을 검토하는 작업과 최종적으로 배포를 위해 준비하는 작업** 까지 가능하다.
* test/karma.conf.js
  - 이 파일은 **카르마 단위 테스트를 위한 설정 파일** 이다. 파일을 열면 사용중인 테스트 프레임워크, 단위 테스트 단계에 포함시키고 싶은 파일들, 사용할 포트 브라우저등을 확인할 수 있다.
* node_modules
  - 폴더명만 봐도 알 수 있듯이, 다양한 package.json에 정의한 Node.js 모듈들을 포함하고 있다. yo-angular 명령어만으로는 이 폴더에 모듈을 인스톨하지 않는다는 점에 주의하자. 다운로드와 설치는 package.json 파일을 생성한 후에 npm install 명령어를 실행해야 한다.
* package.json
  - 설치되어야 하는 Node.js 모듈을 나열한다. 필요한 모듈을 추가하거나 사용하지 않는 모듈을 제거할 때 주의하면 수정하자.
* test/spec/controller/main.js
  - **컨트롤러를 위한 단위 테스트** 를 작성하는 곳이다. main.js 파일이 이미 간단한 단위 테스트를 포함하고 있을 것이다. 요맨의 기본 설정은 자스민(Jasmine)을 사용한다. 모카(Mochas)나 큐유닛(Qunit)을 사용하도록 설정 변경이 가능하다.

여기까지 정리를 해보았다.

---

### 앱 구동

---

이번 장의 앞부분에서 Node.js와 ExpressJS를 통해 어떻게 서버를 설정하는지 알아보았다. 요맨은 자체 서버를 가지고 있고 구동하는 것은 터미널에서 다음 명령어를 입력한다.

`grunt serve`

실행해보면 Allo Allo 라는 단어가 뜨는 페이지가 나온다.

그러면 main.js 파일(script/controllers 아래)과 main.html(views 폴더 아래)을 생각해보면 페이지가 어떻게 그려지고 있는지 알 수 있다.

scripts/controllers/main.js 파일을 열면 이름이 `MainCtrl` 이고 모델명이 `awesomeThings` 인 컨트롤러를 찾을 수 있다. 모델에 다음과 같이 추가하자.

    'use strict';

    angular.module('3rdDevEnvApp')
      .controller('MainCtrl', function ($scope) {
        $scope.awesomeThings = [
          'HTML5 Boilerplate',
          'AngularJS',
          'Karma',
          'E2E',
          'protractor'
        ];
      });


이 후, 뷰에서 awesomeThings 배열을 출력해 보자. main.html에 다음과 같이 추가해 본다.

    <ul class="row">
      <li ng-repeat="things in awesomeThings">
        {{things}}
      </li>
    </ul>

파일을 저장하고 브라우저로 가보면 페이지는 자동으로 업데이트되므로 굳이 직접 갱신할 필요는 없다.

새로고침을 따로 누를 필요도 없다. 이것은 `LiveReload`라는 실용적인 모듈 덕분에 가능하다. package.json 에 정의된 개발 의존성의 일부분으로 설치되는 것을 볼 수 있고, grunt.js 파일에 생성된 관련 테스크도 찾을 수 있다.

이제 서버와 함께 브라우저, 문서 편집기를 나란히 열어 띄워놓고 코드를 작성하며 파일을 저장하자마자 앱이 갱신됨을 볼 수 있다.

---

### 카르마로 단위 테스트

---

![tumblr](http://66.media.tumblr.com/386884d6d5cc8a096cd2203d2461b583/tumblr_ogkpfkhq5L1slhhf0o1_1280.jpg)

AngularJS 프로젝트에서 **자동화된 단위 테스트를 작성하는 것** 은 매우 권장하는 사안이다.

AngularJS 제작자 팀은 초창기부터 자동화된 테스트에 대해서 적극적으로 지지하고 있다.

[www.angularjs.org](www.angularjs.org) 의 모든 에제들은 자동화된 테스트 케이스들을 가지고 있다.

동일한 철학을 지닌 요맨도 카르마를 이용한 몇몇 테스트들을 가지고 있다. 요맨이 카르마와 관련 의존성을 자동으로 설치할 수도 있지만 그래도 node_modules 파일에 다음이 존재하는 지 보자.

* karma
* karma-chrome-launcher
* karma-jasmine

폴더에서 이런 모듈들이 없다면 npm install 로 설치하자. (나의 경우 karma-chrome-launcher가 없어 따로 `npm install karma-chrome-launcher --save-dev` 명령으로 설치 했다.)그럼 karma.conf 파일을 다음과 같이 변경 하겠다.

    // Karma configuration
    // Generated on 2016-11-23

    module.exports = function(config) {
      'use strict';

      config.set({
        // enable / disable watching file and executing tests whenever any file changes
        autoWatch: true,

        // base path, that will be used to resolve files and exclude
        basePath: '../',

        // testing framework to use (jasmine/mocha/qunit/...)
        // as well as any additional frameworks (requirejs/chai/sinon/...)
        frameworks: [
          'jasmine'
        ],

        // list of files / patterns to load in the browser
        files: [
          // bower:js
          'bower_components/jquery/dist/jquery.js',
          'bower_components/angular/angular.js',
          'bower_components/bootstrap/dist/js/bootstrap.js',
          'bower_components/angular-animate/angular-animate.js',
          'bower_components/angular-cookies/angular-cookies.js',
          'bower_components/angular-resource/angular-resource.js',
          'bower_components/angular-route/angular-route.js',
          'bower_components/angular-sanitize/angular-sanitize.js',
          'bower_components/angular-touch/angular-touch.js',
          'bower_components/angular-mocks/angular-mocks.js',
          // endbower
          'app/scripts/**/*.js',
          'app/scripts/*.js',
          'test/mock/**/*.js',
          'test/spec/**/*.js'
        ],

        // list of files / patterns to exclude
        exclude: [
        ],

        reporters: ['progress'],

        // web server port
        port: 9876,

        // Start these browsers, currently available:
        // - Chrome
        // - ChromeCanary
        // - Firefox
        // - Opera
        // - Safari (only Mac)
        // - PhantomJS
        // - IE (only Windows)
        browsers: [
          'Chrome'
        ],

        // Which plugins to enable
        plugins: [
          'karma-phantomjs-launcher',
          'karma-jasmine',
          'karma-chrome-launcher'
        ],

        // Continuous Integration mode
        // if true, it capture browsers, run tests and exit
        singleRun: false,

        colors: true,

        // level of logging
        // possible values: LOG_DISABLE || LOG_ERROR || LOG_WARN || LOG_INFO || LOG_DEBUG
        logLevel: config.LOG_INFO,

        // Uncomment the following lines if you are using grunt's server to run the tests
        // proxies: {
        //   '/': 'http://localhost:9000/'
        // },
        // URL root prevent conflicts with the site root
        // urlRoot: '_karma_'
      });
    };


많은 변화는 아니고 몇가지만 변경되었다. 아무래도 책의 버젼과 다르다보니 몇가지 고칠게 있었다.
특히, 현재는 PhantomJS로 되어있지만 지금은 chrome 으로 고쳐 주었다.(플러그인에도 추가해 주어야 할 수도 있다.)

이후 단위 테스트를 진행하기 위해 다음을 입력한다.

`grunt test`

그러면 한가지에서 오류가 날 것이다.

MainCtrl에서 오류가 날 것인데, 3이라고 예상헀지만 5였다라고 나올 것이다. 그리고 주소는 아마 `test/spec/controller/main.js`
일것이다.

그럼 어떤 문제인지 찾아가 보자.

    it('should attach a list of awesomeThings to the scope', function () {
      expect(MainCtrl.awesomeThings.length).toBe(3);
    });

이 부분인데 3이라고 적혀 있는 것이 보인다.

방금 전 제작시 우리는 컨트롤러를 수정해 5가지를 넣어주었고, 여기서 오류가 나는 것이다. 즉 다음과 같이 변경하자.

    it('should attach a list of awesomeThings to the scope', function () {
      expect(scope.awesomeThings.length).toBeGreaterThan(3);
    });

그리고 다시한번

`grunt test`

이제 정상적으로 에러없이 실행된다. 다가오는 장에서 카르마를 이용해 더 많은 내용을 해볼 것이다.

---

### 프로트랙터를 사용해 종단 간 테스트 하기

---

앞에서 봤듯이 컨트롤러에 있는 코드들이 잘 동작하는지 확인할 수 있는 단위테스트를 작성할 수 있게 되었다. 그러나 **자동화된 UAT(User Acceptance Test)를 수행하거나 사용자와 브라우저 사이의 행위에 대해 모방** 하고 싶다면 **만족스럽지 않다**.

그런 테스트를 위해서는 **프로트랙터** 라고 부르는 새로운 도구를 사용할 것이다.

**프로트랙터** 는 AngularJS에서 **종단 간 테스트를 위한 기본 테스트 프레임워크** 로 초창기에 사용되던 AngularJS 시나리오를 대체한다.

프로트랙터는 **WebDrive.js** 파일 위에서 동작하는데 결과적으로는 **셀레니움 서버를 활용** 한다. **셀레니움** 은 가장 유명한 **브라우저 자동화 도구** 중 하나이다. 이번에는 스탠드얼론 셀레니옴 서버(말 참 어렵다..)를 구동하고, 프로트랙터를 설치하는 방법과 기본 종단 테스트 모음을 실행해 보겠다.

먼저 프로트랙터를 설치하자.

`sudo npm install -g protractor`

---

### 셀레니움 서버 설치

---

셀레니움은 편리한 `webdriver-manager` 스크립트를 제공하는데 이것을 사용하면 셀레니움을 설치하고 실행할 수 있다.

터미널에서 셀레니움 서버를 다운로드해보자.

`webdriver-manager update`

서버의 시작은 다음과 같다

`webdriver-manager start`

그러면 서버의 실행이 보일 것이다. 브라우저에서 `http://127.0.0.1:4444/wd/hub`로 들어가면 셀레니움 서버의 현재 상태를 보여준다.

node_modules 아래에 있는 protractor 폴더는 테스트 코드를 작성하지 않고도 바로 시작해볼 수 있는 몇 가지 기본테스트들을 포함하고 있다. 해당 테스트 케이스는 `/usr/local/lib/node_modules/protractor/example` 에 있다. (MACBOOK 기준)

취향에 따라 jasmine 이나 mocha 를 선택해서 테스트 케이스를 작성할 수 있다. 위 예제 폴더로 부터 conf.js 파일과 example_spec.js 파일을 복사해 새로 생성한 test/protractor-test 파일에 넣어보자.

---

### example_spec.js 파일 분석

---

example_spec.js 파일은 **테스트 케이스를 작성하는 스펙 파일** 이다. 문서 편집기에서 파일을 열고 어떻게 동작하는 지 이해해보자.

우선 테스트 스위트 (test swite :  Test Case의 집합)를 다음과 같이 정의 하자.

`describe('angularjs homepage', function() {`

이어서 테스트 케이스를 살펴보자. 첫 번째는 다음과 같다.

    it('should greet the named user', function() {
      browser.get('http://www.angularjs.org');

      element(by.model('yourName')).sendKeys('Julie');

      var greeting = element(by.binding('yourName'));

      expect(greeting.getText()).toEqual('Hello Julie!');
    });

1.  첫 번째 줄은 테스트 케이스를 설명한다.
2. 다음 줄은 지정한 URL 로 이동한다. 위의 경우 angular 홈페이지다.
3. 홈페이지가 로드되면 yourName 모델에 바인딩된 입력을 찾은 후에 문자 'Julie'를 타이핑 한다.
4. 마지막으로, 표현식 Hello {{yourName}} 을 찾아 그 값을 읽고 Hello Julie인지 확인한다.

두번째 케이스를 보자. 두번째 케이스는 다음과 같이 두 개의 테이스 케이스로 이루어져 있다.

    describe('todo list', function() {
      var todoList;

테스트 스위트의 이름을 todoList로 정의하고 초기화했다. 두 테스트 케이스 모두 같은 URL로 이동해야 하고 모두 todoList를 이용한다. 따라서 다음 에제처럼 beforeEach 구문을 사용해 URL을 초기화하고 todoList 배열에 내용을 채워 넣는다.

      beforeEach(function() {
        browser.get('http://www.angularjs.org');

        todoList = element.all(by.repeater('todo in todoList.todos'));
      });

첫 번째 테스트 케이스는 todoList의 크기가 2인지, 두 번째 오브젝트가 `build an angular app`인지 검사한다.

      it('should list todos', function() {
        expect(todoList.count()).toEqual(2);
        expect(todoList.get(1).getText()).toEqual('build an angular app');
      });

다음 예제처럼 두 번째 테스트 케이스는 todoText 모델을 찾아서 항목을 추가한 후 제대로 추가되었는지 확인한다.

      it('should add a todo', function() {
        var addTodo = element(by.model('todoList.todoText'));
        var addButton = element(by.css('[value="add"]'));

        addTodo.sendKeys('write a protractor test');
        addButton.click();

        expect(todoList.count()).toEqual(3);
        expect(todoList.get(2).getText()).toEqual('write a protractor test');
      });
    });

---

### conf.js 파일 분석

---

conf.js는 설정 파일이다. 문서 편집기에서 열어보면 기본 셀레니움 서버 주소, 공통 URL, 테스트에 사용하는 브라우저, 테스트 케이스 위치 등의 설정들이 보인다.

conf.js와 example_spec.js 파일은 같은 위치에 있으니 읽어들일 스펙 위치를 다음과 같이 지정하자.

`specs: ['example_spec.js'], `

테스트 스위트를 실행하기 위해 터미널 프로그램을 열고 conf.js 파일이 있는 곳에 이동한 후에 다음 명령어를 입력한다.

`protractor conf.js`

그럼 새로운 브라우저 창을 하나 띄우고 스크립트에 있는 순서대로 실행되는 것을 볼 수 있다. 테스트가 완료되면 브라우저는 자동으로 닫히고 터미널은 다음과 같은 메시지를 보여준다.

    3 specs, 0 failures
    Finished in 11.385 seconds
    [22:45:42] I/launcher - 0 instance(s) of WebDriver still running
    [22:45:42] I/launcher - chrome #01 passed

혹시나 `Error:ECONNREFUSED connect ECONNREFUSED 라는 에러가 나오는 데 그럴땐 셀레니움 서버를 껐다 키면 된다.`

---

### 프로트랙터 테스트 케이스 작성

---

이제 어떻게 프로트랙터 테스트 케이스를 작성하고 실행하는 지 알게 되었다.

요맨이 만들어준 기본 스캐폴딩 애플리케이션을 위해 스스로 테스트 케이스를 몇개 만들어보자.

`mytests.js` 를 만들고 protractor-test 파일 밑에 저장하자. 다음으로 테스트 케이스를 예제와 같이 작성해 보자.

`describe('our homepage', function(){`

  첫 번째로 작성할 테스트 케이스는 페이지의 h1 태그로 작성된 제목이 'Allo Allo!' 인지 확인한다.

      it('should say Allo', function(){
        browser.get('http://localhost:9000/#/ ');
        var heading = element(by.tagName('h1'))
        expect(heading.getText()).toEqual("'Allo, 'Allo!")
      });

프로트랙터가 이동할 페이지는 `browser.get()` 함수를 통해 정의한다. h1 태그를 찾아 그 안의 문자를 가져와서 'Allo Allo!' 인지 검증하기 위해 `by.tagName` 선택자를 사용한다.

두 번째 테스트 케이스를 작성하자. 이 테스트 케이스에서는 페이지의 너비가 권장 크기 안에 있는지, 일반 사용자들의 화면 크기를 벗어나는 것은 아닌지 확인한다.

    it.(`should not be greater than 940px`, function(){
      browser.get('http://localhost:9000/#/ ')
      element(by.className('container')).getSize().then(function(size){
        expect(size.width).toBeLessThan(950)
      })
    })

div 컨테이너를 찾기 위해 `by.className` 선택자를 사용하고, 너비가 950px 이상인지 검사하기 위해 getSize 속성을 이용한다.

계약의 일부로 .then() 함수를 사용하는데 결과를 반환하기 전까지 코드를 기다리게 한다. 후에 `AngularJS 앱에 REST 적용하기` 에서 이 부분은 더 자세히 알아볼 것이다.

이제 파일을 저장하고 conf.js 파일로 가서 specs에 해당 파일을 넣어두자.

`specs: ['mytests.js'], `

그럼 일단 서버를 구동하고

`grunt serve`

protractor를 구동해보자.

`protractor conf.js`

혹시 셀레니움 서버가 잘 떠있는지 다시 확인을 하고, 그렇지 않으면 켜주도록 하자.

`webdriver-manager start`

결과가 잘 나오는지 확인한다.

혹시나 브라우저를 매번 띄우고 싶지 않거나 서버에서 보이지 않게 실행하고 싶다면 웹킷(webkit) 엔진에서 제공되는 GUI 없이 동작하는 phantomjs 를 추천한다.

---

### 요약

---

이렇게 개발 도구를 준비하는 단계가 끝이 났다. Node.js, 그런트, 요맨, 카르마, 프로트랙터 같은 상당수 도구들을 살펴봤다. AngularJS 로 프로젝트를 진행할 때 이러한 도구들을 추천하지만, 자신이 만들 프로젝트에 더 적합한 도구들이 있다면 적극적으로 사용하자.

Node.js나 ExpressJS, 그런트 같은 도구들은 대부분 AngularJS를 사용하지 않는 프로젝트에서도 사용 가능하다. 그래서 이런 도구에 익숙해지면 프론트엔드 개발자로서 이득이 될 것이다.

앞서 적어둔 모든 소스는 [이곳](https://github.com/koocci/AngularJS-examples) 에서 보실 수 있습니다.
