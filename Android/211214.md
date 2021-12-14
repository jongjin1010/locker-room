# ViewModel , LiveData

오늘은 강력하고 유지보수가 쉬운 앱을 만들기 위해 AAC를 알아보았다

> **앱 아키텍처 원칙**

 UI 클래스로부터 UI, OS 상호작용을 제외한 다른 로직을 분리하여 UI 클래스에 대한 의존성을 최소화하는 것이 앱 관리 측면에서 좋다

> 💡 **AAC 란?** 

 **AAC (Android Architecture Components)** 는 강력하고 유지관리가 쉬운 앱을 디자인하도록 돕는 라이브러리의 모음이다
 
오늘은 그 중 하나인 **ViewModel** 에 대해 공부했다

AAC는 

## ViewModel

**ViewModel**은 앱의 **Lifecycle**을 고려하여 UI 관련 데이터를 저장하고 관리하는 요소이다

🔑**ViewModel**를 사용하는 가장 큰 이유는 UI와 로직의 분리 때문인데

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fc0JsTS%2Fbtq6rwZXL5N%2FAJSBytvde7iKEnNGhp3bz1%2Fimg.png)

🔊*이를 사용하게 되면 **액티비티, 프래그먼트 생명주기**에 종속되지 않게 할 수 있다는 점이 가장 큰 장점이다.*

Ex) 실행되는 앱을 가로모드, 세로모드로 변경하면 값이 초기화되는데 **ViewModel**을 사용하면 값이 유지된다


## LiveData

**LiveData**는 observable 형태로 사용하여, **LifeCycle** 에 따라 데이터를 관리한다

🔑**LiveData**는 항상 최신 데이터를 유지하는데

🔊*이를 **ViewModel** 과 함께 사용하게 되면 **화면이 전환되도 최신데이터를 유지 할 수 있다**

## 

**ViewModel 과 LiveData** 의 [예제](https://github.com/jongjin1010/study_viewmodel_livedata)는 다음의 링크에서 확인 할 수 있다

(https://github.com/jongjin1010/study_viewmodel_livedata)
