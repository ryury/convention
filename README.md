[TOC]


## 코드 서식(Code formatting)

### 블록(Blocks)

if/while/do/for 문은 한 줄짜리 블록 일 경우 {}를 생략할 수 있다.
하지만 이런 패턴은 코드 구조를 애매하게 만들어 가독성이 떨어지고, 문법적 오류가 아니기 때문에 디버깅이 어렵다.
이런 코드는 이후 오류 발생 확률이 높은 잠재적 위험 요소가 된다.

> 안티패턴 : 반드시 {}로 블록을 명확하게 만든다.

- if/for/while/try 등 조건문은 중괄호({})를 사용하세요.

~~~js
// bad
if (condition) doSomething();

// good
if (condition) {
	doSomething();
}
~~~
~~~js
// bad
if (condition) doSomething();
else doAnything();
// good
if (condition) {
	doSomething();
} else {
	doAnything();
}
~~~
~~~js
// bad
for (var i = 0; i < lists.length; i++) someIterativeFn();

// good
for (var i = 0; i < lists.length; i++) {
	someIterativeFn();
}

// better(1)
var i,
	len = list.length;
for (i = 0; i < len; i++) {
	someIterativeFn();
}
// better(2)
var i = 0,
	len = list.length;
for (; i < len; i++) {
	someIterativeFn();
}
~~~

- 복수행 블록은 중괄호({})를 사용하십시요.

~~~js
// bad
if (test)
  return false;

// good
if (test) {
  return false;
}
~~~

- 여러 블록에 걸친 if와 else를 사용하는 경우, else는 if블록의 끝 중괄호{}와 같은 행에 두세요.

~~~js
// bad
if (test) {
  thing1();
  thing2();
}
else {
  thing3();
}

// good
if (test) {
  thing1();
  thing2();
} else {
  thing3();
}
~~~

### 주석(Comments)

- 복수행의 주석은 `/**...*/`를 사용하세요. 그 안에는 모든 매개 변수와 반환 값에 대한 형식과 값을 표기합니다.

~~~js
// bad
// make() returns a new element
// based on the passed in tag name
//
// @param <String> tag
// @return <Element> element
function make(tag) {
  // ...stuff...
  return element;
}

// good
/**
 * make() returns a new element
 * based on the passed in tag name
 *
 * @param <String> tag
 * @return <Element> element
 */
function make(tag) {
  // ...stuff...
  return element;
}
~~~

- 한 줄 주석에는 `//`를 사용하세요. 주석은 코드의 상단에 작성하세요. 또한 주석 앞에 빈 줄을 넣어주세요.

~~~js
// bad
var active = true;  // is current tab

// good
// is current tab
var active = true;

// bad
function getType() {
  console.log('fetching type...');
  // set the default type to 'no type'
  var type = this._type || 'no type';
  return type;
}

// good
function getType() {
  console.log('fetching type...');
  // set the default type to 'no type'
  var type = this._type || 'no type';
  return type;
}
~~~

- 문구를 지적하고 재고를 촉구하거나 문제의 해결책을 제시하는 경우 등에는 FIXME 또는 TODO를 붙이는 것으로 다른 개발자의 빠른 이해를 도울 수 있습니다.
이들은 어떠한 액션을 따른다는 의미에서 일반 주석과 다를 수 있습니다.
액션은 `FIXME:` 해결책 필요 또는 `TODO:` 구현 필요 입니다.

~~~js
function Calculator() {
  // FIXME: 전역 변수를 사용해서는 안됩니다.
  total = 0;
  return this;
}

function Calculator() {
  // TODO: total은 옵션 매개 변수로 설정되어야 함.
  this.total = 0;
  return this;
}
~~~

### 공백(Whitespace)

- 들여쓰기는 space와 tab을 섞어서 사용하지 마십시요. 프로젝트를 시작할 때 반드시 space와 tab둘 중 하나를 선택하고 space를 사용할 경우 2문자 또는 4문자를 사용하십시요.

~~~js
// bad
function() {
∙∙var name;
--name = 'foo';
}

// bad
function() {
∙var name;
}

// good
function() {
∙∙var name;
}
~~~

- 중괄호{} 앞에 공백을 넣어주세요.

~~~js
// bad
function test(){
  console.log('test');
}

// good
function test() {
  console.log('test');
}

// bad
dog.set('attr',{
  age: '1 year',
  breed: 'Bernese Mountain Dog'
});

// good
dog.set('attr', {
  age: '1 year',
  breed: 'Bernese Mountain Dog'
});
~~~

- 제어 구문(if, while 등)의 괄호() 앞에 공백을 넣어주세요. 함수 선언과 함수 호출시 인수 목록 앞에는 공백을 넣지 않습니다.

~~~js
// bad
if(isJedi) {
  fight ();
}

// good
if (isJedi) {
  fight();
}

// bad
function fight () {
  console.log ('Swooosh!');
}

// good
function fight() {
  console.log('Swooosh!');
}
~~~

- 연산자 사이에는 공백을 넣어주세요.

~~~js
// bad
const x=y+5;

// good
const x = y + 5;
~~~

- 파일의 마지막에 빈 줄을 하나 넣어주세요.
[파일 끝에 개행을 추가해야 하는 이유](http://blog.coderifleman.com/2015/04/04/text-files-end-with-a-newline/)

~~~js
// bad
(function (global) {
  // ...stuff...
})(this);

// bad
(function (global) {
  // ...stuff...
})(this);↵
↵

// good
(function (global) {
  // ...stuff...
})(this);↵
~~~

- 메소드 체인이 길어지는 경우 적절히 들여쓰기(indentation)하세요. 행이 메소드 호출이 아닌 새로운 문장임을 강조하기 위해 선두에 도트(.)를 배치하세요.

~~~js
// bad
$('#items').find('.selected').highlight().end().find('.open').updateCount();
// good
$('#items')
  .find('.selected')
    .highlight()
    .end()
  .find('.open')
    .updateCount();
~~~

### 쉼표(Commas)

- 쉼표로 시작하지 마세요.

~~~js
// bad
var once
  , upon
  , aTime;

// good
var once,
    upon,
    aTime;


// bad
var hero = {
    firstName: 'Bob'
  , lastName: 'Parr'
  , heroName: 'Mr. Incredible'
  , superPower: 'strength'
};


// good
var hero = {
  firstName: 'Bob',
  lastName: 'Parr',
  heroName: 'Mr. Incredible',
  superPower: 'strength'
};
~~~

### 세미콜론(Semicolons)

자바스크립트에서 문장은 세미콜론(;)으로 끝나야 하지만, 문법적으로 이를 강제하지 않기 때문에 생략할 수 있다.
이는 자바스크립트 파서가 이를 자동으로 삽입해주기 때문이다.
하지만 이런 세미콜론(;) 자동 삽입은 종종 의도하지 않았던 코드(전혀 다른 코드)로 해석되어 생각하지 못한 오류를 만들고 디버깅을 어렵게 한다.
또한 자바스크립트 파서가 세미콜론(;)의 위치를 계산하고 삽입하데 추가적인 비용이 발생한다.

- 문장의 종료에는 반드시 세미콜론(;)을 사용하세요.

~~~js
// bad
(function() {
  var name = 'Skywalker'
  return name
})()
// good
(function() {
  var name = 'Skywalker';
  return name;
})();
// good
;(function() {
  var name = 'Skywalker';
  return name;
})();
~~~

## 명명 규칙(Naming Conventions)

### 변수, 함수, 객체

- 하나의 문자로 구성된 이름은 피하세요. 이름에서 의도를 읽을 수 있도록 해야 합니다.

~~~js
// bad
function q() {
  // ...stuff...
}

// good
function query() {
  // ..stuff..
}
~~~

- 객체, 함수 인스턴스에는 camelCase(소문자로 시작)를 사용하세요.

~~~js
// bad
var OBJEcttsssss = {};
var this_is_my_object = {};
var this-is-my-object = {};
function c() {};
var u = new user({
  name: 'Bob Parr'
});

// good
var thisIsMyObject = {};
function thisIsMyFunction() {};
var user = new User({
  name: 'Bob Parr'
});
~~~

- 클래스와 생성자는 PascalCase(대문자로 시작)를 사용하세요.

~~~js
// bad
function user(options) {
  this.name = options.name;
}

var bad = new user({
  name: 'nope'
});

// good
function User(options) {
  this.name = options.name;
}
var good = new User({
  name: 'yup'
});
~~~

- private 속성 이름은 밑줄 _ 을 사용하십시오.

~~~js
// bad
this.__firstName__ = 'Panda';
this.firstName_ = 'Panda';

// good
this._firstName = 'Panda';
~~~

- this의 참조를 저장할 때 _this 를 사용하십시오.

~~~js
// bad
function() {
  var self = this;
  return function() {
    console.log(self);
  };
}

// bad
function() {
  var that = this;
  return function() {
    console.log(that);
  };
}

// good
function() {
  var _this = this;
  return function() {
    console.log(_this);
  };
}
~~~

### 접근자(Accessors)

- 접근자 함수가 필요한 경우 getVal() 이나 setVal('hello') 라고 사용합니다.

~~~js
// bad
dragon.age();

// good
dragon.getAge();

// bad
dragon.age(25);

// good
dragon.setAge(25);
~~~

- 속성이 boolean의 경우 isVal() 이나 hasVal() 라고 사용합니다.

~~~js
// bad
if (!dragon.age()) {
  return false;
}

// good
if (!dragon.hasAge()) {
  return false;
}
~~~

- 일관된다면 get() 이나 set() 이라는 함수를 작성해도 좋습니다.

~~~js
function Jedi(options) {
  options || (options = {});
  var lightsaber = options.lightsaber || 'blue';
  this.set('lightsaber', lightsaber);
}

Jedi.prototype.set = function(key, val) {
  this[key] = val;
};
Jedi.prototype.get = function(key) {
  return this[key];
};
~~~

### 생성자(constructors)

- 새 Object에서 프로토타입을 재정의하는 것이 아니라, 프로토타입 객체에 메서드를 추가해 주십시오.
프로토타입을 재정의하면 상속이 불가능합니다. 프로토타입을 리셋하는것으로 베이스 클래스를 재정의 할 수 있습니다.

~~~js
function Jedi() {
  console.log('new jedi');
}

// bad
Jedi.prototype = {
  fight: function fight() {
    console.log('fighting');
  },
  block: function block() {
    console.log('blocking');
  }
};

// good
Jedi.prototype.fight = function fight() {
  console.log('fighting');
};
Jedi.prototype.block = function block() {
  console.log('blocking');
};
~~~

- 메소드의 반환 값으로 this를 반환함으로써 메소드 체인을 할 수 있습니다.

~~~js
// bad
Jedi.prototype.jump = function() {
  this.jumping = true;
  return true;
};
Jedi.prototype.setHeight = function(height) {
  this.height = height;
};

var luke = new Jedi();
luke.jump(); // => true
luke.setHeight(20) // => undefined

// good
Jedi.prototype.jump = function() {
  this.jumping = true;
  return this;
};
Jedi.prototype.setHeight = function(height) {
  this.height = height;
  return this;
};

var luke = new Jedi();
luke.jump()
  .setHeight(20);
~~~

## 선언과 할당

### 변수(Variables)

- 변수를 선언할 때는 항상 var를 사용하세요.

> var 키워드 없이 선언된 변수는 전역으로 처리된다.
> 실수로 "var"를 사용하지 않았더라도 에러 없이 변수를 사용할 수 있지만,
> 이로 인해 전역 환경이 오염되고, 때때로 매우 찾아내기 어려운 버그를 만들어 낸다.

~~~js
// bad
superPower = new SuperPower();

// good
var superPower = new SuperPower();
~~~

- 여러 변수를 선언하려면 하나의 var를 사용하여 변수마다 줄바꿈하여 선언하세요.

~~~js
// bad
var items = getItems();
var goSportsTeam = true;
var dragonball = 'z';

// good
var items = getItems(),
    goSportsTeam = true,
    dragonball = 'z';
~~~

- 정의되지 않은 변수를 마지막으로 선언하세요.

> 나중에 변수를 정의할 때 유용합니다.

~~~js
// bad
var i, len, dragonball,
    items = getItems(),
    goSportsTeam = true;

// bad
var i, items = getItems(),
    dragonball,
    goSportsTeam = true,
    len;

// good
var items = getItems(),
    goSportsTeam = true,
    dragonball,
    length,
    i;
~~~

- 변수의 할당은 스코프의 시작 부분에서 해주십시오.

> 이것은 변수 선언과 Hoisting 관련 문제를 해결합니다.

~~~js
// bad
function() {
  test();
  console.log('doing stuff..');
  //..other stuff..
  var name = getName();
  if (name === 'test') {
    return false;
  }
  return name;
}

// good
function() {
  var name = getName();
  test();
  console.log('doing stuff..');
  //..other stuff..
  if (name === 'test') {
    return false;
  }
  return name;
}

// bad
function() {
  var name = getName();
  if (!arguments.length) {
    return false;
  }
  return true;
}

// good
function() {
  if (!arguments.length) {
    return false;
  }
  var name = getName();
  return true;
}
~~~

### 문자열(Strings)

- 문자열은 작은 따옴표''를 사용하십시오.

~~~js
// bad
var name = "Bob Parr";

// good
var name = 'Bob Parr';

// bad
var fullName = "Bob " + this.lastName;

// good
var fullName = 'Bob ' + this.lastName;
~~~

- 긴 문자열을 연결할 경우 여러 줄에 걸쳐 기술 할 필요가 있습니다.

~~~js
// bad
var errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';

// bad
var errorMessage = 'This is a super long error that \
was thrown because of Batman. \
When you stop to think about \
how Batman had anything to do \
with this, you would get nowhere \
fast.';

// good
var errorMessage = 'This is a super long error that ' +
  'was thrown because of Batman.' +
  'When you stop to think about ' +
  'how Batman had anything to do ' +
  'with this, you would get nowhere ' +
  'fast.';
~~~

- 태그와 문자열을 결합할 경우 Array#join을 사용하세요. [jsPert](http://jsperf.com/string-vs-array-concat/2)

### 함수(Functions)

- 함수 표현식(Function expresstions)

~~~js
// 익명 함수표현식(anonymous function expression)
var anonymous = function() {
  return true;
};

// 기명 함수표현식(named function expression)
var named = function named() {
  return true;
};

// 익명 즉시실행 함수표현식(immediately-invoked function expression (IIFE))
// Crockford doesn't like parens on the IIFE's outside
// (function(){ ... })()
// because they "look like dog balls"
// https://www.youtube.com/watch?v=taaEzHI9xyY
(function() {
  console.log('Welcome to the Internet. Please follow me.');
}());
~~~

- 블록(if, while 등)내에서 함수 선언문(Function Declarations)을 사용하지 마십시요.

~~~js
// bad
if (currentUser) {
  function test() {
    console.log('Nope.');
  }
}

// good
if (currentUser) {
  var test = function() {
    console.log('Yup.');
  };
}
~~~

- 매개 변수(parameter)에 arguments를 절대로 지정하지 마십시요.

> 함수 영역으로 전달 될 arguments 객체의 참조를 덮어 쓸 수 있게 됩니다.

~~~js
// bad
function nope(name, options, arguments) {
  // ...stuff...
}

// good
function yup(name, options, args) {
  // ...stuff...
}
~~~

### 호이스팅(Hoisting)

- 해당 스코프의 시작 부분에 Hoist된 변수 선언은 할당되지 않습니다.

~~~js
// (notDefined가 전역 변수에 존재하지 않는다고 가정했을 경우)
// 이것은 동작하지 않습니다.
function example() {
  console.log(notDefined); // => throws a ReferenceError
}

// 그 변수를 참조하는 코드 후에 그 변수를 선언한 경우
// 변수가 Hoist된 상태에서 작동합니다.
// Note : true라는 값 자체는 Hoist되지 않습니다.
function example() {
  console.log(declaredButNotAssigned); // => undefined
  var declaredButNotAssigned = true;
}

// 인터 프린터는 변수 선언을 스코프의 시작 부분에 Hoist합니다.
// 위의 예는 다음과 같이 다시 작성할 수 있습니다.
function example() {
  var declaredButNotAssigned;
  console.log(declaredButNotAssigned); // => undefined
  declaredButNotAssigned = true;
}
~~~

- 익명 함수표현식에서는 함수가 할당되기 전에 변수가 Hoist될 수 있습니다.

~~~js
function example() {
  console.log(anonymous); // => undefined
  anonymous(); // => TypeError anonymous is not a function
  var anonymous = function() {
    console.log('anonymous function expression');
  };
}
~~~

- 기명 함수표현식의 경우도 변수가 Hoist될 수 있습니다. 함수 이름과 함수 본체는 Hoist되지 않습니다.

~~~js
function example() {
  console.log(named); // => undefined
  named(); // => TypeError named is not a function
  superPower(); // => ReferenceError superPower is not defined
  var named = function superPower() {
    console.log('Flying');
  };
}

// 함수이름과 변수이름이 같은 경우에도 같은 일이 일어납니다.
function example() {
  console.log(named); // => undefined
  named(); // => TypeError named is not a function
  var named = function named() {
    console.log('named');
  }
}
~~~

- 함수 선언은 함수이름과 함수본문이 Hoist됩니다.

~~~js
function example() {
  superPower(); // => Flying
  function superPower() {
    console.log('Flying');
  }
}
~~~

- 더 자세한 정보는 [Ben Cherry](http://www.adequatelygood.com/)의 [JavaScript Scoping & Hoisting](http://www.adequatelygood.com/2010/2/JavaScript-Scoping-and-Hoisting)를 참조하십시오.


### 배열(Arrays)

- 배열을 만들 때 리터럴 구문을 사용하세요.

~~~js
// bad
var items = new Array();

// good
var items = [];
~~~

- 배열에 항목을 직접 대체하지 말고 Array#push를 사용하세요.

~~~js
var someStack = [];

// bad
someStack[someStack.length] = 'abracadabra';

// good
someStack.push('abracadabra');
~~~

- 배열을 복사 할 필요가있는 경우 Array#slice를 사용하세요. [jsPerf](http://jsperf.com/converting-arguments-to-an-array/7)

~~~js
var items = [1, 2, 3, 4],
  len = items.length,
    itemsCopy = [],
    itemsCopy2 = [],
    i;

// bad
for (i = 0; i < len; i++) {
  itemsCopy[i] = items[i];
}
console.log(itemsCopy); // ==> [1, 2, 3, 4];

// good
itemsCopy2 = items.slice();
console.log(itemsCopy2); // ==> [1, 2, 3, 4];
~~~

- Array와 비슷한(Array-Like)한 Object를 Array로 변환하려면 Array#slice를 사용하세요.

~~~js
function foo() {
    var args = arguments;

    console.log(toString.call(args)); // ==> [object Object]
    args = Array.prototype.slice.call(arguments);
    console.log(toString.call(args)); // ==> [object Array]
}
~~~

### 객체(Objects)

- Object를 만들 때는 리터럴 구문을 사용하세요.

~~~js
// bad
var item = new Object();

// good
var item = {};
~~~

- [예약어(reserved words)](http://es5.github.io/#x7.6.1)를 키로 사용하지 마십시오.
- 예약어 대신 알기 쉬운 동의어(readable synonyms)를 사용하세요.

~~~js
// bad
var superman = {
  class: 'alien'
};

// bad
var superman = {
  klass: 'alien'
};

// good
var superman = {
  type: 'alien'
};
~~~

- 메서드 및 속성 정의(Method and property definitions)
new 키워드를 통해 생성된 객체에 메서드와 속성을 추가하는 방법은 여러가지가 있지만 아래와 같은 스타일이 선호되는 스타일입니다.

~~~js
// properties
/** @constructor */
function Foo() {
 this.bar = value;
}
// methods
Foo.prototype.bar = function() {
 /* ... */
};

var foo = new Foo();
~~~

### delete

- 객체 속성의 수를 변경하는 것은 값을 할당하는 것보다 훨씬 느립니다. key in obj의 결과값을 변경하는 경우가 아니면 가급적 delete 키워드의 사용은 피해주세요.

~~~js
// Prefer this.foo = null
Foo.prototype.dispose = function() {
  this.property_ = null;
};

// instead of
Foo.prototype.dispose = function() {
  delete this.property_;
};
~~~

### 속성(Properties)

- 속성에 접근하려면 도트(.)를 사용하세요.

~~~js
var luke = {
  jedi: true,
  age: 28
};

function getProp(prop) {
  return luke[prop];
}

var isJedi = getProp('jedi');
~~~

## 유형(Types)

### 조건식과 등가식(Conditional Expressions & Equality)

- 항등 연산자인 ==와 !=보다는 삼중 항등 연산자인 ===와 !===를 사용하세요.

> 자바스크립트는 두 값을 비교 또는 산술하기 전에 내부적으로 암묵적인 강제 형 변환이 실행된다.
> 따라서 암묵적인 강제 형 변환이 일어나지 않도록 상중 등호 연산자(===, !==)를 사용하는 것이 좋다.
> 만약 이형 데이터간 비교가 필요하다면 명시적으로 강제 형 변환 후 삼중 등호 연산자(=== 또는 !==)를 사용한다.

- if와 같은 조건문은 ToBoolean방법에 의한 강제 형(Type)변환으로 구분되고 항상 다음과 같은 간단한 규칙을 따릅니다.
	* Objects는 true로 구분됩니다.
	* Undefined는 false로 구분됩니다.
	* Null은 false로 구분됩니다.
	* Booleans은 boolean형의 값으로 구분됩니다.
	* Numbers는 true로 구분됩니다. 그러나, +0, -0, 또는 NaN인 경우 false로 구분됩니다.
	* Strings는 true로 구분됩니다. 그러나, 비어있는 ('')경우는 false로 구분됩니다.

~~~js
if ([0]) {
  // true
  // Array는 Object 이므로 true로 구분됩니다.
}
~~~

- 짧은 형식(Shortchuts)을 사용하세요

~~~js
// bad
if (name !== '') {
  // ...stuff...
}

// good
if (name) {
  // ...stuff...
}

// bad
if (collection.length > 0) {
  // ...stuff...
}

// good
if (collection.length) {
  // ...stuff...
}
~~~

- 더 자세한 내용은 여기를 참조하세요. [Truth Equality and JavaScript](http://javascriptweblog.wordpress.com/2011/02/07/truth-equality-and-javascript/#more-2108) by Angus Croll.


### 형변환과 강제(Type Casting & Coercion)

- 문의 시작 부분에서 형(Type)을 강제합니다.

~~~js
// bad
var totalScore = this.reviewScore + '';

// good
var totalScore = '' + this.reviewScore;

// bad
var totalScore = '' + this.reviewScore + ' total score';

// good
var totalScore = this.reviewScore + ' total score';
~~~

- 숫자형으로 변환하려면 parseInt를 사용하세요. 항상 형변환을 위한 기수(radix)를 인수로 전달하세요.

> 안티패턴 : 항상 두 번째 매개변수를 명시하여 오류를 사전에 예방한다.
> 10진수로 변환이 필요한 경우라면 Number()를 사용하는 것이 속도 측면에서 이득이다.

~~~js
var inputValue = '4';

// bad
var val = new Number(inputValue);

// bad
var val = +inputValue;

// bad
var val = inputValue >> 0;

// bad
var val = parseInt(inputValue);

// good
var val = Number(inputValue);

// good
var val = parseInt(inputValue, 10);
~~~

> **NOTE**
> Bitshift를 연산하면 항상 32-비트 단 정밀도로 돌려 주어집니다([source](http://es5.github.io/#x11.7)).
> 32-비트 이상의 값을 비트 이동하면 예상치 못한 행동을 일으킬 가능성이 있습니다.
> [Discussion](https://github.com/airbnb/javascript/issues/109). 부호있는 32-비트 정수의 최대 값은 2,147,483,647입니다:

~~~js
2147483647 >> 0 //=> 2147483647
2147483648 >> 0 //=> -2147483648
2147483649 >> 0 //=> -2147483647
~~~

##  이벤트(Events)

- (DOM 이벤트, Backbone 이벤트)처럼 자신의 이벤트 페이로드 값을 전달하려면 원시값 대신 해시인수를 전달합니다.
이렇게 하면 나중에 개발자가 이벤트에 관련된 모든 핸들러를 찾아 업데이트하지 않고 이벤트 탑재체(payloads)에 값을 추가할 수 있습니다.
예를 들면:

~~~js
// bad
$(this).trigger('listingUpdated', listing.id);

...

$(this).on('listingUpdated', function(e, listingId) {
  // do something with listingId
});
~~~

- 이쪽을 더 선호합니다.

~~~js
// good
$(this).trigger('listingUpdated', { listingId : listing.id });

...

$(this).on('listingUpdated', function(e, data) {
  // do something with data.listingId
});
~~~

## 모듈(Modules)

- 모듈의 시작은 ! 로 시작하십시오. 이것은 문말에 세미콜론을 넣는것을 잊은 모듈을 연결할때 런타임 오류가 발생하지 않기 때문입니다.
- 파일 이름은 camelCase를 사용하여 같은 이름의 폴더에 저장해주십시오. 또한 단독으로 공개할 경우 이름을 일치시켜주십시오.
- noConflict() 라는 명칭으로 (이름이 겹쳐 덮어 써지기 전의) 모듈을 반환하는 메서드를 추가해주십시오.
- 항상 모듈의 시작 부분에서 'use strict';를 선언해주십시오.

~~~js
// fancyInput/fancyInput.js
!function(global) {
  'use strict';
  var previousFancyInput = global.FancyInput;

  function FancyInput(options) {
    this.options = options || {};
  }

  FancyInput.noConflict = function noConflict() {
    global.FancyInput = previousFancyInput;
    return FancyInput;
  };

  global.FancyInput = FancyInput;
}(window);
~~~

## jQuery(jQuery)


- jQuery 객체 변수 앞에는 $로 구분합니다.

~~~js
// bad
var sidebar = $('.sidebar');

// good
var $sidebar = $('.sidebar');
~~~

- jQuery 쿼리결과를 캐시해주세요.

~~~js
// bad
function setSidebar() {
  $('.sidebar').hide();
  // ...stuff...
  $('.sidebar').css({
    'background-color': 'pink'
  });
}

// good
function setSidebar() {
  var $sidebar = $('.sidebar');

  $sidebar.hide();
  // ...stuff...
  $sidebar.css({
    'background-color': 'pink'
  });
}
~~~

- DOM 검색은 Cascading $('.sidebar ul') 이나 parent > child $('.sidebar > ul') 를 사용해주십시오. [jsPerf](http://jsperf.com/jquery-find-vs-context-sel/16)
- jQuery Object 검색은 범위가 있는 find를 사용해주십시오.

~~~js
// bad
$('ul', '.sidebar').hide();

// bad
$('.sidebar').find('ul').hide();

// good
$('.sidebar ul').hide();

// good
$('.sidebar > ul').hide();

// good
$sidebar.find('ul');
~~~
