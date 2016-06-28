---
layout: post
title:  "[web] jQuery 시작하기 - mobile,UI"
date:   2016-06-28 09:43:53 +0900
categories: WEB
tags: [WEB,jquery,jquery mobile,jquery UI,library,framework,$,DOM]

---

# jQuery mobile

![phone](https://images.unsplash.com/photo-1444356751607-31f0fd2714f1?ixlib=rb-0.3.5&q=80&fm=jpg&crop=entropy&s=e10ae28ea99dcbc5e512a56d60a86c18)

이전 포스팅에서 jQuery에 관한 소개와 여러 속성, 이벤트등을 작성했었다.
그리고 이번 포스팅에서는 간단히 jQuery mobile에 대해 소개해 볼까한다.
내가 jQuery Mobile을 접했던 것은 하이브리드 어플을 제작하기 위해서 였다.
처음엔 `Angular`를 공부해서 `iOnic`으로 만들어볼까 했지만 그래도 좀더 기초에 다가갈 수 있게 `jQuery mobile`과 `PhoneGap`을 이용해서 만들었고, 순차적으로 해당사항에 대해서도 포스팅을 할 계획이다.
그럼 jQuery Mobile에 대해 알아보자.

---

### 정의

난 항상 무언가를 공부할 때 정의는 꼭 제일 먼저 보게된다. 뭐 누구나 그렇겠지만 만든사람의 생각이 가장 명확히 들어난다고 생각하기 때문이다.

`jQuery Mobile is a HTML5-based user interface system designed to make responsive web sites and apps that are accessible on all smartphone, tablet and desktop devices.`

jQuery mobile 사이트에 들어가면 가장 먼저 나오는 문구다.
즉, 위 라이브러리는 모바일이나 테블릿 혹은 데스크탑 등의 모든 환경에서 반응형 웹사이트, 앱에 맞추어서 사용할 수 있도록 나온 것이다.

일반적으로 안드로이드든 아이폰이든 웹 사이트든 반응형은 이제 당연히 해야하는 기술이 되었다.
뭐 아이폰은 그래도 적은 편이지만 안드로이드 폰같은 경우 화면도 너무 다양하고, 크기도, 사양도 너무 다양해서 어떻게 될지 모른다.
따라서 native로 짤 때에도 내가 알기로는 해당 사항을 많이 생각하면서 짜야 하는 것으로 알고 있다.
사용법자체가 jQuery랑 다른 것은 아니니 쉽게 접근을 해보자.

---

### css FrameWork

jQuery mobile에서는 미리 정해진 클래스 이름들이 있는데 해당 클래스를 넣어주면 css가 바뀌게 된다.

해당 DOC는 [여기](http://api.jquerymobile.com/classes/)에 적혀 있다.
일반적으로 jQuery mobile을 많이 써보지 못했을 때에는 대강의 흐름만 보고 예시를 옮겨 쓰거나 했던 적이 많았다. 그러나 최근에는 이러한 세부적인 걸 보게 되면서 미리미리 체킹을 하고 원하는 모양으로 바꾸고 하다보니 훨씬 깔끔하고 이쁘게 되는 걸 확인할 수 있었다.

예시에는 위에 설명한 class가 들어가 있는 경우가 많으니 뺄것은 빼고 원하는 모양을 만들면 될 것이다.
이외에 css FrameWork에는 Grid Layout과 Responsive Grid, Theme이 있는데 나는 Grid Layout과 Responsive Grid의 경우 좀 사용성이 높지 못한것 같아 `bootstrap grid system`을 사용했다.

이외의 내용은 [여기](http://api.jquerymobile.com/category/css-framework/)에서 한번 읽어보면 좋다.

---

### Events

`Event`를 컨트롤 하는 것은 참 까다로운 일이다.
[여기](http://api.jquerymobile.com/category/events/)에 해당하는 Event들이 나열되어 있는데, 개인적으로 많이 썼던 것이나 중요한 부분들을 적어보겠다.

navigate의 경우 `history관리`에 있어서 자주 쓰는데, jQuery mobile상에서 뒤로가기시, 탭상의 history도 저장이 되기 때문에 뒤로 갈때 이전 탭이 선택될 때가 있다. 물론 해당 사항이 원하던 기능이면 상관이 없는데 개인적으로는 탭이 아니라 페이지 형식으로 넘겨야 하는 상황이라 navigate 쪽을 손을 봐서 구현을 했다.

{% highlight ruby %}

$(window).on("navigate", function(event, data) {
  if (data.state.direction == "back" && $(".ui-popup-active").length < 1) {
    event.preventDefault();
    history.back(1);
  }
});

{% endhighlight %}

해당 사항은 내가 만들었던 서비스의 기준이고 원하는 방향이 있다면 수정하면 될 듯 하다.

다음으로 이건 궁금한 사람도 많을 것이고, 한번 정리를 하면 좋을 꺼같아서 작성해 볼것인데,
`Event`중에 페이지 로드될 때의 호출되는 것들이 많은데, 그 상황을 한 번 비교를 해보겠다.
비교 해볼 것들은 
`mobileinit`
`pagebeforecreate`
`bagebeforehide`
`pagebeforeload`
`pagebeforeshow`
`pagecreate`
`pageinit`
`pageload`

이다. 해당 사항들이 언제 호출되는 지는 사실 해당 이벤트 설명에 나와 있으나, 전체를 비교하는 코드를 만들어 보도록 하겠다.

{% highlight ruby %}

<!doctype html>
<html>
<head>
  <title>Example</title>
  <meta charset=utf-8 />
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="stylesheet"  href="http://code.jquery.com/mobile/1.4.5/jquery.mobile-1.4.5.min.css" />
  <script src="http://code.jquery.com/jquery-1.10.2.min.js"></script>
  <script>
// Update configuration to our liking
$( document ).on( "mobileinit", function() {
	console.log("mobileinit : Event indicating that jQuery Mobile has finished loading.");
});
$( document ).on( "pagebeforecreate", function() {
	console.log("pagebeforecreate : Triggered on the page being initialized, before most plugin auto-initialization occurs.");
});
$( document ).on( "pagebeforeload", function() {
	console.log("(d)pagebeforeload : Triggered before any load request is made.");
});
$( document ).on( "pagebeforeshow", function() {
	console.log("(d)pagebeforeshow : Triggered on the 'toPage' we are transitioning to, before the actual transition animation is kicked off.");
});
$( document ).on( "pagecreate", function() {
	console.log("pagecreate : Triggered when the page has been created in the DOM (via ajax or other) and after all widgets have had an opportunity to enhance the contained markup.");
});
$( document ).on( "pageinit", function() {
  console.log( "pageinit : Triggered on the page being initialized, after initialization occurs." );
});
$( document ).on( "pageload", function() {
	console.log("(d)pageload : Triggered after the page is successfully loaded and inserted into the DOM.");
});
$( document ).on( "pageshow", function() {
	console.log("(d)pageshow : Triggered on the 'toPage' after the transition animation has completed.");
});
  </script>
  <script src="http://code.jquery.com/mobile/1.4.5/jquery.mobile-1.4.5.min.js"></script>
</head>
<body>
  <div data-jqm-role="page">
    <div data-jqm-role="header">
      <h2>jQuery Mobile Example</h2>
    </div>
    <div data-jqm-role="content">
    	<h1>안녕</h1>
    </div>
  </div>
</body>
</html>

{% endhighlight %}

자바스크립트를 조금이라도 공부했다면 선언순서가 크게 차이가 없다는 것은 알고 있을 것이다.
console에는 실행 이벤트 명과 언제 나오는지를 적어 두었다.
그럼 해당 구문의 결과를 보자.

{% highlight ruby %}

mobileinit : Event indicating that jQuery Mobile has finished loading.

pagebeforecreate : Triggered on the page being initialized, before most plugin auto-initialization occurs.

pagecreate : Triggered when the page has been created in the DOM (via ajax or other) and after all widgets have had an opportunity to enhance the contained markup.

pageinit : Triggered on the page being initialized, after initialization occurs.

(d)pagebeforeshow : Triggered on the 'toPage' we are transitioning to, before the actual transition animation is kicked off.

(d)pageshow : Triggered on the 'toPage' after the transition animation has completed.

{% endhighlight %}


먼저 `Load`란 단어가 들어간 곳은 출력이 되지 않았다.
참고로 (d)가 들어간 문구는 jquery mobile 1.4부터 deprecated 된것이라 하여, 사용하지 않는 것이 좋다.

즉, 순서를 보면

`mobileinit`이 jquery mobile의 로딩이 끝났을 때, `pagebeforecreate`,`pagecreate`,`pageinit` 순으로 호출이 된다.

이런 호출이 이루어 진다는 건 한번정도 정리해 두면 편하다.
그럼 다른 이벤트를 볼 것인데 바로 scroll이다.

scroll의 경우는 모바일의 경우 참 많이 쓰인다. Listview의 로딩에 있어서도 그렇고, 페이징도 그렇고 본인만의 scroll 노하우를 하나 만들어두는 것이 좋다.

나같은 경우는 `scrollHelper`라는 것을 만들어서 스크롤처리를 하는데, 일반적으로 스크롤이 리스팅의 마지막에 가면 새로운 리스트를 추가적으로 생성되게 하므로, 해당 처리를 해주면 된다.

예를 들어,

{% highlight ruby %}

var activePage = $.mobile.pageContainer.pagecontainer("getActivePage"),
	        screenHeight = $.mobile.getScreenHeight(),
	        contentHeight = $(".ui-content", activePage).outerHeight(),
	        header = $(".ui-header", activePage).outerHeight() - 1,
	        scrolled = $(window).scrollTop(),
	        scrollEnd = contentHeight - screenHeight + header,

{% endhighlight %}

다음과 같은 변수가 있다고 하자.(나 역시 모를때는 구글링으로 해당 방법을 찾았다.)
그럼 현재 보고 있는 뷰에 대한 스크롤 위치를 모두 잡을 수 있다.(`footer`가 있다면 `header`와 같은 방법으로 추가하면 된다.)

{% highlight ruby %}

if (activePage[0].id == "myPage" && scrolled >= scrollEnd && scrollEnd > 0) {
	        myPage_pageNum+=1;
	        addMore("myPage",myPage_pageNum);
	    }

{% endhighlight %}

다음과 같이 해당하는 뷰에서 스크롤의 위치가 마지막에 갈 경우, page를 하나 늘려주고 리스트를 부르는 함수를 실행 시키면 된다.

이외에 `mouseenter` 나 `mouseleave`와 같은 이벤트는 지도에서도 많이 쓰이고, 이미지나 버튼의 형식에서 디자인을 바꾸어 주고 싶을 때,(예를 들면 마우스가 들어가면 버튼의 색이 빠뀌는 등) 사용을 많이 한다.

---

### METHOD

사실, `iCon`과 같은 것도 순서상 있지만, 해당사항은 건너뛰도록 하겠다.
다음으로 볼 것은 `Method` 부분이다.

사실 이전 스크롤부분에서 사용한 것(`activePage`)도 있다.

많이 쓰긴 하면서도 막상 뭐가 있는지 몰라 안쓸때도 많다.
[여기](http://daeson.tistory.com/entry/jQuery-Mobile-API-Methods-API-%ED%95%A8%EC%88%98)에 참조하면 해석도 같이 될 수 있다.

개인적으로 자주 썼던 것은 `jqmData`와 `$.mobile.path.parseUrl (method)` 정도가 있는데, 해당사항에 있어서 본인이 사용할 것이라면 적극 사용하길 권한다.

이외에도 많은데, 특히 `listview`라던지, `popup`과 같은 경우는 자주쓰므로 본인이 사용할 경우 한번 찾아서 써보는 걸 추천한다.

자주하는 실수로는 `popup은 한번에 하나밖에 호출하지 못한다.` 여러개를 호출 하지 못하므로 popup한 이후 해당 popup이 또 다른 popup을 호출한다면 미리 선언되었던 popup을 지우고 띄우던지, 다른 방식으로 해야 할 것이다.

이 후에 `phoneGap`을 다루게 되면 그 때 jQuery Mobile에 대해 좀더 많이 다루게 될 것이다. 역시 코딩은 실전이므로.... 이렇게 하나하나 설명하는 것보다 더 이해가 빠를 것으로 생각된다.

---

### jQuery UI

![mobile](https://images.unsplash.com/photo-1462078563783-650e23af549d?ixlib=rb-0.3.5&q=80&fm=jpg&crop=entropy&s=8f5ad70474ec3c130614c818794b6d81)

`jQuery UI` 역시 나는 내가 쓰고 싶은 것만 썼었기에 사실 어떤 기능이 더 있는지 알지 못한다.
그래도 아마 `jQuery UI`를 사용할 때의 가장 큰 부분은 다 다루지 않을까 싶다.

흔히 이미지를 끌어당기거나, 놓거나, class를 추가해 색을 바꾸거나,Dialog를 만들거나 같은 경우 일 듯 한데 먼저 컴포넌트를 끌어당기고 놓는 것을 한번 보자.

해당사항은 `draggable`과 `droppable`을 사용을 하게 된다. 분명 [여기](https://jqueryui.com/draggable/#sortable)에 좋은 예시들과 함께 나와있지만, 잘 모르는 사람은 헤깔릴 수 있으므로 draggable부터 보면,

{% highlight ruby %}

var dragInit = function() {
	$( ".draggable" ).draggable({
		helper: "clone",
		appendTo: "body",
		stop: handleDragStop
	});
}

{% endhighlight %}

위 함수가 drag를 할수 있게 만드는 것이다.
`helper`는 어떤 방식으로 끌고 오게 할 것인가? clone같은 경우는 해당 사항을 복제한다.
`appendTo`는 어디에 놓을 수 있게 할 것인가 이고
`stop`은 멈췄을 때 어떤 함수를 실행 시킬지를 정한다.
이외에도 많이 있지만 (`z-index`도 설정할 수 있다.) 필요하면 찾아보도록 하자.

{% highlight ruby %}

var dropInit = function(){
	$( ".droppable" ).droppable({
		accept: '.draggable,.A,.B',
		hoverClass: 'hovered',
		drop: handleDrop
	});
}

{% endhighlight %}

위 예시는 `droppable`에 대한 예시이다. 해당사항을 보면 `accept`에서 받을 수 있는 것을 명시해준다. 위의 예시의 경우 `draggable`,`A`,`B`가 선언되어 있는 클래스의 내용들만 끌어와서 넣을 수 있다.
`hoverClass`의 경우 해당 사항을 끌어서 `droppable`에 올렸을 때, 어떤 클래스를 droppable에 추가 해줄지 명시한다. 
위의 예시의 경우 `hovered`라는 클래스를 추가하게 되고, `hovered`가 background를 검은색으로 한다 할 때, 끌어서 해당사항 위에서 잡고 있을 때,(놓으면 사라진다.) background는 검은색으로 되어 있을 것이다.
`drop`은 놓았을 때 실행하는 함수가 될 것이다.


`dialog`의 경우는 사실 예시가 가장 정확하다. 주의할 점만 보면 `bootstrap`과 같이 선언되어 있을 경우, `jQuery UI`를 나중에 선언하지 않으면 이미지가 안보이는 경우가 생길 수 있다(명명이 겹칠 때가 있다.)

UI를 쓰기가 개인적으로 처음엔 까다로웠었다. Document도 잘 읽지 못할 때 사용해서 그런지 시간이 많이 걸렸었는데 한번 하고나면 이해가 정말 쉬우니 한번 해보길 바란다.

이상으로 간단한 `jQuery`에 대한 설명을 마친다.
다음 포스팅을 아직 정하지 못했는데, `node js` 혹은 `phoneGap`이 되지 않을까 싶다.