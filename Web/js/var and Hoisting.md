# var 와 Hoisting

함수 2개를 만들고 두가지 방법으로 실행을 하자.

```javascript
// 함수 먼저
function hello1() {
  console.log("hello1");
}

hello1();

// 함수 호출을 먼저
hello2();

function hello2() {
  console.log("hello2");
}
```

```javascript
hello1;
hello2;
```

그러면 다음과 같이 둘 다 정상적으로 출력이 된다.

여기서 아까의 코드와 같이 아래에 있던 함수를 위에서 호출할 수 있는 형태를 **Hoisting** 현상이라고 한다.

**Hoisting** 현상은 함수뿐만 아니라 변수에서도 발생한다.

```javascript
age = 6;
age++;
console.log(age);

var age;
```

위와 같이 코드를 작성해도 **Hoisting** 이 발생하여

```
7
```

정상적인 결과 값이 출력이 된다.

또 다른 예제를 확인해보자.

```javascript
console.log(name);

name = "Uhyun";
console.log(name);

var name;
```

```javascript
undifined;
Uhyun;
```

이번 코드에는 별다른 예외없이 정상적으로 값들이 출력됐다.

그렇다면 가장 아래에서 변수를 선언할때 미리 값을 넣어준다면 어떻게 될까?

```javascript
console.log(name);

name = "Siwan";
console.log(name);

var name = "Jongjin";
```

결과 값으로

```
Jongjin
Siwan
```

이 나올것이라고 생각할수있으나 실제 결과값은

```
undifined
Siwan
```

이 출력이 된다.

여기서 알 수 있는 점은 **Hoisting** 현상은

```javascript
var name;

console.log(name);

name = "Siwan";
console.log(name);

name = "Jongjin";
```

실제로는 이런구조인것인데 **var** 키워드를 사용하면 이러한 문제들이 야기되기 때문에 많은 혼란을 준다.

그렇다면 **let** 을 사용해보자

```javascript
console.log(name);

name = "Daewoo";
console.log(name);

let name;
```

```
Error: name is not defined
```

**let** 을 사용하게되면 먼저 선언이 되어야 사용이 가능해지기 때문에 **Hoisting** 문제가 사라지면서 **Error** 가 발생한다.
