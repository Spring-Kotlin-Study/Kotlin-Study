코틀린 3강으로 끝내기 - 1강. 코틀린 기본 문법
===========================================

### 0) 기초 정보
 - Kotlin의 entry point는 fun main(){ } 이다.
```kotlin
fun main() {
  println("this is entry point of Kotlin")
}
```
 - Kotlin의 함수 선언은 'fun [function name] : [return value type] {}' 으로 한다.

---
### 1) 함수(Function)
 1. return value이 없는 경우 (Unit: 반환할 데이터가 없다는 것을 의미한다.)

```kotlin
fun helloWorld() : Unit {
  println("Hello World!")
}

// Unit을 생략하여 사용할 수도 있다.
fun helloWorld(): {
  println("Hello World!")
}
```
 2. Parameter와 Return value가 있는 경우
    - Parameter를 작성할 때에는 [variable name : type] 형태로 작성한다.
    - type은 첫 문자를 대문자로 작성한다. (ex) a : Int
```kotlin
fun add(a : Int, b : Int) : Int {
  return a + b
}
```

---
### 2) val vs var
- val은 '읽기 전용 변수선언 키워드'이다.
- var는 선언한 뒤에도 '값 변경이 가능한 변수선언 키워드'이다.
```kotlin
fun declare_func(){
  val a : Int = 10 // 값 변경 불가능
  var b : Int = 9  // 값 변경 가능
  
  // 변수를 선언할 때, type을 명시하지 않아도 complie error는 발생하지 않음.
  val c = 50
  var d = 100
  
  var name = "Wooil"
}
```

---
### 3) String Template
- '$'문자를 사용하여 출력문에서 String Template을 사용할 수 있다.
- '${ 수식 }'을 통해서도 사용가능하다. (즉, {} 내부의 수식은 미리 연산되어 사용될 수 있다.)
```kotlin
val name = "Wooil"
val lastName = "Ahn"
println("My name is $name") // = "My name is Wooil"이 출력됨.
println("My full name is ${name + " " + lastName}" // = "My full name is Wooil Ahn"이 출력됨.
println("Is that true? ${1==0}") // "Is that true? false"이 출력됨.
```

---
### 4) 조건식(Conditional Expression)
- Kotlin에서는 조건식이 들어간 함수를 '='을 통해 만들 수 있다.
- 아래 두 maxBy1, maxBy2 함수는 같은 기능을 수행하는 함수이다.
```kotlin
fun maxBy1(a : Int, b : Int) : Int {
  if(a > b)
    return a
  else
    return b
}

fun maxBy2(a : Int, b : Int) = if(a > b) a else b
```

- Kotlin에서의 'when' 구문은 다른 언어에서의 'swtich' 구문과 유사하다.
```kotlin
fun checkNum(score : Int) {
    when(score) {
        0    -> println("this is 0")
        1    -> println("this is 1")
        2,3  -> println("this is 2 or 3")
        else -> println("I don't know")
    }
    
    // 아래처럼 변수 선언에 'when'을 사용할 경우, 'else'를 필수적으로 사용해주어야 한다.
    var b = when(score) {
        1    -> 1
        2    -> 2
        else -> 3
    }

    when(score) {
        in 90..100 -> println("You are genius") //  90 ~ 100점
        in 10..80  -> println("not bad")        //  10 ~ 80점
        else       -> println("okay")
    }
}
```

- 끝에 값을 만들어내면 Expression이다.
- Kotlin의 모든 함수는 Expression이다.
- Java에서의 void를 return 하는 함수는 Statement이다. (return value가 없기 때문에)

---
### 5) 배열(Array, List)
- Array는 선언때부터 정해진 크기가 있다.
- List는 (1)수정이 불가능한 List와 (2)수정이 가능한 List(MutableList)가 있다.
```kotlin
fun testArrayAndList(){
    val array = arrayOf(1, 2, 3)
    val list = listOf(1, 2, 3)

    // 'Any' type의 Array는 여러 type의 변수를 한번에 담을 수 있다.
    val array2 = arrayOf(1, "d", 3.4f)
    val list2 = listOf(1, "d", 11L)

    // Array에 담겨있는 값들은 mutable하여 값 변경이 가능하다. (List는 불가능)
    array[0] = 3

    // 'ArrayList'는 대표적인 MutableList이다.
    // ArrayList의 주소 자체는 변경되지 않으므로, val로 선언해도 된다.
    val arrayList = arrayListOf<Int>()
    arrayList.add(10)
    arrayList.add(20)
}
```

---
### 6) 반복문(For, While)
  - for문에서 'withIndex()'을 사용하여 index를 쉽게 사용할 수 있다.
  - for문에서 'step', 'downTo', 'until'과 같은 Keyword를 사용할 수 있다.
```kotlin
fun testForAndWhile(){
    val students = arrayListOf("joyce", "james", "jenny", "jennifer")

    for(name in students) {
        println("${name}")
    }

    for((index, name) in students.withIndex()){
        println("${index}번째 학생 : ${name}")
    }

    var sum : Int = 0
    for( i in 1..10 ){
        sum += i
    }
    println(sum)

    sum = 0
    for( i in 1..10 step 2 ){ // [1, 3, 5, 7, 9]의 합
        sum += i 
    }
    println(sum)

    sum = 0
    for( i in 10 downTo 1 ){ // 10 ~ 1까지의 합
        sum += i 
    }
    println(sum)

    sum = 0
    for( i in 1 until 100 ){ // 1 ~ 99까지의 합
        sum += i
    }

    var index : Int = 0
    while(index < 10){
        println("current index : ${index}")
        index++
    }
}
```
