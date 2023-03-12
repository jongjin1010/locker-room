## 정의

Scope는 참조 대상 식별자를 찾아내기 위한 규약이다.

## Local scope vs Global scope

Scope는 참조의 범위에 따라 Local과 Global로 나뉜다.

```javascript
const a = "global a"
const b = "global b"

function Scope() {
  const c = "local c"

  console.log(a); // global a
  console.log(b); // global b
  console.log(c); // local c
}

console.log(c); //ReferenceError: c is not defined
```
위의 코드를 보면 **function Scope**를 기준으로 외부가 Global, 내부가 Local이 된다.

**c**는 Local scope 내부에서 선언되었으므로 Global scope는 Local variable c를 참조할 수 없다.

## Block scope vs Function scope

Block scope와 Function scope를 구분하는 기준은 범위이다.

```javascript
function Sum() { // <- Function scope
  const arr [1, 2, 3];
  let sum = 0;
  
  for (let i = 0; i < arr.length; i++) { // <- Block scope
    sum = sum + arr[i];
  }
}

Block scope는 if문이나 for문 등의 범위('{}')를 가지고

Function scope는 function의 범위('{}')를 갖는다.
```

## Lexical scope(Static scope)

Lexical scope는 함수의 선언 위치에 따라 상위 scope를 결정한다.

여기서의 중요한 점은 함수의 호출 위치가 아닌 선언 위치가 된다.

```javascript
const x = 1;

function foo() {
  const x = 10;
  bar();
}

function bar() {
  console.log(x);
}

foo();
bar();
```

위의 코드를 실행하게 되면 javascript는 Lexical scope를 따르고

bar 함수는 전역에 선언되었기에 bar 함수의 상위 scope는 Global scope이 되고

따라서 x의 값인 1을 2번 출력하게 된다.
