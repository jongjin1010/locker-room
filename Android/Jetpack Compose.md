# Jetpack Compose

오늘은 최근 **Android** 에서 주목을 받고있는**Jetpack Compose** 에 대해 정리해보려고 한다

<br>

>### **😎 Jetpack Compose 란 ?**

<br>

![image](https://miro.medium.com/max/1400/1*2v6zotc8p-bt9oX2mI0vkQ.png)

**Jetpack Compose** 는 ***Swift UI*** 와 같은 선언형 UI 중 하나이다

<br>

 기존의 **Android** 의 ***xml*** 에서는 특정한 상황에 따라 **UI** 가 어떻게 보여질지에 대해 구현을 해야했었다면

**Jetpack Compose** 는 이와 반대로
 특정 상태에 따라 **UI** 가 무엇을 보여주면 되는지에 대해 구현하면 된다

 <br>

 이러한 방식들은 다음과 같은 장점들을 가져온다


- 상황에 따른 **UI** 를 작성하기 위해 더 적은 코드를 사용한다

- **kotlin 100%** 로 이루어져 기존 언어의 유연성을 활용 가능하다

- 뷰의 속성 등을 경우에 따라 상세하게 작성하지 않아도 되므로 재사용이 가능하다

<br>

또 **Jetpack Compose** 는 호출비용(**Composable 함수**) 독특한 랜더링 방식을 가지고 있다

그 랜더링 방식은 다음과 같다

- **Composable 함수** 는 순서와 관계없이 실행될 수 있다

- **Composable 함수** 는 동시에 실행할 수 있다

- **Recomposition** 은 새 상태에 따라서 취소되고 다시 시작할 수 있다

