# Chapter 7 : 스코프

```
    function f(x) {
        return x + 3;
    }
    f(5); // 8
    x; // ReferenceError: x is not defined
```

위에서 x는 함수 바디를 벗어나면 존재하지 않는 것처럼 보인다.

이런 경우 x의 스코프는 함수 f 라고 할 수 있다.

**스코프 = 범위, 해당 영역**이라고 이해하면 편하다.

변수와 상수 또한 만들기 전에는 존재하지 않는다. 즉, `let`이나 `const`로 선언 전에 스코프 안에 존재하지 않는다.

(`var`는 특수한 경우로 뒤에 설명한다.)

===========

## 7.1 스코프와 존재

아직 선언하지 않은 변수나 함수가 종료되면서 존재하지 않게 된 변수는 스코프 안에는 없지만 그 자체가 존재하지 않는다는 말은 아니다.

**스코프**는 프로그램의 실행 컨텍스트에서 현재 보이고 접근할 수 있는 식별자이고, **존재한다는 것**은 그 식별자가 메모리가 할당된 무언가를 가리키고 있다는 뜻이다.

존재하지 않는다고 해도 자바스크립트는 메모리를 바로 회수하지는 않고, 유지할 필요가 없다고 판단되는 경우 주기적으로 일어나는 [가비지 콜렉션(garbage collection)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Memory_Management) 프로세스에서 메모리를 회수한다.

## 7.2 정적 스코프와 동적 스코프

```
    const x = 3;
    function f() {
         console.log(x);
         console.log(y);
    }
    { // 새 스코프
        const y = 5;
        f();
    }
```

정적 스코프 = **함수를 작성(선언)하는 시점**에서 스코프의 범위가 정해진다.

동적 스코프 = **함수를 호출하는 시점**에서 스코프의 범위가 정해진다.

y는 함수 f가 작성되기 전에는 스코프에 해당하지 않고, 함수 f가 호출되는 시점의 스코프에는 존재한다.

함수 f가 정의될 때 접근할 수 있었던 식별자(x)에는 여전히 접근할 수 있지만, 호출할 때 스코프에만 있는 식별자(y)에는 접근할 수는 없다.

**자바스크립트는 정적 스코프로 이루어져 있기 때문이다.**

## 7.3 전역 스코프

스코프는 **계층적**이며 트리의 맨 아래에는 바탕이 되는 무언가가 있어야 한다.

프로그램을 **시작할 때 암시적으로 주어지는 스코프**가 필요한데 이를 **전역 스코프**라 한다.

전역 스코프에서 선언된 것들을 **전역 변수(globals)** 라고 한다.

전역 스코프는 모든 스코프에서 보이기 때문에 수정 또한 모든 곳에서 가능하다. _그리고 이 점을 조심해야 한다._

```
    let name = "Irena"; // 전역
    let age = 25; // 전역
    function greet() {
        console.log(`Hello, ${name}!`);
    }
    function getBirthYear() {
        return new Date().getFullYear() - age;
    }
```

위 경우는 name, age 값을 어디서든 바꿀 수 있으며, 흔한 이름이므로 실수로 건드릴 가능성이 크다.

그래서 해당 정보는 단일 객체에 저장하는 것이 낫다.

```
    let user = {
        name = "Irena",
        age = 25,
    };
    function greet() {
        console.log(`Hello, ${user.name}!`);
    }
    function getBirthYear() {
        return new Date().getFullYear() - user.age;
    }
```

name과 age 말고도 사용자에 관한 정보가 10가지 혹은 100가지 이상인 경우일 수 있으므로 이렇게 객체에 묶는 것이 좋다.

하지만 greet과 getBirthYear 함수는 여전히 전역 user에 의존하며, 객체가 어디서든 수정될 수 있으므로 다음과 같이 수정한다.

```
    function greet(user) {
        console.log(`Hello, ${user.name}!`);
    }
    function getBirthYear(user) {
        return new Date().getFullYear() - user.age;
    }
```

이 함수들은 모든 스코프에서 호출할 수 있고, 명시적으로 user를 전달받는다. _(모듈과 객체지향 프로그래밍을 배우면 더 나은 방법이 있다.)_

## 7.4 블록 스코프

`let`과 `const`는 식별자를 [블록](https://github.com/Jeonjeongho/JEON206/blob/master/Chapter4/index.md#%EB%B8%94%EB%A1%9D-%EB%AC%B8) 스코프에서 선언한다.

```
    console.log('before block');
    {
        console.log('inside block');
        const x = 3;
        console.log(x); // 3
    }
    console.log(`outside block; x=${x}`);   // ReferenceError: x는 정의되지 않았습니다.
```

변수 선언이 이루어진 블록 스코프 밖에서는 해당 변수를 사용할 수 없다.

>  4장에서 독립 블록에 현실적인 쓸모는 별로 없다고 언급한 것을 기억할 겁니다. 이 장에서 독립 블록을 써서 스코프를 관리하는 방법을 소개하겠지만, 필요한 경우는 드뭅니다. 이 장에서 독립 블록을 사용하는 이유는 스코프에 대해 이해하기 쉬워서입니다.

## 7.5 변수 숨기기

```
    {
        const x = 'blue';
        // 1번
        console.log(x);
    }
    // 2번
    console.log(typeof x);
    {
        const x = 3;
        // 3번
        console.log(x);
    }
    // 4번
    console.log(typeof x);
```
[\>\> 예제확인](https://codepen.io/anon/pen/YRKrag?editors=0011)

```
    {
        // 외부 블록
        let x = { color: "blue" };
        let y = x;
        let z = 3;
        {
            // 내부 블록
            let x = 5;
            // 1번
            console.log(x);
            // 2번
            console.log(y.color);
            y.color = "red";
            // 3번
            console.log(z);
        }
        // 4,5,6번
        console.log(x.color);
        console.log(y.color);
        console.log(z);
    }
```
[\>\> 예제확인](https://codepen.io/anon/pen/ZmzXjX?editors=0011)

> 외부 스코프에 있는 같은 이름의 변수에 그늘이 진 듯 만든다는 의미에서 변수 숨김을 변수 섀도우(shadowing)라 부르기도 합니다.

## 7.6 함수, 클로저, 정적 스코프

**함수가 특정 스코프에 접근할 수 있도록 의도적으로 그 스코프에 정의**하는 경우를 클로저라 한다.

스코프를 함수 주변으로 좁히는 것이라고 생각해도 된다.


```
    let globalFunc; // 정의되지 않은 전역 함수
    {
        let blockVar = 'a'; // 블록 스코프에 있는 변수
        globalFunc = function() {
            console.log(blockVar);
        }
    }
    globalFunc(); // "a"
```

globalFunc을 호출하면, 이 함수는 스코프에 빠져나왔음에도 불구하고 blockVar에 접근할 수 있다.

일반적으로 스코프에서 빠져나가면 해당 스코프에서 선언한 변수는 메모리에서 제거해도 안전하다.

하지만 여기서는 **스코프 안에서 함수를 정의**했고, 해당 함수는 스코프 밖에서도 참조할 수 있으므로 자바스크립트는 스코프를 계속 유지한다.

```
let f; // 정의되지 않은 함수
{
    let o = { note: 'Safe' };
    f = function() {
        return o;
    }
}
let oRef = f();
oRef.note = "Not so safe after all!";
```

함수를 정의해 클로저를 만들면 접근할 수 없었던 것들에 접근할 방법이 생긴다.

## 7.7 즉시 호출하는 함수 표현식

함수 표현식으로 익명 함수를 만들고 그 함수를 즉시 호출시키기만 하면 된다.

```
    (function() {
        // IIFE 바디
    })();
```

주로 클로저를 만들고 클로저에서 무언가 반환받을 때에는 유용하게 쓸 수 있다.

```
    const f = (function() {
       let count = 0;
       return function() {
          return `I have been called ${++count} time(s).`;
       }
    })();
    f();  // "I have been called 1 time(s)."
    f();  // "I have been called 2 time(s)."
    //...
```

## 7.8 함수 스코프와 호이스팅

`let`으로 변수를 선언하면, 그 변수는 선언하기 전에는 존재하지 않는다.

```
let var1;
let var2 = undefined;

var1; // undefined
var2; // undefined
undefinedVar; // ReferenceError: notDefined 는 정의되지 않았습니다.
```
```
x;                // ReferenceError: x 는 정의되지 않았습니다.
let x = 3;       // 에러가 일어나서 실행이 멈췄으므로 여기에는 결코 도달할 수 없습니다.
```

반면 var로 변수를 선언하면 선언하기도 전에 사용이 가능하다.

```
x;              // undefined
var x = 3;
x;              // 3
```

var로 선언한 변수는 끌어올린다는 뜻의 **호이스팅** 이라는 메커니즘을 따른다.

단, **선언만 끌어올려지고 할당은 끌어올려지지 않는다.**
```
// 원래 코드
    if(x !== 3) {
        console.log(y);
        var y = 5;
        if(y === 5) {
            var x = 3;
        }
        console.log(y);
    }
    if(x === 3) {
        console.log(y);
    }
```

```
// 자바스크립트가 해석한 코드
    var x;
    var y;
    if(x !== 3) {
        console.log(y);
        y = 5;
        if(y === 5) {
            x = 3;
        }
        console.log(y);
    }
    if(x === 3) {
        console.log(y);
    }
```

`var`를 이용해 변수를 선언하면 자바스크립트는 같은 변수를 여러 번 정의하더라도 무시한다.

```
// 원래 코드
    var x = 3;
    if(x === 3) {
        var x = 2;
        console.log(x);
    }
    console.log(x);
```
```
// 자바스크립트가 해석한 코드
    var x;
    x = 3;
    if(x === 3) {
        x = 2;
        console.log(x):
    }
    console.log(x);
```

같은 함수나 전역 스코프 안에서는 `var`로 새 변수를 만들 수 없으며, `let`으로 가능했던 변수 숨김도 불가능하다.

## 7.9 함수 호이스팅

함수 선언도 스코프 맨 위로 끌어올려진다.

```
f(); // 'f'
function f() {
    console.log('f');
}
```

단, 함수 표현식은 끌어올려지지 않는다. 이 경우는 변수의 스코프 규칙을 그대로 따른다.

```
f(); // ReferrenceError: f 는 정의되지 않았습니다
let f = function() {
    console.log('f');
}
```

## 7.10 사각지대

`let`으로 선언하는 변수는 선언하기 전까지 존재하지 않는다는 직관적 개념을 **사각지대**라 한다.

스코프 안에서 변수의 사각지대는 변수가 선언되기 전의 코드이다.

```
if(typeof x === "undefined") {
    console.log("x doesn't exist or is undefined");
} else {
    // x를 사용해도 안전한 코드
}
```

x가 할당되지 않은 경우에 위처럼 분기처리가 가능하지만 같은 스코프에 `let`이 선언되어있는 경우는 다르다.

```
if(typeof x === "undefined") {
    console.log("x doesn't exist or is undefined");
} else {
    // x를 사용해도 안전한 코드
}
let x = 5;
```

이 경우에는 사각지대 해당하는 곳으로 선언이 되어있지 않기 때문에 `typeof` 를 사용할 수 없다.

## 7.11 스트릭트 모드

ES5 문법에서는 **암시적 전역 변수**라고 해서 `var`로 변수를 선언하는 것을 잊으면 자바스크립트는 전역 변수를 참조하려 한다고 간주하고, 스스로 만들어낸다.

이는 여러 문제를 발생시키기 때문에, 이를 방지하는 **스트릭트 모드**를 도입했다.

`'use strict'` 하나만으로 이루어진 행을 코드 맨 앞에 쓰면 해당 영역이 스트릭트 모드로 실행된다.

주의할 점은 전역에 선언할 경우 모든 스크립트가 스트릭트 모드로 강제되기 때문에 에러가 발생할 수 있다.

때문에 스트릭트 모드로 사용하고 싶은 함수들을 즉시 실행 함수로 감싸서 활용한다.

```
(function() {
    'use strict';
    // 코드를 전부 이 안에 작성합니다.
    // 이 코드는 스트릭트 모드로 동작하지만,
    // 이 코드와 함께 동작하는 다른 스크립트는
    // 스트릭트 모드에 영향받지 않습니다.
})();
```
참고자료 : [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)