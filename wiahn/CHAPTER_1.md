코틀린 3강으로 끝내기 - 1강. 코틀린 기본 문법
===========================================

### 0) 기초
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
    for( i in 1..10 ){ // 1 ~ 10까지의 합
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

---
### 7) NollNull과 Nullable
- Java와 Kotlin을 구분하는 특징점 중 하나이다.
- Java에서 NPE(Null Point Exception)은 Runtime exception이다. 즉, 실행/디버깅을 통해서만 알 수 있는 error이다.
- Kotlin에서는 NPE을 '?'(엘비스 연산, Elvis Operation)을 통해 Complie 할 때 검사할 수 있도록 한다.

```kotlin
fun nullCheck(){
    // 원래 Kotlin에서 String type 변수는 'null'이 할당되면 안된다.
    // (ex) var error_name : String = null은 사용할 수 없다.
    var name : String = "Wooil"
    
    // null을 넣고싶으면 '?'(Elvis Operation)을 type이후에 적어주면 된다.
    var nullName : String? = null
    
    // null이 될 수 있는 변수 다음엔 '?'을 넣어주어야 한다.
    var nameInUpperCase = name.uppercase()
    var nullNameInUpperCase = nullName?.uppercase()

    val lastName : String ?= "Hong"
    val fullName = name + " " +(lastName?: "NO lastName")
}

fun ignoreNulls(str : String?){
    // 특정 변수가 null일 가능성이 없다고 확신할 때, '!!' 을 붙일 수 있다.
    // 하지만, 사용을 지양하는 것이 좋다.
    val mNotNull : String = str!!
    val upper = mNotNull.uppercase()
    println("upper is ${upper}")
    
    // email이 null이 아니기 때문에 let 내부가 실행됨.
    val email : String ?= "joycehongXXXX@nana.com"
    email?.let{
        println("my email is ${email}")
    }
    
    // email2가 null이어서 let 내부가 실행이 안됨.
    val emailNull : String ?= null
    emailNull?.let{
        println("my email is ${emailNull}")
    }
}
```

---
### 8) Class
- Java와 달리, Kotlin에서는 file과 class의 이름이 일치하지 않아도 된다.
- 생성자 (Constructor)
```kotlin
// Method 1. 'contructor' keyword 사용할 때
class Human constructor(val name : String = "Anonymous"){ // name의 default: "Anonymous"
}

// Method 2. 'contructor' keyword 사용하지 않을 때
class Human (val name : String = "Anonymous"){ // name의 default: "Anonymous"
}

// 오버로딩(Overloading)
class human (val name : String = "Anonymous"){
  // kotlin overriding
  constructor(name_ : String, age : Int) : this(name_){
    println("My name is ${name_}, ${age} years old")
  }
}

```

- 클래스 내 메소드 작성과 객체를 생성하는 법
```kotlin
class Human constructor(val name : String = "Anonymous"){
  // init 내부는 객체 생성시에 실행된다.
  init {
    println("New human has been born!")
  }

  fun eatingCake(){
    println("This is so YUMMY!")
  }
}

fun main(){
  // Kotlin에서는 Java와 달리 객체 생성 시에 'New' Keyword를 쓰지 않는다.
  val human = Human()
  human.eatingCake()
}
```

- 상속과 오버라이딩(Overriding)
```kotlin
// Kotlin은 default가 Final class이므로, class앞에 open을 붙여주어야 상속이 가능하다.
open class Human constructor(val name : String = "Anonymous"){
     fun eatingCake() {
        println("This is so YUMMY!")
    }

    open fun singASong(){
        println("lalra!")
    }
}

// 상속을 위해 Kotlin은 ':'을 사용한다. (Java는 'Extend')
// 상속 가능한 클래스 수는 1개로, Java와 같다.
class Korean : Human(){
    // overriding을 위해 원하는 부모클래스의 함수에 'open' keyword를 넣어주어야 한다.
    // override할 함수에는 'override' keyword를 붙여준다. 
    override fun singASong(){
        // 'super' 객체를 통해 부모클래스의 함수를 사용할 수 있다.
        super.singASong()
        println("랄라라")
        println("my name is :${name}")
    }
}

fun main() {
    val korean = Korean()
    korean.singASong()
}

```
