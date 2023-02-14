useEffect 란 

- useEffect는 리액트 컴포넌트가 렌더링될 때마다 특정 작업을 수행하도록 설정할 수 있는 Hook이다

useEffect 는 기본적으로 렌더링 되고난 직후마다 실행되며, 두번째 파라미터 배열에 무엇을 넣느냐에 따라 실행되는 조건이 달라집니다.

Hook 중에 가장 많이 사용되는 Hook 중에 하나이다 


## useEffect는 언제 사용할까?

**useEffect는 리액트 컴포넌트가 렌더링될 때마다 특정 작업을 수행하도록 설정할 수 있는 Hook.** 

1. 컴포넌트가 화면에 보여졌을 때 내가 무언가를 실행하고 싶을때
2. 컴포넌트가 화면에서 사라졌을 때 무언가를 실행하고 싶을떄 

### useEffect와 리렌더링(re-rendering)

 `useEffect`는 화면이 렌더링 될 때마다 실행된다. 따라서 `useEffect()`의 의존성 배열을 활용해서 우리가 원할 때만 코드가 실행될 수 있도록 설정할 수 있다.


### 간단한 예시 

```jsx 
import { useState, useEffect } from "react";

const App = () => {
// useEffect가 속한 컴포넌트가 렌더링될때 실행된다
// 의도치 않는 동작을 볼 수 있다
// 흐름
// 1. input에 값을 입력 2.value 즉 state가 변경
// 3. state가 바뀌었기 때문에 -> App컴포넌트가 리렌더링이된다
// 4. 리렌더링 -> useEffect() 5. 1~4번 반복

const [value, setValue] = useState('');

	useEffect(() => {
		console.log('hello useEffect')
	});
	
	return (
			<div>
				<input
					type={value}
					onChange={(event) => {
					setValue(event.target.value)
				}} />
		</div>
);
}

export default App;
```

input 태그 안에 값을 입력할때마다 input value가 바뀌니깐 App 컴포넌트가 리렌더링이 된다 



##  의존성 배열 (dependency array)

-   의존성 배열(dependency array)이란 쉽게 말해 **"이 배열에 값(`state`)을 넣었을 때만 `useEffect`내의 코드를 실행해줘"** 라는 뜻

이 배열에 값을 넣으면, 그값이 바뀔때만 useEffect를 실행한다

### 처음 렌더링이 되었을때만 랜더링이 하고 싶다면

그럴 때는 의존성 배열에 있는 값을`[ ]`  없는 배열로 넣으면 된다 

```jsx 
import { useState, useEffect } from "react";
const App = () => {

const [value, setValue] = useState('');
	useEffect(() => {
	console.log'(hello useEffect!')
// 어떤값을 변화든지 간에 어떤스테이트가 변해도 이 컴포넌트는 처음 로딩될때만 렌더링이 된다
	}, []);
return (
	<div>
	<input
	type={value}
	onChange={(event) => {
	setValue(event.target.value)
	}} />
	</div>
	);
}

  

export default App;
```

이위에 코드처럼` 비어있는 의존성  `  배열일 때는 최초 렌더링이 될때 단 한번만 실행이 된다.



### Input창에 값을 이력할때마다 랜더링을 하고 싶다면 

``` jsx 
import { useState, useEffect } from "react";
const App = () => {

const [value, setValue] = useState('');

	useEffect(() => {
	console.log(`hello useEffect! ${value}`)
	}, [value]);
	// value state가 바뀔때마다 실행시켜 줘~ 
	return (
		<div>
		<input
		type={value}
		onChange={(event) => {
		setValue(event.target.value)
		}} />
	</div>
  );
}

export default App;
```

의존성 배열에 값이 있을 때는 배열 안에 있는 값(value)이 바뀔 때만 렌더링 실행된다 


### 클린업 (clean up) 

#### 클린업 란 ?

 - **컴포넌트가 화면에서 사라졌을 때 무엇을 실행**하고 싶다면 **clean up**을 사용하면 된다

#### 예시코드

``` jsx 
import React, { useEffect } from "react";

const App = () => {

	useEffect(()=>{
		// 화면에 컴포넌트가 나타났을(mount) 때 실행하고자 하는 함수
		console.log('컴포넌트 있어유~')
		return ()=>{
			// 화면에서 컴포넌트가 사라졌을(unmount) 때 실행하고자 하는 함
			console.log('컴포넌트 사라졌유~')
		}
	}, [])

	return <div>hello react!</div>
};
export default App;
```



## 정리 
1.  #useEffect  컴포넌트가 렌더링 될 때 실행된다.
2.   의존성 배열을 이용해 함수의 실행 조건을 제어 할 수 있다