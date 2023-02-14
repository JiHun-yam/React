### 인자로 들어오는 함수 자체를 기억 (메모이제이션)

useCallback은 특정 함수를 새로 만들지 않고 재사용하고 싶을 때 사용하는 함수이다.  

### 코드를 통해 문제상황 살펴보기 

  Box1 이 만일, count를 초기화 해 주는 코드라고 가정한다

-  App.jsx 

```jsx
...

	// count를 초기화해주는 함수
  const initCount = () => {
    setCount(0);
  };

  return (
    <>
      <h3>카운트 예제입니다!</h3>
      <p>현재 카운트 : {count}</p>
      <button onClick={onPlusButtonClickHandler}>+</button>
      <button onClick={onMinusButtonClickHandler}>-</button>
      <div style={boxesStyle}>
        <Box1 initCount={initCount} />
      </div>
    </>
  );
}

...
```

- Box1.jsx 

```jsx
...

function Box1({ initCount }) {
  console.log("Box1이 렌더링되었습니다.");

  const onInitButtonClickHandler = () => {
    initCount();
  };

  return (
    <div style={boxStyle}>
      <button onClick={onInitButtonClickHandler}>초기화</button>
    </div>
  );
}

...
```


### 완성본 

![](https://camo.githubusercontent.com/8f5e24ca959ab5b59f5065096a8df4a621212838bcdfc4ccba8d8989085fa0bd/68747470733a2f2f692e696d6775722e636f6d2f6a4f33334155492e706e67)

`+버튼`이나  `-버튼`  을 누를 때 `초기화버튼` 을 누를떄 마다 
`App` 컴포넌트 (부모컴포넌트) `Box1`  컴포넌트 (자식컴포넌트) 가 리렌더링이 된다 

React.memo로 Box1.jsx  메모제이션을 했는데도 리렌더링이 되냐요 ? 
된다 우리가 함수형 컴포넌트를 사용했기 떄문이고 App.jsx 가 리렌더링 되면서 

```jsx
const onInitButtonClickHandler = () => {
  initCount();
};
```

코드가 다시 만들어지기 때문이다. 

JS 에서는 함수도 객체의 한 종류이기 때문에 모양은 같더라도 다시 만들어지면 함수를 저장하고 있는 주솟값이 달라지고 이에 따라 하위 컴포넌트인 Box1.jsx는 props가 변경됐다고 리액트에서 인식한다

#### 따라서 Box1.jsx에서는 props(initCount)가 변경 됐다고 인식!


## useCallback 사용을 통한 함수 메모제이션 
#불변성 

### useCallback hook의 적용

```jsx
// 변경 전
const initCount = () => {
  setCount(0);
};

// 변경 후
const initCount = useCallback(() => {
  setCount(0);
}, []);
// [] 의존성 

```

이렇게 아래부분에 [ ] (즉 의존성 배열에 아무것도 넣지않으면 )를 넣어주면 부모컴포넌트가 리렌더링이 되어도 자식 컴포넌트는 리렌더링이되지않는다 




### 더 나아가기 

count를 초기화 할 때, 콘솔을 찍어보면

```jsx
...

// count를 초기화해주는 함수
const initCount = useCallback(() => {
  console.log(`[COUNT 변경] ${count}에서 0으로 변경되었습니다.`);
  setCount(0);
}, []);

...
```

console.log :  COUNT 변경 0에서 0으로 변경되었습니다.

```
위와 같은 현상이 발생하는 니유는 useCallback이 count가 0일 때의 시점을 기준으로 메모리에 함수를 저장했기 때문에 우리는 의존성 배열 의존성 배열(dependency array)이 필요하게 된다. 

기존 코드의 dependency array에 count를 넣으면, count가 변경이 될 때마다 새롭게 함수를 할당하게 된다. 
```

```jsx
...

// count를 초기화해주는 함수
const initCount = useCallback(() => {
  console.log(`[COUNT 변경] ${count}에서 0으로 변경되었습니다.`);
  setCount(0);
}, [count]);

...
```

이렇게 의존성배열에 count를 넣고 useCallback 를 잘써주면 

console.log :  COUNT 변경 5에서 0으로 변경되었습니다.

잘 출력이 된다