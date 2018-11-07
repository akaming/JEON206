# chapter 5. 표현식과 연산자
## 표현식
* 값으로 평가될 수 있는 문
* 무언가를 요청 하는 문
* 결과를 명시적으로 반환 하는 것


```
    let x;      //선언문
    x = 3*5;    //표현식
```
```
    let x,y;         
    y = x = 3*5;    // 곱셈 표현식
                    // 첫번째 할당 x = 15, y = undefined
    y = x = 15;     // 두번째 할당 y = 15
    y = 15;         // x=15, y=15
                    // 이값은 사용하지도 않았고 어딘가에 할당하지도 않으니 그냥 버려집니다.
```
자바스크립트 표현식은 <strong>연산자 우선순위</strong>로 평가
표현식은 대부분 연산자 표현식입니다.
즉, 곱셈 표현식은 곱셈 연산자와 피연산자 두개로 이어집니다. 피연산자는서로 곱하는 두 숫자이며 피연산자 자체도 표현식입니다.

### 연산자
연산자는 하나이상의 피연산자가 있어야 결과로 나타낼 수 있다.

### 산술연산자
* 전위연산자
* 후위연산자


<table>
    <thead>
        <tr>
            <th>연산자</th>
            <th>설명</th>
            <th>예제</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>+</td>
            <td>덧셈 (문자열 병합에도 쓰임)</td>
            <td>3 + 2 // 5</td>
        </tr>
        <tr>
            <td>-</td>
            <td>뺄셈</td>
            <td>3 - 2 // 1</td>
        </tr>
        <tr>
            <td>/</td>
            <td>나눗셈</td>
            <td>3/2 // 1.5</td>
        </tr>
        <tr>
            <td>*</td>
            <td>곱셈</td>
            <td>3*2 // 6</td>
        </tr>
        <tr>
            <td>%</td>
            <td>나머지</td>
            <td>3%2 // 1</td>
        </tr>
        <tr>
            <td>-</td>
            <td>단항 부정</td>
            <td>-x // x의 부호를 바꿈 (x=5 --> -x = -5)</td>
        </tr>
        <tr>
            <td>+</td>
            <td>단항 플러스</td>
            <td>+x // x가 숫자가 아니면 숫자로 변환을 시도</td>
        </tr>
        <tr>
            <td>++</td>
            <td>전위 증가</td>
            <td>++x // x에 1을 더한 다음 평가</td>
        </tr>
        <tr>
            <td>++</td>
            <td>후위 증가</td>
            <td>x++ // x를 평가한 다음 1을 더함</td>
        </tr>
        <tr>
            <td>--</td>
            <td>전위 감소</td>
            <td>--x // x에 1을 뺀 다음 평가</td>
        </tr>
        <tr>
            <td>--</td>
            <td>후위 감소</td>
            <td>x-- // x를 평가한 다음에 1을 뺌</td>
        </tr>
    </tbody>
</table>

뺄셈과 단항 부정은 모두 - 기호를 사용합니다.
단항부정이 먼저, 그 다음 뺄셈을 합니다.

```
    const  x = 5;
    const y = 3 - - x;  // y=8

```
```
    const s = "5";
    const y = 3 + +s;   // 단항플러스 사용 y=8
                        // 단항플로스 사용 하지 않음, 문자열 병합으로 y="35";

    // 단항플러스 줄 맞춤
    const x1 = 0, x2 = 3, x3 = -1.5, x4 = -6.33;
    const p1 = -x*1;
    const p2 = +x2*2;
    const p3 = +x3*3;
    const p4 = -x4*4;

```
단항플러스에도 적용되지만 자주 사용하지않는다.

보통 + 연산자를 사용하는 경우
* <strong>문자열을 숫자로 강제 변환</strong>
* 세로 줄을 맞추고 싶을 때

* 전위연산자 (먼저 변수의 값을 바꾼 다음 평가)
* 후위연산자 (값을 바꾸기 전에 평가)
* 증가와 감소 연산자는 덧셈보다 먼저 실행

```
    let x = 2;
    const r1 = x++ + x++;
    const r2 = ++x + ++x;
    const r3 = x++ + ++x;
    let y = 10;
    const r5 = y-- + y--;
    const r6 = --y + --y;
    const r7 = y-- + --y;
    const r8 = --y + y--;
```
### 연산자 우선순위
```
    8 ÷ 2 + 3 x ( 4 x 2 - 1 )
```
```
    let x = 3,y;
    x += y = 6*5/2;   
```

### 비교 연산자
두개의 값을 비교
* 일치함 ( === )
    * 두 값이 같은 객체를 가르키거나, 같은 타입이고 값도 같다면(원시타입) 일치한다.
    * 확인 연산자 === , !==
* 동등함 ( == )
    * 두 값이 같은 객체를 가르키거나, 같은 값을 갖도록 변환할 수 있다면 동등하다. 
    * 확인 연산자 == , !=
* 대소 관계 ( >,<)

<small>Tip</small> 동등연산자로 문제가 생기는 경우는 대게 null 과 undefined, 빈 문자욜, 숫자 0 때문이다.
위 경우 해당하지 않는 값을 비교한다면 동등연산자를 써도 안전할 때가 많습니다.
일치 연산자를 사용하기를 권한다.

#### 일치연산자와 동등연산자의 예
a,b 에 같은 정보가 들어 있더라도 다른 객체이며 일치하지도, 동등하지도 않는다.
```
    const n = 5;
    const s = "5";
    n === s;
    n !== s;
    n === Number(s);
    n !== Number(s);
    n == s;             // 동등 연산자 권장하지않음
    n != s;             // 동등 연산자 권장하지않음

    const a = {name : "an Object"};
    const b = {name : "an Object"};
    a === b;
    a !== b;
    a == b;             // 동등 연산자 권장하지않음
    a != b;             // 동등 연산자 권장하지않음

```
관계 연산자는 관계있는 값을 비교하며 
관계 연산자는 작다 (<), 작거나같다(<=), 크다 (>), 크거나 같다(>=)


### 숫자비교
* 특별한 숫자형 값 NaN은 그 자신을 표함하여 무엇과도 같지 않다. (NaN === NaN , NaN == NaN 은 false)
* 숫자가 NaN인지 알아보려면 내장된 isNaN 함수를 사용
* isNaN(x) 은 x 가 NaN 일때  false 반환

### 문자열 병합
자바스크립트에서 + 연산자는 덧셈과 문자열 병합에 모두 사용

```
    3 + 5 +"8" // 문자열 "88"
    "3" + 5 + 8 // 문자열 "358"
```

### 논리연산자
false, true 불리언 값만 다룰수 있음.
거짓 같은 값,참같은 값 으로 나눌 수 있음.

#### 거짓 같은 값
* undefined
* null
* false
* 0
* NaN
* '' (빈문자열)

#### 참 같은 값
* 모든 객체 (valueOf() 메서드를 호출 했을때 false를 반환하는 객체도 참 같은 값에  속함)
* 배열 ( 빈 배열도 참 같은 값에 속함 arr.length 를 쓰면 0 을 반환하며 거짓 가은 값으로 확인됨)
* 공백만 있는 문자열 ( ' ' 등 )
* 문자열 "false"


### AND , OR , NOT
자바스크립트가 지원하는 논리 연산자
* AND (교집합) 피산자가 모두 true 일때 true
* OR (합집합) 피연산자가 모두 false 일때만 false
* NOT (부정) 피연산자를 반대로 바꿈

#### 단축 평가
* 두 값을 모두 평가하지 않아도 될때 일어나는 동장 방식
* 하나의 값만 평가하고 결과를 반환
```
    false && 아무 표현식        // false
    true || 아무 표현식         // true
```
```
    const skipIt = true;
    let x = 0;
    const result = skipIt || x++;
```
세번째 행에서 단축평가가 일어나므로 증가 연산자에 해당하는 표현식은 실행되지 않고
x의 값은 그대로 0이다.
skipIt을 false 로 바꾸면 논리연산자의 두 피연산자를 모두 평가해야하고 x 는 증가합니다.
```
    const doIt = false;
    let x = 0;
    const result = doIt && x++;
```
AND 에서 첫번째 피연산자가 false 이므로 두 번째 피연산자를 실행하지 않는다.
result = false 이고, x 는 늘어나지않는다.
doIt을 true 로 바꾸면 두 피연산자를 모두 평가해야하므로 증가 연산이 일어나고, result = 0;


```  
    $pop.css({
        left: function() {return "50%" },
        top: function() { return ( ! isFlow ) && "50%" },
        marginTop: function() { return ( ! isFlow ) && -( $pop.outerHeight() / 2 ) },
        marginLeft: function() {return -( $pop.outerWidth() / 2 ) },
        height: function() { return ( isFlow ) && "100%" }
    });
```

``` 
    let a = true;
    let b = true;
    let c = 3;

    (function(){
        return console.log( a && b && c);
    })()
```

#### 조건 연산자
자바스크립트의 유일한 삼항연산자
```
    const doIt = false;
    const result = doIt ? "Did it\!" : "Didn't do it.";
```
* 물음표 앞 첫번째 연산자가 참 이면 ? 앞의 값
* 거짓이면 ? 뒤의 값

#### 쉼표 연산자
표현식을 결합하여 두 표현식을 평가한 후, 두번째 표현식의 결과를 반환
```
    let x = 0, y = 10, z;
    z = (x++, y++);
```

#### 연산자 그룹
연산자의 우선순위를 높이거나 명확히 포현하는데 쓸 수 있음.

#### 비트 연산자
숫자의 비트를 직접 조작
 
#### typeof 연산자
* 피연산자의 타입을 나타내는 문자열을 반환
* 배열과 배열이 아닌 객체 정확히 구문 못함
* null 과 {}, [] object 라고 반환


#### void 연산자
* 피연산자를 평가 한 후 undefined 반환

#### 할당 연산자 
<table>
    <thead>
        <tr>
            <th>연산자</th>
            <th>동등한 표현</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td> x += y</td>
            <td>x = x + y</td>
        </tr>
        <tr>
            <td> x -= y</td>
            <td>x = x - y</td>
        </tr>
        <tr>
            <td> x *= y</td>
            <td>x = x * y</td>
        </tr>
        <tr>
            <td> x /= y</td>
            <td>x = x / y</td>
        </tr>
        <tr>
            <td> x %= y</td>
            <td>x = x % y</td>
        </tr>
        <tr>
            <td> x <<= y</td>
            <td>x = x << y</td>
        </tr>
        <tr>
            <td> x >>= y</td>
            <td>x = x >> y</td>
        </tr>
        <tr>
            <td> x >>>= y</td>
            <td>x = x >>> y</td>
        </tr>
        <tr>
            <td> x &= y</td>
            <td>x = x & y</td>
        </tr>
        <tr>
            <td> x |= y</td>
            <td>x = x | y</td>
        </tr>
        <tr>
            <td> x ^= y</td>
            <td>x = x ^ y</td>
        </tr>
    </tbody>
</table>

### 해체 할당
ES6 에서 새로 도입한 해체 할당
객체나 배열을 변사로 '해체' 할 수 있습니다
```
    // 객체선언
    const obj = { b:2, c:3, d:4 };

    //해체할당
    const {a,b,c} = obj;
    a;                  // undefined : obj 에는 "a" 프로퍼티가 없다
    b;                  // 2
    c;                  // 3
    d;                  // referenceError : "d" 는 정의되지 않았다.
```

위의 예제는 선언과 할당이 같은문에서 실행했다. 객체 해체는 할당만으로 이뤄질 수도 있지만, 그렇게 하려면 반드시 괄호가 필요합니다.
괄호를 쓰지 않으면 자바스크립트는 표현식 좌변을 블록으로 해석합니다.

```
    const obj = { b:2, c:3, d:4 }
    let a, b, c;

    {a,b,c} = obj;          //에러
    ({a,b,c} = obj);       //동작
```
배열을 해체할 때는 배열 요소에 변수 이름을 마음대로 쓸 수 있으며 
배열 순서대로 대응.
```
    const arr = [1,2,3];

    //배열 해체할당
    let [x,y] = arr;
    x;              // 1
    y;              // 2
    z;              // ReferenceError : 'z'는 정의 되지 않았습니다.
```
```
    const arr = [1,2,3,4,5];

    let [x,y, ...rest] = arr;
    x;              // 1
    y;              // 2
    rest;           // [3,4,5]
```

<a href="https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment" target="_blank" >mdn 비구조할당 참조</a>

### 객체와 배열 연산자
<table>
    <thead>
        <tr>
            <th>연산자</th>
            <th>설명</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>.</td>
            <td>점 연산자</td>
        </tr>
        <tr>
            <td>[]</td>
            <td>대괄호 연산자</td>
        </tr>
        <tr>
            <td>in</td>
            <td>프로퍼티 존재 연산자</td>
        </tr>
        <tr>
            <td>new</td>
            <td>객체 인스턴스화 연산자</td>
        </tr>
        <tr>
            <td>instance of</td>
            <td>프로토타입 체인 테스트 연산</td>
        </tr>
        <tr>
            <td>...</td>
            <td>확장 연산</td>
        </tr>
        <tr>
            <td>delete</td>
            <td>삭제 연산</td>
        </tr>
    </tbody>
</table>

### 템플릿 문자열과 표현식
3장에서 설명 함

### 표현식과 흐름 제어 패턴

#### if문을 단축 평가하는 OR 표현식으로 바꾸기
```
    if (isPrime (n)) {
        label = 'prime';
    } else {
        label = 'non-prime';
    }
```
```
    label = isPrime(n) ? 'prime' : 'non-prime';
```

#### if문을 단축 평가하는 OR 표현식으로 바꾸기
```
    if (!options) options = {};
```

```
    options = options || {};
```