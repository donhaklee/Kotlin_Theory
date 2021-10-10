# 1. 클래스
### 1) 구조
- class name
- property : 기본적으로 visibility를 세팅하면 property는 기본적으로 -로 표시되고 private를 의미한다.
- method
(encapsulation[private로 막는것], abstraction[추상화 / 필요한 것만 정의])

### 2) 생성자
- 코틀린은 자동으로 getter setter를 만든다
- 코틀린에 private을 넣으면 getter setter를 막는다는 의미

### 3) 보조생성자 (constructor)
```kotlin
class Album {
  val id:Int = 0
  var title:String = ""
  constructor (id:Int, title:String) {
    this.id = id
    this.title = title
  }
}

fun main() {
  val album : Album = Album(1, "song1")
  println(album.title) // song1
  album.title = "My song1"
  println(album.title) // My song1
} 
```
### 4) 주생성자
```kotlin
class Album(var id:Int, var title:String) {
  var price: Int = 0
  init { // 주생성자에서 추가로 작업할 내용을 정의
    price = 1200
  }
  fun changePrice(discount:Int) {
    price -= discount
  }
}
fun main() {
  val album : Album = Album(1, "song1")
  println(album.title) // song1
  album.title = "My song1"
  println(album.title) // My song1
} 
```
### 5) 상속
```kotlin
// 상속 : 코틀린은 모든 클래스가 자식을 만들 수 없다 => open 사용
open class Album(var id:Int, var title:String) {
  var price: Int = 0
  init { // 주생성자에서 추가로 작업할 내용을 정의
    price = 1200
  }
  open fun changePrice(discount:Int) {
    price -= discount
  }
}
class SubAlbum : Album {
  constructor(id: Int, title: String) : super(id, title) {
    this.artist = artist
  }
  // 일반함수는 override를 해야한다.
  override fun changePrice(discount:Int) {
    price -= discount
  }
}
fun main() {
  val album : Album = Album(1, "song1", "Boa")
  println(album.artist) // Boa
} 
```

# 2. Data class
```kotlin
// 일반클래스
class Circle(var r:Int) {
  var c1 : Circle(3)
  var c2 : Circle(3)
  c1.equals(c2)  // error
}

// Data class
data class Circle(var r:Int) {
  var c1 : Circle(3)
  var c2 : Circle(3)
  c1.equals(c2)  // error
}

```

# 3. Object class : 익명클래스
```kotlin
var rect = object { // var rect = 객체 참조변수
  var w:Int = 0
  var h:Int = 0
}

rect.w = 5
rect.h = 2 // 선언가능
```

4. Companion class
```kotlin
class Tri {
  conpanion object{
    var b:Int
    var h:Int
  }
}
fun A() { // 객체생성 없이 클래스 이름으로 접근 가능
  Tri.b = 3
}
```
---

# 5. null safety
- 코틀린은 기본적으로 null 불허이기 때문에 초기화를 시켜야한다.
- null point exception 해결
```kotlin
var r:Rect = Rect(3,2)
var r2:Rect ?= null
r2?.calc() // r2에 오브젝트가 있으면 정상 출력, null이면 지정해둔 다른 것을 호출
r2!!.calc() // r2에 오브젝트가 있으면 정상 출력, null이면 error
r2?.calc()?:0 // 0호출
```

# 6. 람다함수
### 1) structured programing
### 2) object-oriented programing
### 3) functional programing
### 4) Logical programing

```kotlin
val f = {a:Int, b:Int->a+b}
val f : (Int, Int) -> Int = { a:Int, b:Int -> a+b }

// 매개변수 x
val sq: () -> Unit = { println(x * x) }

// 매개변수 1개
val sq2: (Int) -> Int = { it * it }
```
