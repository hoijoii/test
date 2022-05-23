# Context (컴포넌트 트리 전체에 데이터 제공하기)

props는 부모 컴포넌트가 자식 컴포넌트에게 데이터를 전해줄 때 사용합니다.

```
//App.js
return <MyComponent name="React">

//MyComponent.js
const MyComponent = ({ name }) => {
    return <div>Hello, {name}!</div>
}
```

편리한 기능이지만 만약 여러 컴포넌트에 이 값을 전달해야 한다면 번거로운 작업이 될 것입니다. 또한 props는 하향식으로 데이터를 전달하는 데에 사용됩니다.
Context는 컴포넌트의 구조와 상관 없이 여러 컴포넌트가 값을 공유할 수 있게 해줍니다.

<br>

## 1. 사용 이유

<br>

## Reference

- React: https://ko.reactjs.org/docs/context.html
