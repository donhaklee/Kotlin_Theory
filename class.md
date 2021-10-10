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
