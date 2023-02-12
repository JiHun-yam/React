## styled Components 란 
#styledComponents

	 리액트에서 CSS-in-JS 방식으로 컴포넌트를 꾸밀수 있게 도와주는 패키지

## Css-In-JS 란 

자바스크립트 코드로 CSS 코드를 작성하여 컴포넌트를 꾸미는 방식이다 


## 기본적인 사용법 

```jsx 
import React from "react";
// styled-components에서 styled 라는 키워드를 import 합니다.
import styled from "styled-components";

// styled키워드를 사용해서 styled-components 방식대로 컴포넌트를 만듭니다. 
const StBox = styled.div`
	// 그리고 이 안에 스타일 코드를 작성합니다. 스타일 코드는 우리가 알고 있는 css와 동일합니다.
  width: 100px;
  height: 100px;
  border: 1px solid red;
  margin: 20px;
`;

const App = () => {
	// 그리고 우리가 만든 styled-components를 JSX에서 html 태그를 사용하듯이 사용합니다.
  return <StBox>박스</StBox>;
};

export default App;
```

syled-components는 백틱을 이용해 스타일을 css에 사용한다 


### 조건부 스타일링 
  styled components는 조건부 스타일링 이 가능하다 
  스타일 코드를 JS 코드를 작성하듯이 스타일 코드를 작성할 수 있다는 점이다 

``` jsx 
import React from "react";
import styled from "styled-components";

// 1. styled-components를 만들었습니다.
const StBox = styled.div`
  width: 100px;
  height: 100px;
  border: 1px solid ${(props) => props.borderColor}; // 4.부모 컴포넌트에서 보낸 props를 받아 사용합니다. 
  margin: 20px;
`;

const App = () => {
  return (
    <div>
			{/* 2. 그리고 위에서 만든 styled-components를 사용했습니다. */}
			{/* 3. 그리고 props를 통해 borderColor라는 값을 전달했습니다. */}
      <StBox borderColor="red">빨간 박스</StBox>
      <StBox borderColor="green">초록 박스</StBox>
      <StBox borderColor="blue">파랑 박스</StBox>
    </div>
  );
};

export default App;
```

StBox에  borderColor를 props로 받아와서 styled-components 애서
조건부로 스타일링이 가능해진다 

1. border: 1px solid ${(props) => props.borderColor}; 
2. (props)⇒{ return props.borderColor } 의 값이 === 'red'
3. border: 1px solid red 인식


## 전역 스타일링 

우리는 프로젝트를 아우르는, 공통적으로 들어가야 할 스타일을 적용해야 할 필요도 있습니다. 그럴 경우 ‘전역적으로(globally)’ 스타일을 지정한다. 라고 표현하는데요. 그럴 때 적용하는 방법이 바로 전역 스타일링이에요 

styled-components - > 해당 컴포넌트 내에서만 사용가능 



### 어떤 경우에 사용이 될까 ? 

공통적으로 적용되는 스타일링 부분에 대해서 

### 사용방법

GlobalStyle.jsx 를 만들고 
``` jsx 
import { createGlobalStyle } from "styled-components";

const GlobalStyle = createGlobalStyle`
  body {
    font-family: "Helvetica", "Arial", sans-serif;
    line-height: 1.5;
  }
`;

export default GlobalStyle;
```

import 적용시킬곳 위에 <GlobalStyle /> 적어둔다 
```jsx 
import GlobalStyle from "./GlobalStyle";
import BlogPost from "./BlogPost";

function App() {
	const title = '전역 스타일링 제목입니다.';
	const contents = '전역 스타일링 내용입니다.';
  return (
    <>
      <GlobalStyle />
      <BlogPost title={title} contents={contents} />
    </>
  );
}

export default App;
```

### css reset 

말그래로 css를 reset 한다는 뜻이다. 

#### 왜 필요할까? 

브라우저는 기본적으로 default style 를 제공한다 . 다양한 브라우저가 있는 만큼 
저마다 조금씩 다른 default style를 제공하기 떄문에. 우리는 이를 초기화하고 
우리가 정하는대로만 표현하기  위해 한다

#### 초기화해보기

reset.css
```css
html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, embed, 
figure, figcaption, footer, header, hgroup, 
menu, nav, output, ruby, section, summary,
time, mark, audio, video {
	margin: 0;
	padding: 0;
	border: 0;
	font-size: 100%;
	font: inherit;
	vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article, aside, details, figcaption, figure, 
footer, header, hgroup, menu, nav, section {
	display: block;
}
body {
	line-height: 1;
}
ol, ul {
	list-style: none;
}
blockquote, q {
	quotes: none;
}
blockquote:before, blockquote:after,
q:before, q:after {
	content: '';
	content: none;
}
table {
	border-collapse: collapse;
	border-spacing: 0;
}
```

index.html 
``` html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <link rel="stylesheet" href="./reset.css" />
  </head>
  <body>
    <span>Default Style을 테스트 해 봅니다.</span>
    <h1>이건 h1 태그에요</h1>
    <p>이건 p 태그에요</p>
  </body>
</html>
```

reset.css 를 적용해서 브라우저  default style를 제거헀다 