# Navigation Component

오늘은 하나의 *Activity* 로 여러 *Fragment* 를 돌려가며 앱을 구성해보았다면 

익숙한 컴포넌트인 __Navigation Component__ 에 대해 내가 공부한 것을 정리해보려고 한다


<br>

## 🧐 Navigation Component 란
---

![image](https://user-images.githubusercontent.com/81551906/156932709-87901dae-1490-44e3-8632-9f2d650115d9.png)

*Navigation Component* 란 Jetpack에 포함되어 있는 컴포넌트로써

 *어플 안의 흐름을 **그래프**로 지정하여 네비게이션처럼 동작하게 하는 것이다*

<br>

## 🤔 왜 Navigation Component 를 써야할까
---
우선 Navigation Component 를 사용하면

![image](https://user-images.githubusercontent.com/81551906/156932626-b6d51503-abbc-46bf-b338-2b17d6fe4346.png)

*Single Activity - Multi fragment* 구조로

여러 Fragment 를 하나의 Activity 로 묶어서 사용한다

이렇게 사용하게되면 이러한 장점들이 생긴다

- *FragmentManager를 통한 화면 전환을 직접 할 필요가 없다*
- **SharedElement Animation을 지원한다**
- *LifecycleOwner로 Fragment를 사용하면 메모리 누수가 발생할 수 있다. LifecycleOwner로 ViewLifecycleOwner를 사용하면 된다*
- **popUpTo 를 사용하면 특정 위치까지 되돌아갈 수 있다**

<br>

## 🔊 사용시 유의점
---
기본적으로 프레그먼트는 액티비티에서 동작하기 때문에 하나의 Window에서 여러 프레그먼트가 존재하는것인데

SystemUI 를 각각 다르게 가져가고 싶을 수 있다

이럴때는 Activity Scope내에서 LiveData 또는 interface를 구현하여

시스템 UI를 변경하는 것이 좋다

<br>

# MVVM

오늘은 내가 _Activity_ 에 모든 코드를 집어넣다가 기능을 바꾸거나 수정을 했을 때 어려움을 겪어

공부했었던 __MVVM__ 패턴에 대해 내가 공부했던 것을 정리해보려한다

<br> 

## 🧐 MVVM 패턴이란
---

*Model* , *View* , *ViewModel* 을 구성으로하는 패턴이다

기존의 있던 디자인패턴인 MVC 와 MVP 를 보강하기 위해 나왔다는 말도 있다

MVVM의 구조는 아래와 같다.

![image](https://user-images.githubusercontent.com/81551906/156981485-96b8b869-3117-48f0-9c13-809737593959.png)


<br>

## 🤔 왜 MVVM 패턴을 사용해야할까

---

![image](https://user-images.githubusercontent.com/81551906/156983568-50f8954a-3fdd-4123-af74-2a573507b140.png)


기존의 __MVC__ 패턴은 구현하기 쉬운 장점이 있지만 _Controller_ 가 _model_ 과 _view_ 사이에서 바쁘게 움직이면서

__Controller 의 동작은 무거워지고 이 때문에 코드를 유지보수 하는데에 있어 메모리 누수 현상등의 어려움을 겪었다__

하지만 __MVVM__ 패턴 에서는

__MVC__ 와 달리 Controller 의 동작을 분리하여 유지보수를 더욱 쉽게 만들어준다

__MVVM 은 Model , View , Viewmodel 로 이루어져 있다__

<br>

### View

- __View__ 는 사용자의 _Action_ 을 받는다 (button click 등)
- 또 __Viewmodel__ 의 데이터를 관찰하여 __UI__ 를 갱신한다

### ViewModel

- __View__ 에서 요청받은 __Data__ 를 __Model__ 에 요청한다
- 또 다시 __Model__ 로 부터 요청받은 __Data__ 를 받는다

### Model

- __Model__ 은 __ViewModel__ 이 요청한 __Data__ 를 반환해준다

<br>


## ✔ 정리

> __View__ 가 필요로 하는 Data 를 ViewModel 이 쥐고있고 View 는 그 Data 를 _Observing_ 하며 UI 업데이트에만 집중한다

이렇기에 __UI 업데이트가 간편해지고 ViewModel 이 Data를 쥐고있기에 메모리 누수 현상이 발생할 가능성이 없어진다__ !

