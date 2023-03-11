Axios는 node.js 와 브라우저를 위한 Promise 기반 HTTP 클라이언트 이다 .
서버 사이드에서는 네이티브 node.js의 http 모듈을 사용하고 , 클라리언트에서는 
XMLHttpRequests를 사용한다 

라이브러리 다운 명령어 

``` jsx
yarn add axios
```


패스 방법 Path 방법 

```
GET    /posts
GET    /posts/1
POST   /posts
PUT    /posts/1
PATCH  /posts/1
DELETE /posts/1
```

쿼리 방법  Query 
좀 더 깊은 속성에 접근하기 위해서는 쿼리 방법을 사용 

```
GET /posts?title=json-server&author=typicode
GET /posts?id=1&id=2
GET /comments?author.name=typicode
```