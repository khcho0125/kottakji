# Kotlin Start

* #### 함수 선언

  ```kotlin
  fun func(a: Int, b: Int): Int {a + b}

  fun func2(a: Int, b: Int) = a + b
  ```

  기본 함수 선언식과 return을 생략하는 함수 대입식이다.

  return을 하지 않는 function은 `: Unit` 을 명시해준다.

* #### NULL 처리 

  function return 으로 NULL이 반환될 수 있으면 타입? 로 명시해준다.

  ```kotlin
  fun func(): Int? = null // null 또는 Int가 반환될 수 있음
  ```

  null을 안전하게 처리하기 위해 `?.` 연산자를 사용한다.

  ```kotlin
  fun func(a: Int?): Unit {
      val num1: Int? = a?.minus(1)
      print(num1)
  }
  ```

  null 대신 default 값을 사용하고 싶을 땐 `?:`을 사용함

  ```kotlin
  fun func(a: Int?): Unit {
    	val num1: Int = a ?: 10
    	print(num1)
  }
  ```

  NotNull을 명시해주려면 `!!`를 사용하면 됩니다.

* #### Type Any

  Any는 Java의 Object에 해당된다.
  is 는 instanceof 라고 보면된다. not 연산을 하려면 `!`를 붙이면 된다.

  ```kotlin
  fun func(a: Any): Int {
      if(a is String) {
          return a.length
      }

      if(a is Int) {
          return a
      }

      return 0
  }
  ```

* #### for-loop

  코틀린의 for-loop 도 대부분의 언어와 비슷하다.  in 키워드를 사용한다.

  ```kotlin
  val arrayList = ArrayList<String>()
  for (s in arrayList) {
    	print(s)
  }
  ```

  범위를 나타내는 방법으로 아래와 같이 만들 수 있다.

  ```kotlin
  for (x in 1..100) [
    	print(x)
  ]
  ```

  ​