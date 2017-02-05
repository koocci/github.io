---
layout: post
title:  "[node js] Node js로 크롤링하기(reTry)"
date:   2017-02-01 11:46:23 +0900
categories: Nodejs
tags: [node js, node, crawling, 크롤링, 노드]

---

# Node JS

---

![haha](https://gongu.copyright.or.kr/gongu/wrt/cmmn/wrtFileImageView.do?wrtSn=364843&filePath=L2Rpc2sxL25ld2RhdGEvMjAxMi8yNS9DTFM0L0FSVF9BNDA3XzEzMF9udXJpbWVkaWFfMjAxMzAyMDU=&thumbAt=Y&thumbSe=b_tbumb&wrtTy=4)

내가 맨 처음으로 포스팅 했던 것이 아마 크롤링 일 것이다.

당시만 해도 내가 아는 지식을 적고자 하는 의도로 포스팅을 시작했는데 참 많이 변질되었다는 생각이 든다. 그냥 내가 적고 싶은 것은 물론 많으나 책을 보고 내가 정리하는 것도 나쁘다고 생각하지는 않는다. 모로 가도 서울만 가도 되지...

어찌됬든 내가 잘하고자 해서 쓰는 포스팅이므로 좀더 경력이 쌓이고 경험이 쌓일 때까지는 이렇게 써 나가기로 했다.

최근에 책을 하나 샀다. 개인적으로 하고자하는 프로젝트도 있고 해서, 크롤링 관련 책을 하나 샀는데, 놀랍게도 node js로 크롤링을 하는 책이라 나오자마자 구매하였다.

워낙 파이썬이 대세인지라, 나 역시 파이썬을 공부해보려 했지만 그래도 내가 잘하는 부분을 좀더 강화시키고 해보려고 한다.

책은 `자바스크립트와 Node.js를 이용한 웹 크롤링 테크닉` 이라는 도서이고 `쿠지라 히코우즈쿠에` 라는 분이 지었다. (제이펍)

이 책을 참고는 하겠지만 앞서 적던 C++ 이나 Angular 포스팅처럼 하지는 않을 예정이다. 넘어갈 것은 넘어갈 것이고, 개인적으로 모르는 것 그리고 실습차원 정도만 기술해 볼 예정이다.

---

### 스크래핑

---

이전 첫 포스팅에서 두서없이 크롤링이 무엇일까 개념부터 해서 `cheerio`를 사용해 크롤링을 했었다. 이 책은 간단한 환경설정(여기서는 환경을 통일시키기 위해 VM을 사용해 모두 리눅스로 통일시켜서 설명한다) 이 후에 HTML 해석으로 시작한다.

그전에 **스크래핑** 이라는 단어의 의미부터 되새겨 보자.

많이 들어보았지만 정의를 보기는 힘들었을 수 있다. 웹에서는 `웹사이트에서 HTML 데이터를 수집하고, 특정 데이터를 추출, 가공하여 저장하는 것`을 말한다.

적어도 이 의미는 쉽게 다가올 것이라 생각한다.

이전에 `cheerio` 를 설치했었었는데, 이 책은 `cheerio-httpcli`를 사용한다. npm 검색을 해보니 일본어로 나온다. 읽지를 못해서 잘은 모르겠지만, 지은이가 일본분인게 아마 적용했지 않을까 한다.

위와 같은 크롤링 모듈, a태그를 찾아 링크를 구하는 방법, request를 이용한 이미지 다운, url 모듈을 이용해 절대경로로 바꾸는 기술과 같이 쉽지만 자주쓰는 스킬들을 처음에 정리해 둔다.

아무래도 `cheerio-httpcli` 를 쓰면 좀더 편하게 크롤링에 다가갈 수 있긴 할 것 같다. 간단히 위에 제시한 것들의 예시를 적어보고 넘어가도록 하자.

    var client = require('cheerio-httpcli');
    var request = require('request');
    var fs = require('fs');
    var urlType = require('url');

    //저장할 디렉터리가 없으면 생성
    var savedir = _ _dirname + '/img';
    if(!fs.existsSync(savedir)){
      fs.mkdirSync(savedir);
    }

    //URL 지정
    var url = 'https://ko.wikipedia.org/wiki/' + encodeURIComponent('강아지');
    var param = {};

    //html 파일 획득
    client.fetch(url, param, function(err, $, res){
      if(err) {console.log(err); return;}
      //img 링크 추출 후 함수 실행
      $('img').each(function(idx){
        var src = $(this).attr('src');
        //상대 경로 -> 절대 경로
        src = urlType.resolve(url, src);

        //저장 파일 이름 설정
        var fname = urlType.parse(src).pathname;
        fname = savedir + '/' + fname.replace(/[^a-zA-Z0-9\.]+/g, '_');
        //다운로드
        request(src).pipe(fs.createWriteStream(fname));
      });
    });



아마 위 예제면 모든 내용이 다 들어있을 것이다.

위 사항들을 이용하면 웹페이지 자체를 긁어오는 게 가능해 질것이다.

---

### cron

---

사실 내가 하고싶었던 것은 `cron` 이다.

정기적으로 프로그램을 실행하는 것인데, 특히 웹에서 공개되는 데이터는 정기적으로 갱신되는 경우가 많다. 주가, 환율, 일기예보 등은 모두 정기적으로 갱신이 된다.

이럴 때 스케줄러를 사용하게 되는데, MAC OS X나 리눅스에는 **cron** 이라는 데몬 프로세스가 있다.

cron을 사용하면 스크립트를 원하는 시점에 자동으로 실행할 수 있다. 비슷하게 윈도우에는 **작업 스케줄러** 라는것이 있다. 이런 스케줄러를 어떻게 사용하는지 알아보자.

정기적인 실행을 하기 좋은 작업은 크게 다음으로 분류된다.

+ 데이터 수집과 같은 애플리케이션의 정기적인 처리
+ 로그, 백업 등 시스템과 관련된 정기적인 처리
+ 시스템이 제대로 동작하고 있는지 정기적으로 감시하는 처리

이 책과 지금 내가 해볼 것은 첫번째가 주를 이룰 것이다.

크론은 vi 에디터가 기본으로 사용되고, 이외의 에디터를 사용하고 싶다면 nano나 다른 걸 사용해도 될 듯하다.

먼저 환율 정보나 다른 정보를 얻을 수 있는 곳을 선택하고 한번 크롤링 해보자.

    var request = require('request');
    var parseString = require('xml2js').parseString;
    var fs = require('fs');

    Date.prototype.yyyymmddhh = function() {
      var yyyy = this.getFullYear();
      var mm = this.getMonth() < 9 ? "0" + (this.getMonth() + 1) : (this.getMonth() + 1); // getMonth() is zero-based
      var dd  = this.getDate() < 10 ? "0" + this.getDate() : this.getDate();
      var hh = this.getHours() < 10 ? "0" + this.getHours() : this.getHours();
      return "".concat(yyyy).concat(mm).concat(dd).concat(hh);
    };

    var date = new Date();

    var url = 'http://opendata.busan.go.kr/openapi/service/AirQualityInfoService/getAirQualityInfoClassifiedByItem';
    var queryParams = '?' + encodeURIComponent('ServiceKey') + '=서비스키'; /* Service Key*/
    queryParams += '&' + encodeURIComponent('numOfRows') + '=' + encodeURIComponent('10'); /*한 페이지 결과 수*/
    queryParams += '&' + encodeURIComponent('pageNo') + '=' + encodeURIComponent('1'); /*페이지 번호*/
    queryParams += '&' + encodeURIComponent('item') + '=' + encodeURIComponent('so2'); /*검사항목원소기호*/
    queryParams += '&' + encodeURIComponent('date_hour') + '=' + encodeURIComponent(date.getFullYear() + "010100"); /*date_hour 측정시간 0 2014101705 년도월일시간 (지정일짜부터 최근까지 조회)*/

    request({
      url: url + queryParams,
      method: 'GET'
    }, function (error, response, body) {
      if(error){
        console.log(error);
        console.log('Reponse received', body);
        return;
      }
      console.log('Status', response.statusCode);
      console.log('Headers', JSON.stringify(response.headers));
      parseString(body, function(err, parseResult){
        var result = JSON.stringify(parseResult);
        console.log(result);
        var fname = "air_Quality_" + date.yyyymmddhh() + ".txt";
        fs.writeFile(fname, result);
      });
    });

위 예제는 데이터포털에서 부산지역 대기상태를 openAPI로 받은 것이고, Service Key 를 넣는다면 올해 1월 1일부터 최근까지 대기 상태를 json 형태로 받을 수 있다.

해당 파일을 매일 체크해서 만들려고 하는게 목적이므로 이 소스를 매일 아침마다 돌리는 형태로 만들려고 한다.

cron을 사용할 건데, **crontab** 명령어로 cron 설정부터 하자.

`crontab -e`

로 e 옵션을 주면, cron 설정화면이 열린다. 아마 처음 해당 명령어를 입력하면 아무런 스케줄 설정이 없을 것이다.
참고로, 난 mac os x 를 기준으로 설정하므로 윈도우 관련한건 따로 하지 않을 것이다.

`0 7 * * * node /path/to/002_getAirQuality.js`

내 파일 이름은 `002_getAirQuality.js` 이고 매일 7시에 해당 파일을 실행하도록 한다. 물론 path/to 는 본인의 환경에 맞게 설정하면 된다.

여기서 환경변수가 중요한데, cron 실행 시에는 환경 변수가 최소한으로 설정되어 있다.
따라서 명령어를 못찾거나, nodejs 모듈을 찾을 수 없을 수도 있다.
그러므로 crontab 설정파일의 서두에 환경변수를 설정해 주자.

터미널에 `pwd`를 치면 현재 디렉토리를 알수 있고, `echo $PATH`를 입력하면 PATH 환경변수를 볼 수 있다.

따라서, crontab 내 파일은 다음과 같은 형식으로 될 것이다.

    PATH=/usr/local/bin:/usr/bin/:/bin
    NODE_PATH=/usr/lib/node_modules/

    0 7 * * * node /path/to/002_getAirQuality.js

여기서 잘못된 설정이 될 수 있는 점은, crontab에서는 환경 변수를 우변에서 사용할 수 없다. 따라서

`PATH=/usr/local/bin:$PATH`

와 같이 설정할 수 없다.

또한 각 행에서 환경변수를 설정할 수 도 있는데,

`0 7 * * * export PATH=/usr/local/bin:/usr/bin/:/bin && NODE_PATH=/usr/lib/node_modules/ node /path/to/002_getAirQuality.js`

다음과 같이 가능하다.

그리고 작업 디렉토리에 있어서 주의할 점이 있다.

cron이 실행될 때의 작업 디렉토리는 사용자의 홈 디렉토리가 된다. 따라서 로그를 저장하거나 전체 경로를 지정하거나, 작업 디렉토리를 변경해야 한다.

위와 같이 진행했을 때,홈 디렉토리에 저장되므로, 실행 디렉토리와 같은 로그 파일이 저장되길 바란다면, 다음과 같이 셸 스크립트를 cron에 등록하자.

    # !/bin/sh

    # PATH 설정
    PATH=/usr/local/bin:/usr/bin/:/bin
    NODE_PATH=/usr/lib/node_modules/

    # 현재 디렉토리를 스크립트의 경로로 변경
    cd "$(dirname "$0")"
    #node 프로그램 실행
    node 002_getAirQuality.js

그리고 crontab에는 다음과 같이 입력한다.

0 7 * * * /path/to/sh_fileName.sh


sh_fileName 에는 만든 셸스크립트 파일 이름이 되면 된다.
여기서 몇가지 내가 처리한 것들이 있는데, 예제 문장에는 `cd "$(dirname "$0")"` 가 아니라 `cd 'dirname $0'`라고 되어있다.
또한 permission 문제가 있었는데, 해당 shell script 파일의 권한을 조금 수정하면 가능해진다.

그럼 crontab의 설정부분만 한번 정리해보고 이번 포스팅을 마무리 하자.

`0 7 * * * ...`

위에서 다음과 같이 선언을 하여 실행했었다. 그렇다면, 이 의미들을 알아야 하는데, 정리를 해보면

`분 시 일 월 요일 실행명령`

순이 된다.

좀더 자세히 보면,

+ 분 : 0 ~ 59
+ 시 : 0 ~ 23
+ 일 : 1~31
+ 월 : 0~7(0혹은 7이 일요일)

또한 여러 값들을 지정해 줄수도 있는데,

+ 리스트
  - ex> 0,10,30
    * 0, 10, 30이라는 각 값을 지정.
+ 범위
  - ex> 1-5
    * 1,2,3,4,5라는 범위를 지정
+ 간격
  - */10
    * 10, 20, 30이라는 10 간격을 지정
+ 와일드카드
  - *
    * 와일드 카드를 지정

그럼 예제 몇개만 들어보도록 하겠다.

`0 * * * * say 'Hello'`
매 시 0분에 Hello를 말하게 한다.

`30 8 * * * say 'Good Morning'`
매일 아침 8시 30분에 Good Morning이라고 말하게 한다.

`32 18 20 * * say 'Use money with care'`
매월 20일 18시 32분에 Use money with care를 말하게 한다.

`08 07 06 05 * say 'Have a nice day.'`
매년 5월 6일 7시 8분에 Have a nice day라고 한다.

`50 07 * * 1 say "쓰레기 버리는 날이야."`
매주 월요일 아침 7시 50분에 쓰레기 버리는 날이라고 한다.

참고로 월말에만 지정하고 싶은 경우가 있는ㄴ데, crontab의 지정만으로는 불가능 하지만, test명령과 조합하면 된다.

`50 23 28-31 * * /usr/bin/test $( date -d '+1 day' + %d ) -eq 1 && 실행을 원하는 명령어`

라고 하면 된다.

cron 실행 시 표준 출력이나 오류 출력이 있을 때 메일로 통지를 하는데, 만약 이를 원하지 않는 다면 crontab 첫머리에서 MAILTO에 빈값을 넣으면 된다.

`MAILTO=""`

이번 포스팅은 여기까지 하고 다음엔 로그인 처리를 해보도록 하자.
