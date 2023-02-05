### Component 란 ? 
#Component #JSX

 리액트로 만들어진 앱을 이루는 최소한의 단위

 기존의 웹 프레임워크는 MVC방식으로 분리하여 관리하여 각 요소의 의존성이 높아 재활용이 어렵다는 단점이 있었다. 반면 컴포넌트는 MVC의 뷰를 독립적으로 구성하여 재사용을 할 수 있고 이를 통해 새로운 컴포넌트를 쉽게 만들 수 있다.  
 
  컴포넌트는 데이터(props)를 입력받아 View(state) 상태에 따라 DOM Node를 출력하는 함수.  
 
  컴포넌트 이름은 항상 대문자로 시작하도록 한다.   
   (리액트는 소문자로 시작하는 컴포넌트를 DOM 태그로 취급하기 때문이다.

  UI를 재사용 가능한 개별적인 여러 조각으로 나누고, 각 조각을 개별적으로 나누어 코딩한다

### 왜 사용하는지 ? 
- Component 쓰는 이유 재사용하고 컴포넌트를 블록을 조립하면서 사이트를 만들기 위햐 

- Component는 JS 함수와 비슷하다 JS함수에서는 인풋을 넣으면 아웃풋이 나오는데 
     Component는 props를 넣으면 React 엘리먼트가 나온다 




## React Component를 표현하는 2가지 방법 
###  1. 함수형 Component 신형  

  ```jsx 
  function Sample() { 
  const text = '함수형 컴포넌트!'; 
  return (
   <div className = "react">{text}</div>
    ) 
   }
```
    

### 2.  Class Component 구형 


#### 차이점 

- 선언방식 
- State 사용 차이 
- Props사용 차이 
- Life Cycle 
- 이벤트핸들링  
  
  

### 함수형 컴포넌트를 선호하는 이유 
-  Hook들을 필요한 곳에 사용하며 Logic의 재사용이 가능하다는 장점이 있어 함수형 **컴포넌트+Hook**을 주로 사용
- 클래스형 컴포넌트는 로직과 상태를 컴포넌트 내에서 구현하기 때문에 상대적으로 복잡한 UI 로직을 갖고 있는 반면, 함수형 컴포넌트는 state를 사용하지 않고 단순하게 데이터를 받아서(props) UI에 뿌려 줌

### 함수형 Component 선언방식 
```jsx
function Sample()
{ const text = '함수형 컴포넌트!';
 return ( 
 <div className = "react">{text}</div> 
 ) 
 }
```

1.  state, lifeCycle 관련 기능사용 불가능하다 [Hook을 통해 해결]
2.  클래스형보다 메모지 자원을 덜 사용한다
3.  컴포넌트 선언이 편하다

### 함수형 Component  State 사용 
```jsx 
const Sample = () => {
const [test1, setTest1] = useState([]);
const [test2, setTest2] = useState(''); 
const [num, setNum] = useState(1);
const testFuntion = () => { setNum(num + 1) };
const text = '함수형 컴포넌트!'
return (
<div className="react">{text}</div> 
	   )
	    }
```

1. useState 함수로 state를 사용한다
2. useState 함수를 호출하면 배열이 반환되는데 첫 번째 원소는 현재 상태, 두번째 원소는 상태를 바꿔주는 함수이다

### 함수형 Component  props 
```jsx 
const Sample = ({num, name}) => 
const text = '함수형 컴포넌트!'
	return (
	<div>{name}의 나이는 {num}</div> 
	 )
	}
```



### 함수형 Component 이벤트핸들링 

```jsx
const Sample = () => {
const [num, setNum] = useState(1);
const clickFuntion = () => { setNum(num + 1) };
const text = '함수형 컴포넌트!'
	return (
	<button onCilck={clickFunction}>증가 버튼</button> 
	) 
  }
```

1.  const + 함수 형태로 선언해야 한다.
2.  요소에 적용할때 this가 필요없다.

class 라는 키워드로 기재가 된 react.Component를 상속받아서 기재하는 랜더 함수를 이용해서 선언 
  우리는 사용하지 않다
    
 2가지 모두 기능상 동일하지만 공식 홈페이지에서는 함수형 Component 사용을 권장한다 그리고 더쉽다 


    



## JSX
#JSX

React에서 HTML를 사용할수 없다 그래서 나온게 JSX이다 
JS를 확장한 문법  React Element를 생성하기 위한 문법 


### JSX 주희사항

컴포넌트에 첫글자는 무조건 대문자여야만 한다 
폴더를 만들떄는 카멜로 규칙을 지켜 만들면 된다 

### 1.  1개의 엘리먼트를 반환해라 
```jsx 
function Main() { 
    return ( 
    <h2> 이러면 오류  </h2>
    <>
   
    <div className="App"> 
        <h2>안녕 </h2>
    </div> 
    <>
    ); 

```
  
  위코드는 h2태그만 반환되기 때문에 에러가 난다 

```Jsx
function Main() { 
    return ( 
    
    <div>
   <h2> 이러면 오류안남   </h2>
    <div className="App"> 
        <h2>안녕 </h2>
    </div> 
    <div>
    ); 
```

해결~ 





### 2. JSX에서 JS사용위치와 JSX문법 사용위치

```jsx

 function app() { 
        // JS 쓰는 곳 
        let name = '지훈';
        let goodDay = true;
	
   return ( 
            // JSX 작스문법 쓰는곳  
            <div> 
            
            <h2> 안녕 지구촌 {name} </h2> //안녕 지구촌 지훈 
            {goodDay === true ? '좋은날' : '나쁜날 '}
            </div>

```
   
   
###  3. class 는  className으로 작성 

```jsx
 <div class='name'>  </div>
```