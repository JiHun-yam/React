##  Meno란 ? 
리렌더링 의 발생 조건 중 3번째 경우. 즉, 부모 컴포넌트가 리렌더링 되면 자식 컴포넌트는 
모두 리렌더링 된 다는 것은 그림으로 보면

![](https://i.imgur.com/s7IMbYD.png)

- 1번 컴포넌트가 리-렌더링 된 경우, 2~7번 컴포넌트가 모두 리렌더링!
- 4번 컴포넌트가 리-렌더링이 된 경우, 6, 7번이 모두 리렌더링!

자녀 컴포넌트 입장에서는 `나는 바뀐게 없는데 왜 리-렌더링이 돼야하지?`라는 의문이 생기게 되는데 이를 해결해주는 도구가 바로 **React.memo**!

## 예시코드


#### App 컴포넌트
```jsx
import React, { useState } from "react";
import Box1 from "./components/Box1";

const boxesStyle = {
  display: "flex",
  marginTop: "10px",
};

function App() {
  console.log("App 컴포넌트가 렌더링되었습니다!");

  const [count, setCount] = useState(0);

  // 1을 증가시키는 함수
  const onPlusButtonClickHandler = () => {
    setCount(count + 1);
  };

  // 1을 감소시키는 함수
  const onMinusButtonClickHandler = () => {
    setCount(count - 1);
  };

  return (
    <>
      <h3>카운트 예제입니다!</h3>
      <p>현재 카운트 : {count}</p>
      <button onClick={onPlusButtonClickHandler}>+</button>
      <button onClick={onMinusButtonClickHandler}>-</button>
      <div style={boxesStyle}>
        <Box1 />
      </div>
    </>
  );
}

export default App;
```
#### Box1 컴포넌트
```jsx 
import React from "react";

const boxStyle = {
  width: "100px",
  height: "100px",
  backgroundColor: "#91c49f",
  color: "white",

  // 가운데 정렬 3종세트
  display: "flex",
  justifyContent: "center",
  alignItems: "center",
};

function Box1() {
  console.log("Box1이 렌더링되었습니다.");
  return <div style={boxStyle}>Box1</div>;
}

export default Box1;
```

 
 App 컴포넌트2에서 버튼을 누르면 Box1에있던 컴포넌트도 리랜더링이 된다 

왜 ? 
부모컴포넌트 에 state가 변경이 되어서 리렌더링이 되어기 때문에 자식컴포넌트인 
Box1 도 리렌더링이 된다 

부모컴포넌트가 렌더링이 되더라도 자식 컴포넌트가 리렌더링이 안되게 하기 위해서

```jsx
export default React.memo(Box1);
```

자식컴포넌트에 React.memo로 보낸다 

