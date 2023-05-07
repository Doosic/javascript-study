# 생성자 함수에 의한 객체 생성

- 객체 생성방법은 다양하다. 그 중 객체 리터럴을 사용하여 객체를 생성하는 방식과
  생성자 함수를 사용하여 객체를 생성하는 방식의 장단점을 알아보자

## Object 생성자 함수

- new 연산자와 함께 Object 생성자 함수를 호출하면 빈 객체를 생성하여 반환한다.
  빈 객체를 생성한 이후 프로퍼티 또는 메서드를 추가하여 객체를 완성할 수 있다.

```
// 빈 객체 생성
const person = new Object();

// 프로퍼티 추가
person.name = 'Lee';
person.sayHello = function () {
    console.log(`Hi ${this.name}`)
};
```
- 생성자 함수란 new 연산자와 함께 호출하여 객체(인스턴스)를 생성하는 함수이다.
- 생성자 함수에 의해 생성된 객체를 인스턴스라 한다.
```
// 자바스크립트가 제공하는 빌트인(기본내장) 생성자 함수
new String();
new Number();
new Boolean();
new Function();
new Array();
new RegExp();
new Date();
```
- 빌트인 생성자 함수는 많지만 자바스크립트에서는 반드시 생성자 함수를 이용해서 변수를 만들지
  않아도 된다. 리터럴을 사용하는 방법이 더 간편하다.
<hr>

## 생성자 함수

### 객체 리터럴에 의한 객체 생성 방식의 문제점

- 객체 리터럴에 의한 객체 생성 방식은 간단하다. 그러나 문제점은 단 하나의 객체만 생성된다는 것이다.
- 따라서 동일한 프로퍼티를 갖는 객체를 여러개 생성해야 하는 경우 매번 같은 프로퍼티를 기술해야 하기 때문에 비효율적이다.
- 동일한 프로퍼티를 갖는 수십 개의 객체를 생성해야 할때 문제가 크다.


### 생성자 함수에 의한 객체 생성 방식의 장점

- 생성자 함수를 이용한다면 클래스처럼 프로퍼티 구조가 동일한 객체 여러개를 간편하게 생성할 수 있다.
```
function Cirlce(radius){
  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };
}

// 인스턴스의 생성
const circle1 = new Circle(5);
const circle2 = new Circle(10);
```
#### this
| 함수 호출 방식    | this가 가리키는 값(this 바인딩) |
|:------------|:-----------------------|
| 일반 함수로서 호출  | 전역 객체                  |
| 메서드로서 호출    | 메서드를 호출한 객체(마침표 앞의 객체) |
| 생성자 함수로서 호출 | 생성자 함수가 (미래에) 생성할 인스턴스 |

```
function foo() {
  console.log(this);
}

// 일반적인 함수로써의 호출
// 전역 객체는 브라우저 환경에서는 window, Node.js 환경에서는 global을 가리킨다.
foo(); // window

const obj = { foo: this };
// 메서드로써의 호출
obj.foo();

// 생성자 함수로서 호출
const inst = new foo(); // inst
```
- 생성자 함수는 이름 그대로 객체(인스턴스)를 생성하는 함수다.
- new 연산자와 함께 호출하면 해당 함수는 생성자 함수로 동작한다.

### 생성자 함수의 인스턴스 생성 과정

- 생성자 함수의 역할은 프로퍼티 구조가 동일한 인스턴스를 생성하기 위한 탬플릿으로서 동작하여 인스턴스를 생성하는 것과
  생성된 인스턴스를 초기화(프로퍼티 추가 및 초기값 할당)하는 것이다.
```
// 생성자 함수
function Circle(radius) {
  // 인스턴스 초기화
  this.radius = radius;
  this.getDiameter = function() {
    return 2 * this.radius;
  };
}

// 인스턴스 생성
const circle1 = new Circle(5);
```
- 위의 코드를 보면 this.에 프로퍼티를 추가하고 필요에 따라 전달된 인수를 프로퍼티의 초기값으로서
  할당하여 인스턴스를 초기화한다.
- 이때 인스턴스를 생성하고 반환하는 코드는 보이지 않는다. 이유는 자바스크립트엔진이 암묵적인 처리를 통해
  인스턴스를 생성하고 반환하기 때문이다.

#### 인스턴스 생성과 this 바인딩

- 바인딩이란 식별자와 값을 연결하는 과정을 의미한다. 변수 선언은 변수 이름(식별자)과 확보된 메모리 공간의 주소를 바인딩하는 것이다.
```
function Circle(radius) {
  // 1.암묵적으로 인스턴스가 생성되고 this에 바인딩된다.
  console.log(this); // Circle {}
  
  // 2.this에 바인딩되어 있는 인스턴스를 초기화한다.
  this.radius = radius;
}
```

#### 인스턴스 초기화

- 생성자 함수에 기술되어 있는 코드가 한 줄씩 실행되어 this에 바인딩되어 있는 인스턴스를 초기화한다.
- 전달받은 인자값으로도 초기화가 가능하다.

#### 인스턴스 반환

- 인스턴스 반환은 내부의 모든 처리가 끝나면 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환된다.
- 만약 명시적으로 this가 아닌 다른 객체를 반환한다면 this가 아닌 명시해둔것이 반환된다.

#### 생성자 함수의 기본동작 요약

- 1.암묵적으로 빈 객체 생성후 this에 바인딩
- 2.인수값을 이용해 this에 바인딩된 인스턴스 초기화
- 3.명시된 반환이 없을시 암묵적으로 this 반환
<hr>

## 내부 메서드 [[Call]]과 [[Construct]]

- construct는 non-constructor과 constructor로 나뉜다.
- non-constructor: 일반 함수로서만 호출할 수 있는 객체
- constructor: 일반 함수 또는 생성자 함수로써 호출할 수 있는 객체

### constructor와 non-constructor의 구분

- 자바스크립트 엔진은 함수 정의를 평가하여 함수 객체를 생성할 때 함수 정의 방식에 따라
  constructor와 non-constructor를 구분한다.
  - constructor: 함수 선언문, 함수 표현식, 클래스
  - non-constructor: 메서드, 화살표 함수
```
// 일반 함수 정의: 함수 선언문, 함수 표현식
function foo() {}
const bar = function() {};

// 화살표 함수 정의
const arrow = () => {};

// 메서드 정의: ES6의 메서드 축약 표현만 메서드로 인정한다.
const obj = {
  x() {}
};

new obj.x(); // TypeError: obj.x is not a constructor
```
- 함수 선언문과 함수 표현식으로 정의된 함수만이 constructor이고 ES6의 화살표 함수의 메서드 축약 표현으로
  정의된 함수는 non-constructor이다.

### new 연산자

- 일반 함수와 생성자 함수에 특별한 형식적 차이는 없다. new 연산자와 함께 함수를 호출하면 해당 함수는 생성자
  함수로 동작한다. 단 new 연산자와 함께 호출하는 함수는 non-constructor가 아닌 constructor 이어야 한다.
```
function Circle(radius){
  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };
}

// new 연산자 없이 생성자 함수 호출하면 일반 함수로서 호출된다.
const circle = Circle(5);

// 일반 함수 내부의 this는 전역 객체 window를 가리킨다.
console.log(radius); // 5
console.log(getDiameter()); // 10

circle.getDiameter(); // TypeError: Cannot read property 'getDiameter' of undefined
```

- Circle 함수를 new 연산자와 함께 생성자 함수로써 호출하면 함수 내부의 this는 Circle 생성자 함수가 생성할 인스턴스를
  가리킨다. 하지만 circle 함수를 일반적인 함수로서 호출하면 함수 내부의 this는 전역 객체 window를 가리킨다.

### new.target

- new 연산자와 함께 생성자 함수로서 호출되면 함수 내부의 new.target은 함수 자신을 가리킨다.
  new 연산자 없이 일반 함수로서 호출된 함수 내부의 new.target은 undefined다.
- new 연산자 없이 호출했을 경우 생성자 함수를 재귀 호출을 통해 생성자 함수로서 호출할 수 있다.

```
// 생성자 함수
function Circle(radius) {
  // 이 함수가 new 연산자와 함께 호출되지 않았다면 new.target은 undefined다. falsy
  if (!new.target) {
    // new 연산자와 함께 생성자 함수를 재귀 호출하여 생성된 인스턴스를 반환한다.
    return new Circle(radius);
  }
  
  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };
}
```

- 재귀 호출을 통해 new 연산자 없이 생성자 함수를 호출해도 new.target을 통해 생성자 함수로써 호출가능
- new.target 은 ES6에서 도입된 최신 문법으로 IE에서는 지원하지 않는다. 이때는 스코프 세이프 생성자 패턴을 사용하자.
- 별거없다. new.target을 if(!(this instanceof Circle))로 변경할뿐이다.