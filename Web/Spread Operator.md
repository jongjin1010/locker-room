## 정의

Spread Operator는 기존 배열이나 객체의 전체 또는 일부를 다른 배열이나 객체로 복사하는 연산자이다.

## 배열에서의 spread 연산자

### 병합

```javascript
// ======= 기존 방법 ========
const first = ['apple', 'banana'];
const second = ['grape', 'peach'];

var all = first.concat(second);

console.log(all); // ['apple', 'banana', 'grape', 'peach']

// ======= ES6 Spread 연산자 ========
const all = [...first, ...second];

console.log(all); // ['apple', 'banana', 'grape', 'peach']
```

위의 코드를 보면 원래 두 개의 배열을 하나로 합치는 경우 concat을 사용했지만

ES6에서는 spread 연산자를 사용하여 더 깔끔하게 배열을 병합한다.

### 복사

참조와 복사의 차이는 기존의 것이 변경되느냐 안되느냐의 차이이다.

기존의 변수에 할당된 배열을 새 변수에 할당하면 새 변수는 기존의 배열을 참조하게 되고

새 변수는 기존의 배열에 변경사항이 생기면 같이 변경된다.

```javascript
// ====== 참조 ======
const array = [{ name: "jongjin" }, { age: 19 }];
const ref = array;

array[0]['name'] = "minje";

console.log(ref[0]); //minje
```

이러한 이유 때문에 ES5는 slice와 map을 선택해 배열을 복사했다.

```javascript
// ======= 기존 방법 ========
var first = ['apple', 'banana'];
var second = first.map((item) => item);

var second.push('grape');

console.log(first); // ['apple', 'banana']
console.log(second); // ['apple', 'banana', 'grape']

// ======= ES6 Spread 연산자 ========
const first = ['apple', 'banana'];
const second = [...first, 'grape'];

console.log(first); // ['apple', 'banana']
console.log(second); // ['apple', 'banana', 'grape']
```

하지만 ES6의 spread 연산자를 활용해 더 깔끔한 사용이 가능하다.

## 객체에서의 spread 연산자

객체의 속성을 수정하거나 복사할때도 spread 연산자가 사용된다.

```javascript
const me = { name: "jongjin", age: 19 };
me = { ...me, hobby: "soccer" };

console.log(me); // { name: "jongjin", age: 19, hobby: "soccer" }

me = { ...me, age: 21 }
console.log(me); // { name: "jongjin", age: 21, hobby: "soccer" }
```
