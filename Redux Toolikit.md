## 리덕스 툴킷 이란 


## 새로운 것인가 ? 

### 아니다 

`리덕스툴킷`은 우리가 배웠던 **리덕스 와 구조나 패러다임이 모두 동일하다 **

즉 새로운 것이 아니다  **리덕스의 전체 코드의 양을 줄이기 위해 새로운 API**가 추가되었고
**ducks 패턴의 요소들이 어느정도 자동화되었다 **

컴포넌트에서 `useSelector` 를 통해서 사용하는 것은 모두 동일 
바뀐 부분은 그저` 모듈 파일 `뿐이다 


 #reduxjs/toolkit
 
 ```txt
 // 리덕스랑 리덕스튤킷 같이 깔셈 
 yarn add react-redux @reduxjs/toolkit
 // 리덕스 있으면 리덕스 튤킷만 깔아요 
 yarn add @reduxjs/toolkit
```


 리덕스 튤킷을 사용하면 스토어 구성하는 걸 간소화 할 수 있다 

Redux를 사용하면 Redux-toolkit을 사용할 수있다 

store 만드는 데 도움
createSlice 라는 유용한 API를 통해 action.item reducer를 한번에 만드는 역할을 수행 
불변성 신경 안서도 Immer 내장 
devTool  내장 


## devTool

다른 패키지에서는 찾아볼 수 없는 굉장히 강력한 개발툴이다
현재 프로젝트의 state 상태라던가, 어떤 액션이 일어났을 때 그 액션이 무엇이고, 
그것으로 인해 state가 어떻게 변경되었는지 등 리덕스를 사용하여 개발할 때 
아주 편리하게 사용할 수 있습당 




Flux 앱플레이케이션에 데이터 취금하기 위한 패턴 
MVC 문제를 해결할 목적으로 구현된 아키텍처 

크게 3가지로 구분 

dispatch -> store- > view 


단방향 데이터 흐름 
