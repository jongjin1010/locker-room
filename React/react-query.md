# React-Query

## **개념**

<br>

**React-Query**는 데이터 Fetching, 동기화, 서버 데이터 업데이트 등을 쉽게 만들어 주는 React 라이브러리이다.

기존에 **Recoil**과 같은 상태 관리 라이브러리들은 클라이언트 쪽의 데이터들을 관리하기에 적합할 순 있어도
서버 쪽의 데이터들(+ 비동기)을 관리하기에는 적합하지 않은 점들이 있어 **React-Query**를 공부하게되었다.

<br>

## **사용하게된 이유**

<br>

React-Query는 앞서 말했듯이 Fetching이나 서버 데이터 업데이트 등에 효과적이다.

React-Query를 프로젝트에 도입하게된 이유는 게시판 프로젝트를 진행하던중에 댓글의 작성, 수정, 삭제를 개발하면서

**Optimistic UI Update** (_먼저 페이지의 UI 상에서 백엔드의 요청을 기다리지 않고 즉각적으로 반응이 보이도록 하는것_)를 사용해야했고

이에 대한 방법을 찾던 중 React-Query를 사용하게 되었다.

<br>

## **react-query 사용법**

<br>

### **데이터 가져오기**

우선 먼저 기본 데이터를 GET Method를 통해 가져와야하는데 이때는 **useQuery를** 사용한다.

아래는 **useQuery의** 기본 구조이다.

```typescript
const requestData = useQuery(query key, query method, 옵션);
```

**Key는** 추후 업데이트가 일어난 후 변화된 데이터를 적용하기위해 사용된다.

**Method는** **Key가** 호출이될때 실행이되는 Fetching Method 이다.

옵션은 꽤 많은 옵션들이 존재하고 이는 [공식문서](https://tanstack.com/query/v4)에 자세히 나와있다.

이러한 구조에따라 다음과같이 코드를 작성할수있다.

```typescript
const fetching = async () => {
  try {
    await axios.get("BASE_URL/getData");
  } catch (e: any) {
    console.log(e);
  }
};

const commentsQuery = useQuery({
  queryKey: "comment",
  queryFn: fetching,
});
```

<br>

### **데이터 업데이트하기**

데이터 변경 및 삭제에서는 **useMutation을** 사용한다.

아래는 **useMutation의** 기본 구조이다.

```typescript
const requestData = useMutation(API Method, Callback);
```

**API Method로 Data의 변경이나 삭제에대한 요청을 한다.**

**Callback은 onSuccess, onErrored, onSettled를 통해 요청 후 로직을 작성하고,**

**그 로직안에서 useQuery의 Key를 통해 쿼리를 무효화해서 새로운 데이터를 패칭하도록 해야한다.**

다음은 댓글을 추가하는 코드이다.

```jsx
<Button onClick={() => addComment()}></Button>
```

```typescript
const onAddComment = async () => {
  return comment.addComment(Number(params.postId), content); //댓글추가 api (POST)
};

// mutation
const { mutate: addComment } = useMutation(onAddComment, {
  onSuccess: () => {
    queryClient.invalidateQueries("comment");
  },
  onErrored: (error) => {
    // Error 로직
  },
  onSettled: () => {
    queryClient.invalidateQueries("comment");
  },
});
```

**코드를 보면 onClick을 통해 mutate 메서드를 이용하여 useMuation이 실행된다.**

그러면 onAddComment를 통해 댓글이 추가되고

콜백함수들에 따라 추후 로직이 실행이된다.

**여기서 onSuccess, onErrored는 성공과 실패 후의 작업을 말하고, onSettled는 성공, 실패 여부에 상관없이 실행되는 작업을 뜻하는데**

이렇게 되면 성공이나 실패시 아까 **useQuery** 에서 선언해두었던 key를 통해 **invalidateQueries**() method를 이용하면 쿼리가 무효화되고
_->_ `queryClient.invalidateQueries("comment")`

이에 따라 새 데이터가 패칭이되며 **Optimistic UI Update** 가 구현된다.

다음 글과 함께 읽는 것을 추천한다.

https://roronoa-jongjin.tistory.com/5
