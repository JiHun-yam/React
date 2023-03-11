##  Json - server 란 

아주 간단한 DB와 API 서버를 생성 해주는 패키지 

## Json - server 사용하는 이유

BE에서 실제 DB와 APIServer가 구축될때까지는 FE 개발에 임시적으로 사용할 mock data를 
생성하기 위함  ** 즉 BE쪽에서 준비가 안되었는데 FE에서 테스트 할수 있는 환경**


(fake server , mock data )


JSON - server 터미널에서 시행 방법 
우선  프로젝트에  json - server 다운 

```jsx 
yarn add json-server 
```

json 서버 로컬로 띄우기 

```jsx 
yarn json-server --watch db.json --port 4000
```

db.json을 port번호 4000 즉 locahost:4000에 띄우기 