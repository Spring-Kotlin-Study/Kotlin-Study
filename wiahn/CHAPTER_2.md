코틀린 3강으로 끝내기 - 2강. 코틀린 심화 문법
===========================================

### 1) 람다식 (Lambda Expression, Anonymous Function)
- 람다식(Lambda Expression)은 value처럼 다룰 수 있는 익명함수(Anonymous Function)이다.
- 람다식은 메소드의 parameter로 넘겨줄 수 있다.
- 람다식은 return 값으로 사용할 수 있다.
- 람다식은 기본적으로 아래처럼 할 수 있다.
 
```kotlin
// val [lambdaName] : [Type] = {[argumentList] -> [codeBody]}
val square_1 : (Int) -> (Int) = {number -> number*number}
val square_2 = {number : Int -> number*number}

fun main(){
  println(square_1(12))
  println(square_2(12))
}
```

- 람다식에서는 마지막에 있는 코드 줄이 return 값이다.
```kotlin
val nameAge = {name : String, age : Int ->
  "My name is ${name} and I am ${age}"
}

fun main(){
  println(nameAge("Wooil", 27))
}
```

- 람다를 표현하는 다른 방법도 있다.
```Kotlin
fun invokeLambda(lambda_func : (Double) -> Boolean) : Boolean {
    return lambda_func(5.2343)
}

fun main(){
      val lambda = {number : Double ->
        number == 4.3213
    }

    println(invokeLambda(lambda))
    println(invokeLambda({it > 3.22}))
    println(invokeLambda { it > 3.22 })
}
```

---
### 2) 확장함수(Extension Function)
- 클래스에 일부만 변경하여, 혹은 추가하여 사용하고 싶은 경우 확장함수를 사용할 수 있다.
```kotlin
val pizzaIsGreat : String.() -> String = {
    this + "Pizza is the best!" // return value
}

fun extendString(name : String, age : Int) : String {
    val introduceMyself : String.(Int) -> String = {
        "I am ${this} and ${it} years old" // this: String, it: Int
        // parameter가 1개 일때에는 it으로 지칭할 수 있음.
    }
    return name.introduceMyself(age)
}

fun main() {
    val temp1 = "Wooil said"
    val temp2 = "Woody said"
    println(temp1.pizzaIsGreat())
    println(temp2.pizzaIsGreat())

    println(extendString("ariana", 27))
}
```

---
### 3) 데이터 클래스(Data Class)
- 'data class'에서는 4개의 함수(toString(), hashCode(), equals(), copy())를 바로 사용할 수 있다.
```Kotlin
// Create 'data class'
data class Ticket(val companyName : String, val name : String, var date : String, var seatNumber: Int)
// Create 'normal class'
class TicketNormal(val companyName : String, val name : String, var date : String, var seatNumber: Int)

fun main(){
    val ticketA = Ticket("koreanAir", "WooilAhn", "2020-02-16", 14)
    val ticketB = TicketNormal("koreanAir", "WooilAhn", "2020-02-16", 14)

    // data class의 내용이 출력됨.
    println(ticketA)
    // 메모리 주소값이 출력됨.
    println(ticketB)
}
```

---
### 4) Companion Object
-  Kotlin에서 정적인 메소드나 정적인 변수를 선언할 때 사용될 수 있다. (Java의 'static' 대신 사용되는 느낌)
```kotlin
class Book private constructor(val id : Int, val name : String){
    // 이름 설정 가능
    companion object BookFactory : IdProvider{
        override fun getId() : Int {
            return 123
        }

        val myBook : String = "new Book"
        fun create() = Book(0, myBook)
    }
}

interface IdProvider {
    fun getId() : Int
}

fun main(){
    val book = Book.create()
    val bookId = Book.BookFactory.getId()
    -
    println("${book.id} ${book.name}")
}
```

---
### 4) Object
- Singleton Pattern이 사용된다. (객체가 한번만 생성되도록 한다.)
- 이에, 불필요한 메모리 사용을 막을 수 있다는 장점이 있다.
```Kotlin
object CarFactory {
    val cars = mutableListOf<Car>()

    fun makeCar(horsePower: Int) : Car {
        val car = Car(horsePower)
        cars.add(car)
        return car
    }
}

data class Car(val horsePower : Int)

fun main() {
    val car = CarFactory.makeCar(10)
    val car2 = CarFactory.makeCar(200)

    println(car)  // Car(horsePower=10)
    println(car2) // Car(horsePower=200)
    println(CarFactory.cars.size.toString()) // 2
}
``
