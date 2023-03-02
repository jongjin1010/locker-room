# Recoil

Recoil이란 React 전용 전역 상태관리 라이브러리이다.

<br>

## 기존의 문제점

기존의 전역 상태관리 라이브러리의 **문제**는 다음과 같다.

### Reacrt 전용 라이브러리가 아니다

- 이는 호환성의 부족을 의미한다

### 복잡성

- Store, Action, Reducer 등의 다양한 구성요소가 필요하다
- 러닝커브가 높다.

<br>

## Recoil 설치

---

```
npm install recoil
yarn add recoil
```

## Recoil 적용

Recoil을 활용하기 위해서는 index.tsx의 최상위컴포넌트에서 RecoilRoot로 감싸주면 된다.

```javascript
import React, { StrictMode } from "react";
import ReactDOM from "react-dom";
import { RecoilRoot } from "recoil";
import "./index.css";
import App from "./App";

ReactDOM.render(
  <StrictMode>
    <RecoilRoot>
      <React.Suspense fallback={<div>Loading... </div>}>
        <App />
      </React.Suspense>
    </RecoilRoot>
  </StrictMode>,
  document.getElementById("root")
);
```

<br>

## Atoms

### <b>정의</b>

Atom은 상태의 일부를 나타낸다.

Atoms는 어떤 컴포넌트에서나 읽고 쓸 수 있으며 값을 읽는 컴포넌트들은 atom을 구독한다.

그래서 atom에 어떤 변화가 있으면 그 atom을 구독하는 모든 컴포넌트들이 재 렌더링 되는 결과가 발생한다.

```javascript
const textState = atom({
  key: "textState", // unique ID (with respect to other atoms/selectors)
  default: "", // default value (aka initial value)
});
```

### <b>값 읽고 쓰기</b>

atom의 값을 읽고 쓰기위해서는 useRecoilState()를 사용한다.

```javascript
function CharacterCounter() {
  return (
    <div>
      <TextInput />
      <CharacterCount />
    </div>
  );
}

function TextInput() {
  const [text, setText] = useRecoilState(textState);

  const onChange = (event) => {
    setText(event.target.value);
  };

  return (
    <div>
      <input type="text" value={text} onChange={onChange} />
      <br />
      Echo: {text}
    </div>
  );
}
```

<br>

## Selector

### <b>정의</b>

Selector는 상태의 변화에 일부를 나타낸다.

```javascript
const charCountState = selector({
  key: "charCountState", // unique ID (with respect to other atoms/selectors)
  get: ({ get }) => {
    const text = get(textState);

    return text.length;
  },
});
```

### <b>값 읽고 쓰기</b>

우리는 useRecoilValue() 훅을 사용해서 charCountState 값을 읽을 수 있다.

```javascript
function CharacterCount() {
  const count = useRecoilValue(charCountState);

  return <>Character Count: {count}</>;
}
```

<br>

## 참고문서 및 예제

### 예제

[TodoListWithRecoil](https://github.com/jongjin1010/State-Management/tree/main/recoil)

### 문서

[Recoil\_공식문서](https://recoiljs.org/ko/docs/introduction/getting-started)
