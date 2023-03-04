## Promise란?

Promise란 자바스크립트 비동기 처리에 사용되는 객체이다.

비동기 연산이 끝나면 결과에 대해 처리기를 연결하여 마치 동기 메서드처럼 값을 반환한다.

## Promise의 상태

Promise는 세 가지 상태를 보유한다.

- fulfilled : 작업이 성공적으로 수행됨
- rejected : 작업이 실패함
- pending : fulfilled도, rejected도 아닌 상태 (보류 상태)

여기서 Promise의 결과는 fulfilled, rejected 뿐이며

결과가 나온 시점을 settled 라고 표기한다.

## Promise 생성하기

기본적으로 간단한 Promise를 생성해보자.

```javascript
function contdown (seconds){
      return new Promise(
    		funciton(resolve, reject){
    	    for(let i=seconds; i >=0; i--){
    	      setTimeout(function(){
    	        if(i>0)
    	          console.log(i+ '...');
    	        else
    	          resolve(console.log('GO!'));
    	      }, (seconds-1) * 1000);
    	    }
      });
    }
```

생성을 할 때에는 resolve와 reject를 callback으로 가지는 함수로 Promise 인스턴스를 생성 가능하다.

## Promise 사용하기

그렇다면 이제 생성된 함수를 기반으로 Promise를 사용해보자.

보통 Promise를 사용할 때에는 보편적으로 두 가지 방법이 존재한다.

### 1. Then

```javascript
countdown(10).then({
  function() {
    // 성공
  },
  function(error) {
    // 에러처리
  },
});
```

### 2. Then + Catch

```javascript
const dummy = countdown(10);

dummy.then(function () {
  // 성공
});
dummy.catch(function () {
  // 에러처리
});
```
