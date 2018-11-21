# Chapter 4 : 제어문

## 4.1 제어문의 기초

### 블록 문

문(statement) 여러 개를 중괄호로 묶은 것을 블록 문(= 복합 문)이라 한다.

```
{ // 블록 문을 시작합니다.
    console.log('statement 1');
    console.log('statement 2');
} // 블록 문을 끝냅니다.
```

개별적으로 사용 시 큰 의미가 없으며, 제어문과 함께 쓸 때 주로 사용된다.

```
    let funds = 50;
    while(funds > 1 && funds < 100) {
        funds = funds + 2;
        fund = funds - 1;
    }
```

제어문에서 문이 한 개인 경우에는 블록 문을 쓰지 않아도 된다.
```
    let funds = 50;
    while(funds > 1 && funds < 100)
        funds = funds + 2;
```

### 공백

아래와 같이 공백이 있어도 제어문은 작동하지만 두 구문이 연관되어 보이지 않기 때문에 지양해야 한다.

```
    let funds = 50;
    while(funds > 1 && funds < 100)

        funds = funds + 2;
```

또한 블록 문을 쓰지 않은 상황에서 들여쓰기가 모호한 부분도 조심해야 한다.

```
    let funds = 50;
    while(funds > 1 && funds < 100)
        funds = funds + 2;
        console.log(funds); // while 루프가 끝난 다음 실행.
```

같은 if 문 안에서 블록 문과 블록 없는 문을 섞어 쓰는 방법도 혼란을 초래한다.


```
if (funds > 1) {
    console.log('There's money left!');
    console.log('That means keep playing!');
} else
    console.log('I`m broke! Time to quit.');
```
```
    if (funds > 1)
        console.log('I`m broke! Time to quit.');
    else {
        console.log('There's money left!');
        console.log('That means keep playing!');
    }
```

문 하나인 경우에도 블록 문으로 처리하거나, 위 사례들을 조심히 하여 처리하는 것이 좋다.

```
    while (funds > 1 && funds < 100) {
        funds = funds + 2;
    }
```
```
    while (funds > 1 && funds < 100) funds = funds + 2;
```

위 코드처럼 가능한 방식은 여러가지지만 개인적인 의견에 따라 스타일을 정하면 되며,

팀이나 오픈 소스 프로젝트에서 협력중인 경우는 개인 스타일보다는 해당 가이드에 맞게 진행히도록 한다.

## 4.2 자바스크립트의 제어문

### 제어문의 예외

제어문의 일반적인 실행 방식을 바꾸는 4가지 문

1. break

    : 루프 중간에 빠져나간다.

2. continue

    : 루프에서 다음 단계로 바로 건너뛴다.

3. return

    : 제어문을 무시하고 현재 함수를 즉시 빠져나간다. (6장 참고)

4. throw

    : 예외 핸들러에서 반드시 처리해야 할 예외(exception)를 일으킨다. (11장 참고)

### if...else 문을 체인으로 연결하기

```
if (new Date().getDay() === 3) {
    totalBet = 1;
} else if (funds === 7) {
    totalBet = funds;
} else {
    console.log('No superstition here!');
}
```

### 메타 문법

다른 문법을 설명하는 문법.

1. 대괄호([]) : 옵션
2. 생략 부호(...) : '여기 들어갈 내용이 더 있다' 라는 뜻

#### while 문

```
    while(condition)
        statement
```
condition이 참 같은 값이면 statement를 실행한다.

_'참 같은 값' 이라는건 실제로 true 가 아니더라도 불리언으로 판단 시 true와 같은 경우를 뜻하는 듯.._

#### if...else 문
```
    if(condition)
        statement1
    [else
        statement2]
```
condition이 참 같은 값이면 statement1을 실행하고, 그렇지 않고 else 부분이 있으면 statement2를 실행한다.

#### do...while 문
```
    do
        statement
    while(condition);
```
statement는 최소한 1번 실행하고, condotion이 참 같은 값인 동안 반복해서 실행한다.

#### for 문
```
    for([initialization]; [condition]; [final-expression])
        statement
```
1. initialization을 먼저 실행한다.
2. condition이 true인 경우 statement를 실행하고, false인 경우에 해당 문을 종료한다.
3. final-expression을 실행한 이후 2번으로 돌아간다.

### for 루프의 다른 패턴

쉼표 연산자를 사용하면 초기화와 마지막 표현식에 여러 문을 결합할 수 있다.
```
    for(let temp, i=0, j=1; j<30; temp=i, i=j, j=i+temp)
        console.log(j);
```
for 루프의 제어부에 아무것도 쓰지 않으면 무한 루프가 만들어진다.
```
    for(;;) console.log('I will repeat forever!');
```
for 루프에서 조건을 생략하면 항상 true로 평가된다.

보통 정수 인덱스를 늘이거나 줄이면서 반복하지만 여러 표현식으로 사용 가능하다.
```
    let s = '3';
    for(; s.length < 10; s = ' ' + s); // 여기서 사용한 for 루프 마지막에 세미콜론이 없으면 에러가 일어남.

    for(let x = 0.2; x < 3.0; x += 0.2) // 제어 변수가 정수가 아니어도 괜찮습니다.
        console.log(x);

    for(; !player.isBroke;) // 조건에 객체 프로퍼티를 사용
        console.log('Still playing!');
```

for 루프는 모두 While 루프로 고쳐 쓸 수 있다.

```
    for([initialization]; [condition]; [final-expression])
        statement
```
```
    [initialization]
    while([condition]){
        statement
        [final-expression]
    }
```
for 루프가 제어부가 첫 번째 행에 모여 있어서 육안상 확인이 쉽고, let으로 초기화한 변수가 루프 내에서만 유효하다는 장점이 있기 때문에 주로 쓰인다.

### switch 문

조건 하나로 여러 가지 중 하나를 선택할 수 있는 제어문이다.
```
    switch(expression){
        case value1:
            // expression을 평가한 결과가 value1일 때 실행.
            [break;]
        case value2:
            // expression을 평가한 결과가 value2일 때 실행.
            [break;]
            ...
        case valueN:
            // expression을 평가한 결과가 valueN일 때 실행.
            [break;]
        default:
            // expression을 평가한 결과가 맞는 것이 없을 때 실행.
            [break;]
    }
```
expression을 평가하고 그에 일치하는 첫 번째 case를 찾아서 break, return, ~~continue, throw~~를 만나거나 switch 문이 끝날 때까지 문을 실행한다.

```
    switch(totalBet){
        case 7:
            totalBet = funds;
            break;
        case 11:
        case 13: // 조건이 11인 경우에도 break 문이 없었기 때문에, 13과는 일치하지 않아도 실행된다.
            totalBet = 0;
            break;
        case 21:
            totalBet = 21;
            break;
    }
```

이처럼 한 블록문 안에서도 여러가지 형태가 될 수 있기 때문에 주의해서 사용해야 한다.

```
    switch(totalBet){
        case 7:
            totalBet = funds;
            break;
        case 13:
            funds = funds - 1;
        case 11:
            totalBet = 0;
            break;
        case 21:
            totalBet = 21;
            break;
    }
```

해당 구문을 봤을때에 case 13에서 break 문을 실수로 빠뜨렸다고 착각하기가 쉽다.

```
    switch(totalBet){
        case 7:
            totalBet = funds;
            break;
        case 13:
            funds = funds - 1;
            // 13인 경우에는 1펀즈를 깎고 totalBet을 0으로 한다.
        case 11:
            totalBet = 0;
            break;
        case 21:
            totalBet = 21;
            break;
    }
```

이처럼 break 문이 없는 case 절에서는 해당 내용을 설명하거나 break 문이 없음이 맞음을 명시하는 주석을 달아주는 것이 좋다.

```
    function adjustBet(totalBet, funds) {
        switch(totalBet){
            case 7:
                return funds;
            case 13:
                return 0;
            default:
                return totalBet;
        }
    }
```

함수인 경우에는 즉시 함수를 빠져나가는 return 문을 break 문 대신 사용이 가능하다.


> switch 문은 표현식 하나로 여러 가지 옵션 중에서 하나를 선택해야 할 때 아주 유용합니다.
> 그렇긴 하지만, 9장에서 동적 디스패치에 대해 배우고 나면 switch 문을 그리 많이 쓰지는 않게 될 겁니다.

_기껏 다 해봤더니 책 마무리가 이랬다..-.-_

### for...in 루프

객체의 프로퍼티에 루프를 실행하도록 설계된 루프이다.
```
    for(variable in object)
        statement
```
> 9장에서 이 예제에 대해 더 배우게 됩니다.

### for...of 루프

ES6에서 새로 생긴 반복문이며 컬렉션의 요소에 루프를 실행하는 다른 방법이다.

```
    for(variable of object)
        statement
```

배열은 물론 이터레블(9장 참고) 객체에 모두 사용할 수 있는 범용적인 루프이다.

```
    const hand = [randFace(), randFace(), randFace()];
    for(let face of hand)
        console.log(`You rolled...${face}!`);
```

for...of는 각 요소의 인덱스를 알 필요는 없을 때 알맞으며, 인덱스를 알아야한다면 일반적인 for 루프를 사용하면 된다.
```
    const hand = [randFace(), randFace(), randFace()];
    for(let i=0; i < hand.length; i++)
        console.log(`Roll ${i+1}: ${hand[i]}`);
```

## 4.3 유용한 제어문 패턴

### continue 문을 사용하여 조건 중첩 줄이기

특정 조건이 맞을 때만 루프 바디를 실행해야 하는 경우(반복문 안에 조건문)

```
    while(funds > 1 && funds < 100){
        let totalBet = rand(1, funds);
        if(totalBet === 13) {
            console.log('Unlucky! Skip this round...');
        } else {
            console.log('play...');
            ...
        }
    }
```

이러한 경우를 **제어문 중첩**이라 부른다.

while 루프의 바디에서 할 일은 대부분 else 절에 있고, if 절이 하는 일은 console.log 호출뿐이다.

continue 문을 써서 이 구조를 간결하게 만든다.

```
    while(funds > 1 && funds < 100) {
        let totalBet = rand(1, funds);
        if(totalBet === 13) {
            console.log('Unlucky! Skip this round...');
            continue; // 해당 루프는 건너 뛰고 다음 루프 실행
        }
        console.log('play...');
        ...
    }
```

### break나 return 문을 써서 불필요한 연산 줄이기

뭔가를 실행하고 난 이후 계속 루프를 할 필요가 없어진 경우가 있을 수 있다.

```
    let firstPrime = null;
    for(let n of bigArrayOfNumbers) { // bigArrayOfNumbers -> 대충 100만개의 숫자 배열
        if(isPrime(n) && firstPrime === null) firstPrime = n; // isPrime -> 소수 유무 체크 함수
    }
```

찾는 값이 초반에 있다면 굳이 뒤의 몇 십만개의 배열을 다 뒤질 필요는 없기 때문에 break 문을 사용하여 즉시 루프에서 빠져나간다.

```
    let firstPrime = null;
    for(let n of bigArrayOfNumbers) {
        if(isPrime(n)){
            firstPrime = n;
            break;
        }
    }
```

해당 루프가 함수 안에 있었다면 break 대신 return 문을 써도 된다.

### 루프를 완료한 뒤 인덱스 값 사용하기

루프를 종료한 이후 종료 당시 인덱스 변수 값이 필요한 경우가 있다.

초기값을 for 문 바깥에서 선언하고, break 문을 통해 즉시 루프를 끝내도록 해야만 사용이 가능하다.

```
    let i = 0;
    for(; i < bigArrayOfNumbers.length; i++){
        if(isPrime(bigArrayOfNumbers[i])) break;
    }
    if(i === bigArrayOfNumbers.length) console.log('No prime numbers!');
    else console.log(`First prime number found at position ${i}`);
```

### 배열을 수정할 때 감소하는 인덱스 사용하기

```
    for(let i = 0; i < bigArrayOfNumbers.length; i++){
        if(isPrime(bigArrayOfNumbers[i])) bigArrayOfNumbers.splice(i, 1); // i 인덱스의 요소 1개 제거
    }
```

인덱스는 점점 커지는데 해당 인덱스의 배열 요소를 제거하고 있으므로 이로 인한 오류나 무한루프에 빠질 수 있다.

이런 문제의 경우에선 감소하는 인덱스를 쓰면 간단히 해결된다.

```
    for(let i = bigArrayOfNumbers.length-1; i >= 0; i--){
        if(isPrime(bigArrayOfNumbers[i])) bigArrayOfNumbers.splice(i, 1);
    }
```

1. 배열의 인덱스는 0에서 시작하므로 배열 길이보다 1 작은 값으로 시작한다.
2. 루프의 종료 조건을 i가 0보다 크거나 같다로 정한다.

======

_수고하셨습니다 :)_