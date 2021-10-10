# 0. 환경설정
### 1) JDK(Java SE)
- Java_Home
- Path <br>

### 2) Android Studio (JetBrains - intellij)
- 안드로이드 sdk - API level 31
- Plugin(sdk tools) - HAXM(Emulator : 하드웨어를 본 딴 소프트웨어)
- Android Virtual Device

## 0-1.컴파일 과정
### 1) c언어
source -- 컴파일 --> exe
### 2) java
source -- (a.java) 컴파일 --> Byte code --(a.class) 인터프리터 (jvm)--> running
                         
### 3) kotlin
source -- 컴파일 --> Byte code -- 인터프리터 --> running
<br>
APK
- Byte code에서 DEX파일을 만듬 (.class)
- DEX을 받아 러닝 시켜주는 ART
<center>
<table>
  <tr>
    <td colspan="2">APP</td>
  </tr>
  <tr>
    <td colspan="2">Java</td>
  </tr>
  <tr>
    <td>C/C++</td>
    <td>ART</td>
  </tr>
  <tr>
    <td colspan="2">HAL</td>
  </tr>
  <tr>
    <td colspan="2">Kernel</td>
  </tr>
  <tr>
    <td colspan="2">HW</td>
  </tr>
</table>
</center>
Activity = kotlin + resource files


## 0-2. component
앱 구성 중요 컴포넌트
- Activity : front-end
- service : back-end
- broadcast : 방송
- content provider : 공유

안드로이드 스튜디오
- manifests : 앱의 환경설정
- java : 프로그램파일
- res : 레이아웃, 리소스

---
# 1. 코틀린 개요
### 1) class가 없어도 시작가능, c++과 비슷
- Data Type : Int, Short, Byte, Float => class이기 때문에 대문자
- Value, variable => class 타입의 변수이기 때문에 object가 된다.

### 2) 코틀린은 Strong Type, Week Type 중 Strong Type을 사용한다.

### 3) val, var
- val : 변경 불가 (read only)
- var : 변경 가능
```kotlin
val x : short = 10
var y : Int = 5
```
### 4) scope
- global, local로 나눠진다.
```kotlin
// global scope
val g1 = 8
lateinit var g2:String // lateinit : 초기화를 하지 않는 표시
var g3:Float = 0.0F

fun test() {
  val x = 5 // read-only
  var y = 10
  println("$x : $y")
}

```

### 5) 함수
```kotlin
// 함수정의
fun add(var x:Int, var y:Int) : Int {
  fun areasize()
}

// class정의
class Rect {
  var r:Int
  fun areaSize() {
  }
}
class Rect(var r:Int) {
  fun areaSize() {
  }
}

// object(객체) 생성
var r : Rect = Rect()


// random : (min..max).random()
(a..b).random()
```
---
#2. 제어문
- 조건문 : if, when
- 반복문 : for, while, do~while
```kotlin
// 1. if
// statement 형태
if(a<8) {
  b = ++a
  c = b+2
} else {
  b = --a
  c = b-2
}
// expression 형태
a = if(b>3) ++b else --b
```
```kotlin
// 2. when
when(a) {
  1 -> println("1")
  2 -> println("2")
  a > 10 -> println("10초과")
}

```
---
# 3. 클래스
1) 구조
- class name
- property : 기본적으로 visibility를 세팅하면 property는 기본적으로 -로 표시되고 private를 의미한다.
- method
(encapsulation[private로 막는것], abstraction[추상화 / 필요한 것만 정의])

2) 생성자
- 코틀린은 자동으로 getter setter를 만든다
- 코틀린에 private을 넣으면 getter setter를 막는다는 의미
```kotlin
// constructor 사용 : 보조생성자
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
```kotlin
// 주생성자
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

```kotlin
//list
var numlist: List<Int> = listOf(1,2,3,4,5)
val books = mutableListOf<String>() // 변경가능 리스트
```
