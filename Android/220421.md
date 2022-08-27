# Paging Library

<br>

오늘은 **DiffUtil** 을 공부하다가 알게된 **Paging Library** 에 대해 정리해보려고한다

<br>

<br>

## 😎 Paging Library 란 무엇일까 ?

<br>

**Paging Library** 는 **로컬 DB** 또는 **Remote** 의 데이터를 페이지 단위로 **UI** 에 쉽게 

표현할 수 있도록 도와주는 라이브러리다

<br>

원래 **Paging** 을 구현할 때 **Library** 를 사용하지 않으면 **RecyclerView** 의 리스트가

상단이나 하단에 도달했는지 구분해주는 코드를 작성하고 다음의 리스트를 로드하는 

코드를 작성해야했었다

<br>

페이징이 필요한 모든 **View** 에 위와같은 로직을 작성했고 예외 처리 코드도 가득했다

<br>

이러한 문제점들을 포함한 다양한 문제들을 해결하기 위해 출시된게 **Jetpack Paging Library** 이다

*현재는 Paging 3 버전 Library 를 사용한다*

<br>

<br>

## 👻 Paging Library 3

<br>

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FsNvbv%2Fbtq79MOD243%2FbZ69OgaksIHed4VBPK7o5K%2Fimg.jpg)

<br>

**Paging 3** 은 **Project** 의 관심사 분리를 필요로 하며 , **Android** 권장 아키텍처에 통합된다

이러한 **Paging 3** 은 **Repository**, **ViewModel**, **UI** 이 3가지 레이어에서 작동된다

<br>

- **Repository Layer**


  - **PagingData**

    이미 **Paging** 작업이 끝난 데이터의 **Container** 역할을 한다 

    데이터가 새로고침되면 이에 맞는 **PagingData** 가 별도로 만들어진다

    <br>

  - **PagingSource**

    **로컬 DB** 나 네트워크로 데이터를 불러오는 추상클래스다 

    **Paging Source** 는 데이터 소스와 데이터를 가져오는 방법을 정의한다

    <br>

  - **RemoteMeditor**

    네트워크에서 불러온 데이터를 **로컬 DB** 에 캐시 후 불러온다

    오프라인 환경에도 캐시된 데이터를 불러온다

    <br>

- **ViewModel Layer**


  - **Pager**

    **Repository Layer** 에서 구현된 **Paging Source** 와 함께 **Paging Data**

    인스턴스를 구성하는 반응형 스트림을 생성한다

    <br>

- **UI Layer**

    - **PagingDataAdapter**


       **PagingData** 를 ***RecyclerView*** 에 바인딩하기 위해 사용된다

        데이터를 어느 시점에서 더 받아올 것인가 등 **UI** 와 관련된 대부분의 일을 책임진다



