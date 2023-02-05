### 1.  VS Code React snippet


### 1-1 rfce 
#rfce

현재 있는 JS 파일 이름을 기반으로 Component 가 만들어진다 

```jsx
import React from 'react'

function App() {
	return (
	<div>App</div>
	)
}
export default App
```


### 1-2   
#rfc

현재 있는 JS 파일 이름을 기반으로 Component 를 만들어주고 
다른 파일에 import 할수 있게 export default 해준다 

```jsx 
import React from 'react'

export default function App() {
	return (
	<div>App</div>
	)
}
```