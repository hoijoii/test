# Data Binding

```
{{ dataBinding }}
```
Javascript 데이터를 Vue의 Template Syntax(HTML 코드)에서 사용할 수 있게 해준다.  
데이터 바인딩은 Vue의 핵심적인 장점들을 가지고 있다고 볼 수 있다. 바로 '선언적 렌더링(Declarative Rendering)'과 '반응성(Reactivity)'을 보여주기 때문이다! Vue가 React보다 쉽다고 여겨지는 이유 중 하나일 것이다. 아래에서 자세히 알아보자.

<br>

## 1. Data Binding 사용법

#### 1-1. template에서 데이터 출력( {{ }} )
```
<!-- HomeView.vue -->
<template>
  <div>
    <!-- data() 안에 있는 데이터를 {{ }} 에 넣어 출력 -->
    <p>{{ message }}</p>
  </div>
</template>
<script>
export default {
  name: 'HomeView',
  data(){
    return {
        //여기에 html에서 쓸 모든 데이터들을 저장
        //object형태로 작성
        message : 'Hello World',
    },
  },
}
</script>
```
script의 data() 함수 리턴값인 데이터들을 template 코드에서 {{}} 표현을 통해 화면에 나타낼 수 있다. 
만약 data() 안의 데이터가 바뀐다면 화면에 나타나는 값도 실시간으로 바뀐다. template에 하드코딩하는 것보다 data() 안에서 데이터들을 관리할 수 있어 유지보수성이 좋다.

위 코드의 경우 화면에 'Hello World'가 출력된다. 

 사실 위 코드는 Vue의 두 가지 핵심 중 하나인 선언적 렌더링의 예시로도 많이 활용되는 형태의 예제다.

> 선언적 렌더링(Declarative Rendering): Template 구문을 이용해 데이터를 DOM에 렌더링하는 것.

위 설명이 이해되지 않을 수 있다. 선언적 렌더링은 DOM을 렌더링하는 방식 중 하나로 볼 수 있다.

Javascript는 DOM을 만들기 위해 명령적 렌더링(Imperative Rendering)을 한다. 간단히 설명하면 데이터, element에 대해 루프를 돌며 element를 조립해 상위 element에 끼워넣는 방식이다. 트리를 만들어야 하니까. 

문제는 데이터가 많아질 때 조립해야 하는 것이 많아지며 코드가 중복되고 복잡해진다는 점이다. (forEach를 엄청 사용한다.)

반면! 선언적 렌더링을 하는 Vue는 DOM을 미리 만들어놓고 data()의 데이터가 변할 때마다 

#### 1-2. 요소의 속성 바인딩(v-bind:)
- 요소의 속성같은 경우에도 데이터바인딩이 가능한데, 이때 'v-bind'를 사용한다. shortcut은 ':'이다. 

```
<!-- HomeView.vue -->
<template>
  <div>
    <!-- 요소의 속성에 데이터바인딩할 때는 속성 앞에 ':' 쓰기(v-bind) -->
    <p :style="style">{{ message }}</p>
  </div>
</template>
<script>
export default {
  name: 'HomeView',
  data(){
    return {
        //여기에 html에서 쓸 모든 데이터들을 저장함.
        //object형태로.
        message : 'Hello World',
        //style도 가능
        style : 'color : red',
    },
  },
}
</script>
```

#### 1-3. 양방향 데이터 바인딩(v-model)





<br>

## 2. Data Binding이 가진 장점

- 변경 및 수정이 용이하다. data() 안에 들어있는 값만 수정하면 html에 있는 관련 data가 전부 바뀌기 때문이다.

- Vue에는 실시간 자동 렌더링 기능이 있는데, data() 내부의 값이 바뀌면 자동으로 html에 실시간 반영이 된다. -> 부드러운 화면 전환이 가능하다.

<br>

## Reference

- 코딩애플 : https://www.youtube.com/watch?v=0BbF7UxKKvg&t=139s
- Vue : https://kr.vuejs.org/v2/guide/syntax.html
