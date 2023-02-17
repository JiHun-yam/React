서버와 데이터를 통신하는 방법 

### JS 객체문버에 토대를 둔 문자 기반의 데이터 교환 형식 

####    구조

```jsx 
{
  "squadName": "Super hero squad",
  "homeTown": "Metro City",
  "formed": 2016,
  "secretBase": "Super tower",
  "active": true,
  "members": [
    {
      "name": "Molecule Man",
      "age": 29,
      "secretIdentity": "Dan Jukes",
      "powers": [
        "Radiation resistance",
        "Turning tiny",
        "Radiation blast"
      ]
    },
    {
      "name": "Madame Uppercut",
      "age": 39,
      "secretIdentity": "Jane Wilson",
      "powers": [
        "Million tonne punch",
        "Damage resistance",
        "Superhuman reflexes"
      ]
    },
    {
      "name": "Eternal Flame",
      "age": 1000000,
      "secretIdentity": "Unknown",
      "powers": [
        "Immortality",
        "Heat Immunity",
        "Inferno",
        "Teleportation",
        "Interdimensional travel"
      ]
    }
  ]
}
```

작은 따옴포(’’)가 아닌 끝 따옴표(””)만이 허용됩니다.

## 메서드 

### JSON -> 문자열 형태 -> 서버 - 클리이언간 데이터 전송 시 사용 

1. JS 객체를 JSON 형태로 전송 할때 
	(내가 데이터 JSON 형태로 바꿔야 할떄  )

`자바스크립트 객체 → JSON 문자열 변환`

### stringify()

```jsx 
console.log(JSON.stringify({ x: 5, y: 6 }));
// Expected output: "{"x":5,"y":6}"

console.log(JSON.stringify([new Number(3), new String('false'), new Boolean(false)]));
// Expected output: "[3,"false",false]"

console.log(JSON.stringify({ x: [10, undefined, function(){}, Symbol('')] }));
// Expected output: "{"x":[10,null,null,null]}"

console.log(JSON.stringify(new Date(2006, 0, 2, 15, 4, 5)));
// Expected output: ""2006-01-02T15:04:05.000Z""
```

	주의사항 undefiend , 함수 , symbol은 JSON 으로 교환시 null 로 변환 된다 


3. JSON 형태를 JS 객체 형태로 사용 
	(내가 데이터를 받아 JSON을 JS 객체 형태로 바꿔야 할떄 )

`JSON 문자열 → 자바스크립트 객체 변환`

### parse()

```jsx 
const json = '{"result":true, "count":42}';
const obj = JSON.parse(json);

console.log(obj.count);
// Expected output: 42

console.log(obj.result);
// Expected output: true
```

## JSONPlaceholder (fake server )

 가짜 서버 프론트 엔드가 테스트하기 위한  사이트 이다 

아래 API를 통해 JSON 기반 DB 통신을 해보자 ! 

```jsx
fetch('https://jsonplaceholder.typicode.com/posts')
  .then((response) => response.json())
  .then((json) => console.log(json));
```

이걸 가지고 내코드에 대입 해보기 

```jsx
import "./App.css";
import { useEffect, useState } from "react";

function App() {
  const [data, setData] = useState([]);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/posts")
      .then((response) => {
        console.log();
        console.log("response.json()", response);
        return response.json();
      })
      .then((json) => {
        console.log("json", json);
        setData([...json]);
      });
  }, []);

  return (
    <div>
      {data.map((item) => {
        return (
          <div
            style={{
              border: "1px solid black",
              margin: "3px",
            }}
            key={item.id}
          >
            <ul>
              <li>userId : {item.userId}</li>
              <li>id : {item.id}</li>
              <li>title : {item.title}</li>
              <li>body : {item.body}</li>
            </ul>
          </div>
        );
      })}
    </div>
  );
}

export default App;
```

useEffect 훅을 이용해서 렌더링을 될때 데이터를 불러오게 했다 의존성 배열을 빈배열을 넣어서 
첫 렌더링 될때만 데이터를 가져오게 구현했다. 가져온 데이터를 data 라는 State에 저장 하고 
데이터 바인딩 까지 해봤다 