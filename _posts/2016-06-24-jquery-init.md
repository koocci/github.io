---
layout: post
title:  "[web] jQuery 시작하기"
date:   2016-06-24 14:51:23 +0900
categories: WEB
tags: [WEB,jquery,jquery mobile,jquery UI,library,framework,$,DOM]

---

# jQuery 시작하기

![computer](https://images.unsplash.com/photo-1421757381940-5d269570b21c?ixlib=rb-0.3.5&q=80&fm=jpg&crop=entropy&s=84969eec38041db4a36565671737b5ba)

처음 웹을 접하기 시작했을 때 부터, 가장 많이 들었던 라이브러리가 바로 jQuery다.
무엇보다 jQuery가 많이 언급 되는 이유는 역시 `크로스 브라우져`이다.
사실 내가 web쪽을 공부하기 시작한건 모바일관련해서 하이브리드 어플도 만들어보고, 실제 런칭도 해보고, 네이티브로도 갈아타 보고.. 또 자바스크립트 관련해서도 딥하게 들어가기 위해서 이리저리 하게 됬는데, jQuery는 자신이 직접 만들던지 뭘하던지 일단 알고는 있어야 할 듯 했다.(워낙 많이 써서 데이터도 많고 어떤 형식으로든 도움이 될 듯했다.)

비슷하게 적용되는 한국 서비스로 네이버에서 만든 `Jindo` 도 있고, 어플을 위해서 `아이오닉`이나 `자마린` 서비스를 이용해볼까도 했지만 역시 기본부터 하자 싶어서 `jQuery`를 선택했다.

---

### jQuery란?

`jQuery is a fast, small, and feature-rich JavaScript library. It makes things like HTML document traversal and manipulation, event handling, animation, and Ajax much simpler with an easy-to-use API that works across a multitude of browsers. With a combination of versatility and extensibility, jQuery has changed the way that millions of people write JavaScript.`

jQuery에서 공식적으로 설명해 놓은 문구다.
가장 잘 설명된 문구이기도 하다.

jQuery는 많은 사람들이 쓰는 javascript 라이브러리로 HTML 문서의 여러 형태의 이벤트들을 쉽게 쓸 수 있도록 해준다.

---

### 라이브러리? 프레임워크?

많이들 헤깔려하는 단어 두개다.
라이브러리는 무엇이고 프레임워크는 무엇일까?
먼저 공식적인 설명을 보자.

`라이브러리 : 소프트웨어를 만들 때 쓰이는 클래스나 서브루틴들의 모임을 가리키는 말`
`프레임워크 : 프로그래밍에서 특정 운영 체제를 위한 응용 프로그램 표준 구조를 구현하는 클래스와 라이브러리 모임`

딱 보면 일단 '아! 프레임워크가 라이브러리를 포함하구나!' 라고 생각할 수 있다. 맞는 말이기는 한데 조금 차원이 다르다.

아는 강사님께서 처음 나한테 라이브러리와 프레임워크의 차이를 설명해 주셨던 말은 다음과 같다.

`라이브러리는 삽이다. 프레임워크는 포크레인이다. 너가 화분에 담을 흙을 퍼담을 때와 건축공사를 하려고 흙을 팔 때를 생각해 보자. 라이브러리는 삽이니까 모종삽으로 만들어서 화분에 흙을 퍼 담아도 되고, 건축공사 할 때는 힘들겠지만 정말 큰 삽을 만들어서 퍼면 되. 하지만 포크레인은 일단 너가 포크레인 사용법을 배워야 하고, 이후에 화분에 흙을 넣든, 건축할때 땅을 파든, 큰 포크레인으로 해야만 하는 거야.`

단번에 이해 되었다.
다른 커뮤니티에 나온 글도 비슷하다. [이곳](https://kldp.org/node/124237)에 가면 쉬운 예시들이 많이 있다.

그리고 jQuery는 라이브러리다.

---

### jQuery를 시작해 보자.

먼저, html 문서를 간단히 만들자. (해당 예시는 html5로 제작되었다.)

{% highlight ruby %}

<!DOCTYPE html>
<html>
<meta charset="utf-8">
<head>
	<title>jQuery 시작하기</title>
	<script src="http://code.jquery.com/jquery.min.js"></script>
</head>
<body>
	<h1>안녕</h1>
</body>
</html>

{% endhighlight %}

간단히 안녕이라는 단어를 h1태그에 넣어 보여주는 뷰이다. 중요한것은 jquery 선언인데, 위와 같이 스크립트로 jquery를 선언하면 된다.

이와 같이 link를 이용해 jquery를 선언 하는 것을 `CDN`이라고 하며 정확하기 말해서 `Contents Delibery Network`다.

실제로 사용은 보통, CDN 선언으로 개발을 하고, 후에 배포작업시에 필요한 부분에 해당하는 것들만 다운받아 저장하는 방식이다.

위 예시의 경우는 단순히 선언 방식이며, 아직 jQuery를 사용하진 않은 것이다.
그럼 이제 스크립트에서 jQuery를 사용해 보도록 하자.
간단히 셀렉터를 볼 것이다.

{% highlight ruby %}

<!DOCTYPE html>
<html>
<meta charset="utf-8">
<head>
	<title>jQuery 시작하기</title>
	<script src="http://code.jquery.com/jquery.min.js"></script>
</head>
<body>
	<h1 id="test-id" >안녕</h1>
	<script type="text/javascript">
		console.log($("#test-id"));
		console.log(document.getElementById("test-id"))
	</script>
</body>
</html>

{% endhighlight %}

위 소스를 보면, `jQuery`와 `HTML DOM Method` 형식, 두가지로 같은 변수를 지칭해두었다.

둘은 같은 의미지만 위 `$` 문자가 들어간 것이 jQuery의 선언법이다.
작은 차이지만 후에는 매우 크게 느껴진다.

그런데 왜 스크립트를 body 내부에 선언해 두었을까?
그것은 호출 순서 때문이다.
다음을 보자.

{% highlight ruby %}

<!DOCTYPE html>
<html>
<meta charset="utf-8">
<head>
	<title>jQuery 시작하기</title>
	<script src="http://code.jquery.com/jquery.min.js"></script>
    	<script type="text/javascript">
		console.log($("#test-id"));
		console.log(document.getElementById("test-id"))
	</script>
</head>
<body>
	<h1 id="test-id" >안녕</h1>
</body>
</html>

{% endhighlight %}

위 예시의 결과를 보자.

아마 jQuery는 실행이 되지만, getElementById는 `null`로 처리가 되어 나올 것이다.

---

### 실행순서

이왕 하는 김에 스크립트 실행 순서도 같이 한번 알아보자.

{% highlight ruby %}

<!DOCTYPE html>
<html>
<meta charset="utf-8">
<head>
	<title>jQuery 시작하기</title>
	<script src="http://code.jquery.com/jquery.min.js"></script>
	<script type="text/javascript">
		console.log("1")
		console.log($("#test-id"));
		console.log(document.getElementById("test-id"))
	</script>
	<script type="text/javascript" src="./test2.js"></script>
	<script type="text/javascript">
		console.log("3")
		console.log($("#test-id"));
		console.log(document.getElementById("test-id"))
	</script>
	<script type="text/javascript" src="./test4.js"></script>
</head>
<body>
	<script type="text/javascript">
		console.log("5")
		console.log($("#test-id"));
		console.log(document.getElementById("test-id"))
	</script>
	<h1 id="test-id" >안녕</h1>
	<script type="text/javascript">
		console.log("6")
		console.log($("#test-id"));
		console.log(document.getElementById("test-id"))
	</script>
</body>
</html>

{% endhighlight %}

위와 같이 하고, test2.js,test4.js 에는

{% highlight ruby %}

console.log("2")
console.log($("#test-id"));
console.log(document.getElementById("test-id"))

console.log("4")
console.log($("#test-id"));
console.log(document.getElementById("test-id"))

{% endhighlight %}

를 넣어 주었다.

그럼 결과를 확인해보자.

뭐 역시나.. 1,2,3,4,5,6 순서로 나오고, 6의 경우만 getElementById 값이 나온다.

이로서 스크립트 실행이 어떻게 되는지 알 수 있고, 6의 경우만 getElementById가 실행됨을 봐서, 해당 실행 중 HTML보다 먼저 id호출이 실행이 되면 인식하지 못함을 알 수 있었다.

그렇다면 jQuery는 어떻길래 해당사항이 실행되는 것일까?

속내를 보도록 하자.

위 코드를 다음과 같이 바꿔보도록 한다.


{% highlight ruby %}

<!DOCTYPE html>
<html>
<meta charset="utf-8">
<head>
	<title>jQuery 시작하기</title>
	<script src="http://code.jquery.com/jquery.min.js"></script>
	<script type="text/javascript">
		console.log("1")
		console.log($("#test-id")[0]);
		console.log(document.getElementById("test-id"))
	</script>
	<script type="text/javascript" src="./test2.js"></script>
	<script type="text/javascript">
		console.log("3")
		console.log($("#test-id")[0]);
		console.log(document.getElementById("test-id"))
	</script>
	<script type="text/javascript" src="./test4.js"></script>
</head>
<body>
	<script type="text/javascript">
		console.log("5")
		console.log($("#test-id")[0]);
		console.log(document.getElementById("test-id"))
	</script>
	<h1 id="test-id" >안녕</h1>
	<script type="text/javascript">
		console.log("6")
		console.log($("#test-id")[0]);
		console.log(document.getElementById("test-id"))
	</script>
</body>
</html>

{% endhighlight %}

위와 같이 하고, test2.js,test4.js 에는

{% highlight ruby %}

console.log("2")
console.log($("#test-id")[0]);
console.log(document.getElementById("test-id"))

console.log("4")
console.log($("#test-id")[0]);
console.log(document.getElementById("test-id"))

{% endhighlight %}

를 실행시켜 보자.

결과가 어떠한가? 아마 둘다 undefined와 null로 나올 것이다.(6번 실행은 같은 값이 나올것이고, 실행순서는 당연히 차이가 없다.)
코드의 변화는 단 하나 `[0]`값이다.
즉, $라는 문자는 jquery객체 자체를 말하며, 해당 아이디의 값은 배열로서 [0]에 저장이 된다는 사실을 알 수 있었고, 처음 [0]이 붙기 전에는 jquery 객체를 지정함으로써 처음 보는 사람은 값이 있구나! 라고 착각할 수도 있지만 사실 속으론 아무 값도 (undefined) 없게 된 것이다.
물론 [0]를 붙인 값이나 getElementById 값은 HTML DOM 객체를 지정하므로서 실행 순서에 따라 값이 없다고 지칭이 되는 것이다.

그렇다면 어떻게 스크립트 내에서 실행을 할까?

---


![computer](https://images.unsplash.com/photo-1453799527828-cf1bd7b2f682?ixlib=rb-0.3.5&q=80&fm=jpg&crop=entropy&s=4660f9591de335c3f6a5e83c45fbac88)


### jQuery ready vs load

jQuery를 쓸 때면, `$(document).ready` 라는 함수를 참 많이 쓰게 된다.
혹여나 jQuery를 쓰지 않는다면 `window.load`라는 함수를 쓰게 되는데, 흔히 둘은 같다고 착각할 수가 있다. 

사실은 실행순서에 차이가 있다.

순서는 다음과 같다.

`사용자 웹 출력요청 - 브라우져 웹 read  - DOM 생성 - 이미지, script 생성 - 로드 완료`

여기서 ready 함수는 DOM생성 직후에 실행이 되지만 load는 무든 로드가 완료된 후 실행 된다.

따라서 ready 함수와 같은 식으로 쓰려면 사실

{% highlight ruby %}

document.addEventListener("DOMContentLoaded", function(event) { 
    //Do work
});

{% endhighlight %}

와 같은 형식의 함수를 사용해야 하는데, 잘 쓰지는 않는 듯 하다.

하여튼 우리가 위의 예시에서 console의 출력을 가져오려면 ready나 load함수를 선언하고 그 내부에 적어주어야 제대로 실행이 된다.

---

### $

조금 얘기가 다른 방향으로 빠진 듯 하지만 분명 중요한 것들이니 적어 두었다.
자 이제 $라는 것을 알게 되었다.....
근데 이게 뭘까? jQuery에서 쓰는 것???...

정확한 명칭은 `DOM 엘리먼트셀렉터` 이다.
이전에 우리가 했던 것들을 보면 그 이유를 알 수 있다.
document라던지, id등은 DOM의 element들이다. (document도 document의 하나의 node다.)
[여기](http://www.w3schools.com/jsref/dom_obj_all.asp)를 보면 잘 정리가 되어 있다.

아이디를 지칭할 때 우리는 $("#id")와 같이 선언하였다.
클래스는 $(".class") 와 같다.
어디선가 보았다.
그렇다 `css`에서도 위 예시처럼 사용을 한다.

이처럼 사용성이 굉장히 높다.

오늘의 포스팅은 여기까지 하고, 셀렉터,속성,이벤트 등은 다음 포스팅에 이어서 하겠다.
