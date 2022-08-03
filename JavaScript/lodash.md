# lodash

배열, 객체, 숫자, 문자열 등을 보다 손쉽게 다룰 수 있게 해주는 라이브러리. 특히 배열, 객체, 문자열의 반복 / 값 조작 및 테스트 / 복합함수의 생성 등에 유용하다.

<br>

### Methods
- <a href="#find">_find / _.findIndex</a>
- <a href="#set">_.set</a>
- <a href="#cloneDeep">_.cloneDeep</a>

<br>

## <p id="find">_.find / _.findIndex</p>

```
_.find(collection, 'key'/조건을 나타낼 표현식)
```
key에 해당하는 요소를 반환하거나,
표현식이 true인 경우의 요소를 찾아 반환한다. (요소가 객체인 경우 요소 전체 반환)

```
private videoContents = [
  { type: 'video', title: 'vue', date: '2022-08-01' },
  { type: 'video', title: 'react', date: '2022-07-31' },
  { type: 'video', title: 'jQuery', date: '2022-07-30' }
];

_.find(contents, (item) => item.title === 'vue')
// {type: 'video', title: 'vue', date: '2022-08-01'}

_.find(contents, {type: 'video', date: '2022-07-31'})
// {type: 'video', title: 'react', date: '2022-07-31'}

_.find(contents, ['title', 'jQuery'])
// {type: 'video', title: 'jQuery', date: '2022-07-30'}

_.find(contents, 'title')
// {type: 'video', title: 'vue', date: '2022-08-01'}
// 두 번째 자리에 key 값만 쓰면 그에 해당하는 맨 처음 요소만 출력된다.
```

_.findIndex는 요소의 인덱스를 반환한다. _.find와 동일한 형태로 사용한다.

```
private videoContents = [
  { type: 'video', title: 'vue', date: '2022-08-01' },
  { type: 'video', title: 'react', date: '2022-07-31' },
  { type: 'video', title: 'jQuery', date: '2022-07-30' }
];

_.findIndex(contents, (item) => item.title === 'vue')
// 0

_.findIndex(contents, {type: 'video', date: '2022-07-31'})
// 1

_.findIndex(contents, ['title', 'jQuery'])
// 2

_.findIndex(contents, 'title')
// 0
```

----


## <p id="set">_.set()</p>

객체 내부의 특정 경로에 값을 설정하는 데 사용된다.

```
_.set(object, path, value)
```

- object: 내부 값을 바꿀 객체
- path: value를 설정할 경로(key)
- value: 설정할 값

_.set 메소드는 주어진 객체(object)를 수정하고 수정된 객체를 반환한다.
두 가지 용도로 쓰일 수 있는데, 객체 내부의 값을 변경하거나 새로운 값을 생성할 때 사용할 수 있다.

1. 값 변경

```
  const object = {
    'name': 'SooYeon',
    'education': {
      'school': {
        'name': 'OY high school',
        'yop': 2018
      }
    }
  }
  const path = 'education.school'
  const collegeEducation = {
    'name': 'HY-E university',
    'yop': 2023
  }

  console.log(_.set(this.object, this.path, this.collegeEducation))
```
<img src="../imgs/lodash_set.png">

path는 객체 내부의 key를 의미한다. name값을 변경하려면 path를 'name'으로 설정하면 되고, 객체 내부의 객체의 경우에도 위처럼 'education.school' 같은 형태로 사용하면 된다.

2. 값 추가

```
  const object = {
    'name': 'SooYeon',
    'education': {
      'school': {
        'name': 'OY high school',
        'yop': 2018
      }
    }
  }
  const path = 'education.school'
  const collegeEducation = {
    'name': 'HY-E university',
    'yop': 2023
  }

  console.log(_.set(this.object, this.path, this.collegeEducation))
```
<img src="../imgs/lodash_set_2.png">

path에 새로운 key값을 입력하면 된다.

---

## <p id="cloneDeep">_.cloneDeep()</p>

객체를 깊은 복사할 때 사용. 복사된 모든 값이 내부 자식 요소를 포함해 모두 새로운 값이 매핑되는 형태로 복사된다.

> 깊은 복사 (deep copy) : 독립적인 메모리에 값 자체를 할당하여 생성하는 것

- 깊은 복사가 필요한 이유: 객체나 배열을 복사하는 경우 복사하는 값은 원본을 참조한다.
```
  const obj = { val: 'a' }
  const newObj = this.obj;

  newObj.val = 'b'

  console.log(obj.val) // b
```

이는 데이터가 같은 값으로 새로 생성되는 것이 아니라 메모리 주소를 전달하여 결국 한 데이터를 공유하게 되기 때문에 발생한다.

<strong>cloneDeep</strong>
```
_cloneDeep(복사할 배열/객체)
```
얕은 복사가 되었던 위 코드를 cloneDeep을 사용해 다시 작성해보면 아래와 같다.
```
  const obj = { val: 'a' }
  const newObj = _.cloneDeep(obj)
  
  newObj.val = 'b'

  console.log(obj.val) // a
```

<strong>다른 방법과의 차이점</strong>

깊은 복사를 하는 방법은 cloneDeep 외에도 다양하다. 전개연산자, Object.assign 등이 있다. 하지만 이 방법들에는 문제가 있다.

```
  const obj = { 
    val: {
      a: 1
    }
   }
  const newObj = Object.assign({}, obj)
  // 전개연산자라면 { ...obj }
  
  newObj.val.a = 2

  console.log(obj) // { val: { a: 2 } }
```
2차원 객체에서 얕은복사가 일어났다.
반면 cloneDeep은 객체의 내부객체까지 깊은복사가 가능하다.

```
  const obj = { 
    val: {
      a: 1
    }
   }
  const newObj = _.cloneDeep(obj)
  
  newObj.val.a = 2

  console.log(obj) // { val: { a: 1 } }
```

---


<br>

## Reference

- lodash: https://lodash.com/
- lodash document: https://lodash.com/docs/4.17.15

