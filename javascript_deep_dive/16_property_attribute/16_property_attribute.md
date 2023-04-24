# 프로퍼티 어트리뷰트

- 프로퍼티와 어트리뷰트를 이해하기 위해서는 내부 슬롯과 내부 메서드의 개념을 알아야 한다.
  - 1.내부 슬롯과 내부 메서드는 자바스크립트 엔진의 구현 알고리즘을 설명하기 위해 사용하는
    의사 프로퍼티와 의사 메서드다.
  - 2.내부 슬롯과 내부 메서드는 자바스크립트 엔진에서 실제로 동작하지만 개발자가 직접 접근할 수 있도록
    공개된 프로퍼티는 아니다. 단 일부 내부 슬롯과 메서드에 한하여 접근할 수 있다.
  - 3.모든 객체는 [[Protorype]] 이라는 내부 슬롯을 갖는데 해당 슬롯에는 __proto__를 통해 접근이 가능하다.
```
const o = {};

o.[[Prototype]] // -> Uncaught SystaxError: ....

o.__proto__ // -> Object.protorype
```

## 프로퍼티 어트리뷰트와 프로퍼티 디스크립터 객체

- 자바스크립트 엔진은 프로퍼티를 생성할 때 프로퍼티의 상태를 나타내는 프로퍼티 어트리뷰트를 기본값으로 정의한다.
  - 1.프로퍼티의 값 [[Value]]
  - 2.값의 갱신 가능여부 [[Writable]]
  - 3.열거 가능 여부 [[Enumerable]]
  - 4.재정의 가능여부 [[Configurable]]
- 직접적인 접근을 불가능하지만 Object.getOwnPropertyDescriptor 메서드를 통하여 접근 가능하다.
```
const person = {
    name: 'Lee'
};

console.log(Object.getOwnPropertyDescriptor(person, 'name'));
// {value: "Lee", writable: true, enumerable: true, configurable: true}
```
- key, value 형태로 값을 전달해준다.
<hr>

## 데이터 프로퍼티와 접근자 프로퍼티

- 프로퍼티는 데이터 프로퍼티와 접근자 프로퍼티로 구분할 수 있다.
  - 1.데이터 프로퍼티
    - 키와 값으로 구성된 일반적인 프로퍼티다.
  - 2.접근자 프로퍼티
    - 자체적으로는 값을 갖지않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 호출되는 접근자 함수로 구성된 프로퍼티.
