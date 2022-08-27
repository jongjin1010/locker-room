# 효율적인 코딩

오늘은 효율적인 코딩에 대해 배운 것을 써보려고 합니다

효율적인 코딩을 하는이유에는 여러가지 이유가 있겠지만 오늘은 속도에 중점을 두어 써보겠습니다

## 예제

**두개의 숫자를 입력받아 두 수의 합을 구하는 문제를 풀어보자**

```
fun main(){
    val sc : Scanner = Scanner(System.`in`)

    val a = sc.nextInt()
    val b = sc.nextInt()

    println(a+b)
}
```
*보통은 이렇게 간단하게 풀수있습니다*

**하지만 여기서 효율적으로 코드를 작성하면**
```
fun main() = with(BufferedReader(InputStreamReader(System.`in`))) { 

    print(
        readLine() 
        .split(" ") 
            .sumOf { it.toInt() }) 
    
}
```
**이렇게 작성해볼 수 있는데,**

 **이렇게 코드를 짜면 첫번째 코드와 입출력 속도의 차이를 8배나 낼 수 있습니다**

---

## 코드설명

그럼 이 코드 한 줄 한 줄 마다 쓰는 이유를 파악해보겠습니다
```
fun main() = with(BufferedReader(InputStreamReader(System.`in`)))
```
-  첫번째 줄의 이 코드는 입력시간의 효율을 위해 작성했으며, 별다른 의미는 없습니다

```
    readLine()
```
- 이 부분은 그냥 말 그대로 한줄을 스캔한다는 의미입니다

```
.split(" ")
```
- 이 부분은 공백단위를 구분하기 위해 작성하였습니다

```
.sumOf { it.toInt() }) 
```
- 이 부분에서는 입력받은 배열의 합을 구하기 위해 sumOf 라는 메서드를 이용한 코드입니다

---

# 결론
> 코드의 사소한 차이에 따라 다른 면에서의 큰 차이를 불러올 수 있다 !
