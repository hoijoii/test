# enum

열거형. 이름이 있는 상수들의 집합을 정의할 수 있다. -> 의도를 문서화할 수 있고 구분되는 사례집합을 더 쉽게 만들 수 있다.
Typescript의 경우 숫자, 문자열 기반 열거형을 제공한다.

기존의 방법을 사용하여 상수들을 정의할 때 문자열, 숫자를 나타내는 string, number, static 등을 사용하는데 enum을 이용해서도 같은 효과를 낼 수 있다.

enum을 사용하는 이유는 간단하다. 기존의 방법을 사용했을 때 실수로 우리가 기대하는 값과 다른 값이 할당되었을 때 결과가 엉뚱하게 나타날 수 있는데, 컴파일 시에 문제를 감지하지 못하기 때문이다. 
하지만 enum을 통해 type을 지정해주면 기대하는 값과 다른 값이 할당될 경우 오류가 발생한다.

<br>

## 1. enum의 장점

- 코드가 단순해지고 가독성이 좋다.
- 인스턴스 생성, 상속을 방지해 상수값의 타입 안정성이 보장된다.
- <strong>새로운 상수들의 타입을 정의함으로써</strong> 정의된 타입 이외의 타입을 가진 데이터값을 컴파일 시 체크한다. (타입이 정의되는 집합이라는 점에서 interface와 비슷한데, interface는 key(변수)들과 그에 대한 변수 type들이 정의되어 있다. 반면 enum은 상수들의 집합이다.)
- 'enum' 키워드를 사용함으로써 구현의 의도가 열거임을 분명하게 알 수 있다.

<br>

## 2. enum의 사용

### 2-1. 숫자 열거형 (Numeric enums)
```
enum Direction {
  Up = 1,
  Down,
  Left,
  Right,
}
```

Up이 1로 초기화되면 그 아래 Down부터 2, 3, 4 자동으로 증가되는 값을 가진다. 물론 전부 초기화하지 않아도 된다.

```
enum Direction {
  Up,
  Down,
  Left,
  Right,
}
```
자동 증가 기능은 enum 멤버 자체와는 관련이 없지만 만약 enum 안에 같은 이름의 값이 있을 때 구별하는 데에 유용하다.

(ex)
```
enum UserResponse {
  No = 0,
  Yes = 1,
}
 
function respond(recipient: string, message: UserResponse): void {
  // ...
}
 
respond("Princess Caroline", UserResponse.Yes);
```
enum을 어떤 변수의 type으로 선언할 수 있다.

<br>

### 2-2. 문자열 열거형 (String enums)

각 멤버들을 문자열 리터럴, 혹은 다른 문자열 열거형의 멤버로 상수를 초기화시켜야 한다.
```
enum Direction {
  Up = "UP",
  Down = "DOWN",
  Left = "LEFT",
  Right = "RIGHT",
}
```
Numeric enums 처럼 자동 증가 기능은 없지만 serialize 한다는 이점이 있다. 숫자만으로는 어떤 유의미한 정보를 제공할 수 없으므로, string enums로 의미 있고 읽기 좋은 값을 전달할 수 있다. 

<br>

## Reference

- Typescript : https://www.typescriptlang.org/ko/docs/handbook/enums.html
