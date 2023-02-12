##  props 란 ? 
#props

``` txt 
Compoennt 간의 정보교환 방식 
하위 컴포넌트에 값을 전달할 때 사용
```

 ![[스크린샷 2023-02-09 19.20.16.png]]
### 규칙
 
  - props는 반드시 위에서 아래 방향으로 흐린다 
	 [부모]->[자식1] O /  [자식1]->[부모] X / [자식1] -> [자식2] X
	
  - props는 반드시 읽기 전용으로 취급하며, 변경하지 않는다 


### 간단한 사용법 
 ``` jsx 
    import React from 'react'

 // 2. 정보를 사용하는 법
function Son(props) {
    console.log('props ', props)
    return <div>나는 {props.motherNam}아들</div>
}

 // 1.  부모 => 자식 정보를 전달했다
function Mother() {
    const name = '지훈';
    return <Son motherName={name} />
    // 부모컴포넌트에서 자식컴포넌트로 어떤한 데이터를 전달했다 
}

function main() {
    return (
        <div>
            <Mother />
        </div>
    )
}

export default main
```

### default Props
- defaultProps는 props 값을 따로 지정하지 않았을 때 설정하는 기본값
- 하위 컴포넌트에 전달되는 props가 없을 때 defaultProps를 설정하여 값을 지정할 수 있다

```jsx
import Component from './Component';

function Sample() {

  return (
    <React.Fragment>
      <Component/>
    </React.Fragment>
  );
}

```

```jsx
function Component(props) {
  return (
    <React.Fragment>
      <div>{props.text}</div>
    </React.Fragment>
  );
}

Component.defaultProps = {
	text: '8기 b반 파이팅!'
};
```

###  children props
#children

 props의 children을 사용하면 컴포넌트 태그 사이의 내용 확인 가능


 1.  User 컴포넌트에 여는 태그 닫는 태그 사이에 어떤 값을 두면 
    React에서는 children 이라는 props를 가지고 있다
    안녕하세요 는 Children 으로 인식이된다
    
```jsx
function TO() {

return <User>안녕하세요</User>

}
```

2. children props 사용하는 법 

```jsx
function TO() {

return <User>안녕하세요</User>

}

function User(props) {

console.log('props', props) //props {children: '안녕하세요'}

// childrenprops로 값을 받으려면

return <div>{props.children}</div>;

// 안녕하세요 출력

}
```



#### 왜 children props를 사용할까 ?

 상위컴포넌트로 항상 부터 children를 받아서 쓰게 되면 
 레이아웃을 다른곳에서 import 해오면 동일한 값을 받아 사용이 가능해진다

 






### propsdrilling 

#propsdrilling #드릴


사이가 먼 컴포넌트에 props를 정보를 줄려고 할때 데이터를 전달해주기 위한 용도로만 
쓰이는 컴포넌트가 생기게 된다  props가 사이가 먼 컴포넌트에 가기 까지 계속 드릴 하면서
드릴 처럼 계속 내려오는 현상을 props drilling 이라 한다 

[부모]=>[자식]=>[그 자식]=>[그 자식의 자식]=>이 테이터를 받기 위해 무려 3번이나
데이터를 내려줘야한다 이걸 바로 props drilling 이라 한다 

 props drilling이 만약 60개 가 되면 중간에 오류가 나면 찾기가 힘들다 
 유지 보수측면에서 너무 어렵게 떄문에 이런 문제를 해결하기 위해 리덕스를 사용하자 





### props 와 state 
- 둘 다 JavaScript 객체이고 렌더링에 영향을 줌
- props는 단반향 데이터 흐름의 리액트를 상위에서 하위로의 데이터 전달을 위해 사용함 (=함수에 전달하는 매개변수)
- state는 컴포넌트 내부에서 관리되는 데이터의 상태를 의미 (=함수 내부에 선언된 변수)!

![[스크린샷 2023-02-05 12.32.16.png]]


