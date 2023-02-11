
 함수형 컴포넌트에서 Context 를 보다 더 쉽게 사용 할 수 있습니다.

## react context의 필요성
    
이전 까지 일반적으로 부모컴포넌트 → 자식 컴포넌트로 데이터를 전달해 줄 때 `props` 를 사용했었다.

그러나 `부모` → `자식` → `그 자식` → `그자식의 자식` 이렇게 너무 깊어지게 되면 `prop drillin` 현상이 일어나게 된다


### prop drilling의 문제점


1.  깊이가 너무 깊어지면 이 prop이 어떤 컴포넌트로부터 왔는지 파악이 어려움
2.  어떤 컴포넌트에서 오류가 발생할 경우 추적이 힘들어지니 대처가 늦게 된다.

![스크린샷 2023-02-11 16 36 57](https://user-images.githubusercontent.com/95469708/218246603-8cb89a79-fa6f-4380-97fc-efc73d8743b6.png)

그래서 등장한 것이 바로 **react context API**라는 것이구요. useContext hook을 통해 우리는 쉽게 **`전역 데이터를 관리`**할 수 있게 되었습니다.

-   **(2) context API 필수 개념**
-   `createContext` : context 생성 (Context 객체생성 )

-   `Consumer` : context 변화 감지 

-   `Provider` : context 전달(to 하위 컴포넌트)


### useContext를 사용 X 

 `부모` → `자식` → `그 자식` → `그자식의 자식` 으로 prop drilling 시켜줬다. 이 과정에서 Father은 부모의 prop을 Child에 전달하는 그저 거쳐가기만 했다. (쓸모없는 과정 발생)

이것을 useContext로 해결할 수 있다.

### useContext 사용 했을 때

1.  우선 context 라는 폴더를 만들고 FamilyContext.jsx를 생성한다.

[
```FamilyContext.jsx
import { createContext } from "react";

export const FamilyContext = createContext(null);
```


나중에 props로 주입하는 하위 컴포넌트에서 사용할 수 있는 FamilContext가 완성 되었는데, 용돈과 집안 이름은 할아버지로 부터 나왔기 때문에 GrandFather 컴포넌트에서 사용할 수 있다.

```
title: null의 의미?

createContext의 파라미터에는 context의 기본 값을 설정 할 수 있다. 여기서 사용한 ==null은 context를 쓸 때 값을 따로 지정하지 않을 경우 사용되는 기본 값이다.== 
```

2.  GrandFather.jsx 코드 수정


```jsx 
import React from 'react';
import Father from './Father';
import { FamilyContext } from '../context/FamilyContext';

const GrandFather = () => {
  const houseName = '스파르타';
  const pocketMoney = 10000;
  return (
    // Provider: context 전달 (to 하위 컴포넌트)
    // 키와 값을 넣어준다 
    <FamilyContext.Provider value={{ 
    houseName: houseName, 
    pocketMoney: pocketMoney }}>
      <Father />
    </FamilyContext.Provider>
  );
};

export default GrandFather;```


3.  Father.jsx 수정 Father로 전달하는 `props`를 넘겨주지 않고 context만든것을 통해 외부로 접근할 수 있게 해준다.
``` jsx
import React from 'react';
import Child from './Child';

const Father = ({ houseName, pocketMoney }) => {
  console.log('Father:', houseName, pocketMoney); // 스파르타 10000
  return <Child />;
};

export default Father;
```


4.  Child.jsx 수정

자식 컴포넌트에 useContext, FamilyContext를 import해주고, 컴포넌트 내부에 data 라는 변수를 생성하고 useContext를 사용해 FamilyContext 데이터를 불러온다.

그리고, data.houseName과 같이 부모가 전달해준 값을 출력해주면 된다.

```
- 이 방식은 props로 내려준 값을 쓴것이 아니다. 
- context를 이용해 값을 받아온것!
```


```jsx
import React, { useContext } from "react";
import { FamilyContext } from "../context/FamilyContext";

function Child({ houseName, pocketMoney }) {
  const stressedWord = {
    color: "red",
    fontWeight: "900",
  };

  const data = useContext(FamilyContext);
  console.log("data", data);

  return (
    <div>
      나는 이 집안의 막내에요.
      <br />
      할아버지가 우리 집 이름은 <span style={stressedWord}>{data.houseName}</span>
      라고 하셨어요.
      <br />
      게다가 용돈도 <span style={stressedWord}>{data.pocketMoney}</span>원만큼이나
      주셨답니다.
    </div>
  );
}

export default Child;
```

콘솔을 잘 찍어 보면 houseName과 pocketMoney가 잘 출력된다 
오…! GrandFather → Context(중앙 관리소) → Child 순서로 잘 전달이 되었다는 뜻이다 
바인딩을 하면 잘 출력이 된다 !! 

Props로 받아온게 아니고 context로 가져왔다를 잘 기억해야만 한다 

## 주의사항

-   `useContext`를 사용할 때, Provider에서 제공한 value가 달라지게 되면 useContext를 사용하기 있는 모든 컴포넌트가 리렌더링이 되게 된다.
-   따라서 value 부분을 항상 신경을 써주어야한다.

### 해결방안 

- 메모이제이션

