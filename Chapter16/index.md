# chapter16 Math

Math 객체는 수학함수를 담고 있다. Math 객체의 프로퍼티를 매서드라 부르지않고 함수라 부른다.

* 자바스크립트에는 정수 전용 클래스가 없음.
* 자바스크립트의 숫자는 국제 IEEE 754 표준에 따라 두배 정확도(double precision)의 부동 소수점 숫자(floating point numbers), 64비트로 저장
* 자바스크립트는 아주 복잡한 숫자나 큰 숫자를 지원하지 못함.

## 16.1 숫자형식
자바스크립트의 **숫자 형식 메서드는 문자열을 반환**합니다.  숫자를 저장하거나 계산할 때는 따로 형식을 지정하지 않은 숫자 타입이어야 합니다.

### 16.1.1 고정 소수점
```
const x = 19.51;
x.toFixed(3); // "19.510"
x.toFixed(2); // "19.51"
x.toFixed(1); // "19.5"
x.toFixed(0); // "20"
```
이 숫자는 반올림으로 계산

### 16.1.2 지수 표기법
```
const x = 3800.5; // 지수표기법 : 3.8005e + 3;
x.toExponential(4); //"3.8005e+3";
x.toExponential(3); //"3.801e+3";
x.toExponential(2); //"3.80e+3";
x.toExponential(1); //"3.8e+3";
x.toExponential(0); //"4e+3";
```
이숫자는 **반올림**으로 계산
**매개변수로 넘긴 정밀도에 따라 소수점 뒤에 숫자가 몇개**가 나타날지 정해진다

### 16.1.3 고정 전체 자리수
소수점이 어디 나타나든 관계없이 숫자 몇개로 표현하느냐가 중요하다면 toPrecision()을 사용한다
```
let x = 1000;
x.toPrecision(5); // "1000.0"
x.toPrecision(4); // "1000"
x.toPrecision(3); // "1.00e+3" //일부상황에서는 지수 표기법이 반환 될 수 있음.
x.toPrecision(2); // "1.0e+3"
x.toPrecision(1); // "1e+3"

x = 15.335;
x.toPrecision(6) // "15.3350"
x.toPrecision(5) // "15.335"
x.toPrecision(4) // "15.34"
x.toPrecision(3) // "15.3"
x.toPrecision(2) // "15"
x.toPrecision(1) // "2e+1"
```
**반올림** 된 숫자
**전체 자릿수는 매개변수로 넘긴 자릿수와 일치**한다.

### 16.1.4 다른 진수
2진수나 8진수,16진수 표현을 원한다면 toString()
```
const x = 12;
x.toString(); // "12" (10진수)
x.toString(10); // "12" (10진수)
x.toString(16); // "c" (16진수)
x.toString(8); // "14" (8진수)
x.toString(2); // "1100" (2진수)
```
### 16.1.5 고급 숫자 형식
* 수천자리의 아주 큰 숫자
* 괄호를 쓰는 등 음수 표현을 다르게 해야 하는 경우
* 공학 표기법(지수표기법과 비슷합니다.)
* milli-, micro-, kilo-, mega- 등의 SI 접두사가 필요한 경우

위의 기능을 사용하려면 <a href="http://numeraljs.com/" target="_blank">numeral.js</a>를 권합니다.

## 16.2 상수
Math 객체에는 몇 가지 중요한 상수가 프로퍼티로 내장돼 있습니다.
```
//기본적인 상수
Math.E   //자연로그의 일수 : ~2.718 (~는 근삿값)
Math.PI   // 원주율 : ~3.142

// 로그 관련 상수는 Math 객체의 프로퍼티에도 호출해도 되지만, 자주 사용한다면
// 따로 상수에 할당해서 편리하게 사용하는게 좋습니다.
Math.LN2   // 2의 자연로그 : ~0.693
Math.LN10   // 10의 자연 로그 : ~2.303
Math.LOG2E   // Math.E의 밑수가 2인 로그 : ~1.433
Math.LOG10E   //Math.E의 상용 로그 : 0.434

// 대수 관련 상수
Math.SQRT1_2   // 1/2의 제곱근 : ~0.707
Math.SQRT2   // 2의 제곱근 : ~1.414

```
### 16.3 대수 함수
#### 16.3.1 거듭제곱
제곱 관련 기본 함수는 Math.pow 이며 제곱근, 세제곱근, e의 거듭제곱 등 자주 쓰이는 연산에는 간편 함수가 있습니다.

#### 제곱．제곱근 관련함수
| 함수 | 설명 | 예제 |
| --- | --- | --- |
| Math.pow(x,y) | x 의 y 제곱 | Math.pow(2, 3)      // 8  <br>Math.pow(1.7, 2.3)  // ~3.39 |
| Math.sqrt(x) | 주어진 숫자에 루트(√ ) | Math.sqrt(16)    // 4 <br>Math.sqrt(15.5)  // ~3.94 |
| Math.cbrt(x) | 세제곱근.<br>x는 Math.pow(x, 1/3)와 같습니다. | Math.cbrt(27)   // 3 <br>Math.cbrt(22)   // ~2.8 |
| Math.exp(x) | e의 x제곱.<br>Math.pow(Math.E, x)와 같습니다. | Math.exp(1)     // ~2.718  <br>Math.exp(5.5)   // ~244.7 |
| Math.expm1(x) | e의 x제곱 - 1.<br> Math.exp(x) - 1와 같습니다. | Math.expm1(1)     // ~1.718  <br>Math.expm1(5.5)   // ~243.7 |
| Math.hypot (x1, x2,...) | 매개변수의 제곱을 합한 수.<br>루트(√ )( x1의제곱 + x2의 제곱 + ... )의 제곱근입니다. | Math.hypot(3, 4)    // 5  <br>Math.hypot(2, 3, 4) // ~5.36 |


#### 16.3.2 로그함수 
자바스크립트의 log는 자연로그이다. 자연로그의 함수는 Math.log 이다.<br>
es6에서 자주 쓰이는 사용로그 Math.log10 함수가 생겼습니다.

| 함수 | 설명 | 예제 |
| --- | --- | --- |
| Math.pow(x,y) | x의 자연로그 | Math.log(Math.E) // 1  <br>Math.log(17.5)   // ~2.86 |
| Math.log10(x) | x의 상용로그.<br>Math.log(x)/Math.log(10)와 같습니다. | Math.log10(10)   // 1  <br>Math.log10(16.7) // ~1.22 |
| Math.log2(x) | x의 밑수가 2인 로그.<br>Math.log(x)/Math.log(2)와 같습니다. | Math.log2(2)   // 1  <br>Math.log2(5)   // ~2.32 |
| Math.log1p(x) | 1 + x의 자연로그.<br>Math.log(1 + x)와 같습니다. | Math.log1p(Math.E - 1) // 1  <br>Math.log1p(17.5)    // ~2.92 |

#### 16.3.3 기타함수
절댓값, 부호, 배열 의 최솟값/최댓값 등 숫자 관련 함수

| 함수 | 설명 | 예제 |
| --- | --- | --- |
| Math.abs(x) | x의 절댓값 | Math.abs(-5.5) // 5.5 <br>Math.abs(5.5)  // 5.5 |
| Math.sign(x) | x의 부호. <br>x가 음수면 -1, 양수면 1, 0이면 0입니다. | Math.sign(-10.5) // -1  <br>Math.sign(6.77)  // 1 |
| Math.ceil(x) | x의 올림. <br>x보다 크거나 같은 정수 중 가장 작은 수 | Math.ceil(2.2)  // 3  <br>Math.ceil(-3.8) // -3 |
| Math.floor(x) | x의 내림. <br>x보다 작거나 같은 정수 중 가장 큰 수 | Math.floor(2.8)  // 2  <br>Math.floor(-3.2) // -4 |
| Math.trunc(x) | x의 버림. | Math.trunc(7.7)  // 7  <br>Math.trunc(-5.8) // -5 |
| Math.round(x) | x의 반올림 | Math.round(7.2) // 7  <br>Math.round(7.7) // 8  <br>Math.round(-7.7) // -8  <br>Math.round(-7.2) // -7 |
| Math.min(x1, x2,...) | 매개변수 중 최솟값 | Math.min(1, 2)  // 1  <br>Math.min(3, 0.5, 0.66)  // 0.5  <br>Math.min(3, 0.5, -0.66) // -0.66 |
| Math.max(x1, x2,...) | 매개변수 중 최댓값 | Math.max(1, 2)  // 2   <br>Math.max(3, 0.5, 0.66)   // 3  <br>Math.max(-3, 0.5, -0.66) // 0.5 |

#### 16.3.2 의사 난수 생성
자바스크립트에서 난수(정의된 범위 내에서 무작위로 추출된 수)를 생성할때 Math.random()을 사용합니다.<br>
0 이상 1 미만의 숫자를 반환합니다.<br>
아래표에서 x와 y는 실수, m과 n은 정수이다.

| 범위 | 예제 |
| --- | --- |
| 0 이상 1 미만 | Math.random() |
| x 이상 y 미만 | x + (y-x)*Math.random() |
| m 이상 n 미만의 정수 | m + Math.floor((n-m)*Math.random()) |
| m 이상 n 이하의 정수 | m + Math.floor((n-m+1)*Math.random()) |

자바스크립트는 의사 난수를 발생기는 시드 숫자를 쓸 수 없다는 단점이 지적되곤 합니다.
의사 난수를 사용하는 알고리즘 중에는 시드 숫자가 중요할 때가 많습니다. 시드를 사용해 의자 난수를 생성해야 한다면 데이비드 바우의 <a href="https://github.com/davidbau/seedrandom" target="_blank">seedrandom.js</a> 패키지 참고

### 16.4 삼각함수
사인,코사인,탄젠트, 아크사인, 아크코사인, 아크탄젠트입니다.
자바스크립트 의 삼각함수는 모두 라디안 값을 기준으로 합니다.

| 함수 | 설명 | 예제 |
| --- | --- | --- |
| Math.sin(x) | x의 사인 | Math.sin(Math.PI/2) // 1  <br>Math.sin(Math.PI/4) // ~0.707 |
| Math.cos(x) | x의 코사인 | Math.cos(Math.PI)   // -1  <br>Math.cos(Math.PI/4) // ~0.707 |
| Math.tan(x) | x의 탄젠트 | Math.tan(Math.PI/4) // ~1  <br>Math.tan(0)         // 0 |
| Math.asin(x) | x의 아크사인(결과는 라디안입니다) | Math.asin(0)             // 0  <br>Math.asin(Math.SQRT1_2)  // ~0.785 |
| Math.acos(x) | x의 아크코사인(결과는 라디안입니다) | Math.acos(0)             // ~1.57+  <br>Math.acos(Math.SQRT1_2)  // ~0.785+ |
| Math.atan(x) | x의 아크탄젠트(결과는 라디안입니다) | Math.atan(0)            // 0  <br>Math.atan(Math.SQRT1_2) // ~0.615 |
| Math.atan2(y, x) | x 축에서 점 (x, y)까지의 시계 반대방향 각도를<br>라디안으로 나타낸 값 | Math.atan2(0, 1)  // 0  <br>Math.atan2(1, 1)  // ~0.785 |

**매개변수에 각도를 쓸 수 없으므로 라디안 값으로 바꿔야합니다.** <br>
**180으로 나누고  파이(π)를 곱하면 됩니다.**
```
function deg2rad(d) { return d/180*Math.PI; }
function read2deg(r) {return r/Math.PI*180; }
```

### 16.4 쌍곡선 함수
| 함수 | 설명 | 예제 |
| --- | --- | --- |
| Math.sinh(x) | 설명 | x의 퍼볼릭 사인 | Math.sinh(0) // 0  <br>Math.sinh(1) // ~1.18 |
| Math.cosh(x) | x의 하이퍼볼릭 코사인 | Math.cosh(0) // 1  <br>Math.cosh(1) // ~1.54 |
| Math.tanh(x) | x의 하이퍼볼릭 탄젠트 | Math.tanh(0) // 0  <br>Math.tanh(1) // ~0.762 |
| Math.asinh(x) | x의 하이퍼볼릭 아크 사인 | Math.asinh(0) // 0  <br>Math.asinh(1) // ~0.881 |
| Math.acosh(x) | x의 하이퍼볼릭 아크 코사인 | Math.acosh(0) // NaN  <br>Math.acosh(1) // 0 |
| Math.atanh(x) | x의 하이퍼볼릭 아크 탄젠트 | Math.atanh(0) // 0  <br>Math.atanh(0) // ~0.615 |


