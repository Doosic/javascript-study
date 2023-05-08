# 함수와 일급객체

다음과 같은 조건들을 만족하는 객체를 일급 객체라 한다.
- 1.무명의 리터럴로 생성할 수 있다. 즉, 런타임에 생성이 가능하다.
- 2.변수나 자료구조(객체,배열 등)에 저장할 수 있다.
- 3.함수의 매개변수에 전달할 수 있다.
- 4.함수의 반환값으로 사용할 수 있다.

자바스크립트의 함수는 위의 모든 조건을 만족하므로 일급 객체다.

```
// 1.함수는 무명의 리터럴로 생성이 가능하다.
// 2.함수는 변수에 저장할 수 있다.
// 런타임(할당 단계)에 함수 리터럴이 평가되어 함수 객체가 생성되고 변수에 할당된다.
const increase = function (num) {
    return ++num;
};

// 2.함수는 객체에 저장할 수 있다.
const auxs = { increase };

// 3.함수의 매개변수에 전달할 수 있다.
// 4.함수의 반환값으로 사용할 수 있다.
function makeCounter(aux){
    let num = 0;
    
    return function () {
        new = aux(num);
        return num;
    };
}

// 3.함수는 매개변수에게 함수를 전달할 수 있다.
const increase = makeCounter(auxs.increase);
```

- 함수는 객체이지만 일반 객체와는 차이가 있다. 일반객체는 호출할 수 없지만 함수 객체는 호출이 가능하다. 그리고
  함수 객체는 일반 객체에는 없는 함수 고유의 프로퍼티를 소유한다.
<hr>

# 함수 객체의 프로퍼티

- 함수는 객체다. 따라서 함수도 프로퍼티를 가질 수 있다.

### arguments 프로퍼티

- arguments 프로퍼티 값은 arguments 객체다. arguments 객체는 함수 호출시 전달된 인수들의 정보를
  담고 있는 순회 가능한 유사 배열 객체이다. 함수 내부에서만 사용 가능하며 지역변수처럼 사용된다.
- arguments 객체는 인수를 프로퍼티 값으로 소유한다. 프로퍼티 키는 인수의 순서를 나타낸다.
- arguments 객체는 매개변수 개수를 확정할 수 없는 가변 인자 함수를 구현할 때 유용하다.

```
function sum() {
  let res = 0;
  
  // arguments 객체는 length 프로퍼티가 있는 유사 배열 객체이므로 for문으로 순회할 수 있다.
  for (let i = 0; i < arguments.length; i++){
    res += arguments[i];
  }
  
  return res;
}
```
- 유사 배열 객체는 배열이 아니므로 배열 메서드를 사용할 경우에는 에러가 발생한다. 따라서 배열에 데이터를 넣어
  간접 호출해야하는 번거로움이 발생한다. 따라서 ES6에서는 아래와 같이 Rest parameter를 사용하여 해결한다.

```
// ES6 Rest parameter
function sum(...args){
  return args.reduce((pre, cur) => pre + cur, 0);
}

console.log(sum(1, 2)); // 3
```

### length 프로퍼티

- 함수 객체의 length 프로퍼티는 함수를 정의할 때 선언한 매개변수의 개수를 가리킨다.

```
function foo(x, y){
  return x + y;
}

console.log(foo.length); // 2
```

- 주의할것은 arguments 객체의 length 프로퍼티와 함수 객체의 length 프로퍼티 값은 다를 수 있다.
- 함수 객체의 length는 매개변수의 개수를 가리킨다.
- arguments 객체의 length 프로퍼티는 인자의 개수를 가리킨다.(가변인자일 경우 동적)

### name 프로퍼티

- 함수 객체의 name 프로퍼티는 함수 이름을 나타낸다. es6에서 정식 표준이되었다. 있다는 것만 알아두자.
- 익명함수의 경우 es5에서는 name 프로퍼티는 빈 문자열이다. es6에서는 함수 객체를 가리키는 식별자를 값으로 갖는다.

```
var namedFunc = function foo() {};
console.log(namedFunc); // foo
```

### __proto__접근자 프로퍼티

- 모든 객체는 [[Prototype]]이라는 내부 슬롯을 갖는다. 해당 슬롯은 객체지향 프로그래밍의 상속을 구현하는
  프로토타입 객체를 가리킨다.
- __ proto __프로퍼티는 [[Prototype]] 내부 슬롯이 가리키는 프로토타입 객체에 접근하기 위해 사용하는 접근자다.
- [[Prototype]] 내부 슬롯은 직접 접근이 불가하여 __ proto __ 접근자 프로퍼티를 통해 간접적으로 접근한다.
- prototype 프로퍼티는 함수 객체만이 소유한다.