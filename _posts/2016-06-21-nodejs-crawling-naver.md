---
layout: post
title:  "[node js] Node js로 크롤링하기 -naver API"
date:   2016-06-21 01:45:23 +0900
categories: Nodejs
---

# Node js로 크롤링 하기 - NAVER API

![coding](https://images.unsplash.com/photo-1417733403748-83bbc7c05140?ixlib=rb-0.3.5&q=80&fm=jpg&crop=entropy&s=1df0633aecd7ac2763d7548c671cebf9)

포스팅 하고 싶은게 많지만, crawling을 하나의 포스팅으로만 끝내기도 아쉽고 예제를 다루기로 했으니, 이번엔 NAVER API를 이용한 크롤링을 알아보기로 하자.

---

### NAVER API

naver api 에는 재밌는 것이 참 많다.

[naver api](http://developer.naver.com/wiki/pages/SrchAPI)를 들어가 보면, 검색, 지도, 네이버 로그인, 카페 등등이 있는데, 아마 가장 자주 쓰는게 검색 쪽이 아닐까 한다. 

개인적으로 지도 api도 한번 깊이 파봤는데, 구글을 많이 쓰는 건 이유가 있다... 아니면 차라리 SK나 다음 쪽 API도 괜찬다. 확실히 네비게이션이 있는 곳이 좋은 것 같은 느낌도 든다.

하여튼, 검색 API에는 여러가지 지원해준다. 블로그, 뉴스, 책, 지역, 지식in등이 있는데, 아마 지역을 가장 많이 쓰지 않을까 한다. 
지역 검색은 꾀나 크게 도움이 되기 떄문이다. (한국에서 가장 많이 쓰는 사이트이기도 하고..)

---

### 검색 API - 지역

대부분 비슷한 형태로 나오기 때문에 지역만 해도 다른 곳에 유추해서 활용이 가능 할 것이다.
먼저, naver api를 쓰기 위해 세팅이 필요하다. 앱을 등록하고 키를 발급 받아야 하는데, 해당하는 건 크게 다루지 않겠다. 다만, 네이버 API가 얼마전 업그레이드 하므로써 이전에 쓰던 API 키 같은 경우 사용이 안되니 조심하도록 한다.

![site](https://images.unsplash.com/photo-1452882628481-6a2da9481239?ixlib=rb-0.3.5&q=80&fm=jpg&crop=entropy&s=955801ecdc6020a1dd8403fdee1fd635)

지역 API는 [여기](https://developers.naver.com/docs/search/local)에 나와있다.
API 설명이 참 잘 되어있다. 무엇을 요청하고 무엇을 받는지..
사실 API를 처음 접하는 사람이 아니면, 쉽게 따라할 수 있는 부분이다.

설명을 한번 보자.

`METHOD GET, https://openapi.naver.com/v1/search/local.xml,  OUTPUT : XML`
다음과 같다.

get으로 요청하면 XML형식으로 나온다는 것이다. 아주 직관적이다.
요청변수는 
`query : 요청할 문자열`
`display : 출력 건수`
`start : 검색 시작 위치`
`sort : 정렬 옵션`

위와 같이 구성되어 있는데, 원하는 형태로 요청을 하면 된다.
`start`의 경우 어디서 부터 시작할 지를 정하는 것이므로, 1부터 시작하고 싶으면 1로 설정하고, `display`가 5면 5개가 보이는 것이다. 그리고 겹치지 않게 다음을 설정하려면? 당연히 `start`를 6으로 맞추어 주어야 한다.

그럼 일단 요청을 코딩해보자 

---

### request

{% highlight ruby %}
var request = require('request');
var cheerio = require('cheerio');

var options = {
	headers : {
		"X-Naver-Client-Id" : "Your Client ID",
		"X-Naver-Client-Secret" : "Your Client Secret"
	},
	method : 'get',
	encoding: "utf-8",
	url : 'https://openapi.naver.com/v1/search/local.xml',
	qs : {
	  query : "GS25",
	  display : 1,
	  start : 1,
	  sort : "random"
	}
}

request(options, function(err, res, html) {
	console.log(html);
});
{% endhighlight %}

자, 요청 쿼리는 매우 간단해 보인다.

option을 보면 대부분의 정보가 다 들어간다.
header 부분은 각자 개인이 받은 부분이 들어갈 것이고, 
qs는 query stream으로 보면 될 것이다. 

다음과 같이 하면 console에는? 

xml형식으로 하나의 검색된 GS25시가 나온다.
(검색에는 횟수 제한이 있으므로 조심한다.)

이제 xml을 다뤄야 하는데, 우리는 xml보다 json 형식이 더욱 편하고 쉬울 것이다.

그럼 변환을 해보자

---

### XML to JSON

{% highlight ruby %}
var request = require('request');
var cheerio = require('cheerio');
var xml2js = require('xml2js');
var parser = new xml2js.Parser({
    explicitArray: false
});

var options = {
	headers : {
		"X-Naver-Client-Id" : "Your Client ID",
		"X-Naver-Client-Secret" : "Your Client Secret"
	},
	encoding: "utf-8",
	method : 'get',
	url : 'https://openapi.naver.com/v1/search/local.xml',
	qs : {
	  query : "GS25",
	  display : 1,
	  start : 1,
	  sort : "random"
	}
}

request(options, function(err, res, html) {
	parser.parseString(html, function(err, result) {
		console.log(result);
	});
});
{% endhighlight %}


간단히 모듈을 사용한다.
[xml2js](https://www.npmjs.com/package/xml2js)라는 모듈인데 상당히 좋다.
특히, parser라는 부분으로 xml2js를 쓸 수 있게 만들면서, option을 지정해 줄 수 있는데, 다른 것보다 explicitArray 같은 경우, false로 하면 내용이 있을 경우만 배열로 묶는다.

이외의 옵션은 document로...

이렇게 한다면 result값이 json형태로 바뀌는 것을 볼 수 있다. 아주 재미있다.

이것을 어떻게 사용할까? 그것은 뭐 본인이 원하는 방식으로 하면 된다.

개인적으로는 루프 돌려놓고, 매일 정해진 쿼리수 극한까지 돌리고 다음날 되면 다시 돌아가는 형식으로 해서 긁어본 경험이 있다.

활용은 본인의 몫이다.

---

### 좌표 변환

원래 이대로 포스팅을 끝내려 했으나, 한가지 문제를 더 짚고 가고 싶어졌다.
naver 지역 api의 좌표 문제인데, naver는 우리가 흔히 아는 위경도 좌표를 주지 않는다..

따라서 변환이 필요한데, 변환 API는 여러 개가 있다.

[다음](https://developers.daum.net/services/apis/local)에도 있고, [SK](https://developers.skplanetx.com/apidoc/kor/t-map/geocoding/)에도 있는데 들어가서 확인해보면 API가 다 똑같은 형식이라는 것을 알 수 있다.

처음 할 때는 SK쪽에도 있는 지 모르고 다음을 썼는데, 다음에는 검색 횟수 제한이 3000회로 되어 있으니 조심하도록 한다.

간단히 다음을 보면

{% highlight ruby %}
var option = {
    apikey : "Your api KEY",
    fromCoord : "KTM",
    x : mapx,
    y : mapy,
    toCoord : "WGS84",
    output : "json"
}
{% endhighlight %}

와 같이 옵션을 준다면 KTM 좌표계에서 WGS84 좌표계로 변환이 가능할 것이다. 당연히 여기서 mapx와 mapy는 위 네이버 검색에서 얻은 좌표 x값과 좌표 y값이 되겠지?

---

### 끝

그리 어렵지 않은 크롤링 기술이다.
아마 이 기술보다 본인이 원하는 것에 맞추어 변환 시키는 작업이 더 오래 걸릴 것이다.
화이팅...



