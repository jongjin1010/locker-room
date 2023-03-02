## 정의

1. URI(Uniform Resource Identifier)는 우리말로 [통합 자원 식별자]라는 뜻을 가진다 
- Uniform: 리소스를 식별하는 통일된 방식
- Resource: URI로 식별이 가능한 모든 종류의 자원(웹 브라우저 파일 및 그 이외의 리소스 포함)
- Identifier: 다른 항목과 구분하기 위해 필요한 정보 

2. URL(Uniform Resource Locator)는 네트워크상에서 통합 자원의 위치를 나타내기 위한 규약이다

   URL은 흔히 말하는 웹 주소이다

<p align="center">
  <img width="90%" alt="스크린샷 2023-03-02 오후 12 23 56" src="https://user-images.githubusercontent.com/81551906/222323081-d0b058ee-08cb-419f-ab93-4cb8e62bcdd5.png">
</p>

정리하자면 URI는 식별하고, URL은 위치를 가르킨다.

## 비교

### **1. URI가 더 포괄적인 개념이다**

<p align="center">
  <img width="90%" alt="스크린샷 2023-03-02 오후 12 02 06" src="https://user-images.githubusercontent.com/81551906/222320118-4766b6c8-5e8f-40ea-9d8a-db990e941523.png">
</p>

모든 URL은 URI일수있지만 모든 URI는 URL이 될 수 없다

```
ex -> {
  naver.com > URI
  https://www.naver.com > URL, URI
}
```

### **2. URL은 프로토콜과 함께 이루어져 있다**

URL은 어떻게 위치를 찾고 도달할 수 있는지까지 포함되어야 하기 때문에 `https`, `http`, `ftp`, `file`등과 결합되어 있는데 

여기서  `https`, `http`, `ftp`, `file`등을 **프로토콜** 이라고 부른다

```
ex -> {
  프로토콜(https) + 이름(naver.com)
  -> https://www.naver.com === URL
}
```

### **3. URI는 그자체로 이름이 된다**

URI는 그 자체로 이름(elancer.co.kr)이거나

이름 + 위치(```https://www.naver.com```)를 나타낸 형태 모두가 해당한다

식별자 + 위치를 나타내는 URL은 URI의 일종이기 때문이다
