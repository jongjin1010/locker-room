# 사전빌드업 

MVC 패턴 공부전에 모르는 단어들을 공부했다

> 💡 **MVC 패턴이란?**

MVC는 안드로이드와 관계없이 프로그래밍 시 가장 널리 사용되는 구조 중 하나이며 간단하게 **Model, View, Controller**의 약자인데,

그래서 Model과 View , 그리고 Controller를 알아보았다 
# MVC 패턴에서 Model, View, Controller 가 하는 일
![](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/48a5c07a-016f-4ad5-890f-3d95f9e83265/Untitled.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=AKIAT73L2G45EIPT3X45%2F20211208%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20211208T141727Z&X-Amz-Expires=86400&X-Amz-Signature=ba27a9d2c04006a0e48417ca76091faf2a19776d24e1e63b40ed2370c616c4a5&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22Untitled.png%22&x-id=GetObject)
## Model
- **애플리케이션의 정보, 데이터**를 나타낸다. 
- 데이터베이스, 처음의 정의하는 상수, 초기화값, 변수 등을 뜻한다
## View
- 안로이드에서 **눈에 보이는 모든 것**을 의미한다 . 
- 배치하는 모든 View 들은 Class로 제공되는데 모두 View 라는 클래스를 상속 받은 것이다
## Controller
- 애플리케이션에서 **발생하는 일을 담당**하는 것이다. 
- 모델에서 데이터가 변화되는 것에 따라 컨트롤러는 **뷰의 상태를 적절하게 업데이트**하도록 결정할 수 있다

