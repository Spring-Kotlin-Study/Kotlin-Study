# 1. Kotlin 기본 문법
## 1) 함수
```kotlin
fun 함수이름(파라미터) : ReturnType {
  CodeBody
}

fun helloWorld() : Unit {
    println("hello world")
}

fun add(a : Int, b : Int) : Int {
    return a + b
}
```
- Unit : Return type void와 같은 개념이며 생략해줘도 된다.

## 2) val vs var
```kotlin
fun valvar() {
    val a : Int = 10
    var b : Int = 9
    // a = 100 (다시 할당 불가)
    b = 100
}
```
- 변수 생성 시 초기값을 할당한다면 변수 타입 지정안해줘도 된다. (자동 추론)
- val : 변하지 않는 값 / var : 변할수 있는 값

## 3) String Template
```kotlin
fun stringTemplate() {
    var hangul = "가나다"
    var alpha = "abc"

    println("output : ${hangul + alpha}")
}
```
- {} 안에 표현식 계산해서 return해준다.

## 4) 조건식
### [참고] Expression vs Statement
- Expression : 값을 리턴 / Statement : 실행이 목적
- 즉, Kotlin의 모든 함수는 Expression이다. (Return type이 없더라도 Unit을 반환)

### 1.4.1 if문
```kotlin
fun maxBy(a: Int, b: Int) : Int {
    if(a > b) return  a
    else return b

    var temp = if(a > 100) 100 else a
}

fun maxBy2(a: Int, b: Int) : Int = if(a>b) a else b
```
- if문을 사용해서 삼항연산자처럼 쓰일 수 있다. (if문을 expression으로 사용)

### 1.4.2 when
```kotlin
fun whenPractice(score: Int) {
    when(score) {
        0 -> println("this is 0")
        1, 2 -> println("this is 1, 2")
    }
}
```
- Kotlin의 when구문은 다른 언어에서의 switch문을 대체

```kotlin
fun whenPractice(score: Int) {
    var temp = when(score) {
        0 -> 1
        1 -> 2
        else -> 3
    }
    
    when(score) {
        in 90..100 -> println("90 over")
        in 10..80 -> println("not bad")
        else -> println("okay")
    }
}
```
- 리턴 식으로도 쓸 수 있음 (이 경우, else를 꼭 써줘야 함)
- in .. 을 사용해서 범위도 지정할 수 있다.

## 5) Array vs List
### 1.5.1 Array
```kotlin
fun arrayPractice() {
    val array : Array<Int> = arrayOf(1, 2, 3)
    val array2 : Array<Any> = arrayOf(1, "2", 4.5f)
}
```
- 메모리가 할당되어지기 때문에 이후에 크기를 변경할 수 없음
- array는 mutable하다. 즉, 인덱싱을 통해 값을 변경하는 것이 가능하다.

### 1.5.2 List
```kotlin
fun listPractice() {
    val list : List<Int> = listOf(1, 2, 3)
    val list2 : List<Any> = listOf(1, "2", 3.3f)
    
    // MutableList
    val arrayList : ArrayList<Int> = arrayListOf<Int>()
    arrayList.add(10)
    arrayList.add(20)    
}
```
- Immutable List는 get()을 통해 값을 가져올 수 있으나 add() 할 수 없다.
- List를 Mutable하게 사용하기 위해서는 대표젹으로 ArrayList를 사용한다.

## 6) 반복문
```kotlin
fun forPractice() {
    val tempStrings : ArrayList<String> = arrayListOf("abc", "가나다", "123")

    for(name in tempStrings) {
        println("${name}")
    }

    for((idx, name) in tempStrings.withIndex()) {
        println("${idx}번째 ${name}")
    }
}
```
- 반복문 내에서 index값을 사용할 경우 : arrayList.withIndex()로 호출

```kotlin
fun forPractice() {
    for(v in 10 downTo 2 step 2) {
        println(v)
    }
}
```
- 범위 표현 방식
1. x..y : x부터 y
2. x until y : x부터 y-1
3. x..y step z : x부터 y (z 간격)
4. x downTo y step z : x부터 y (z 간격)

## 7) Nullable / NonNull
### 1.7.1 Nullable
```kotlin
fun nullCheck() {

    var name = "kim"
    var nullName : String? = null

    var nameToUpperCase = name.uppercase()
    var nullNameToUpperCase = nullName?.uppercase() // null이면 null return

    // ?: 연산자
    var temp : String? = null
    var fName : String? = "$name " + (temp ?: "No temp")  // ?: null이면 리턴할 값 설정 가능

}
```
- 변수 생성시, Type 뒤에 ?를 붙이면 null값을 할당할 수 있다.
- 메소드 실행 시, 객체가 null일 수 있다면 객체의 변수명 뒤에 ?를 붙인다.
  - 이 경우, null이라면 null을 리턴한다.
- ?: 연산자
  - null이라면 리턴할 값을 설정할 수 있다.

### 1.7.2 NonNull
```kotlin
fun ignoreNull(str: String?) {
    var mNotNull : String = str!! // 절대 여기에 null이 들어오지 않음을 보장할 때 !!사용
    println(mNotNull.uppercase()) // ? 안붙여도 에러 발생하지 않는다.

    var email : String? = "email@naver.com"
    // 이 경우, email값이 null이 아니면 {} 안의 구문을 실행
    email?.let {
        println(email.uppercase())
    }
}
```
- !! : nulll이 아님을 보장할 때 사용
- let 함수: 자신의 receive 객체를 람다식 구문 안에서 사용 시 선언

## 8) Class
### 1.8.0 Class 기본 구현
```kotlin
class Human(val name: String = "initial Name") {

    var humanName : String? = null
    var humanAge : Int? = null
    
    init {
      // 생성되었을 시 호출 (가장 먼저 실행)
    }

    // 부생성자를 통해 오버로딩
    constructor(name : String, age: Int) : this(name) {
        humanName = name
        humanAge = age
    }

    fun eatingCake() {
        println("good")
    }

}

fun main() {
    var hm = Human("kim")    // new 키워드 필요 X

    var hm2 = Human("zzz", 12)
}
```
### 1.8.0 상속
- constructor 키워드를 통해 생성자를 구현
- 부 생성자를 선언하여 오버로딩할 수 있다.
  - 부 생성자 constructor는 항상 주 생성자의 위임을 받아야함

```kotlin
open class Human(name: String = "initial Name") {

    var humanName : String? = name
    var humanAge : Int? = null


    constructor(name : String, age: Int) : this(name) {
        humanName = name
        humanAge = age
    }

    open fun eatingCake() {
        println("good")
    }

}

class Korean : Human() {

    override fun eatingCake() {
        super.eatingCake()
        println("eatingCake in korean")
    }
}

fun main() {
    var korean = Korean()

    korean.eatingCake()
}
```
- kotlin의 class는 기본적으로 final 이라서 상속받을 class를 open 붙여줘야 함
- 메소드를 오버라이딩할 때도 부모 class의 메소드를 open해줘야 한다.

# 2. Kotlin 고급 문법
## 1) 람다식
```kotlin
val square : (Int) -> (Int) = {num -> num*num}  // { } 안에 argumentList에서 type 지정해줘도 됨

val nameAge = {name:String, age:Int ->
    "my name is ${name} and I'm ${age}"
}
```
- 람다의 기본 정의
  - val lambdaName : Type = {argumentList -> codeBody}

- Lambda : value처럼 다룰 수 있는 익명 함수
  - 메소드의 파라미터로 넘겨줄 수 있음
  - return 값으로 사용할 수 있음


## 2) 확장함수
```kotlin
val pizzaIsGreat : String.() -> String = {
    this + "pizza is the best"
}

fun extendString(name : String, age : Int) : String {

    val intrduceMyself : String.(Int) -> String = {
        "my name is ${this} I'm ${it}"
    }   // this : 확장함수를 call하는 object, it : param

    return name.intrduceMyself(age)
}
```

## 3) 람다의 return

```kotlin
val calculageGrade : (Int) -> String = {
    when(it) {
        in 0..40 -> "fail"
        in 41..70 -> "pass"
        in 71..100 -> "perfect"
        else -> "error"
    }
}
```

## 4) 람다의 다른 표현 방법
```kotlin
fun main() {
    val lambda : (Double) -> Boolean = {
        it == 4.123
    }
    println(invokeLamda(lamda))
    println(invokeLamda({ it == 5.234 }))
    println(invokeLamda{it == 5.234 })   //funtion의 마지막 파라미터가 lamda일 때는 () 생략 가능
}

fun invokeLamda(lamda : (Double) -> Boolean) : Boolean {
    return lamda(5.234)
}
```


## 5) data class
```kotlin
data class Ticket (val companyName : String,
                   val name: String,
                   var date : String,
                   var seatNumber:Int)
```
- toString(), hashCdoe(), equals(), copy()

## 6) companion object
```kotlin
class Book private constructor(id:Int, name : String) {
    companion object BookFactory {  // Interface 상속도 가능함
        fun create() = Book(0, "temp")
    }
}

fun main() {
  var book : Book = Book.Companion.create()
}
```
- companion object
  - 자바의 static 대신에 사용되는 것으로 정적인 변수나 정적인 메소드를 선언할 때 사용
  - private property or method를 읽을 수 있음


## 7) Object
```kotlin
// Singleton Pattern
object CarFactory {
    val Cars : ArrayList<Car> = arrayListOf()

    fun makeCar(horsePower: Int) : Car {
        val car = Car(horsePower)
        Cars.add(car)
        return car
    }

}
```

