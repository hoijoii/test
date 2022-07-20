# Decorators are not valid here.

> Decorators are not valid here.

vue와 typescript 연습을 하다가 발생한 오류.
변수 선언을 하자마자 문제가 생겼다.

<br />

## 1. 문제 상황 및 출처

```
// HomeView.vue

...

<script lang="ts">
import { Options, Vue } from 'vue-class-component';

...

@Options({
	components: {
		TodoInput,
		TodoList,
	},
})

const moment = require("moment")

export default class HomeView extends Vue {
    ...
}

</script>
```

Javascript의 moment 라이브러리를 사용하기 위해 import (require)하는 과정에서, decorator 부분인 '@Options'에 빨간 줄이 생기며 컴파일에 실패했다.

<br>

## 2. 원인 및 해결

```
//Home.js
//잘못된 사용
@Options({
	components: {
		TodoInput,
		TodoList,
	},
})

const moment = require("moment")

//해결된 코드

const moment = require("moment")

@Options({
	components: {
		TodoInput,
		TodoList,
	},
})

```

moment를 @Options 밑에서 선언했기 때문에 오류가 생겼다.

typescript에서 decorator(@)는 class, method, property, attribute, parameter 등을 장식해주는 역할을 한다. class의 앞에 쓰인다면 class의 역할, 정의를 확장해주는 것이다. 그러므로 decorator와 class는 붙어있어야 한다.

<br>
