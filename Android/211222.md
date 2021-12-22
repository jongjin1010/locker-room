# Thread

Thread 란 작업의 흐름이다

> 💡그렇다면 작업의 흐름이란 뭘까 ? 

```앱이 실행됨 -> Launcher Activity 가 실행됨 -> 버튼이 눌림 -> . . .```

다음과 같은 앱의 실행 과정이라 볼 수 있다

### MainThread
---
어떤 프로그램이 실행되기 위해서는 **반드시 Thread 가 하나 이상 존재해야한다**

이때의 무조건 존재해야 하는 하나의 Thread를 **Main Thread** 라고 한다

 >🔑Main Thread의 특징
 - **Main Thread** 는 *UI Thread* 라고 부를 수 있다
    - **UI Thread** => 사용자의 input을 받는 Thread
- **Main Thread** 는 정지시켜선 안된다
- **MainThread** 는 앱이 시작해서 꺼질때까지 꾸준히 흐른다


> 🔊그렇다면 Thread가 여러개일땐 어떻게 될까 ?

Thread가 여러개가 있다면

 기존의 *MainThread* 에서 순차적으로 했던 작업들을 각 **Thread** 가 나누어서 동시에 작업하게된다

---

---
 
 # Sharedpreference

 안드로이드의 데이터베이스에는

 - SQLiteDataBase
 - Sharedpreference

대표적으로 위의 두개가 있는데 오늘은 주로 쓰이는 **Sharedpreference** 를 공부했다

개발을 진행하다 보면, 앱의 데이터들을 저장하여 관리해야 할 상황에 직면하게 되는데

 데이터의 양이 많거나 중요한 데이터라면 서버나 DB, 파일의 형태로 저장을 하면 되겠지만

 간단한 설정 값이나 문자열 같은 데이터들은 DB에 저장하기에는 부담스럽고 애매한 경우가 있다
 
  이런 경우 안드로이드에서 기본적으로 제공되는
  
  **SharedPreferences를 사용하여 데이터를 관리한다면 좀 더 편리하게 사용이 가능하다**

  🔊*Sharedpreference* 를 사용하면 쉽게 자동로그인과 같은 기능을
 구현 할 수 있다 

> 💡Sharedpreference 란 ?

**Sharedpreference** 란 뜻처럼 공유된 사용자의 기호를 저장하는 데이터베이스이다

 >🔑Sharedpreference의 특징
 - **Sharedpreference** 는 Key - Value 형식으로 이루어져 있다
 - **Sharedpreference** 는 용도가 가벼운 데이터 저장이기에 하드하게 데이터베이스 시스템을 구축 할 수 없다
 
---

---

# Async

**Async** 는 말 그대로 비동기를 뜻한다

여기서의 **비동기 방식** 은 작업을 순서대로 처리하는 동기 방식과 달리

**Thread** 를 만들어 작업을 따로 처리 하는 것 입니다

>💡 Async 사용방법
- AsyncTask 를 상속 받는다
    - *onPreExcute* : Thread 가 출발하기 전 할 작업
    - *doIntBackground* : Thread 가 할 작업
    - *onPregressUpdate* : Threa 가 작업 중 중간중간 MainThread 로 오는것
    - *onPostExcute* : 작업을 다 마친 후 MainThread 로 온다
>🔊 Async 장점
- MainThread 를 기다리게 할 필요가 없다
- 네트워크 작업 (서버통신) 등에 유용하다

https://github.com/jongjin1010/Async










