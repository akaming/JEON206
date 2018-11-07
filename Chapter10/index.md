# chapter10 : 맵과 셋 
맵은 키와 값을 연결한다는 점에서 객체와 비슷하고, 셋은 중복을 허용하지 않는다는 점만 제외하면 배열과 비슷하다.

## 10.1 맵
es6 이전에는 키와 값을 연결하려면 객체를 사용해야 했다. 하지만 객체를 이런 목적으로 사용하면 여러 가지 단점이 생긴다.
* 프로토타입 체인 때문에 의도하지 않은 연결이 생길 수 있다. 
    * [프로토타입 체인](https://goo.gl/LrMeeg){: target="_blank" } : 객체와 객체의 연결을 통한 단방향 공유 관계
* 객체 안에 연결된 키와 값이 몇 개나 되는지 쉽게 알아낼 수 있는 방법이 없다.
* 키는 반드시 문자열이나 심볼이어야 하므로 객체를 키로 써서 값과 연결할 수 없다.
* 객체는 프로퍼티 순서를 전혀 보장하지 않는다.

Map 객체는 이들 결함을 모두 해결했고, 키와 값을 연결할 목적이라면 (문자열만 키로 쓴다 해도) 객체보다 나은 선택이다.

1.사용자 객체가 여럿 있고 이들에게 각각 역할을 부여 한다고 해보자.
```
    const u1 = {name: 'Cynthia'};
    const u2 = {name: 'Jackson'};
    const u3 = {name: 'Olive'};
    const u4 = {name: 'James'}
```
2.맵을 만든다.
```
    const userRoles = new Map();
```
3.맵의 set() 메서드를 써서 사용자 역할을 할당한다.
```
    userRoles.set(u1, 'User');
    userRoles.set(u2, 'User');
    userRoles.set(u3, 'Admin');
    //애석하지만 제임스에게는 역할이 없다.
```
4.set() 메서든느 체인으로 연결할 수 있어서 타이핑하는 수고를 덜어 준다.
```
    userRoles
        .set(u1, 'User')
        .set(u2, 'User')
        .set(u3, 'Admin');
```
5.생성자에 배열의 배열을 넘기는 형태로 써도 된다.
```
    const userRoles = new Map([
        [u1, 'User'],
        [u2, 'User'],
        [u3, 'Admin']
    ]);
```
6.이제 u2의 역할을 알아볼 때는 get() 메서드를 쓰면 된다.
```
    userRoles.get(u2);      //"User"
```
7.맵에 존재하지 않는 키에 get을 호출하면 undefined를 반환한다. 맵에 키가 존재하는지 확인하는 has() 메서드도 있다.
```
    userRoles.has(u1);      //true
    userRoles.get(u1);      //"User"
    userRoles.has(u4);      //false
    userRoles.get(u4);      //undefined
```
8.맵에 이미 존재하는 키에 set()을 호출하면 값이 교체된다.
```
    userRoles.get(u1);          //'User'
    userRoles.set(u1,'Admin');
    userRoles.get(u1);          //'Admin'
```
9.size 프로퍼티는 맵의 요소 숫자를 반환한다.
```
    userRoles.size;         //3
```
10.keys() 메서드는 맵의 키를, values() 메서드는 값을, entries() 메서드는 첫 번째 요소가 키이고 두 번째 요소가 값인 배열을 각각 반환 한다. 이들 메서드가 반환 하는 것은 모두 이터러블 객체이므로 for...of 루프를 쓸 수 있다.
* [이터러블 객체](https://goo.gl/e5aUtY): [Symbol.iterator] 메소드를 구현하고 있고, 이터레이터 객체를 반환하는 객체
```
    for(let u of userRoles.keys())
        console.log(u.name);

    for(let u of userRoles.values())
        console.log(r);

    for(let u of userRoles.entries())
        console.log(`${ur[0].name}: ${ur[1]}`);
    
    //맵도 분해(destruct)할 수 있다.
    //위 코드는 다음과 같이 단축해서 쓸 수 있다.
    for(let [u,r] of userRoles)
        console.log(`${u.name}: ${r}`);
```
11.이터러블 객체보다 배열이 필요하다면 확산 연산자(spread operator)를 쓰면 된다.
```
    [...userRoles.values()];        //["User","User","Admin"]
```
12.맵의 요소를 지울 때는 delete() 메서드를 사용한다.
```
    userRoles.delete(u2);
    userRoles.size;         //2
```
13.맵의 요소를 모두 지울 때는 clear() 메서드를 사용한다.
```
    userRoles.clear();
    userRoles.size;         //0
```

## 10.2 위크맵
WeakMap은 다음 차이점을 제외하면 Map과 완전히 같다.
* 키는 반드시 객체여야 한다.
* WeakMap의 키는 [가비지 콜렉션](https://goo.gl/EWWHnZ)에 포함될 수 있다.
* WeakMap은 이터러블이 아니며 clear() 메서드도 없다.
