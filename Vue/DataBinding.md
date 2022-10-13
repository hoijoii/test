# Data Binding

```
{{ dataBinding }}
```
Javascript 데이터를 HTML 코드에서 사용할 수 있게 해준다. 
데이터 바인딩은 Vue의 핵심적인 장점들을 가지고 있다고 볼 수 있다. 바로 '선언적 렌더링(Declarative Rendering)'과 '반응성(Reactivity)'을 보여주기 때문이다! 아래에서 자세히 알아보자.

<br>

## 1. Data Binding 사용법

```
<!-- HomeView.vue -->
<template>
  <div>
    <!-- data() 안에 있는 데이터를 {{ }} 에 넣어 사용 -->
    <!-- 요소의 속성에 데이터바인딩할 때는 속성 앞에 ':' 쓰기(v-bind) -->
    <p :style="style">{{ price }}</p>
  </div>
</template>
<script>
export default {
  name: 'HomeView',
  data(){
    return {
        //여기에 html에서 쓸 모든 데이터들을 저장함.
        //object형태로.
        price : 60,
        //style도 가능
        style : 'color : red',
    },
  },
}
</script>
```
- script 내부 data() 함수 안에 들어있는 데이터들을 html 코드에서 {{}} 표현을 통해 사용할 수 있다.
- 요소의 속성같은 경우에도 데이터바인딩이 가능한데, 이때 'v-bind'를 사용한다. shortcut은 ':'이다. 

<br>

## 2. Data Binding 사용 이유

- 변경 및 수정이 용이하다. data() 안에 들어있는 값만 수정하면 html에 있는 관련 data가 다 바뀌기 때문이다.
- Vue에는 실시간 자동 렌더링 기능이 있는데, data() 내부의 값이 바뀌면 자동으로 html에 실시간 반영이 된다. -> 부드러운 화면 전환이 가능하다.

<br>

## Reference

- 코딩애플 : https://www.youtube.com/watch?v=0BbF7UxKKvg&t=139s
- Vue : https://kr.vuejs.org/v2/guide/syntax.html
