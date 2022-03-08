# Data class 와 Enum class

오늘은 __class__ 를 공부하면서 알게된 **data class** 와 **enum class** 에 대해

내가 공부 한 것을 정리해보려고 한다 😎

<br>

## 🤷‍♂️ data class 란 무엇일까

---

![image](https://miro.medium.com/max/1280/1*0aJHAfRmoOM2BSw_dPGDMw.jpeg)

**data class** 는 **Data** 를 다루기에 최적화된 **class** 이다

이러한 **data class** 는 5가지 기능을 내부에서 자동적으로 구현을 해준다

<br>

### **1. equals()**

<br>

*equals()* 는 이름 그대로 내용의 동일성을 판단해준다

```
fun main() {
    
    val a = Data("다준", 501)

    println(a == Data("다준", 501))
}

data class Data(val name: String, val id: String)
```

다음과 같은 코드를 입력하면 
```
true 
```
라는 결과값이 출력된다

<br>

### **2. hashcode()**

<br>

*hashcode()* 는 객체의 내용에서 고유한 코드를 생성해준다

```
fun main() {
    
    val a = Data("다준", 501)

    println(a.hashcode())
}

data class Data(val name: String, val id: String)
```

다음과 같은 코드를 입력하면

```
46909878
```

위와 같은 고유 코드가 출력된다

<br>

### **3. toString()**

<br>

*toString()* 은 포함된 속성을 보기쉽게 나타내준다

```
fun main() {
    
    val a = Data("다준", 501)

    println(a)
}

data class Data(val name: String, val id: String)
```

```
Data(name=다준, id=501)
```

위와 같은 결과값이 나온다

<br>

### **4. copy()**

<br>

*copy()* 도 이름 그대로 객체를 복사하여 똑같은 내용의 새 객체를 만든다

```
fun main() {
    
    val a = Data("다준", 501)

    println(a.copy())
    println(a.copy("종진"))
    println(a.copy(id = 502))
}

data class Data(val name: String, val id: String)
```

다음과 같은 코드를 입력하면

```
Data(name=다준, id=501)
Data(name=종진, id=501)
Data(name=다준, id=502)
```

위와 같은 결과값이 나온다

<br>

### **5. componentX()**

<br>

*componentX()* 는 속성을 순서대로 반환해준다

```
fun main() {
    val list = listof(Data("태인", 212),Data("오성", 213),Data("현빈", 214))

    for((a,b) in list) {
        println("${a}, ${b}")
    }
}

data class Data(val name: String, val id: String)
```

다음과 같은 코드를 입력하면

```
태인, 212
오성, 213
현빈, 214
```

이런 결과 값들이 출력된다

<br>

## 🤷‍♂️ enum class 란 무엇일까

---

![image](https://www.journaldev.com/wp-content/uploads/2018/02/kotlin-enum-class.png)

**enum class** 는 *enumerated type* 으로 열거형의 준말이며 **enum class** 내에서

상태를 구분하기 위해 객체들에 이름을 붙여 여러개 생성해두고 그 중 하나의 상태를

선택하여 나타내기 위한 클래스이다

<br>

이런 **enum class** 도 여러가지 특징을 가지고 있다

<br>

### **1. 대문자**


<br>

```
enum class Color {
    RED,
    BLUE,
    GREEN
}
```

**enum class** 안의 객체들은 위와 같이 대문자로 기술한다


<br>

### **2. 속성**

<br>

**enum class** 의 객체들은 고유한 속성을 가질 수 있다

```
enum class Color (val message: String){
    RED("레드"),
    BLUE("블루"),
    GREEN("그린")
}
```

위와 같이 **enum** 에 생성자를 만들어 객체를 선언하도록 하면

객체를 선언 할 때 속성도 설정 할 수 있다

이것을 직접 확인해보면

```
fun main() {
    
    val color = Color.BLUE
    println(color.message)
}


enum class Color (val message: String){

    RED("레드"),
    BLUE("블루"),
    GREEN("그린")
}
```

```
블루
```

다음과 같은 결과 값이 나오는 것을 확인 할 수 있다

<br>

### **3. 함수**

**enum class** 도 일반 **class** 처럼 함수를 추가 할 수 있다 

함수를 추가 할 땐

```
enum class Color (val number: Int){
    RED(1),
    BLUE(2),
    GREEN(3);

    fun isRed() = this == Color.RED
}
```

위와 같이 객체의 선언이 끝나는 위치에 *세미콜론(;)* 을 추가한 후

함수를 적어주면 된다

그리고 이 함수를 직접 사용하면

```
fun main() {

    val color = Color.RED
    println(color.isRed())
}


enum class Color() {

    RED,
    BLUE,
    GREEN;

    fun isRed() = this == Color.RED
}
```

```
true
```

위와 같은 값이 출력된다


<br>

## 🔊 정리

---

**data class** 와 **enum class** 는 

일반 클래스에서 제공되지 않는 특정한 용도의 기능들을 제공해주고 있다

따라서 여러가지 상황에서 잘 사용하면 유용 할 수 있을 것 같다
