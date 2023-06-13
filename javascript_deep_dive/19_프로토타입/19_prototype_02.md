## 프로토타입의 생성 시점

 - 객체는 리터럴 표기법 또는 생성자 함수에 의해 생성되므로 결국 모든 객체는 생성자 함수와 연결되어있다.
 - 프로토타입은 생성자 함수가 생성되는 시점에 더불어 생성된다.
 - 생성자 함수는 사용자가 직접 정의한 사용자 정의 생성자 함수와 자바스크립트가 기본 제공하는 빌트인 생성자 함수로
  구분할 수 있다.

### 사용자 정의 생성자 함수와 프로토타입 생성 시점

- 생성자 함수인 constructor은 함수 정의가 평가되어 함수 객체를 생성하는 시점에 프로토타입도 더불어
  생성된다.

```
// 함수 정의(constructor)가 평가되어 함수 객체를 생성하는 시점에 프로토타입도 더불어 생성된다.
console.log(Person.prototype); // {constructor: f}

// 생성자 함수
function Person(name) {
  this.name = name;
}

// non-constructor인 애로우펑션은 프로토타입이 생성되지 않는다.
const Person = name => {
  this.name = name;
};

console.log(Person.prototype); // undefined
```

- 생성된 프로토타입은 오직 constructor 프로퍼티만을 갖는 객체다. 프로토타입도 객체이고 모든 객체는
  프로토타입을 가지므로 프로토타입도 자신의 프로토타입을 갖는다. 생성된 프로토타입의 프로토타입은 Object.prototype이다.
- 이처럼 빌트인 생성자 함수가 아닌 사용자 정의 생성자 함수는 자신이 평가되어 함수 객체로 생성되는 시점에 프로토타입도 더불어 생성되며,
  생성된 프로토타입의 프로토타입은 언제나 Object.prototype이다.

### 전역 객체

- 전역 객체는 코드가 실행되기 이전 단계에 자바스크립트 엔진에 의해 생성되는 특수한 객체다. 전역 객체는 클라이언트 사이드 환경에서는
  window, 서버 사이드 환경에서는 global 객체를 의미한다.
- 객체가 생성되기 이전부터 생성자 함수와 프로토타입은 이미 객체화되어 존재한다. 이후 생성자 함수 또는 리터럴 표기법으로 객체를 생성시 프로토타입은
  생성된 객체의 [[Prototype]] 내부 슬롯에 할당된다.

## 프로토타입 체인

```
function Person(name){
  this.name = name;
}

// 프로토타입 메서드
Person.prototype.sayHello = function () {
  console.log(`Hi, My name is ${this.name}`);
};

const me = new Person('Lee');

// hasOwnProperty는 Object.prototype의 메서드다.
console.log(me.hasOwnProperty('name')); // true 
```
person 생성자 함수에 의해 생성된 me 객체는 Object.prototype의 메서드인 hasOwnProperty를 호출할 수 있다.
이는 me 객체가 Person.prototype 뿐만 아니라 Object.prototype도 상속받았다는 것으 의미한다.

프로토타입의 프로토타입은 언제나 Object.prototype이다.
<img src="https://github.com/Doosic/javascript-study/assets/82255957/230344e2-2dcf-454a-8d57-39953d6d23d4" width="400" height="250"/>

자바스크립트의 객체의 프로퍼티에 접근 할 때 해당 객체에 접근하려는 프로퍼티가 없다면 [[Prototype]] 내부 슬롯의 참조를 따라 자신의 부모 역할을 하는
프로토타입의 프로퍼티를 순차적으로 검색하여 접근한다. 이를 프로토타입 체인이라고 한다. 프로토타입 체인은 자바스크립트가
객체지향 프로그래밍의 상속을 구현하는 메커니즘이다.


