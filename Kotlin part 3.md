# Kotlin part 3

* ## 예외처리

  kotlin의 예외 인스턴스는 Java와 다르게 `new` 생성자 없이 사용한다.

  ```kotlin
  fun errorTest() {
      throw IllegalArgumentException("Throw")
  }
  ```

  * 실행 로그

  ```
  Exception in thread "main" java.lang.IllegalArgumentException: Throw
  	at MainKt.errorTest(Main.kt:11)
  	at MainKt.main(Main.kt:2)
  	at MainKt.main(Main.kt)
  ```

  ---

  kotlin의 `try - catch - finally` 는 java와 같다.

  ```kotlin
  fun errorTest(): Int? {
      val line = readLine()
      try {
          return Integer.parseInt(line)
      } catch (e: NumberFormatException) {
          return null
      }
  }
  ```

  하지만 kotlin은 `try` 문을 식으로 사용할 수 있다.
  위의 코드를 아래와 같이 줄일 수 있다.

  ```kotlin
  fun errorTest(): Int? {
      val line = readLine()
      return try {
          Integer.parseInt(line)
      } catch (e: NumberFormatException) {
          null
      }
  }
  ```

  try 식은 `finally` 은 실행되지 않는다.

* ## Lamdba

  kotlin의 람다식도 java와 크게 다르지 않다.

  * 매개변수가 없는(생략가능한) 람다식 

  ```kotlin
  testLambda { "lambda" }
  testLambda { UUID.randomUUID().toString() + "abc" }
  ```

  ```kotlin
  fun testLambda(function: () -> String) {
      for(i in 0..3) {
          println(function())
      }
  }
  ```

  * 매개변수가 하나일 때 람다식

  ```kotlin
  testLambda { a -> "http $a" }
  testLambda { "hello $it" } // it을 사용해 표현 가능
  ```

  ```kotlin
  fun testLambda(function: (String) -> String) {
      for (i in 0..3) {
          println(function("khcho"))
      }
  }
  ```

  * 매개변수가 여러개일 때

  ```kotlin
  testLambda { a, b -> "http $a $b" } // 매개변수명 생략불가
  testLambda { _, b -> "http $b" } // 매개변수 생략시 언더바 사용
  ```

  ```kotlin
  fun testLambda(function: (String, String) -> String) {
      for (i in 0..3) {
          println(function("local", "host"))
      }
  }
  ```