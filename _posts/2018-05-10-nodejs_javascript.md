---
layout: post
title:  "[Node js] Nodejs & javascript"
date:   2018-05-10 16:26:00 +0900
categories: Nodejs
tags: [Nodejs, javascript, 면접]

---

## Nodejs & Javascript 면접 질문
---


![node](http://farm1.static.flickr.com/199/447771112_24cd5d5564_z.jpg)

면접을 볼 때, 나는 항상 가장 자신있는 언어를 **javascript** 라고 말한다. 물론, 왜 알고리즘은 C++로 풀었냐고 물어본 분도 있지만.... (항상 C++로 알고리즘을 풀었기 때문이라고 대답했다가 떨어진적도 있다)

그래도 일단은 가장 많이 써본 언어가 javascript이기 때문에 그렇게 대답했다.

그런데 javascript라는게 참 어렵다. Nodejs도 어렵고 정말 어려운 언어라고 생각한다. 물론, 웹에서도 쓰고 서버에서도 같은 언어로 호환한다는 장점이 있지만 사실 통신을 조금만 해봐도 크게 의미 없다고 느낀다. 어짜피 정형화된 통신규칙으로 데이터를 주고받으니 서로 맞춰서 처리하면 그만이다.

굳이 장점을 말하면, 처음 개발할 시에 프론트, 백엔드 따로 언어를 공부하는 것보다 진입장벽이 2개에서 1개로 줄일 수 있다는 것??

그렇지만 개발을 하다보면 한가지 언어로만 개발하기는 쉽지 않다.

나처러 허접한 개발자만해도, JAVA로 안드로이드 개발을 했고, Python으로 인공지능이나, Django, Flask등을 사용했다. (HTML, CSS는 논외로..)


어떻든 일단, 면접 질문이 이번에 핵심 포인트니, 하나씩 떠올려보며 적어보도록 하겠다.

그전에 한가지만, javascript가 무엇인지만 정리해보고 가자.

---

### javascript 란?

---

자바스크립트를 가장 처음 접하는 사람은 아무래도 프론트앤드에서 접하는 사람이 많지 않을까한다. 동적인 움직임을 주기 위해, 와 같은 문장으로 알아볼 수도 있지만, 언어 자체에 대해 알아보자.

출처 : [About Javascript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/About_JavaScript)

`JavaScript® (often shortened to JS) is a lightweight, interpreted, object-oriented language with first-class functions, and is best known as the scripting language for Web pages, but it's used in many non-browser environments as well. It is a prototype-based, multi-paradigm scripting language that is dynamic, and supports object-oriented, imperative, and functional programming styles.`

JavaScript® (줄여서 JS)는 일급 함수를 사용하는 가벼운 객체 지향 인터프리터 언어이며 웹페이지의 스크립트 언어로 잘 알려져 있지만, 브라우저가 아닌 환경에서도 많이 사용된다. 프로토타입 기반, 다중 패러다임 스크립트 언어이며, 동적이고 명령어, 객체 지향, 함수 프로그래밍 스타일을 지원한다.

---

#### first-class functions(1급 함수)

---

**first-class functions(1급 함수)** 라는 단어는 나도 처음 들어봤는데, 이에 대해 [잘 설명 해둔 곳 (https://bestalign.github.io/2015/10/18/first-class-object/)](https://bestalign.github.io/2015/10/18/first-class-object/)이 있어서 이 글을 빌려오겠다.

`first class citizen(1급 시민)`이라는 개념을 먼저 소개하는데, 세가지 조건을 충족하면 1급 시민이라고 한다.

1. 변수(variable)에 담을 수 있다
2. 인자(parameter)로 전달할 수 있다
3. 반환값(return value)으로 전달할 수 있다

따라서, 어떤 언어에서 객체(object)가 이런 1급 시민 조건을 충족할 때, **1급 객체(first class object)** 라고 한다.

따라서, 함수(function)이 이런 조건을 충족하면 **first-class functions(일급 함수)** 라고 하는데, 학자에 따라 추가적인 조건이 붙는다.

1. 런타임(runtime) 생성이 가능하다
2. 익명(anonymous)으로 생성이 가능하다

따라서, 이런 추가 조건에 의해, C는 1급 함수가 될 수 없다.

Javascript는 1급 객체이자 1급함수가 된다.

여기서 1급 함수가 중요한 이유를 이렇게 설명한다.

`고차 함수(high order function)가 가능하다`
`클로져(clusure)로 인해, Lexical Environment를 기억하게 되는데, 함수를 주고받게 되면 이 Lexical Environment도 함께 전달된다. 이것을 이용해서 커링(currying)과 메모이제이션(memoization)이 가능해진다.`

고차 함수라 함은,
1. 함수를 파라미터로 전달 받는 함수
2. 함수를 리턴하는 함수

중 하나 이상을 만족하는 함수를 말한다.

**클로져(closure)** 는 면접질문에서도 자주 나오고 워낙 중요하니, 정리하고 넘어가보도록 하겠다.

**클로저는 함수와 함수가 선언된 어휘적 환경(Lexical Environment)의 조합**

이라는 정의를 가지고 있는데, 간단히 말해서, `클로져 안의 함수는 그 환경을 기억한다.`

출처 : [https://hyunseob.github.io/2016/08/30/javascript-closure/](https://hyunseob.github.io/2016/08/30/javascript-closure/)

흔히,  함수 내에서 함수를 정의하고 사용하면 클로저라고 하는데, 예시를 보면 더 화끈하게 이해된다.
``` JavaScript
var base = 'Hello, ';
function sayHelloTo(name) {
  var text = base + name;
  return function() {
    console.log(text);
  };
}
var hello1 = sayHelloTo('승민');
var hello2 = sayHelloTo('현섭');
var hello3 = sayHelloTo('유근');
hello1(); // 'Hello, 승민'
hello2(); // 'Hello, 현섭'
hello3(); // 'Hello, 유근'
```

여기서 기억한다가 바로 **memoization** 를 의미한다. 그럼, **currying** 이란 무엇일까?

출처 : [https://medium.com/@jinro4/%EA%B0%9C%EB%B0%9C-currying-in-javascript-e7ccdd7862e0](https://medium.com/@jinro4/%EA%B0%9C%EB%B0%9C-currying-in-javascript-e7ccdd7862e0)

사실 나도 처음 들은 단어인데, 위키피디아에서 다음과 같이 말한다.

`수학과 컴퓨터 과학에서 커링이란 다중 인수 (혹은 여러 인수의 튜플)을 갖는 함수를 단일 인수를 갖는 함수들의 함수열로 바꾸는 것을 말한다. 모지즈 쇤핑클에 의해 도입되었고, 이후 해스켈 커리에 의해 발전하였다.`

흔히 클로져에서 사용되고, 예시는 위 출처에 잘 표현되어 있다.

다음은 인터프리터에 대해 알아보자.

---

#### 인터프리터 언어

---

인터프리터 언어와 컴파일 언어의 차이는 대부분 잘 안다.
간단히 정리하고 넘어가면,

**컴파일언어** 는 고급언어로 되어있는 프로그램을 컴퓨터가 이해할 수 있는 번역과정(컴파일)이 필요한 언어로, 번역과 실행과정을 거쳐야 하기 때문에 시간이 오래 걸리지만, 한번 번역하고 난 다음에는 빠르게 수행할 수 있다.

**인터프리터언어** 는 프로그램을 한 단계씩 기계어로 해석하여 실행하는 언어로, 줄 단위로 번역, 실행된다.
따라서, 변화에 적응이 빠르고 대화형에 적합하지만, 한단계씩 해석하며 가므로 실행 시간이 길어져 속도가 느리다. 또한 프로그램이 직접 실행되므로 목적 프로그램이 생성되지 않는다.

또 한가지 덧붙이면, 3개의 CORE로 이루어진 프로그램이 있다할 때, 한개라도 오류가 날 경우, 컴파일언어는 컴파일과정에서 오류를 낸다. 그러나, 인터프리터언어는 언어 자체의 문법이 잘못되어 있는 경우가 아니라면 해당 부분에 실행이 되기 전까지 오류를 내지 않는다. (실행을 해봐야 잘못된지 아는 경우)

---

#### 스크립트 언어

---

`기존에 이미 존재하는 소프트웨어(애플리케이션)를 제어하기 위한 용도로 쓰이는 언어`를 **스크립트 언어** 라고 한다.

컴파일 언어에서는 컴파일 시간 때문에 오래걸리겠지만, 인터프리터 언어는 한줄씩 실행하기 때문에 수정이 빈번하게 일어나도 대응하기 쉽다. 따라서 스크립트 언어는 이를 충분히 활용하기에 적합하다고 한다.


---

### ECMAScript 란?

---

난 학부생이고 (졸업 유예긴 하지만) 학부에서 ECMA에 대해 배웠다는 건 보지 못했다. (javascript 조차도 실험(프로젝트 개발) 시간에 개인적으로 공부해서 적용하는 수업이 전부였다.)

그러나, ECMAscript에 대한 면접질문을 받은 적이 있다. 아무래도 javascript에 자신감이 있다고 해서 그런듯 하다.

그래서 좀 자세히 알아보고 넘어가 보려고 한다.

일단 표준이 무엇이냐 하면 ECMAScript이다. 그리고 javascript나 Jscript 등, 이런 ECMAScript와 호환을 목표로 맞추어가고 있고, 추가적인 기능을 제공하고 있다고 보면 된다.

ECMA6가 제공하는 기능에 대해 적으려면 책 한권이기 때문에 중요한 것만 언급해보자.

---

#### 호이스팅의 문제점을 줄이고 있다.

---

호이스팅은 면접 때 자주 물어본다.

자바스크립트 변수의 **범위(scope)** 와 **호이스팅(hoisting)** 이 매우 중요한데, 세세한 부분은 다음을 참고하도록 하자 [http://chanlee.github.io/2013/12/10/javascript-variable-scope-and-hoisting/](http://chanlee.github.io/2013/12/10/javascript-variable-scope-and-hoisting/)

호이스팅에 대해 설명하자면, 자바스크립트는 `변수의 정의가 그 범위에 따라 선언과 할당으로 분리`된다. 즉, 선언이 되어만 있으면 이후에 실행할 때, 선언부만 최상단으로 선언을 끌어올린다.

따라서,
``` JavaScript
function showName() {
     console.log("First Name : " + name);
     var name = "Ford";
     console.log("Last Name : " + name);
}
showName();
// First Name : undefined
// Last Name : Ford
// First Name이 undefined인 이유는 지역변수 name이 호이스트 되었기 때문입니다.
```

``` JavaScript
function showName() {
     var name; // name 변수는 호이스트 되었습니다. 할당은 이후에 발생하기 때문에, 이 시점에 name의 값은 undefined 입니다.
     console.log("First name : " + name); // First Name : undefined
     name = "Ford"; // name에 값이 할당 되었습니다.
     console.log("Last Name : " + name); // Last Name : Ford
}
// First Name : undefined
// Last Name : Ford
// First Name이 undefined인 이유는 지역변수 name이 호이스트 되었기 때문입니다.
```

위 두개를 똑같이 해석해버린다.

그럼 다음을 참조하면서 진행해보겠다.

[https://blog.perfectacle.com/2016/11/10/es6-scope/#ES5%EC%9D%98-%ED%95%A8%EC%88%98-%EB%8B%A8%EC%9C%84%EC%9D%98-%EC%8A%A4%EC%BD%94%ED%94%84](https://blog.perfectacle.com/2016/11/10/es6-scope/#ES5%EC%9D%98-%ED%95%A8%EC%88%98-%EB%8B%A8%EC%9C%84%EC%9D%98-%EC%8A%A4%EC%BD%94%ED%94%84)

호이스팅이 어떤 문제가 생기는가는 뻔하다. 값을 덮어씌워버리거나, 상위에 아직 선언되지 않은 변수에 하위에 있다고해서 접근할 수가 있다.

이런 문제점을 줄이기 위해, **TDZ(Temporal Dead Zone)** 라는 것을 이용해 호이스팅이 되긴 하되 오류가 나도록 해결했다. (레거시 환경(var) 때문에 아예 없애지는 못한것 같다고 예상하는 듯 하다.)

---

#### 함수 단위 스코프 -> 블록 단위 스코프

---

함수 단위 스코프를 설명하기 위해서는, 여러가지 기본 개념이 필요하다.

**스코프** **콜 스택** **실행 컨텍스트** 에 대한 설명이 필요한데, 스코프는 앞서 링크를 걸었었고, 다른 두개는 [이 곳](https://www.zerocho.com/category/JavaScript/post/597f34bbb428530018e8e6e2)과 [이곳](https://www.zerocho.com/category/Javascript/post/5741d96d094da4986bc950a0)을 참조하며 보도록 하자.

그리고 **이벤트 루프** 개념도 꼭 알아두어야 하니, 상위 링크에서 알아두도록 하자. (면접 질문을 콜 스택, 태스크 큐, 이벤트 루프로 받은 적이 있다.)

var를 여전히 지원하지만(레거시) **const** 나 **let** 을 권장하도록 되었다.

var는 함수 단위 스코프인데, 위 링크의 내용을 보면 전역적으로 선언이 되어 파일이 분리되어 있을 떄 문제가 생길 수 있다는 것을 알 수 있다.

그러나 블록 단위 스코프를 사용하는 const와 let을 사용시, 이런 문제점이 사라지게 된다.

그 외의 중요한 부분은 **Arrow Function** 이나 **Promise** 가 있다.

이를 다 설명하려면 정말 오래 걸리기 때문에, Promise가 Call back Hell을 해결해준다는 것 정도 알고 넘어가자.

---

### javascript에서 프로토타입은 무엇인가

---

**프로토타입** 을 물어보는 회사는 그렇게 많지 않을듯하다. 그래도 개발자라면, 개발자가 가고싶어하는 회사를 가려면 알아두어야하는 개념이다.

프로토타입은 먼저 javascript가 OOP적으로 동작한다는 개념을 먼저 가지고 시작해야한다.

그러므로 **생성자** 에 대한 개념부터 시작해보자.

이 부분의 개념은 [이곳](https://www.zerocho.com/category/JavaScript/post/573c2acf91575c17008ad2fc)에서 확인하자.

단지, ECMA6부터 class에 대한 개념이 생겼기 때문에, 없지는 않고, 프로토타입 기반의 OOP의 성격을 더욱 명확하게 하기 위해, 없진 않다고 알아두면 된다.

흔히, `new 생성자(인자);`라는 문법으로 생성자를 사용하는데, `A.prototype.B = function` 이라고 선언해서 변수나 메소드를 추가한다면, 해당 생성자로 만들어지는 모든 객체가 공유하게 된다.

또한 `__proto__` 와 같이, 생성자로 선언했을 때, 새로운 객체가 생기는 걸 볼 수 있는데, 생성자의 prototype이 참조된 것이다.

상당히 헤깔리는 개념이니 잘 알아두도록 하자.

정리하면,

1. constructor는 생성자 함수 그 자체를 가리킴
2. prototype은 생성자 함수에 정의한 모든 객체가 공유할 원형
3. `__proto__`는 생성자 함수를 new로 호출할 때, 정의해두었던 prototype을 참조한 객체
4. prototype은 생성자 함수에 사용자가 직접 넣는 거고, `__proto__`는 new를 호출할 때 prototype을 참조하여 자동으로 만들어짐
5. 생성자에는 prototype, 생성자로부터 만들어진 객체에는 `__proto__`
6. 따라서 사용자는 prototype만 신경쓰면 된다. `__proto__`는 prototype이 제대로 구현되었는지 확인용으로 사용한다.

이 관계를 다시 정리하면

prototype과 constructor는 부모자식 관계라고 생각하면 된다. Person.prototype.constructor === Person; 이다.
또한 Person.prototype === (Person생성자로 만들어진 객체).\_\_proto\_\_; 이기 때문에 (Person생성자로 만들어진 객체).\_\_proto\_\_.constructor === Person; 도 성립한다.

사실 이 부분은 더욱 정확히 알아가야할 부분이다.

따라서 다른 링크로 좀더 보완해보겠다.

[http://insanehong.kr/post/javascript-prototype/](http://insanehong.kr/post/javascript-prototype/)

난 위 링크 사람보다 프로토타입에 대해 정밀하게 분석해본적이 없기 때문에, 링크를 이해한다면 프로토타입을 이해했다고 봐도 될 듯하다.

면접에서는
`프로토타입이 무엇인가?`
`프로토타입으로 선언된 객체와 new로 선언된 객체의 차이는 어떻게 되는가`

정도를 물어봤었는데, 아마 그 답이 될 것이다. 매우 어렵다.

나는 처음에는 대답 못했지만 지금이라면 이렇게 대답할 듯하다.

프로토타입이란, 객체의 원형을 이용해 새로운 객체를 만들어내는 기법이다.

new로 선언된 객체는 생성자를 이용해 생성된 객체이고, prototype으로 선언된 객체는 해당 객체의 원형인 prototype에 선언되어진 객체로, 동일한 생성자를 가진 객체들이 모두 공유하게 된다.

이 다음에도 웹과 nodejs, javascript의 면접중 받은 질문을 계속해서 진행해보겠다.
