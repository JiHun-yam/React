
#DOM
#VirtualDOM


## DOM  (Document Object Model)

브라우저를 돌아다니다 보면 수 많은  **컴포넌트** 구성된 웹페이지를 보게 된다 , 그페이지를 
`문서(document)`라고 한다 , 페이지를 이루는 컴포넌트를 `엘리먼트(element)` 라고 한다
DOM은 이 엘리먼트를 tree 형태로 표현한 것이다 ! 

![](https://camo.githubusercontent.com/c59bf966cc931fb575df4c91e6c8d41af25cbe170fe138623da3e24aeb7df587/68747470733a2f2f692e696d6775722e636f6d2f59625542696e492e706e67)

트리의 요소 하나하나를 `노드` 라고. 각각의 ‘노드’는 해당 노드에 접근과 `제어(DOM 조작)`를 할 수 있는 API를 제공한다 

> API라는 말이 헷갈리면  단순히 `HTML 요소에 접근해서 수정할 수 있는 함수` 정도로 이해! 

```js 
// id가 demo인 녀석을 찾아, 'Hello World!'를 대입해줘.
document.getElementById("demo").innerHTML = "Hello World!";

// p 태그들을 모두 가져와서 element 변수에 저장해줘
const element = document.getElementsByTagName("p");

// 클래스 이름이 intro인 모든 요소를 가져와서 x 변수에 저장해줘
const x = document.getElementsByClassName("intro");
```

### **Vurtual Dom  (가상돔)**

#### **리액트** 는 왜 가상돔을 사용할까 ?

실제 돔을 조작하는것보다 메모리상에 올라와 있는 JS 객체를 변경하는 작업이 훨씬 더 가볍기

때문에 리액트에서는 버츄얼돔을 사용한다 

가상돔은 실제돔 과 구조가 완벽하게 동일한 **복사본 형태** 라고 보면 된다 

실제 돔은 아니지만 돔요소를 복사본 형태로 객체 상태로 메모리에 저장한다. 

그래서 실제돔보다 버츄얼돔이 더 빠르게 작동한다! 

#### 그럼 가상돔이 실제돔을 변경하는게 아니라면 **어떻게** 화면이 바뀌는걸까 ? 

**[STEP 1]**

  리렌더링이 일어나면 리액트는 항상 2가지 버전의 가상돔을 가지고 있다 

  1. 화면 업데이트 전 가상돔 

  2. 화면 업데이트 후 가상돔

  리렌더링이 일어났으니 2번에 해당되는 가상돔을 만든다 

**[STEP 2 : diffing] 비교** 

업데이트 전 가상돔과 업데이트 후 가상돔 상당히 빠르게 비교후 어느부분에 변화가 일어났는지 파악

**[STEP 3 : 재조정(reconciliation)]  반영**

파악이 끝나면, 변경이 일어난 **그 부분만** 실제 DOM에 적용, 하나하나 적용시키지 않고, 변경사항 을 모두 모아 한 번만 적용을 시킨다

  = > **Batch Update** 라고 한다   ( **변경된 모든부분을  한꺼번에 반영  )**

![](https://blog.kakaocdn.net/dn/boy0hL/btrYRRkJqW3/9rJfItMjADerwY6OEmknPK/img.png)

가상돔과 브라우저돔(실제돔)

**버튼클릭 한 번으로 화면에 있는 1000개의 엘리먼트가 바뀌어야 한다면**

-   **실제 DOM : **1000**번의 화면 갱신 필요**
-   **가상 DOM : Batch Update로 인해 단 한번만 갱신 필요**

****Batch Update**** 돔에서 페인팅 작업을 최소화할 수 있다. 그렇기 때문에 React가 엄청나게 빠른것이당!