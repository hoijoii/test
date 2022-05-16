# TypeError: Cannot read properties of undefined

> Uncaught TypeError: Cannot read properties of undefined (reading '\_context')

사용자 정보를 전역적으로 사용하기 위해 Context API를 적용하다가 발생하였습니다.

<br />

## 1. 문제 상황 및 출처

```
//UserContexts.js
...
const initState = {
    user: null,
};

const reducer = (state, action) => {
    switch (action.type) {
        case "LOGIN":
            return {
                user: action.user,
            }
        case "LOGOUT":
            return {
                user: null,
            }
        default:
            return state;
    }
}

export const UserStateContext = createContext(null);
export const UserDispatchContext = createContext(null);

export const User Provider = ({children}) => {
    ...
}

export const useUserState = () => {
    const state = useContext(UserStateContext);
    return state;
}

export const useUserDispatch = () => {
    const dispatch = useContext(UserDispatchContext);
    return dispatch;
}
...


//Home.js
import UserStateContext from "../contexts/UserContext"
...

const userIdContext = useContext(UserStateContext)
console.log(userIdContext.user)
...
```

contexts.js에서 context들을 정의하고, useReducer를 통해 user 값을 업데이트할 수 있도록 새로운 Hooks를 만들었습니다. Provider 함수는 state(context)를 업데이트합니다.

Home.js에서는 Provider를 통해 변화된 context의 user를 콘솔에 출력하려고 합니다.

<br>

## 2. 발생 조건

console.log(userIdContext) 코드를 이용해 콘솔 출력을 해보니 오류는 아니지만 'undefined'가 발생합니다. UserStateContext가 처음 상태에서 업데이트되지 않은 모양입니다.. 아니, 초깃값이 null인데 undefined 출력인 것을 보면 아예 불러오지도 못한 것 같습니다.

애초에 'TypeError: Cannot read properties of undefined' 에러도 값이 정의되지 않았을 때 발생하는 에러입니다. 사실 React 실습 및 프로젝트마다 흔히 보이는 오류인데, 이번엔 원인을 알기가 쉽지 않았습니다.

<br>

## 3. 원인 및 해결

```
//Home.js
//잘못된 사용
import UserStateContext from "../contexts/UserContext"

//해결된 코드
import { UserStateContext } from "../contexts/UserContext"
```

문제는 '{ }' 의 부재였습니다... 타 컴포넌트에서 export default로 export한 경우에는 중괄호를 없애야 하고, default 없이 export를 한 경우에는 중괄호를 반드시 써주어야 합니다.

해결 후, context가 문제 없이 작동하여 userIdContext.user가 잘 출력되었습니다.

<br>
