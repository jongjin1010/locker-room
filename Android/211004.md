# 스코프 함수

> **Scope 함수란**

Scope 함수는 함수형 언어의 특징을

조금 더 편리하게 사용할 수 있도록 기본 제공하는 함수이다

클래스에서 생성한 인스턴스를 Scope 함수에 전달하면

인스턴스의 속성이나 함수를 좀 더 깔끔하게 불러 쓸 수 있다

> **🙃 종류**

Scope 함수에 종류로는 

**apply , run , with , also , let** 등이 있다

>> **apply**

apply 는 인스턴스를 생성한 후 변수에 담기 전

초기화를 하는 과정에서 많이 쓰인다

```kotlin
fun main() {

    val a = Book("주는나무", 10000)
}

Class Book (var name: String, var price: Int) {

    fun discount(){
        price -= 2000
    }
}
```
다음과 같은 코드에서 "아낌없이" 라는 문자열을 넣고 discount 를 수행해야한다고 하자

```kotlin
var  a = Book("주는나무", 10000)
a.name = "[아낌없이]" + a.name
a.discount()
```

기존의 경우 위와같이 

인스턴스를 저장한 변수를 통해 참조연산자를 이용해야 했지만

apply 를 사용하면

```kotlin
var a = Book("주는나무", 10000).apply {
    name = "[아낌없이]" + name
    discount()
}
```

다음과 같이 인스턴스를 생성하자 마자

인스턴스에 참조연산자를 사용하여 apply 를 붙이고

중괄호로 람다함수를 만들어

apply 의 scope 안에 직접 인스턴스의 속성과 함수를

참조연산자 없이 사용 가능하다 또 apply 는 

인스턴스 자신을 반환하므로 이렇게 생성되자마자

바로 변수에 넣어줄수 있다 이렇게 되면 코드가 깔끔해질 수 있다

>> **run**

run 은 apply 처럼 scope 안에서 참조연산자를 사용하지 않아도 된다는 점은 똑같지만

```kotlin
var b  = a.run {
    println(a.price)
    a.name

    /* 가격은 출력하지만 마지막 구문인
     이름은 b라는 변수에 할당됨*/
}
```

일반 람다함수처럼 인스턴스 대신 마지막 구문의 결과값을 반환한다

그래서 이미 인스턴스가 만들어진 후에 인스턴스의 함수나 속성을 scope 내에서 사용해야 할 때 유용하다

>> **with**

with 은 run 과 동일한 기능을 가지지만

```kotlin
a.run {...}
with(a) {...}
```

인스턴스를 참조연산자 대신 패러미터로 받는다는 차이가 전부이다

>> **also/let**

also 는 apply 와 (**처리가 끝나면 인스턴스 반환**),  let 은 run 과 (**처리가 끝나면 최종값을 반환**) 같은 기능을 가지고있지만

공통적인 차이점이 한가지 있다

apply 와 run 이 참조연산자 없이 인스턴스의 변수와 함수를

사용할 수 있었다면 also 와 let 은 패러미터로 인스턴스를 넘긴 것처럼 

it을 통해서 인스턴스를 사용할 수 있다

패러미터를 통해 인스턴스를 사용하는 과정을 거치는 이유는

같은 이름의 변수나 함수가 scope 바깥에 중복되어 있는 경우에 

혼란을 방지하기 위해서이다

```kotlin
fun main() {

    var price = 5000

    val a = Book("주는나무", 10000).apply {
        name = "[아낌없이]" + name 
        discount()
    }

    a.run {
        println("상품명: &{name}, 가격: ${price}")
    }
}

Class Book (var name: String, var price: Int) {

    fun discount(){
        price -= 2000
    }
}
```

이해를 돕기위해 코드를 작성하였다

원래는 출력된 가격의 값이 8000원이 나와야하지만

결과값은 main 함수에서 만든 변수의 값인 5000이 나온다

이는 run 함수가 인스턴스 내의 price 속성보다

run 이 속해있는 main 함수의 price 변수를 우선시하기 때문이다

그렇기 때문에


```kotlin
fun main() {

    var price = 5000

    val a = Book("주는나무", 10000).apply {
        name = "[아낌없이]" + name 
        discount()
    }

    a.let {
        println("상품명: &{it.name}, 가격: ${it.price}")
    }
}

Class Book (var name: String, var price: Int) {

    fun discount(){
        price -= 2000
    }
}
```

run 을 let 으로 바꿔준후 it 을 사용하여 출력을 하면 

원래의 price 의 결과값인 8000 이 나오게 된다

apply 의 경우도 also 와 바꿔 사용하면 된다

<br>

>**✔ 정리**

scope 함수를 사용하면 인스턴스의 속성이나 함수를

scope 내에서 깔끔하게 분리하여 사용할 수 있기 때문에

코드의 가독성을 향상시킬 수 있다



