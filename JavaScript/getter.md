# getter

getter는 accessor property이다.

> accessor property: property를 읽거나 쓸 때 호출하는 함수를, 값 대신에 지정할 수 있다. getter, setter가 있고 값을 각각 get, set하는 역할. property 값을 객체 바깥에서 읽거나 쓸 수 있게 해준다.

```
get prop() { /* ... */ }
```
prop은 주어진 함수에 바인딩하기 위한 속성의 이름을 말한다.
get 구문은 클래스 바깥에서 내부에 있는 메소드 혹은 변수를 조회할 때 사용한다.
하지만 get을 사용하지 않아도 외부 클래스에 있는 메소드/변수 조회는 가능하다. 그렇다면 왜 get을 사용하는 것일까?

<br>

## 1. getter 사용 이유

- 동적으로 계산된 값을 반환하는 프로퍼티가 필요할 때 (getter는 종속성(dependency)이 변경될 때 실행된다.)
- 명시적 함수 호출 없이 객체의 내부 변수 상태를 반영하는 값을 나타내고 싶은 경우(일반 프로퍼티처럼 사용하기 때문)

<br>

## 2. getter의 특징

- get을 떼면 method지만 마치 property처럼 접근한다.
```
const obj = {
  name: ['Soo-Yeon', 'Kim'],
  get firstName() {
    return this.name[0]
  }

  console.log(obj.firstName) // "Soo-Yeon"
  console.log(obj.firstName()) // firstName is not a function
}
```
만약 get을 사용하지 않는다면 그냥 일반 메소드가 된다. 이때는 두번째 콘솔 출력처럼 obj.firstName()으로 이 메소드를 호출할 수 있다.
- getter를 처음 호출할 때 계산하는 동시에 캐싱된다. -> 추가 접근 시 캐시에서 값을 즉시 반환하므로 값을 다시 계산하지 않을 수 있다.

<br>

## 3. 일반 메소드와 getter

일반 메소드보다 getter를 사용하는 것이 좋은 경우가 있다.
바로 '캐싱' 때문이다. 

> 캐싱(caching) : 사용자가 자주 사용하는 프로그램에 대한 데이터를 미리 메모리 영역에 대기시킴. 

다음 상황에서는 일반 메소드보다 getter를 추천한다.

- 값의 계산 비용이 큰 경우
- 절대 바뀌지 않는 값이나 다시 계산해서는 안 되는 값을 여러 번 사용하는 경우
	- 주의: 변화할 수 있는 값에 getter를 사용하면 안 됨. 값이 바뀌어야 하는 상황에서도 접근자의 값이 항상 동일할 것이기 때문..

일반 메소드는 화면의 UI가 바뀔 때마다 계산된다는 점을 생각해보면 위같은 상황에서는 좋은 선택이 아니다.

값이 지금 당장은 필요하지 않은 경우(나중에 사용할 수 있고, 아예 사용하지 않을 수도 있는 경우)에도 getter를 사용하면 좋다. getter는 객체에 속성을 정의하되 접근 전에는 계산하지 않을 수 있기 때문이다. 

<br>

## Reference

- MDN : https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/get
- Javascript Info : https://ko.javascript.info/property-accessors
- stack overflow : https://stackoverflow.com/questions/73076259/why-use-getter-for-functions-that-use-moment-js-vuejs-typescript

