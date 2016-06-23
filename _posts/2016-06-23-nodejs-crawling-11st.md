---
layout: post
title:  "[node js] Node js로 크롤링하기 -11번가 API"
date:   2016-06-23 16:18:23 +0900
categories: Nodejs
tags: [node js, node, crawling, 크롤링, 노드, 11번가]

---

# Node js로 크롤링 하기 - 11st

![computer](https://images.unsplash.com/photo-1438354886727-070458b3b5cf?ixlib=rb-0.3.5&q=80&fm=jpg&crop=entropy&s=9ed9e5f9ea45c8d1d99d71e06c1d99df)

naver에 이어 11번가에 대해 크롤링을 해볼 것이다.
11번가는 몇가지 기술이 더 들어가므로 재미있을 것이다.
사실 법적인? 문제가 생길지도 모르기에 API자체만 긁는 기술을 적고 더 세세한 내용은 따로 적어두지 않으려고 한다.

---

### 11st API

11번가 api는 메인 이미지도 주고, 상품 번호 등 다양한 정보를 준다.

해당 API 는 [11st api](http://openapi.11st.co.kr/openapi/OpenApiSearch.tmall) 에 들어가면 볼 수 있고, 이전에 naver API와 같이 형식도 나와있으므로 쉽게 접근이 가능하다.
naver API를 할 때, API 문서를 보는 것부터 차근히 했으므로 바로 진행해 보겠다.

---

### API 요청

이전과 형태는 비슷하다.

{% highlight ruby %}
var request = require('request');

var options  = { encoding: "utf-8", method: "GET", uri: "http://openapi.11st.co.kr/openapi/OpenApiService.tmall?key=YOURKEY&apiCode=CategoryInfo&categoryCode=127648&option=Products&pageSize=200&pageNum=1"};

request(options, function(err, res, html) {
	console.log(html);
});
{% endhighlight %}

요청 쿼리를 option에 넣어서 해주어도 되지만, URL에 넣어주어도 상관 없으므로, 위와 같이 넣어주었다.
YOUR KEY 값은 11번가 OPEN API를 사용할 때, 가입하는 조건으로 제공이 되며, 내가 선택한 CATEGORY CODE는 건강식품이고, 물품 정보를 받을 것이며, 200개의 리스팅, 그중 1페이지를 가져오는 쿼리이다.

그럼 console창을 한번 보길 바란다.
{% highlight ruby %}

<?xml version="1.0" encoding="EUC-KR"?><CategoryResponse><Request><Arguments><Argument name="key" value="8eab672e39f8648
a2a2c92b2b5627085"></Argument><Argument name="apiCode" value="CategoryInfo"></Argument><Argument name="categoryCode" val
ue="127648"></Argument><Argument name="option" value="Products"></Argument></Arguments><ProcessingTime>0.04 sec</Process
ingTime></Request><Category><CategoryCode>127648</CategoryCode><CategoryName><![CDATA[�ǰ���ǰ]]></CategoryName></Category
><Products><TotalCount>216457</TotalCount><Product><ProductCode>1194666535</ProductCode><ProductName><![CDATA[������ ���
�-����ŰĿ 30��+����ŰĿ ��ư7�� ����/ ���������� �� �ٿ���������]]></ProductName><ProductPrice>22900</ProductPrice><Product
Image><![CDATA[http://i.011st.com/t/080/am/6/6/6/5/3/5/1194666535_L300_V24.jpg]]></ProductImage><ProductImage100><![CDAT
A[http://i.011st.com/t/100/am/6/6/6/5/3/5/1194666535_L300_V24.jpg]]></ProductImage100><ProductImage110><![CDATA[http://i
.011st.com/t/110/am/6/6/6/5/3/5/1194666535_L300_V24.jpg]]></ProductImage110><ProductImage120><![CDATA[http://i.011st.com
/t/120/am/6/6/6/5/3/5/1194666535_L300_V24.jpg]]></ProductImage120><ProductImage130><![CDATA[http://i.011st.com/t/130/am/
6/6/6/5/3/5/1194666535_L300_V24.jpg]]></ProductImage130><ProductImage140><![CDATA[http://i.011st.com/t/140/am/6/6/6/5/3/....

{% endhighlight %}

어떤가? 분명 이전과 같은 형식으로 해주었는데, 코드가 깨져 나온다.
이유가 뭘까? 당연히 인코딩 문제다.

---

### ENCODING

흔히 인코딩 문제를 직면할 경우에 다음과 같이 깨져서 나오는 건 자명하다.
물론, 해당 URL을 검색할 때는 잘 보이는 것을 확인 할 수 있다.
그럼 인코딩 문제를 해결해 보자.

사실 처음 11번가를 접했을 때, 좀 고생했던 부분이다. 뭐 몇시간 노닥거린 수준이긴 하지만 크롤링에 익숙치 않았던 나로써는 검색을 열심히 할 수 밖에 없었다.

위 콘솔에 찍힌 결과를 보자.

`EUC-KR` 라는 인코딩 상황이 떡 하니 보일 것이다.

그럼 EUC-KR을 UTF-8으로 바꾸는 작업이 필요하다. 잠깐 검색해 보아도, Iconv라는 모듈의 정보를 쉽게 접할 수 있을 것이다.

그럼 적용을 해보자.

{% highlight ruby %}

var request = require('request');
var Iconv = require('iconv').Iconv;
var euckr2utf8 = new Iconv('EUC-KR', 'UTF-8');

var options  = { encoding: "utf-8", method: "GET", uri: "http://openapi.11st.co.kr/openapi/OpenApiService.tmall?key=YOURKEY&apiCode=CategoryInfo&categoryCode=127648&option=Products&pageSize=1&pageNum=1"};

request(options, function(err, res, html) {

	var result = euckr2utf8.convert(html);
    //var result = euckr2utf8.convert(html).toString();
	console.log(result);
});

{% endhighlight %}

위와 같이 했을 때 콘솔에 무엇이 나오는지 보자.

역시나 안된다.

그럼 스트링으로 고치면 되는 걸까?

주석을 풀고 진행해보자..

역시나 깨지면서 나온다..

다른 여러가지 방법을 해보았지만 단순히 이런 변환을 통해서는 크게 찾지못했다.

그 이유는 get 요청에 있다.

요청시 binary로 요청을 해야 EUC-KR문서가 UTF-8으로 변환이 된다.

사실 포스팅 하면서 그 이유를 찾아보았는데, 그 이유가 설명된 곳은 찾지 못했다.

게다가 아무것도 모를 때는 찾을 때 굉장히 힘들었는데, 지금 찾으니 10초만에 찾아지는 놀라움...

하여튼 binary로 변환을 해보자.

{% highlight ruby %}

var request = require('request');
var Iconv = require('iconv').Iconv;
var euckr2utf8 = new Iconv('EUC-KR', 'UTF-8');

var options  = { encoding: "binary", method: "GET", uri: "http://openapi.11st.co.kr/openapi/OpenApiService.tmall?key=YOURKEY&apiCode=CategoryInfo&categoryCode=127648&option=Products&pageSize=1&pageNum=1"};

request(options, function(err, res, html) {

	var contents = new Buffer(html, 'binary'); //인코딩 변환
	var result = euckr2utf8.convert(contents).toString()
    //var result = euckr2utf8.convert(html).toString();
	console.log(result);
});

{% endhighlight %}

보면 갑자기 Buffer가 생긴걸 볼수 있다.
node.js는 버퍼구조내에 바이너리 데이터를 생성하고 읽고, 쓰고, 조작하기 위한 Buffer 모듈을 제공한다. 전역적으로 선언 되기 때문에, require도 필요가 없다.

버퍼를 왜 쓸까?

자바스크립트 자체는 유니코드에 친화적이지만 바이너리 데이터에는 별로 좋지 않다. TCP 스트림이나 파일시스템을 다룰 때 옥텟(octet) 스트림을 다룰 필요가 있다. Node에는 옥텟 스트림을 조작하고, 생성하고, 소비하는 여러 전략이 있다. 

출처 : [여기](http://nodejs.sideeffect.kr/docs/v0.8.20/api/buffer.html)

따라서 저 옥텟 스트림을 다루기 위해 버퍼가 필요했고, binary 데이터를 올바르게 읽어드릴 수 있게 되었다.

---

### IFRAME

자 이제 값이 보인다!

그런데!!

해당 물품의 이미지는 잘 보이지만 그 물품을 설명해 놓은 이미지는 API로 제공이 안된다.
따라서, 해당 물품번호로 찾아 들어가서 이미지를 긁으려 해보니...

IFRAME 내부에 해당하는 이미지가 놓여져 있다.

IFRAME 내부를 긁을 방법은 없을까??

한번 해보자.
{% highlight ruby %}

var request = require('request');
var Iconv = require('iconv').Iconv;
var euckr2utf8 = new Iconv('EUC-KR', 'UTF-8');
var cheerio = require('cheerio');
var xml2js = require('xml2js');
var parser = new xml2js.Parser({
    explicitArray: false
});

var options  = { encoding: "binary", method: "GET", uri: "http://openapi.11st.co.kr/openapi/OpenApiService.tmall?key=YOURKEY&apiCode=CategoryInfo&categoryCode=127648&option=Products&pageSize=1&pageNum=1"};

request(options, function(err, res, html) {

	var contents = new Buffer(html, 'binary');
	var result_encoding = euckr2utf8.convert(contents).toString();
	parser.parseString(result_encoding, function(err, result) {
		var product = result.CategoryResponse.Products.Product;
		var subRequest = { encoding: "binary", method: "GET", uri: product.DetailPageUrl}

		request(subRequest, function(err,res,html2){
			var strContents = new Buffer(html2, 'binary');
	    strContents = euckr2utf8.convert(strContents).toString();
  		var $ = cheerio.load(strContents);
  		console.log($("#prdDescIfrm"));
		});
	});
});

{% endhighlight %}

코드가 길어졌다.

이전에 설명했던 cheerIO도 썼고,xml2js도 사용했고 parser로 string 값을 변환도 해주었다.
그리고 내부에서 해당 물품에 접근 하기 위해 request도 한번 더 써주었다.

iframe에 접근해 보면 알 것이다. 내부 크롤링을 하려고 하면, 값이 나오질 않는다..

iframe 특성상 내부에 내부 html이 있는 형태로 접근이 힘든 것이다.

그럼 긁을 수 없는 것일까?

나도 많이 생각을 해봤지만 (다른 툴을 쓴다면 할 수 있을지도 모르지만,) 가장 쉬운 방법은 iframe에 해당하는 URL을 가져오는 것이 가장 쉽다.

해당 사항은 불법적인 역할이 될 수 있다고 판단되서 따로 URL을 적거나 하진 않겠지만 iframe도 접근이 불가능 한 것은 아니다.

이상으로 11번가 포스팅은 마치도록 하겠다.

---

### 추가

사실 얼마전에 지인이 크롤링에 대해 물어본 것이 있다.

URL에 접근을 하는데, 한 5초쯤 있다가 redirect 된다고 한다. 그 redirect되는 곳을 크롤링 하고 싶다는데..

듣고 나서 redirect가 왜 5초나 걸리지? 라는 생각을 했다. 물론 로딩속도가 걸린다거나 시간을 줄순 있지만 해당 뷰는 그런 상황은 아닌 듯 했다.

스크립트를 대충 훑어보니... 역시나 redirect가 아니라 javascript로 redirect처럼 보이도록 실행을 해두었다.

해당사항은 사실 크롤링하기가 상당히 까다롭다.

대강 알아보니 Phantom.js라는 걸 써서 따와야 한다고 한다. (나도 아직 안해봤다)

시간이 있을 때 한번 해보도록 해야겠다.



















