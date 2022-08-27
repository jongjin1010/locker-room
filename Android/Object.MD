# Object

> **Object 란**

object란 생성자 없이 객체를 직접 만들어 내는 것이다

기존에 배웠던 class 는 인스턴스 객체를 만들기 위한

틀이어서 내부 속성이나 함수를 사용하려면 

생성자를 통해 실체가 되는 인스턴스 객체를 만들어야 했다

그런데 여러개의 인스턴스 객체가 필요하지 않고

단 하나의 객체만으로 공통적인 속성과 함수를 사용할 때는 

object 를 사용하면 된다

결국 이런 object 는 싱글톤 패턴을 언어차원에서 지원하는 것이다

> **✍ 구현**

```
fun main() {

    println(Counter.count)

    Counter.countUp()
    
    println(Counter.count)

    Counter.clear()

    println(Counter.count) 
}

object Counter {
    
    var count = 0

    fun countUp() {
        count++
    }

    fun clear() {
        count = 0
    }
}
```

**결과 값**

```
0
1
0
```

> **🚛 과정**

object 는 인스턴스를 생성하지 않고 그 자체가 객체이기에

생성자는 사용하지 않으며

object 로 선언된 객체는 최초사용시 자동으로 생성되고

이후에는 코드 전체에서 공용으로 사용 될 수 있으므로

프로그램이 종료되기 전까지 공통적으로 사용할 내용들을

묶어 만들 수 있다

그렇기에 

변수 count 와 countUp() 그리고 clear() 에 의해

0 1 0 과 같은 값이 나온 것을 알 수 있다

> **➕ 기존의 클래스안에도 object 를 만들순 없을까 ?**

이런 경우엔 Companion Object 를 사용한다

Companion Object 는 클래스의 인스턴스 기능은 그대로 사용하면서

인스턴스 간의 공용으로 사용할 속성이나 함수를 별도로 만들어준다

> **✍ 구현**

```
fun main() {

    var a = President("이")
    var b = President("윤")

    a.vote()
    a.vote() 

    b.vote()
    b.vote()

    println("${a.name} : ${a.count}")
    println("${b.name} : ${b.count}")
    println("총 : ${President.total}")
}

class President (val name: String) {

    companion object {
        var total = 0
    }

    var count = 0

    fun vote() {
        total++
        count++
    }
}
```

**결과 값**

```
이 : 2
윤 : 2
총 : 4
```

> **🚛 과정**

결과 값이 2, 2, 4 가 나온 이유는

companion object 내에 있는 total 을 공유하고 있기에

모든 인스턴스에서 투표수를 누적할 수 있기 때문이다






