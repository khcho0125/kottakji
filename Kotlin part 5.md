# Kotlin part 5

* ### Extension Function

  Extension function(확장함수)는 기존에 정의된 클래스에 함수를 추가하는 기능이다.

  자신이 만든 클래스는 라이브러리에서 가져오는 클래스보다 새로운 함수가 필요할 때 추가하기 쉽다.

  예로들어 정수로 구성된 리스트에서 절댓값이 3이 넘는 요소만 출력하고 싶다면 리스트는 `toString()` 메서드를 지원하기 때문에 출력에는 문제가 없지만 절댓값이 3보다 큰 요소를 찾아주는 함수는 없다.

  그렇기 때문에 아래와 같이 `absFilter(value : Int)` 라는 메소드를 지원한다면 코드가 매우 간결해지고 가독성이 올라갈 것입니다.

  ```kotlin
  fun main() {
      val list = listOf(0, -1, 2, -3, 4, -5, 6, -7, 8, -9)
      print(list.absFilter(3).toString())
  }
  ```

  #### 확장 함수를 정의하는 방법

  확장함수는 `fun 클래스 이름.함수이름(인자타입): 반환 값 { 구현부 }` 로 정의 할 수 있다.

  아래는 `absFilter(value : Int)` 를 구현한 것이다.

  ```kotlin
  fun List<Int>.absFilter(value : Int): List<Int> {
      return filter { abs(it) > value }
  }
  ```

  #### Generic class 확장 함수

  위에서는 List에 대한 확장 함수를 정의 했다. Generic class 에 대해 확장 함수 정의를 하고 싶다면

  `fun <E> 클래스이름<E>.함수이름(인자타입): 반환 값 { 구현부 }` 로 정의 가능하다.

  대신 구현부에선 모든 타입을 고려해야 한다.

  ```kotlin
  fun <E> List<E>.absFilter(value: Int): List<E> {
      return filter { abs(it as? Int ?: 0) > value }
  }
  ```

  #### 상속을 이용한 확장 함수

  List를 상속한 새로운 클래스를 만들고 그 클래스에 확장 함수를 정의할 수 있다.

  ```kotlin
  class FilterList<E> : ArrayList<E>() {
      fun absFilter(value: Int): List<E> {
          return filter { abs(it as? Int ?: 0) > value }
      }
  }

  fun main() {
      val list = FilterList<Int>()
      list.addAll(listOf(-1, 2, -3, 4,-5, 6, -7, 8, -9))
      print(list.absFilter(3).toString())
  }
  ```

  ​