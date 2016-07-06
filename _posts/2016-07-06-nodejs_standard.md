---
layout: post
title:  "[node js] Node js 기초 다지기"
date:   2016-07-06 15:30:53 +0900
categories: Nodejs
tags: [node js, node, standard, 기초]

---

# Node js

![computer](https://images.unsplash.com/photo-1452601395039-3184bc03cb09?ixlib=rb-0.3.5&q=80&fm=jpg&crop=entropy&s=19b13f692c4fcbe1b881106650982b03)

예전에 `node js로 크롤링하는 법`을 다룬 적이 있다.
그 때 당시에는 기초적인 문법은 다루지 말고, 사람들이 궁금해 하거나 내가 알고 싶어서 찾아봤던 것들을 가지고 적어보자라는 의견이였는데, 하다보니 기초가 역시나 중요하구나 라는 생각이 들었다.
난 처음에 어떻게 배웠을까를 생각해 보다가 그럼 Node js는 내가 어떻게 시작했었는지를 알아보는게 낫겠다는 생각을 했다.
node js는 결국 `javascript` 이기 때문에 javascript의 특징을 공부하는 것이 가장 좋다.
개인적으로는 웹 프론트에서 사용하는 javascript보다 서버쪽에서 사용하는 것을 먼저 했는데, 당시 아무것도 모를때라 같은 언어지만 다르게 사용하겠지? 라는 생각이였지만 맞기도 하고 틀리기도 하다. 언어적인 성격은 같지만 일반 브라우져에서 사용하는 것과는 분명 차이가 있다.

그럼 기초를 한번 공부해 보자.

---

### Node js

node js를 만든 사람은 node js를 뭐라고 말하는 지 한번 보자.

`Node.js® is a JavaScript runtime built on Chrome's V8 JavaScript engine. Node.js uses an event-driven, non-blocking I/O model that makes it lightweight and efficient. Node.js' package ecosystem, npm, is the largest ecosystem of open source libraries in the world.`

`Node.js®는 Chrome V8 JavaScript 엔진으로 빌드된 JavaScript 런타임입니다. Node.js는 이벤트 기반, 논 블로킹 I/O 모델을 사용해 가볍고 효율적입니다. Node.js의 패키지 생태계인 npm은 세계에서 가장 큰 오픈 소스 라이브러리 생태계이기도 합니다.`

하나는 실제 사이트에서 가져온 문구이고, 밑의 문구는 한글문구이다.
결국 V8 엔진을 이용한 javascript 서버 체계이다. (V8은 까보면 C++로 이루어져 있는 것으로 알고있다.)

가장 중요한 것은 `이벤트 기반`이라는 것과 `비동기 방식`이라는 것이다.
그리고 무엇보다 javascript이기 때문에 브라우져에서 javascript를 사용하던 사람들도 쉽게 접근할 수 있다.

배울 때 `express` 프레임워크를 사용해 배우면 사실 서버 만들기가 정말 간단하다.
그러나 프레임워크를 사용할 때는 내부가 어떻게 구현되는 지 알고 사용하는게 좋다. 물론 당장은 알기 힘들겠지만 하나하나 차근히 해보자.
이제 부터는 node js를 바로 들어가기보다 성격들과 기본적인 언어 사용법부터 시작하겠다.
따로 설치법은 워낙 많으니 적지는 않겠다. 간단히 설치를 하고 js 파일들을 node로 실행을 하는 방식으로 하겠다.


---

### Array

`Array` 는 C 기반 언어들을 사용해본 사람이라면 다들 알고 있는 것이다.
그럼 javascript에서의 간단한 Array를 예제로 보고 가자.

{% highlight ruby %}

var cars = ['Mercedes', 'Volvo', 'BMW'];

cars.push('poli');
// [ 'Mercedes', 'Volvo', 'BMW', 'Poli' ]
console.log(cars);

cars[4] =  'Hyundai';
// [ 'Mercedes', 'Volvo', 'BMW', 'Poli', 'Hyundai' ]
console.log(cars);

cars.splice(3,1);
// [ 'Mercedes', 'Volvo', 'BMW', 'Hyundai' ]
console.log(cars);

cars.pop();
// [ 'Mercedes', 'Volvo', 'BMW' ]
console.log(cars);

cars[1] = 'Porche';
// [ 'Mercedes', 'Porche', 'BMW' ]
console.log(cars);

cars.sort();
// [ 'BMW', 'Mercedes', 'Porche' ]
console.log(cars);

cars.sort(function(a, b) {
   return a.length < b.length; //true/ false 값으로 순서 조절.
});
// [ 'Mercedes', 'Porche', 'BMW' ]
console.log(cars);

var cars2 = cars.concat(['Audi', 'Toyota']);
// [ 'Mercedes', 'Porche', 'BMW', 'Audi', 'Toyota' ]
console.log(cars2);

var germanCars = cars2.slice(0,4);
// [ 'Mercedes', 'Porche', 'BMW', 'Audi' ]
console.log(germanCars);

cars2.splice(3, 2);
// [ 'Mercedes', 'Porche', 'BMW' ]
console.log(cars2);

{% endhighlight %}

기본 예시들이다. 하나하나 알아가 보자.

`cars`라는 변수에 배열을 선언했다.
먼저 `push`이다 다들 알다시피 배열에 값을 추가해준다. (제일 뒤의 index로 추가 된다.)
물론 해당 index를 안다면 직접 입력해주어도 된다.
`splice`자체는 index,길이로써 원하는 값을 도출해준다. 도출을 하게 된다면 해당 배열에서 사라진다는 것을 볼 수 있다. **string에서와 다르다.**
해당 예시도 확인해 볼 수 있다.
`pop`은 제일 뒤의 값을 삭제한다.
`sort`는 보다시피 제일 선두의 알파벳순으로 정렬이 기본이다. 그러나 함수를 만들어 원하는 sort를 해줄 수도 있다.
`concat`은 배열의 연결임을 확인 할 수 있다.

---

### closure

`closure`개념은 사실 처음 보는 사람도 있을 것이라 생각한다. 깊게 들어간다면 상당히 까다로울 때도 있다. 지금은 간단히 보여주겠지만 추후에 javascript에 대해 한번더 적게 된다면 좀더 자세하게 적는 시간이 있을 것이다.

{% highlight ruby %}

function add(i,j,handler){
	var ret = i + j;
	handler(ret);
}

add(1, 2, function(val){
	console.log('1 + 2 = ' + val);
});

function showConsole(ret){
	console.log('Result = ', ret);
}

add(1,2,showConsole);

{% endhighlight %}

다음이 클로져의 기본적인 모습이다.

`handler`라는 함수를 함수의 파라미터로 넣어주는 것을 볼 수 있다.
다음과 같이 한다면 handler에 어떤 함수를 넣어주냐에 따라 도출되는 값이 달라지는 것을 알 수 있다.

조금 다르게 보도록 하자.

{% highlight ruby %}

unction wrapValue(n) {
var localVariable = n;
return function() {
        return localVariable;
    };
}

var wrap1 = wrapValue(1);
var wrap2 = wrapValue(2);
console.log(wrap1()); // . 1
console.log(wrap2()); // . 2

{% endhighlight %}

다음 예시가 있다 할때, parameter를 달리 주면 내부의 로컬변수가 변경되어 출력됨을 볼 수 있다. 즉, `함수의 인스턴스들이 선언때 마다 따로 저장됨을 볼 수 있는 것이다.`

{% highlight ruby %}

function multiplier(factor) {
return function(number) {
    return number * factor;
    };
}

var twice = multiplier(2);
console.log(twice(5)); // . 10

{% endhighlight %}

다음과 같은 예시도 있다.

마치 `twice`라는 변수에 `multiplier(2)` 라는 인스턴스가 저장되고 해당 사항에 있어서 값이 저장되 있음을 볼 수 있다.

추가 예시는 다음을 들 수 있다.

{% highlight ruby %}

var arr = [1,2,3,4,5,6,7,8,9,10];
var generateFilter = function(x){
    return function(n) { return n%x == 0;};
}

var filter2x = generateFilter(2);
var filter3x = generateFilter(3);

generateFilter = null;

arr.filter(filter2x); //[2,4,6,8,10]
arr.filter(filter3x); //[3,6,9]

{% endhighlight %}

다음과 같이 원 함수가 null이 되더라도 각각이 인스턴스를 따로 저장하구나라는 것을 느낄 수 있다.

이를 이용하면 `getter` `setter` 도 구현이 될 것이고 재밌는 활용이 가능 하다.

즉, 클로져는 외부함수에 접근하는 내부함수를 구현하는 것인데, `scope chain`을 이해할 수 있을 것이다.

---

### exception

예외처리는 다들 기본적으로 아는 `try catch`만 에시를 들고 넘어가도록 하겠다.

{% highlight ruby %}

var value;
try{
	console.log(value.length);
}
catch(err){
	console.log('Error : ', err.message);
}
finally{
	console.log('Finally!');
}

{% endhighlight %}


---

### filter

배열에서 사용하는 `filter`가 있다.
내가 원하는 filter를 구현함으로서 배열에 적용시킬 수 있다.

{% highlight ruby %}

var array = [-1,1,3,-2,2];

var filtered = array.filter(function(item){
	if(item < 0)
		return item;
});
var filtered2 = array.filter(function(item){
	if(item >= 0)
		return item;
});

var result = filtered.concat(filtered2);
console.log(result);

{% endhighlight %}

---

### function

지금까지 함수를 자연스럽게 썼기 때문에 따로 적어야 할지 모르겠지만, 자바스크립트에서 함수는 매우 중요하기 때문에 적는 것이 좋을 듯하다.
먼저 기본 예시부터 들겠다.

{% highlight ruby %}

function add(i, j){
	return i+j;
}

console.log('1 + 2 = ', add(1,2));

var minus = function(i,j){
	return i = j;
}

console.log('2 - 1 = ', minus(2,1));

function circle(radius){
var pi = 3.14;

function area (r){
	return r*r*pi;
}
return area(radius);
}

var ret = circle(3);
console.log('circle(3) = ', ret);

//Error
//undefinedFunction();

{% endhighlight %}

보자면 `closure`를 사용한 `circle`까지 있다.

함수라는 것에 좀더 구체적인 설명을 하자면,

일반적으로 언어라 하면 `voca`라는 것이 있다. 프로그래밍언어도 마찬가지고 voca가 있는데, 함수는 내가 사용하는 voca를 만든다고 보면 간단히 이해 할 수 있다.

{% highlight ruby %}

1. function declaration (함수 선언)
function factorial(x){
    if(x <= 1)
    return 1;

    return x * factorial(x-1);
}

2. function 생성자
var factorial = new Function("x",
    "if (x<=1) return 1;"
    \+ "return x * factorial(x - 1);"
);

3. function literal (함수 리터럴) * 가장 많이 씀
var square = function(x) {
    return x * x;
}

{% endhighlight %}

세가지 선언법이 있는데 일반적으로 3번을 가장 많이 쓴다. 그 이유는 간단하면서도 `호이스팅`이 방지되기 때문이다.

호이스팅이라 함은 변수를 어떻게 적냐에 따라(정의에 따라) 선언과 할당에 있어서 나눠지는 것을 말하는데, 예를 들어 보자.

{% highlight ruby %}

var A;

function A(){
	return "A function";
}

var B = "B var";

function B(){
	return "B function"
}

var C;

var C = function(){
	return "C function";
}

var D = "D var";

var D = function(){
	return "D function";
}

console.log(A,B,C,D);

{% endhighlight %}

자 여기서 중요한 것은 **B**이다.
A,C,D는 함수라고 선언이 될 것이다.
그러나 B는 호이스팅에 의해 함수가 아니라 변수라고 생각이 되고 `B var`가 출력되는 현상이 생긴다.
변수라고 선언되어 있는 것은 javascript에서 먼저 선언을 한다. 따라서 B가 문제가 생기는 것이다.

---

### object

객체라 함은 참 재밌다. 한 때 학교에서 java수업을 들을 때 교수님이 object는 세상 모든 물질이라고 설명을 했었다.
그 물질에 대한 `property`도 넣을 수 있고, 만듦에 따라서 성격이 나눠진다.

{% highlight ruby %}

var iu = {
	name : 'IU',
	phone : '010-1234-5678'
};

// property access
console.log(iu.name);
console.log(iu['phone']);

//class
function Singer(name){
	this.name = name;
}

var taeyon = new Singer('태연');
taeyon.phone = '010-1357-2468';

console.log(taeyon.name);
console.log(taeyon['phone']);

//Prototype
Singer.prototype.sing = function(){
	console.log('노래 부르기');
}

// constructor

var hani = new Singer('하니');

// Delete property
hani.charactor = '털털';
console.log(hani);
delete hani.charactor;
console.log(hani);
//없는 프로퍼티 접근
console.log(hani.charactor);

taeyon.sing();
hani.sing();

//새로운 클래스
function Actor(name){
	this.name = name;
}

var hyoju = new Actor('한효주');

console.log(iu.constructor);//object로 만든 것은 따로 소속이 나오지 않는다.
console.log(taeyon.constructor);
console.log(hani.constructor);
console.log(hyoju.constructor);

if(taeyon.constructor == hani.constructor){
	console.log('Singer.constructor == Singer.constructor');
}

if( hani.constructor == hyoju.constructor){
	console.log('Singer.constructor == Actor.constructor');
}

{% endhighlight %}

위 예시는 `prototype` 과 `constructor`까지 넣어두었다.
`prototype`을 제대로 알려면 사실 이정도의 예시를 가지고는 힘들다.
그건 추후 javascript에서 다루도록 하고, 여기에서는 `instance`들이 prototype으로 설정된 `sing`이라는 함수를 모두 상속받는 것을 볼 수 있다.

---

![photo](https://images.unsplash.com/photo-1445539962947-a7199602bd79?ixlib=rb-0.3.5&q=80&fm=jpg&crop=entropy&s=12d9298596ca12ec28f75a05283f4de8)

### overloading

답부터 말하자면 overloading은 되지 않는다. (overloading이 되도록 만들 수는 있다.)
예시를 보자.

{% highlight ruby %}

function add(i, j, k){
	return i + j + k;
}

function add(i,j){
	return i + j;
}

console.log(add(1));
console.log(add(1,2));
console.log(add(1,2,3));

function MyClass(){
	this.sayHello = function(){
		console.log('Hello');
	}

	this.sayHello = function(who){
		console.log('How are you ' + who);
	}
}

var obj = new MyClass();
obj.sayHello();
obj.sayHello('IU');
//overloading이 되지 않기 때문에, 값이 들어갈 때 마지막으로 지정해준 함수가 덮어 씌움.

{% endhighlight %}

위 코드에서 제대로 나오는 값은 많이 없다.

{% highlight ruby %}

NaN
3
3
How are you undefined
How are you IU

{% endhighlight %}

위와 같이 나오는데 주석으로 된 설명처럼 덮어 씌움을 볼 수 있다.

---

### typeOf

`typeof` 는 javascript에서 상당히 조심히 사용해야한다. 그래서 코드상에 꼭 필요한 부분 아니면 typeOf를 쓰지 않는 것이 좋다는 말도 들은 적이 있는데, 일단 기본 예시를 보자.

{% highlight ruby %}

var num = 123;

console.log(typeof num);
if( typeof num == 'number'){
	console.log(num + ' is number');
}

//string
var str = '123';

console.log(typeof str);
if ( typeof str == 'string'){
	console.log(str + ' is string');
}

//Object
var obj = {
	name : 'IU'
};

console.log(typeof obj);
if ( typeof obj == 'object'){
	console.log(obj + ' is object');
	//문자열로 찍으면 object Object로 나오고, 그냥 찍으면 object 값들 그대로 나옴.
}

var Singer = function(name) {
	this.name = name;
}

var iu = new Singer('IU');
console.log(typeof iu);


//Function
function add(i,j){
	return i + j;
}

console.log(typeof add);
if ( typeof add == 'function') {
	console.log(add + ' is function');//찍으면 add 함수 자체가 나온다. 즉 text형식으로 저장해두고 해석을 하는 것.
}

{% endhighlight %}

기본 예시를 보면 크게 이상할 부분이 없어 보인다.

그러나 다음을 한번 보자.

{% highlight ruby %}

var A = null;
var B = undefined;

console.log(typeof A);
console.log(typeof B);

{% endhighlight %}

여기서 `null`의 type은 무엇일까??
놀랍게도 **object**가 나온다.

이러한 형태의 예외가 (특히 null) 있기 때문에, typeof를 잘 안쓰는 경향이 있다고 한다.
물론 당연히 잘 쓰면 더 좋다.

---

### undefined

`undefined`와 `null`은 확실히 다르다.
선언에 있어서의 차이인데 `값 할당`의 차이라고 볼 수 있다.
선언이 되지 않았거나 선언에 값 할당이 안되어 있을 경우가 undefined이다.

다음을 보자.

{% highlight ruby %}

console.log(' var x');
var x;

if(x) {
	console.log('if (x)');
}

if (x == undefined){
	console.log('if ( x == undefined )');
}

if ( x == 'undefined') {
	console.log('if x == "undefined" )');
}

if( x === undefined) {
	console.log('if ( x === undefined )');
}

if( x == null) {
	console.log('if ( x == null )');
}

console.log('var y = null;');
var y = null;

if (!y){
	console.log('if ( !y )');
}

if ( y == null) {
	console.log ('if ( y == null )');
}

if ( y == undefined ) {
	console.log ( 'if ( y == undefined )');
}

{% endhighlight %}

따라서 연산자 `===`는 `==`과의 차이랄 야기 함으로 잘 쓸수 있도록 해야 한다.

---

### 마치며

이번에는 사실 node js 라기 보다 javascript의 성질에 관한 얘기가 대부분이 였다. 다음 포스팅 부터는 제대로 서버부터 만들어보고 시작하도록 해보겠다.






