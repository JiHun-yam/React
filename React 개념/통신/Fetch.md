ES6부터 도입된 JS 내장 라이브러리 

하지만 단점이 많아 AXIOS를 많이 사용한다 

- 미지원 브라우저 존재 
- 개발자에게 불친절한 responese
- axios에 비해 부족한 기능 

### Fetch AXIOS 데이터 불러오는 방식

#### 1. feach 

```js
const url = "https://jsonplaceholder.typicode.com/todos";

fetch(url)
.then((response) => response.json())
.then(console.log);
```

fetch().then을 한 상태여도 여전히 JSON 포맷의 응답이 아니기 때문에 response.json()을 한번 더 해주는 과정이 필요합니다. 즉 feach로 데이터를 요청하는 경우에는 두 개의 .then()이 필요하다 

#### 2. axios 

```jsx
const url = "https://jsonplaceholder.typicode.com/todos";

axios.get(url).then((response) => console.log(response.data));
```

axios 는 응답을 기본적으로 JSON 포맷으로 제공해준다 즉 ***우리가 JSON형태를 객체타입으로 
변화하는 과정을axios가 대신 해준다 **

### Fetch AXIOS  에러 처리 

#### 1. axios 

```jsx
const url = "https://jsonplaceholder.typicode.com/todos";

axios
  .get(url)
  .then((response) => console.log(response.data))
  .catch((err) => {
    console.log(err.message);
  });
```
-   axios.get()요청이 반환하는 Promise 객체가 갖고있는 상태코드가 2xx의 범위를 넘어가면 거부(reject)를 합니다.
-   따라서, 곧바로 catch() 부분을 통해` error handling`이 가능합니다. 

- catch를 통해 에러 핸들링방법
```js
const url = "https://jsonplaceholder.typicode.com/todos";

// axios 요청 로직
axios
  .get(url)
  .then((response) => console.log(response.data))
	.catch((err) => {

		// 오류 객체 내의 response가 존재한다 = 서버가 오류 응답을 주었다	
		if (err.response) {
		// 에러 객체가 리스폰스식으로 상세히 주기 떄문에 에러 핸들링 가능   
	    const { status, config } = err.response;
	
			// 없는 페이지
	    if (status === 404) {
	      console.log(`${config.url} not found`);
	    }

			// 서버 오류
	    if (status === 500) {
	      console.log("Server error");
	    }
	
		// 요청이 이루어졌으나 서버에서 응답이 없었을 경우
	  } else if (err.request) {
	    console.log("Error", err.message);
		// 그 외 다른 에러
	  } else {
	    console.log("Error", err.message);
	  }
	});
```

#### 2. fetch 

```js
const url = "https://jsonplaceholder.typicode.com/todos";

fetch(url)
  .then((response) => {
    if (!response.ok) {
      throw new Error(
        `This is an HTTP error: The status is ${response.status}`
      );
    }
    return response.json();
  })
  .then(console.log)
  .catch((err) => {
    console.log(err.message);
  });
```