# 불리언과 관련 연산자

- == 둘의 값이 같아야한다.(타입은 암묵적으로 동일하게 타입케스팅이 된다)
- != 둘의 값이 달라야 한다.(타입은 암묵적으로 동일하게 타입케스팅된다)
- === 둘의 값과 타입이 같아야 한다.
- !== 둘의 값과 타입이 달라야 한다.
- && 둘의 조건이 같아야 한다. true && true
- || 둘중 하나만 만족하면 된다 true || false, true || true

## 단축평가 short circuit

- &&: 앞의 것이 false면 뒤의 것을 평가할 필요 없음
- ||: 앞의 것이 true면 뒤의 것을 평가할 필요 없음
- 평가는 곧 실행 - 이 점을 이용한 간결한 코드
- 연산 부하가 적은 코드를 앞에두는 것이 좋다!!! - 리소스 절약

ex) &&은 앞의것이 true일때만 뒤의 코드를 실행한다. 왜냐하면 둘다 true를 만족시켜야 하는데 앞의것이 false라면
조건을 만족하지 못하기 때문에 뒤의것은 실행조차 하지 않는 것이다.

ex) ||는 앞의것이 false일때만 뒤의 코드를 실행한다. 왜냐하면 둘중 하나만 true를 만족시키면 되기 때문에 뒤의 것을
굳이 계산하지 않아도 되기 때문이다.

### 삼항연산자

- const gender = userGender === 'M'? 'MAN' : 'GIRL';

#### Truthy vs Falsy (boolean이 아닌 값들이 true 또는 false로 평가되는 값들)

- 1.23 ? true : false;
- -999 ? true : false;
- '0' ? true : false;
- ' ' ? true : false;
- Infinity ? true : false;
- -Infinity ? true : false;
- {} ? true : false;
- [] ? true : false;
- 위의 값들은 모두 true가 나온다. (NaN 제외)

let x = 2;
let y = 3;
ex) x % 2 ? '홀' : '짝'; x를 2로 나누면 0이되고 0은 Falsy다.
ex) y % 2 ? '홀' : '짝'; y를 2로 나누면 1이되고 1은 Truthy이다.

- 이것들을 확실히 하는 방법은
  !!1, !!0과 같은 방법으로 2번 부정하여 확실하게 true 또는 false를 사용한다.
