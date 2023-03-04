## async, await

async와 await은 Promise를 조금 더 편히 사용하기 위한 상당히 쉬운 문법이다.

## async

async는 function 앞에 자리한다.

```javascript
async function AsyncTest() {
  return 1;
}
```

위와 같이 function 앞에 async가 자리하게 되면

해당 function은 항상 Promise를 반환한다.

설령 Promise가 아닌 다른 값을 반환하더라도 resolved promise로 감싸 반환시킨다.

## await

await은 '기다리다' 라는 뜻을 가졌다.

말 그대로 await은 Promise가 처리될 때까지 기다린다.

await은 일반 함수에 사용될 수 없으며 promise.then 보다 가독성도 좋고 쓰기도 쉽다.

```javascript
async function AsyncTest() {
  let promise = new Promise((resolve, reject) => {
    setTimeout(() => resolve("완료!"), 1000);
  });

  let result = await promise;

  alert(result);
}

AsyncTest();
```

위의 코드를 실행하면 await의 성질에 따라 1초뒤에 "완료"가 출력된다.
