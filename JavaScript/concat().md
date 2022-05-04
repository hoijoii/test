# concat() : 배열 / 문자열 합치기

concat()은 두 개 이상의 배열/문자열을 연결하여 새로운 배열/문자열을 반환할 때 사용하는 메소드입니다. (새롭게 반환하는 것이 아니라 기존 배열에 원소를 추가하기만 하는 'push'와는 다릅니다.)

concat은 배열과 문자열 말고도 Number, Boolean 등에도 사용할 수 있습니다.

<br />

## 1. 배열 합치기

```
array1.concat(array2, array3, ... , arrayX)
```

array1 뒤에 array2, array3, ... , arrayX가 차례로 추가되어 새로운 배열 객체가 반환됩니다. 물론 원본 배열은 바뀌지 않습니다.
이때 원본 배열과 새로운 배열은 <b>독립적</b>입니다.

만약 인자를 생략한다면 원본 배열의 얕은 복사로 인한 얕은 사본을 반환하게 될 것입니다.

> ▸ 얕은 복사: 배열을 복사했을 때 이 배열에 독립적이지 않은 사본이 만들어진다. 이 사본은 원본 배열을 참조하며, 원본이 변경되면 사본도 변형된다. <br>
> ▸ 깊은 복사: 배열을 복사했을 때 두 배열이 독립적이다.

```
//두 개의 배열 합치기
const arr1 = ['a', 'b', 'c'];
const arr2 = ['d', 'e', 'f'];
const conArr = arr1.concat(arr2);
//conArr = ['a', 'b', 'c', 'd', 'e', 'f']

//세 개의 배열 합치기
const arr1 = ['a', 'b', 'c'];
const arr2 = ['d', 'e', 'f'];
const arr3 = ['g', 'h', 'i'];
const conArr = arr1.concat(arr2, arr3);
//conArr = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i']

//배열에 값을 이어붙이기
const arr = ['a', 'b', 'c'];
arr.concat(1, [2, 3])
//결과: ['a', 'b', 'c', 1, 2, 3]
```

<br>

## 2. 문자열 합치기

concat은 배열이 아닌 문자열을 합칠 때에도 유용하게 사용됩니다.

```
string1.concat(string2, string3, ... , stringN)
```

배열에서 그랬던 것처럼, string2, 3, ... N은 string1의 뒤에 붙여져서 새로운 문자열이 반환될 것입니다.

```
const string1 = "Hello, "
const string2 = "Developer!"

string1.concat(string2)
//결과: Hello, Developer!
```

물론 빈 문자열에도 붙일 수 있습니다.

```
''.concat(string1, string2)
''.concat('Hello, ', 'Developer!')
//결과: Hello, Developer!
```

하지만 붙일 문자열이 적거나 문자열이 짧은 경우에는 '+'를 사용하여 문자열을 붙이는 편이 더 좋을 것 같습니다.

```
// + 사용해서 문자열 붙이기
const string3 = string1 + string2
console.log(string3)

// 문자열 직접 붙이기
const string3 = 'Hello, ' + 'Developer!'
```

'+'를 사용했을 때에도, 원본 문자열이 바뀐다고 해서 사본 문자열이 바뀌지 않습니다.

<br>

## Reference

- Tech on the Net(javascript) : https://www.techonthenet.com/js/string_concat.php
- W3Schools(javascript) : https://www.w3schools.com/jsref/jsref_concat_array.asp
