# Chapter 8 : 배열과 배열처리

## 8.1 배열의 기초

* 배열은 객체와 달리 본질에 순서가 있는 데이터 집합이며 0으로 시작하는 숫자형 인덱스를 사용합니다.
* 배열은 다른 배열이나 객체도 포함 가능합니다.

```
const arr1 = [1, 2, 3];                         // 숫자
const arr2 = ["One", 2, "Three"]                // 숫자와 문자열
const arr3 = [                                  // 객체와 객체 내의 배열, 배열 내의 배열, 숫자, 함수, 문자열로 구성된 배열
    {name : "Fred", age : 30, number : [1, 2, 3]},
    [
        [1, 2, 3],
        ["One", "Two", 3],
    ],
    1,
    function(){
        return "Hello World!";
    },
    "Three"
]
```

## 8.2 배열 요소 조작

배열 메서드 중 일부는 배열 자체를 수정하며, 다른 일부는 새 배열을 반환합니다.

### 8.2.1 배열 처음이나 끝에 요소 추가 / 제거

&nbsp;  | 첫 번째   | 마지막 번째
------- |--------- | ---------
__추가__|unshift() | push()
__삭제__|shift() | pop()

```
const arrFirst = [1, 2];
arrFirst.unshift("One");    // ["One", 1, 2]
arrFirst.shift();           // [1, 2]
arrFirst.push("Three", 4);  // [1, 2, "Three", 4]
arrFirst.pop();             // [1, 2, "Three"]
```

### 8.2.2 배열 끝에 여러 요소 추가

* concat() : 배열의 끝에 여러 요소를 추가한 사본을 반환합니다. (https://msdn.microsoft.com/ko-kr/library/2e06zxh0(v=vs.94).aspx)

```
const arrConcat = [1, 2, 3];
arrConcat.concat(4, 5, 6);  // [1, 2, 3, 4, 5, 6] arr은 바뀌지 않습니다.
```

### 8.2.3 배열 일부 가져오기

* slice() : 배열의 일부만 가져올 때 사용하고 두 개의 매개변수를 받을 수 있습니다.
  * 매개변수 1개만 사용하면 지정한 인덱스부터 배열의 마지막까지 값을 반환합니다.<br>
    매개변수 2개 모두 사용하는 경우 : 지정한 인덱스부터 배열부터 바로 앞의 인덱스 값을 반환합니다
  * slice()는 음수 인덱스를 사용할 수 있습니다.
  * 음수 인덱스를 사용하는 경우 : 배열의 끝에서부터 시작

```
const arrSlice = [1, 2, 3, 4, 5];
arrSlice.slice(2);                 // [3, 4, 5]
arrSlice.slice(1, 3);              // [2, 3]
arrSlice.slice(-1);                // [5]
arrSlice.slice(0, -2);             // [1, 2, 3]
arrSlice.slice(-3, 5);             // [3, 4, 5]
```

### 8.2.4 임의의 위치에서 요소 추가 / 제거

* splice() : 배열을 자유롭게 수정할 때 사용할 수 있습니다.

    * 매개변수는 첫 번째 수정을 시작할 인덱스, 두 번째는 배열을 제거 할 개수 입니다.<br>
      아무 요소도 제거를 하지 않는 경우 0을 넘깁니다.<br>
      나머지 매개변수는 배열에 추가될 요소입니다.

```
const arrSplice = [1, 4, 5];
arrSplice.splice(1, 0, 2, 3);       // [1, 2, 3, 4, 5]
arrSplice.splice(1, 3);             // [1, 5]
arrSplice.splice(0, 0, 'One', 2);   // ["One", 2, 1, 5]
```

### 8.2.5 배열 안에서 요소 교체

* copyWithin() : ES6에서 도입한 새로운 메서드 입니다.<br>
                 배열 요소를 복사해서 다른 위치에 붙혀넣고, 기존의 요소를 덮습니다.

    * 첫 번째 매개변수는 복사한 요소를 붙여넣을 위치,<br>
    * 두 번째 매개변수는 복사를 시작할 위치,<br>
    * 세 번째 매개변수는 복사를 끝낼 위치입니다.
    * copyWithin() 또한 음수 인덱스를 사용해 배열의 끝부터 셀 수 있습니다.

```
const arrCw = [1, 2, "Three", 4, 5];
arrCw.copyWithin(2, 4);                 // [1, 2, 5, 4, 5]

const arrCW1 = [1, 2, 3, 4, 5, 6, 7, 8, 9];
arrCW1.copyWithin(1, 3, 6);              // [1, 4, 5, 6, 5, 6, 7, 8, 9]
```

### 8.2.6 특정 값으로 배열 채우기

* fill() : copyWithin과 마찬가지로 fill 메서드도 ES6에서 새로 도입한 메서드 입니다.<br>
           배열의 시작 인덱스부터 마지막 인덱스까지 배열 요소를 채웁니다.

```
const arrFill = [1,2,3];
arrFill.fill(5);                // [5, 5, 5]
arrFill.fill(3, 1);             // [5, 3, 3]
arrFill.fill('C', 2, 5);        // [5, 3, "C"]
```

### 8.2.7 배열 정렬과 역순 정렬

* reverse() : 배열 요소의 순서를 반대로 바꿉니다

```
const arrReverse = [1, 3, 5, 2, 4];
arrReverse.reverse();                   // [4, 2, 5, 3, 1];
```

* sort() : 배열 요소의 순서를 정렬 합니다.

```
const arrSort = [4, 5, 1, 2, 4];
arrSort.sort();                   // [1, 2, 3, 4, 5];
```

객체가 들어있는 배열함수를 정렬하는 방법

```
const arrSort1 = [
    {name : "John"}, {name : "Jim"},
    {name : "Trevor"}, {name : "Amanda"},
]

arrSort1.sort();
arrSort1.sort((a, b) => a.name > b.name);
arrSort1.sort((a, b) => a.name[1] > b.name[1]);
```

## 8.3 배열 검색

* 배열안에서 요소를 검색하는 방법

1. indexOf() : 첫 번째 배열부터 검색을 하여 정확히 일치하는 첫 번째 인덱스를 반환합니다.
2. lastIndexOf() : 마지막 번째 배열부터 검색을 하여 정확히 일치하는 첫 번째 인덱스를 반환합니다.

```
const arrIdx = [1, 2, 3, 4, 1, 2, 3, 4];
arrIdx.indexOf(2);                         // 1
arrIdx.lastIndexOf(2);                     // 5
arrIdx.indexOf(2, 2);                      // 5
arrIdx.lastIndexOf(2, 2);                  // 1
```

3. findIndex() : 호출 함수에 지정된 테스트 조건을 충족하는 첫 번째 배열 요소의 인덱스 값을 반환합니다.

```
const arrFindIdx = [{id : 1, name : 'Apple'}, {id : 2, name : 'Banana'}];
arrFindIdx.findIndex(o => o.id == 2);              // 1
arrFindIdx.findIndex(o => o.name == 'Apple');      // 0
arrFindIdx.findIndex(o => o.id == 3);              // -1
arrFindIdx.findIndex(o => o.name == 'Melon');      // -1
```

4. find() : findIndex()는 해당하는 배열의 인덱스 값을 반환하지만 find()는 요소 자체를 반환합니다.

```
const arrFind = [{id : 1, name : 'Apple'}, {id : 2, name : 'Banana'}];
arrFind.find(o => o.id == 2);              // {id: 2, name: "Banana"}
arrFind.find(o => o.name == 'Apple');      // {id: 1, name: "Apple"}
arrFind.find(o => o.id == 3);              // undefined
```

5. some() : 조건에 맞는 요소를 찾으면 즉시 검색을 멈추고 true를 반환하고 찾지 못하는 경우 false값을 반환합니다.

```
const arrSome = [5, 16, 2, 47, 8];
arrSome.some(x => x%2 == 0);         // true
arrSome.some(x => x == 64);          // false
```

6. every() : 배열의 모든 요소가 조건에 맞아야 true를 반환하고 그렇지 않은 경우 false값을 반환합니다.

```
const arrEvery = [2, 4, 6, 8];
arrEvery.every(x => x%2 == 0);      //true
arrEvery.every(x => x%4 == 0);      //false
```

## 8.4 map과 filter

map과 filter는 배열 메서드 중 가장 유용한 메서드 입니다.

1. map 메서드는 배열 요소를 변형합니다.

* 일정한 배열의 형식을 변환

```
const person = [{name : "Koo", age : 15}, {name : "Joo", age : 20}];
const names = person.map(x => x.name);         // ["Koo", "Joo"]
const ages = person.map(x => x.age);           // [15, 20]
const agesPlus = ages.map(x => x+2);           // [17, 22]
```

* 두 배열을 객체로 결합

```
const names = ["Koo", "Joo"];
const ages = [15, 20];
const person = name.map((x, i) -> ({name : x, ages : age[i]}));     // [{"name":"Koo","age":15},{"name":"Joo","age":20}]
```

2. filter() : 콜백 함수에 지정된 조건을 충족하는 배열의 요소를 반환합니다.

```
const cards = [];
for(let suit of ['H', 'C', 'D', 'S']){
    for(let val = 1; val <=13; val++){
        cards.push({suit, val});
    }
}
cards.filter(c => c.val === 2);     // {
                                    //  {suit: "H", val : 2}
                                    //  {suit: "C", val : 2}
                                    //  {suit: "D", val : 2}
                                    //  {suit: "S", val : 2}
                                    // }

cards.filter(c => c.suit === "D");

cards.filter(c => c.val > 10);

cards.filter(c => c.val > 10 && c.suit === 'H');
```

## 8.5 reduce

- reduce() : 배열의 모든 요소에 대해 지정된 콜백을 호출합니다.<br>
  콜백 함수의 반환 값은 결과에 누적되며 다음 콜백 함수를 호출할 때 인수로 제공합니다.

```
const arrReduce1 = [1, 2, 3, 4];
const sum1 = arrReduce1.reduce((a, x) => a += x, 0);      // 10

const arrReduce2 = [1, 2, 3, 4];
const sum2 = arrReduce2.reduce((a, x) => a += x);         // 10
```

reduce는 보통 숫자나 문자열 같은 원시 값을 누적값으로 사용하지만, 객체 또한 누적값이 될 수 있습니다.

```
const words = ['Apple', 'Test', 'Str', 'Bee', 'Console', 'Hello', 'World'];

const word = words.reduce((a, x) => {
    if(!a[x[0]])
        a[x[0]] = [];
        a[x[0]].push(x);
        return a;
}, {});
```

## 8.6 문자열 병합

* join() : 배열의 문자열을 조합 할 경우 join()을 사용합니다.<br>
join() 매개변수로 구분자를 하나 받고 요소들을 하나로 합친 문자열을 반환합니다.<br>
Array.prototype.join의 기본값은 쉼표( , )입니다.

```
const arrStr = ['Chapter', null, false, 8, 'Array', true, undefined];
arrStr.join();              // Chapter,,false,8,Array,true,
arrStr.join('');            // Chapterfalse8Arraytrue
arrStr.join('|');           // Chapter||false|8|Array|true|
```