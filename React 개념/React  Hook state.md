 #Hook

React에서는 상태를 다루기 위해 State를 쓴다 
JS에서는 상태를 다루기 위해 변수나 상수를 이용한다 



## React에는 여러가지 Hook 이있다 

```jsx
useState,  useEffect, useContext, useReducer 등등
```

## React에서는 State를 왜 쓸까  ?

```txt
UI 를 바꾸기 위해서다
즉 렌더링을 다시하기 위해서 , 변경된 값을 사용하기 위해 
```

<div style="text-align: center"> </div>
## State 사용법
```
import React from 'react'


function main() {

	//hook
	

	return (
	<div>m</div>
		)
	}

export default main
```

<div style="text-align: center"> </div>
### useState 사용방법 
#useState

```jsx
import React from 'react'
import { useState } from 'react';

function main() {

// 변수, count를 변경할수 있는 변수 배열 비구조화 할당 문법
let [count, setCount] = useState(0);
// 배열 형태에 state
let [todolist, setTodolist] = useState([]);

return (
<div> <p>
    현재 카운터 값은 <b>{count}</b> 입니다.
      </p>
      <button onClick={() => setCount(count + 1)}>+1</button>
      <button onClick={() => setCount(count - 1)}>-1</button>
	</div>
	)
}

export default main
```

setState를 사용하기 위해서는 setCount(변경될 값 ) 이런식으로 적으면 된다 

### useState  예제 2

```jsx
import { useState } from 'react';

import './App.css';

  
  
  

function App() {

// 숫자나 문자열은 잘 나오지만 boolean, obj는 출력이 되지않는다

const [fruit, setFruit] = useState('과일');

  return (

	<div className="App">
		<input
		//입력된 값을 의미
		value={fruit}
		// input창에 입력이 될 때마다 setFruit를 이용해
		// fruit의 값을 입력값으로 바꾼다
		onChange={(e) => {
		setFruit(e.target.value)
		}} />
		<br />
		//input에 입력된 값 출력 
		<p>{fruit}</p>
		</div>
		);
	}
```

