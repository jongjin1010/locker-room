# Recoil

Recoil 이란 React 전용 전역 상태관리 라이브러리이다.

---

<br>

> ### 기존의 문제점

<br>

기존의 전역 상태관리 라이브러리의 **문제**는 다음과 같다.

### Reacrt 전용 라이브러리가 아니다

- 이는 호환성의 부족을 의미한다

### 복잡성

- Store, Action, Reducer 등의 다양한 구성요소가 필요하다
- 러닝커브가 높다.

<br>

> ### Recoil 시작

 <br>

### 설치 및 적용

설치는 npm 혹은 yarn 을 통해 진행이된다.

```
npm install recoil
yarn add recoil
```

이제 적용을 해보자.

Recoil 을 활용하기 위해서는 index.tsx 최상단의 App 컴포넌트를 RecoilRoot 로 감싸주면 된다.

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
