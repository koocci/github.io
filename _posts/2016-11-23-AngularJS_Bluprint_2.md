---
layout: post
title:  "[AngularJS] AngularJS 블루프린트 2"
date:   2016-11-21 16:34:11 +0900
categories: AngularJS
tags: [Angularjs, 프로그래밍, MEAN stack, 기초, 블루프린트, IONIC]

---

# 개발 환경 점검

---

![music](https://cdn.pixabay.com/photo/2015/07/31/15/01/guitar-869217_1280.jpg)

지난번에 말했듯이, 이번에는 개발 환경에 대한 얘기를 조금 나누도록 하겠다. 사실 이렇게 개발환경을 많고 자세히 나오는 책이 잘 없어 많은 공부가 되었다.

AngularJS의 사용에 있어서 간단한 문서 편집기와 브라우저만으로도 완전히 동작하는 앱을 개발할 수 있다.

그러나 역시나 편리하고 생산성있게 잘 개발하려면 개발 툴들이 필요하다. 그럼 몇가지 알아볼껀데 다음과 같다.

1. Node.js
2. Grunt(그런트)
3. Yeoman(요맨)
4. Karma(카르마)
5. Protractor(프로트랙터)

나는 현재 맥을 기본적으로 사용하지만 이 책에는 대부분의 운영체제에 대한 내용이 나오므로 참고바란다.

---

### Node.js 설정

---

개인적으로는 딱히 필요없지만 간단히 적어 두도록 하겠다.

그러나 분명 루비 혹은 Node.js의 경우, 둘중 하나 정도는 꼭 깔아두길 바란다.

AngularJS의 경우 대부분의 생산성 향상을 위한 도구들과 플러그인들이 노드 패키지 관리자(Node Package Manager : NPM)형태이기 때문에 NPM과 Node.js를 동시에 설치하자.
간단히 [www.node.org](www.node.org) 에서 다운받을 수 있고, 버전을 잘 보고 관리할 수 있도록 하자.

참고로 node.js는 그래픽 사용자 인터페이스(GUI)를 제공하지 않는다. 즉, 눈으로 보고 클릭하는 것으로 사용할 수가 없다. 따라서 터미널을 이용하게 되는데, 잘 갈고 닦아 두도록 하자.

이후, 터미널에서
`node --version`
을 입력한다. 그러면 현재 버전이 나오고 그 다음 `npm --version` 을 입력하자. 그러면 설치된 NPM 버전이 나온다.

---

### ExpressJS와 Node.js 웹 서버 생성

---

사실 이전부터 이부분을 한번 적을까 했는데, 여기서 적게 될줄은 몰랐다. 기본적으로 간단한 AngularJS 앱은 웹 서버를 필요로 하지 않지만, JSON 형태로 데이터를 주고받는 것은 일반적인 상황이다.

AngularJS의 장점은 어떤 웹서버에서도 잘 동작한다는 것이다.

난 운영중인 서버가 있지만 간단히 다시 볼겸, Express 를 한번 설치해 보겠다.

`npm install -g express-generator`

안된다면 앞에 sudo를 붙여주자.(전역이 싫다면 -g를 지워준다.)

이 후, `express my-server` 라고 원하는 파일 내에서 입력하면 간단히 만들어진다.

그럼 다음과 같이 명령어를 입력한다.

`cd my-server`

`npm install`

`npm start`

이 후에 (http://localhost:3000/)[http://localhost:3000/]에 들어가서 Express라는 단어가 보인다면 간단한 로컬서버가 열리게 된 것이다.

이제 1장에서 완성한 주소록 앱을 테스트 하기위해 index.html, addressBook.js, addressBook.css 파일들을 **public** 폴더안에 넣어두자. 그러나 AngularJS 라이브러리 파일은 CDN으로 할 것이므로 남겨두자.

`<script src="//ajax.googleapis.com/ajax/libs/angularjs/1.2.17/angular.min.js"></script>`

`<script> window.angular || document.write('<script src="lib/angular/angular.min.js"></script>');</script>`

윗 줄은 원래 있던 angular.min.js의 코드를 지우고 넣으면 CDN이 연결되는 것이고, 만약 이것이 접근이 불가능할 경우, 파일과 연결할 수 있도록 2번째 줄로 대비책을 적어 둔다.

그러면 (http://localhost:3000/index.html)[http://localhost:3000/index.html] 를 한번 브라우저에 입력해 보자.

매우 잘 동작하는 걸 확인하자.

---

### 그런트 설정

---

![music](https://cdn.pixabay.com/photo/2016/10/19/19/09/branch-1753745_1280.jpg)

그런트(Grunt)는 **자바스크립트 기반의 빌드 도구** 다. **단위 테스트나 결합 및 병합을 수행하고 JS와 CSS를 압축하는 등의 자동화 태스크를 수행하는 것** 이 주 목적이다. 셀 명령어도 실행이 가능하다. 그런트를 이용하면 서버 정리와 코드 배포가 매우 쉬워진다. 루비와 레이크(Rake) 또는 자바의 아파치 앤트/메이븐 같은 관계가 자바스크립트-그런트의 관계라 볼 수 있다.

---

### 그런트 명령어 입력기 설치

---

그런트 명령어 입력기의 설치는 다른 Node.js 모듈 설치와는 조금 다르다. 먼저 그런트의 명령어 입력기(CLI, Command Line Interface)를 다음과 같이 입력한다.

`npm install -g grunt-cli`

안된다면 sudo를 해보도록 한다.

이 때 관리자의 권한으로 실행해야 한다. 여기서 그런트 명령어 입력기를 설치한다해도 그런트와 관련된 라이브러리는 설치 되지 않으니 주의하자. 단순히 그런트 파일과 같이 설치된 버전의 그런트를 호출 할 뿐이다. 처음에는 조금 혼란스럽지만 이렇게 함으로써 같은 장치에서 다른 종류의 그런트를 수행할 수 있게 된다.특히, 나의 프로젝트가 **그런트에 대한 의존성** 을 가지면 특히나 편리해 진다.

---

### package.json 파일 생성

---

그런트를 설치하기 위해 먼저 my-project 폴더와 package.json 파일을 생성한 후 다음과 같이 입력한다.

    {
      "name": "my-project",
      "version": "1.0.0",
       "devDependencies": {
        "grunt": "~0.4.5",
        "grunt-contrib-jshint": "~0.10.0",
        "grunt-contrib-concat": "~0.4.0",
        "grunt-contrib-uglify": "~0.5.0",
        "grunt-shell": "~0.7.0"
      }
    }

참고로 책에는 devDependencies 라는 단어가 없지만, 해당 단어를 추가 해주어야 제대로 구동이 된다.

`grunt (v0.4.5): 그런트 메인 애플리케이션`

`grunt-contrib-jshint (v0.10.0): 코드 분석에 사용`

`grunt-contrib-concat (v0.4.0): 두 개 이상의 파일을 하나로 합침`

`grunt-contrib-uglify (v0.5.0): JS 파일 압축`

`grunt-shell (v0.7.0): 셸 명령어를 사용하는 그런트 셸`

사용가능한 그런트 플러그인의 리스트와 정확한 이름, 버전은 (http://gruntjs.com/plugins)[http://gruntjs.com/plugins]에서 확인이 가능하다.

참고로, `npm init` 명령어를 쓰면 package.json 파일이 자동으로 만들어진다.

이 후, 내부를 수정해도 된다.

그럼 이제 터미널에서 my-project로 이동 후, 그런트를 설치해 보자.

`npm install --save-day`

를 실행하면 연속해서 콘솔에 출력되는 라인을 볼 수 있다.

수행이 왼료되면 `grunt --version` 으로 확인하자.

혹시나 에러가 발생 한다면,

`rm -rf node_modules`

`npm cache clean`

`npm install`

명령어로 재설치 해보자.

---

### 그런트 생성

---

그런트 태스크를 실행하려면 자바스크립트 파일이 필요하다. 이전에 작성한 자바스크립트 파일을 복사해서 my-project 폴더에 넣자.

그리고 그런트가 수행해야 하는 태스크를 나열해놓은 그런트 파일을 생성한다.

여기서는 파일 안에 네 가지의 단순한 태스크를 정의할 것이다. 우선, `JSHint`를 이용해 작성한 자바스크립트가 잠재적인 문제나 에러가 있는지 검사한다.

그리고 병합, 압축하고 마지막으로 셸 명령어를 이용해 정리해 보자.

먼저, package.json 파일이 있는 곳에 gruntfile.js 파일을 만든다.

그리고 다음과 같이 입력한다.

    module.exports = function(grunt){
      //프로젝트 구성
      grunt.initConfig({
        jshint:{
          all: ['addressBook.js'],
          options: {
            reporterOutput: ""
          }
        }
      });
      grunt.loadNpmTasks('grunt-contrib-jshint');
      //기본 태스크
      grunt.registerTask('default', ['jshint']);
    };

책에는 options 부분이 없으나 나는 해당부분을 추가해주어야 출력이 올바르게 되었다.

처음으로 **JSHint 태스크를 하나 추가하고 검증할 자바스크립트 파일을 명시** 한다.

다음 줄에는 **grunt-contrib-jshint를 노드 패키지 관리자 태스크로 지정해 로드** 되게 한다.

마지막으로 **JSHint 그런트가 디폴트 모드로 동작할 때 같이 수행되는 태스크로 정의** 한다.

파일을 저장하고 터미널에 다음과 같이 입력하자.

`grunt`

그럼 다음과 같이 출력된다.

    Running "jshint:all" (jshint) task

       addressBook.js
          7 |  ]
                ^ Missing semicolon.
         12 |  }
                ^ Missing semicolon.
         16 |  }
                ^ Missing semicolon.

    >> 3 errors in 1 file
    Warning: Task "jshint:all" failed. Use --force to continue.

오류가 약간은 다를 수 있다.

그러나 아마 비슷할 것이라 생각한다.

JSHint가 각 라인에 세미콜론이 빠졌음을 말해준다. 이는 나중에 있어서 문제가 생길 수 있기 때문에 추가하고 다시 한번 실행해보자.

    Running "jshint:all" (jshint) task
    >> 1 file lint free.

    Done, without errors.

이제는 메세지가 녹색으로 완료되는 것을 볼 수 있다.

이제 그런트 태스크를 몇 가지 더 추가하자.

이번에는 자바스크립트 파일들을 합쳐볼 예정이다.

먼저 두가지 더미 파일을 더 만들어보자.

각각의 이름은 간단히 script1, script2 라고 하겠다.

    //합쳐질 스크립트 1
    function Script1Function(){
      //----------//
    }

    //합쳐질 스크립트 2
    function Script2Function(){
      //----------//
    }
각각의 파일에 위 두 함수를 각자 넣어주면 된다.

물론, 이 파일들은 addressBook.js 파일과 **동일한** 위치에 넣어둔다.

---

### 여러 파일들의 병합과 연결

---

그럼 위 그런트 파일에 다음 처럼 추가해 보자.

    module.exports = function(grunt){
      //프로젝트 환경 설정
      grunt.initConfig({
        jshint:{
          all: ['addressBook.js'],
          options: {
            reporterOutput: ""
          }
        },
        concat: {
          dist: {
            src: ['addressBook.js', 'script1.js', 'script2.js'],
            dest: 'merged.js'
          }
        },
        uglify: {
          dist: {
            src: 'merged.js',
            dest: 'build/merged.min.js'
          }
        }
      });
      grunt.loadNpmTasks('grunt-contrib-jshint');
      grunt.loadNpmTasks('grunt-contrib-concat');
      grunt.loadNpmTasks('grunt-contrib-uglify');
      //기본 태스크
      grunt.registerTask('default', ['jshint','concat','uglify']);
    };

한 번 분석해보자.

먼저 JSHint 태스크 다음에 `concat` 태스크를 추가했다. src 속성에 합치고 싶은 파일을 구분하고, dest 속성에 최종적으로 병합된 파일의 이름을 명시했다.

**단, 여기서 병합되는 순서대로 입력하는 것이 중요하다. 순서가 틀리면 병합된 자바스크립트 파일은 앱에서 에러가 일어난다.**

uglify 태스크는 자바스크립트 파일을 압축할때 사용하고 구조도 concat과 유사하다.

참고로 build 파일을 자동으로 만들어진다.

이 후 하단에 필요한 것들을 기본 태스크로 추가하고 실행하면 아마 완료된 파일들을 볼 수 있을 것이다.

---

### 그런트로 셸 명령어 실행

---

grunt-shell 은 또 다른 유용한 플러그 인이다. 이 플러그인은 **임시 파일들을 삭제하거나 파일의 이동과 같이 정리하는 작업들을 효율적으로 처리** 한다.

어떻게 그런트 파일에 셸 태스크를 추가하는지 알아보자.

    module.exports = function(grunt){
      //프로젝트 환경 설정
      grunt.initConfig({
        jshint:{
          all: ['addressBook.js'],
          options: {
            reporterOutput: ""
          }
        },
        concat: {
          dist: {
            src: ['addressBook.js', 'script1.js', 'script2.js'],
            dest: 'merged.js'
          }
        },
        uglify: {
          dist: {
            src: 'merged.js',
            dest: 'build/merged.min.js'
          }
        },
        shell: {
          multiple: {
            command: [
              'rm -rf merged.js',
              'mkdir deploy',
              'mv build/merged.min.js deploy/merged.min.js'
            ].join('&&')
          }
        }
      });
      grunt.loadNpmTasks('grunt-contrib-jshint');
      grunt.loadNpmTasks('grunt-contrib-concat');
      grunt.loadNpmTasks('grunt-contrib-uglify');
      grunt.loadNpmTasks('grunt-shell');
      //기본 태스크
      grunt.registerTask('default', ['jshint','concat','uglify','shell']);
    };

추가된 코드를 확인해 보자.

먼저, **merged.js 를 삭제** 하고 **deploy 파일을 생성** 한 이후에, **merged.min.js 파일을 이동** 시키고 있다.

만약 윈도우 사용자라면 DOS 명령어로 바꿔야 한다.

그런트가 여러 셸 명령어를 실행하도록 하려면, `.join(&&)` 을 사용하는 점을 주목하자. 다음은 npm 태스크를 로드하고 셸을 기본 태스크로 등록하는 것이다. 이제 실행을 해보자.

태스크가 모두 종료되면 어떻게 진행됬는지 파일을 열어 확인해보면 된다. 이런 플러그인 외에도 다양한 지원을 하니 알아보면 좋다. 주의해야 할 점은 기본 그런트 명령은 개발자가 지정한 특별한 태스크가 없다면 `grunt.register`에 있는 모든 태스크를 수행한다. 따라서 특정 태스크만 수행하려면 다음을 실행한다.

`grunt jshint`

그렇지 않으면 `grunt concat` 이나 `grunt uglify`도 가능하다.

만약 두가지 태스크만 실행하고 싶다면 그런트 파일안에 기본 묶음이 아니라 분리된 새로운 태스크 묶음을 선언할 수 있다.

`grunt.registerTask('concat-min', ['concat','uglify']);`

위 명령어를 추가하면 concat-min 이라는 태스크를 추가하고 두가지만 실행한다.

만약 나의 그런트 파일에서 지원하는 플러그인을 모두 보고 싶다면, `grunt --help` 를 입력하면 된다.

다음 포스팅은 요맨 부터 시작하겠다.

앞서 적어둔 모든 소스는 [이곳](https://github.com/koocci/AngularJS-examples) 에서 보실 수 있습니다.
