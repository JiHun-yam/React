## styled Components 란 

 동일한 컴포넌트에서 컴포넌트 이름을 쓰듯 스타일을 지정하는 것을  `styled-components`라고 한다
 


### Css in Js 
자바스크립트 코드로 CSS 코드를 작성하여 컴포넌트를 꾸미는 방식이다 

### 장점 
 - css 파일을 밖에 두지 않고, 컴포넌트 내부에 넣기 때문에, css가 전역으로 중첩되지 않도록 만들어주는 장점이 있습니다.

### 사용방법 

``` jsx 
import React from 'react';
import styled from 'styled-components';

const Circle = styled.div`
  width: 5rem;
  height: 5rem;
  background: black;
  border-radius: 50%;
`;

function App() {
  return <Circle />;
}
export default App;
```

import 로 styled를 받아오고 `Cricle` 라는 컴포넌트만들어 사용 

### props 사용 방법

```jsx 
import React from 'react';
import styled from 'styled-components';

const Circle = styled.div`
  width: 5rem;
  height: 5rem;
// 배경색을 props 받고 css에 넣기 
  background: ${props => props.color || 'black'};
  border-radius: 50%;
`;

function App() {
  return <Circle color="blue" />;
}

export default App;
```

Circle 컴포넌트 props로 원하는 조건에 맞게  원하는 값을 넣어주면 원하는 css가능해진다 


### props 사용방법 2

```jsx
import React from 'react';
import styled, { css } from 'styled-components';

const Circle = styled.div`
  width: 5rem;
  height: 5rem;
  background: ${props => props.color || 'black'};
  border-radius: 50%;
  ${props =>
    props.huge &&
    css`
      width: 10rem;
      height: 10rem;
    `}
`;

function App() {
  return <> 
// 사이즈 큰 원 생성 
<Circle color="red" huge/>;
// 기본 사이즈 원 생성 
<Circle color="red" />;
<>
}

export default App;
```

동일한 `컴포넌트`를 이용해서 원하는 컴포넌트에 css로 `커스텀아이징` 할수 있다

여러 줄의 CSS 코드를 조건부로 보여주고 싶다면 `css`를 사용해야한다, `css`를 불러와 사용을 해야 그 스타일 내부에서도 다른 `props`  를 조회 할 수 있다

자주 쓰이는 `컴포넌트`를 만들고 기본값을 주고 각각의 상황에맞게 `props` 를주워서 원하는 조건에 맞게 생성이 가능해진다


## global css 
 - `프로젝트 전역` 으로 발동하는 css를 만들 수 있다 . 
 
```jsx
import styled, { createGlobalStyle } from "styled-components";

export const GlobalStyle = createGlobalStyle`
  body{padding:0; margin:0}
`;
```
 
 `reset.css or font `등등 원하는 것을 전역으로 발동시킨다 

## global Theme

1. theme.js 만들고 색깔이나 폰트사이즈 등과 같이 전역으로 필요한 css 설정 

```jsx
// theme.js
const theme = {
  successColor: blue;
  dangerColor: red;
}
export default theme
```

2. index.jsx props로 연결하기 

3. 전역이나 원하는 곳에서 호출하여 사용 

	```jsx
// Container.jsx
import React, { Component } from "react";
import styled, { ThemeProvider } from "styled-components";
import theme from "./theme";

const Container = () => {
  return <Button>test</Button>;
};

// 아래와 같이 props.theme로 불러서 전역으로 사용한다.
const Button = styled.button`
  border-radius: 30px;
  padding: 25px 15px;
  background-color: ${props => props.theme.successColor};
`;

export default Container;
```


## ## Mixin css props
-   css props는 자주 쓰는 css 속성을 담는 변수입니다.
-  `css 변수명 = css`스타일`...` 로 사용합니다.
   ```jsx
const flexCenter = css`
display: flex;
justify-content: center;
align-items: center;
`;

const FlexBox = div`
  ${flexCenter}
`; 
```

### 다른파일에서 컴포넌트 Import 
-  해당 파일에서 정의한 css를 export하여 다른 파일에서 import 할 수 있습니다.

```jsx
// Login.jsx
export const LoginContainer = styled.div`
  background: red;
`;

// Other.jsx
import { LoginContainer } from ".Login";

const Other = () => {
  return <LoginContainer>...</LoginContainer>;
};

```