# 타입 변환과 단축 평가

## 타입 변환이란?

- 자바스크립트의 모든 값은 타입이있다.
- 개발자가 의도적으로 값의 타입을 변환하는 것을 명시적 타입 변환 또는 타입 캐스팅이라 한다.
```
var x = 10;

// 명시적 타입변환 숫자 => 문자
var str = x.toString();

console.log(x); // '10'
```
- 개발자의 의도와는 상관없이 **표현식을 평가하는 도중에 자바스크립트 엔진에 의해 암묵적으로 타입이 변환되기도 한다
  이를 암묵적 타입변환 또는 타입 강제 변환이라 한다.**
- 명시적 타입 변환이나 암묵적 타입변환이 기존 원시 값을 직접 변경하는 것은 아니다. 원시값은 변경 불가능한 값이므로
  변경할 수 없다. **타입 변환이란 기존 원시 값을 사용해 다른 타입의 새로운 원시 값을 생성하는 것이다.**
- 명시적 타입변환은 개발자가 타입을 변경하겠다는 의지가 드러나지만 암묵적 타입변환은 자바스크립트 엔진에 의해 변경되므로
  어떤 타입의 값으로 변환되는지, 그리고 변환된 값으로 표현식이 어떻게 평가될 것인지 예측 가능해야한다.
<hr>

## 암묵적 타입 변환

- 자바스크립트 엔진은 표현식을 평가할 때 **개발자의 의도와는 상관없이 코드의 문맥을 고려해 암묵적으로 데이터 타입을
  강제 변환할 때가 있다.**
```
// 피연산자가 모두 문자열 타입이어야 하는 문맥
'10' + 2 // '102'

// 피연산자가 모두 숫자 타입이어야 하는 문맥
5 * '10' // 50

// 피연산자 또는 표현식이 불리언 타입이어야 하는 문맥
!0 // true
```
- 코드의 문맥에 부합하지 않는 다양한 상황이 발생할 수 있다. 이때 프로그래밍 언어에 따라 에러를 발생시키기도 하지만
  자바스크립트는 가급적 에러를 발생시키지 않도록 암묵적 타입변환을 통해 표현식을 평가한다.

### 문자열 타입으로 변환
```
1 + '2' // "12"
```
- 자바스크립트 엔진은 **문자열 연결 연산자 표현식**을 평가하기 위해 문자열 연결 연산자의 피연산자 중에서
  문자열 타입이 아닌 피연산자를 문자열 타입으로 암묵적 타입 변환한다.
- 우리가 개발을 하다보면 흔히 보는게 있다. 바로 "[object Object]" 라는것이다.
  해당 문자열은 객체를 문자열로 타입변환시 저렇게 된다.
```
({}) + '' // "[object Object]"
[10, 20] + '' // "10,20"
Array + '' // "function Array() { [native code] }"
```

### 숫자 타입으로 변환
```
1 - '1' // 0
1 * '10' // 10
1 / 'one' // NaN
```
- 자바스크립트 엔진은 **산술 연산자 표현식**을 평가하기 위해 산술 연산자의 피연산자 중에서 숫자 타입이 아닌 피연산자를
  숫자 타입으로 암묵적 타입 변환한다. 이때 피연산자를 숫자로 타입변환이 불가능할 경우 NaN을 반환한다.
- 비교 연산자 ('>' , '<') 들의 역할은 불리언 값을 만드는 것이다. '>' 비교 연산자는 피연산자의 크기를 비교하므로
  문맥상 모두 숫자 타입이어야 한다. 그렇기에 숫자 타입이 아닌 피연산자를 숫자 타입으로 암묵적 타입 변환을 한다.

### 불리언 타입으로 변환

- if문이나 for 문과 같은 제어문 또는 삼항 조건 연산자의 조건식은 불리언 값, 즉 논리적 참/거짓으로 평가되어야 하는 표현식이다.
  자바스크립트 엔진은 조건식의 평가 결과를 불리언 타입으로 암묵적 타입 변환 한다.
- 이때 **자바스크립트 엔진은 불리언 타입이 아닌 값을 Truthy 값(참으로 평가되는 값) 또는 Falsy 값(거짓으로 평가되는 값)으로 구분한다.**
- 즉, 제어문의 조건식과 같이 불리언 값으로 평가되어야 할 문맥에서 Truthy는 true로, Falsy 값은 false로 암묵적 타입 변환된다.
- 아래는 Falsy로 평가되는 모든 값들이다.
```
- false
- undefined
- null
- 0, -0
- NaN
- '' (빈 문자열)
```
- Falsy 값 외의 모든 값은 모두 true로 평가되는 Truthy 값이다.
<hr>

## 명시적 타입 변환

- 명시적 타입 변환이란 개발자의 의도에 따라 타입을 변경하는 것이다.
- 표준 빌트인 생성자 함수와 표준 빌트인 메서드는 자바스크립트에서 기본 제공하는 함수다.

### 문자열 타입으로 변환

- 문자열 타입이 아닌 값을 문자열 타입으로 변환하는 방법
  - 1.String 생성자 함수를 new 연산자 없이 호출하는 방법
  - 2.Object.prototype.toString 메서드를 사용하는 방법
  - 3.문자열 연결 연산자를 이용하는 방법
```
// 1.String 생성자 함수를 new 연산자 없이 호출하는 방법
String(1);  // "1"
// 2.Object.prototype.toString 메서드를 사용하는 방법
(1).toString();  // "1"
// 3.문자열 연결 연산자를 이용하는 방법
1 + '';  // "1"
```

### 숫자 타입으로 변환

- 숫자 타입이 아닌 값을 숫자 타입으로 변환하는 방법
  - 1.Number 생성자 함수를 new 연산자 없이 호출하는 방법
  - 2.parseInt, parseFloat 함수를 사용하는 방법
  - 3.'+' 단항 산술 연산자를 이용하는 방법
  - 4.'*' 산술 연산자를 이용하는 방법
```
// 1.Number 생성자 함수를 new 연산자 없이 호출하는 방법
Number('0')  // 0
// 2.parseInt, parseFloat 함수를 사용하는 방법
parseInt('0')  // 0
// 3.'+' 단항 산술 연산자를 이용하는 방법
+ '0'  // 0
// 4.'*' 산술 연산자를 이용하는 방법
'0' * 1;  // 0
```

### 불리언 타입으로 변환

- 불리언 타입이 아닌 값을 불리언 타입으로 변환하는 방법
  - 1.Boolean 생성자 함수를 new 연산자 없이 호출하는 방법
  - 2.! 부정논리 연산자를 두 번 사용하는 방법
```
// 1.Boolean 생성자 함수를 new 연산자 없이 호출하는 방법
Boolean('x') // true
// 2.! 부정논리 연산자를 두 번 사용하는 방법
!!'x' // true
```
<hr>

## 단축평가

### 논리 연산자를 사용한 단축 평가

- 논리합(||) 또는 논리곱(&&) 연산자 표현식의 평가 결과는 **불리언이 아닐수도 있다** 논리합 또는 논리곱 연산자 표현식은
  언제나 2개의 피연산자 중 어느 한쪽으로 평가된다라는 것이다.
- 논리합 연산자와 논리곱 연산자는 논리 연산의 결과를 결정하는 피연산자를 타입 변환하지 않고 그대로 반환한다.
  이를 **단축 평가(short-circuit evaluation)라고 한다. 단축 평가는 표현식을 평가하는 도중에 평가 결과가 확정된 경우
  나머지 평가 과정을 생략하는 것을 말한다.**

| 단축 평가 표현식         | 평가 결과    |
|:------------------|:---------|
| true 또는 anything  | true     |
| false 또는 anything | anything |
| true && anything  | anything |
| false && anything | false    |

```
// 논리합(||) 연산자
'Cat' || 'Dog' // "Cat"
false || 'Dog' // "Dog"
'Dog' || false // "Dog"

// 논리곱(&&) 연산자
'Cat' && 'Dog' // "Dog"
false && 'Dog' // false
'Cat' && false // false
```

- 객체를 가리키기를 기대하는 변수가 null 또는 undefined가 아닌지 확인하고 프로퍼티를 참조할 때
```
var elem = null;
// elem이 null이나 undefined와 같은 Falsy 값이면 elem으로 평가되고
// elem이 Truthy 값이면 elem.value로 평가된다.
// 단축평가를 이용한 객체 null 방지
var value = elem && elem.value; // null
```

### 옵셔널 체이닝 연산자
- ES11에서 도입된 옵셔널 체이닝 연산자 ?.는 좌항의 피연산자가 null또는 undefined인 경우 undefined를 반환하고
  그렇지 않으면 우항의 프로퍼티 참조를 이어간다.

### null 병합 연산자
- ES11에서 도입된 null 병합 연산자 ??는 좌항의 피연산자가 null또는 undefined인 경우 우항의 피연산자를 반환하고
  그렇지 않으면 좌항의 피연산자를 반환한다. 변수에 기본값을 설정할 때 유용하다
```
var foo = null ?? 'default string';
console.log(foo); // 'default string'
```
- 다만 Falsy 값인 '', 0 들은 조심하자 null이 아닌 false로 평가된다.
