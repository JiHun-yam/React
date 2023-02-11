## useRef 란 ? 
DOM 요소에 접근할 수 있도록 하는 React Hook 이다. 



###  어떤 상황에서 사용하는지 ? 

리액트에 DOM을 선택해야 할떄 

예를 들어 네이버에 접속을 하면 포커싱이 input 창으로 focusing 되어 있을경우 
그럴 경우를 위해 우리는 useRef Hook을 사용한다 

사용방법 

```jsx 
import "./App.css";
import { useRef } from "react";

function App() {
  const ref = useRef("초기값");
  console.log("ref", ref);

  return (
    <div>
      <p>useRef에 대한 이야기에요.</p>
    </div>
  );
}

export default App;
```

콘솔로 출력을 하면 rer{ current: '초기값'}으로 나온다 

그리고 변경도 가능하다! 

```jsx 
import "./App.css";
import { useRef } from "react";

function App() {
  const ref = useRef("초기값"); //ref 1 { current ' 초기값 '}
  console.log("ref 1", ref);

  ref.current = "바꾼 값";
  console.log("ref 1", ref);  //rref 1 { current '바꾼 값'}
  return (
    <div>
      <p>useRef에 대한 이야기에요.</p>
    </div>
  );
}

export default App;
```

**이렇게 설정된 ref 값은 컴포넌트가 계속해서 렌더링 되어도 unmount 전까지 값을 유지합니다!**

이러한 특징 때문에 useRef는 다음 2가지 용도로 사용됩니다.

1.  저장공간

    1.  state와 비슷한 역할을 한다. 다만 state는 변화가 일어나면 다시 렌더링이 일어나다. 내부 변수들은 초기화가 되죠.
        
    2.  ref에 저장한 값은 렌더링을 일으키지 않아요. 즉, ref의 값 변화가 일어나도 렌더링으로 인해 내부 변수들이 초기화 되는 것을 막을 수 있다
        
    3.  컴포넌트가 100번 렌더링 → ref에 저장한 값은 유지돼요.
        

    4.  정리하면
        
        1.  state는 리렌더링이 꼭 필요한 값을 다룰 때 쓰면 된다.
        2.  ref는 리렌더링을 발생시키지 않는 값을 저장할 때 사용한다.

2.  DOM
    1.  설명 초반에 말씀드렸던 부분이에요! 렌더링 되자마자 특정 input이 focusing 돼야 한다면 useRef를 사용하면 됩니다.




### 예제 코드로 특징 살펴보기 

####  state 와 ref 차이점 

즉 state영역은 리렌더링이되면서 우리눈에 값이 변한게 보이고 
Ref 영역 값은 변경되어도 렌더링이 되지않는다 

state는 변경되면 렌더링이 되고, ref는 변경되면 렌더링이 안된다는걸 알면 된다 

 ```jsx 
 import "./App.css";
import { useRef, useState } from "react";

function App() {
  const [count, setCount] = useState(0);
  const countRef = useRef(0);

  const plusStat = () => {
    setCount(count + 1);
  };

  const plusStat = () => {
    countRef.current++;
  };

  return (
    <>
      <div>
        state 영역입니다. {count} <br />
        <button onClick={plusState}>state 증가</button>
      </div>
      <div>
        ref 영역입니다. {countRef.current} <br />
        <button onClick={plusRef}>ref 증가</button>
      </div>
    </>
  );
}

export default App;
```


#### DOM 접근 


input에 ref 에 속성을 이용하여 해당 DOM 요소로 접근하고 렌더링이 되면 
그부분으로 포커싱이 되게 만들었다

```jsx 
import { useEffect, useRef } from "react";
import "./App.css";

function App() {
  const idRef = useRef("");


  // 렌더링이 될 때
  useEffect(() => {
    idRef.current.focus();
  }, []);

  return (
    <>
      <div>
        아이디 : <input type="text" ref={idRef} />
      </div>
      <div>
        비밀번호 : <input type="password" />
      </div>
    </>
  );
}

export default App;>)
```


위 코드에서 아이디가 10자리 입력되면 자동으로 비밀번호 필드로 이동하려면 어떻게 코드를 짜야할까 ? 

``` jsx 
import { useEffect, useRef, useState } from "react";
import "./App.css";

function App() {
  const idRef = useRef("");
  const pwRef = useRef("");

  const [id, setId] = useState("");

  const onIdChangeHandler = (event) => {
    setId(event.target.value);
  };

  //처음 렌더링이 될 때 만 실행 
  useEffect(() => {
    idRef.current.focus();
  }, []);

  //배치 업데이트 때문에 이렇게 넣었다 
  useEffect(() => {
    if (id.length >= 10) {
      pwRef.current.focus();
    }
//의존성 배열 이 값이 변하면 이걸 수행 해주세요 
  }, [id]);

  return (
    <>
      <div>
        아이디 :
        <input
          type="text"
          ref={idRef}
          value={id}
          onChange={onIdChangeHandler}
        />
      </div>
      <div>
        비밀번호 : <input type="password" ref={pwRef} />
      </div>
    </>
  );
}

export default App;
```


