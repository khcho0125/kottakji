# Kotlin part 4

* ## Kotlin Scope Function

  Scope Function이란 함수들을 이용해 호출하면 일시적인 Scope(범위)가 생겨 이 범위 안에 객체에 대해 접근하게 해주는 함수입니다.

  Scope Function 내에서 실제 객체명 대신, `it`과 `this`등으로 참조하게 됩니다.

  ```kotlin
  fun scopeRun() {
      val user = User( "1234","KyungHyeon")
      user.run {
          print("Name : $name") // this.name
      }
  }
  ```

  ```kotlin
  fun scopeRun() {
      val user = User( "1234","KyungHyeon")
      user.let {
          print("Name : ${it.name}")
      }
  }
  ```

  ### Scope Funtion의 차이점

  ---

  #### Context Object

  * `this`로 참조하는 함수 : `run`, `with`, `apply`
  * `it`으로 참조하는 함수 :  `let`, `also` 

  #### Return Value

  * `apply`, `also`는 Context Object를 반환
  * `let`, `run`, `with`은 람다식 결과를 반환

  ```kotlin
  fun scopeRun() {
      val user = User( "1234","KyungHyeon")
      user.also {
          it.name = "khcho0125"
      }.also {
          it.name = "khcho"
      }.run {
          print(name)
      }
  }
  ```

  `also` 함수는 Context Object를 반환하기 때문에 체인 형식으로 사용 가능하다. 

  ---

  ### 각 Scope Function의 쓰임

  * #### let

    객체의 결과값에 하나 이상의 함수를 호출하는데 사용한다.
    또한, null이 아닌 객체에 대해 연산을 시도할 때 안전한 수행 연산자( `?.` )를 `let`과 함께 사용한다.

    ```kotlin
    /** let 안썼을 때 */
    val numbers = mutableListOf("one", "two", "three", "four", "five")
    val resultList = numbers.map { it.length }.filter { it > 3 }
    println(resultList)    

    /** let 사용 시 */
    val numbers = mutableListOf("one", "two", "three", "four", "five")
    numbers.map { it.length }.filter { it > 3 }.let { 
        println(it)
        // 추가적인 함수 호출 가능
    } 
    ```

  * #### run

    이미 생성된 Context Object 객체를 사용할 때 호출한다.
    안전한 수행 연산자( `?.` )을 붙여 사용할 수도 있다.

    ```kotlin
    val person = Person("KyungHyeon")
    val number = person?.run {
      	"$name" + number
    }
    print(number)
    ```

  * #### apply

    객체 초기화시 자주 사용된다.

    ```kotlin
    val person = Person().apply {
      	name = "KyungHyeon",
      	age = 18
    }
    ```

  * #### with

    `run`과 마찬가지로 Context Object를 인자로 받아서 사용하는 것이 효율적일때 사용한다.
    하지만 `run`과 다르게 안전한 수행 연산자( `?.` )를 붙여 null 체크를 할 수 없기 때문에 `with`보다는 `run`이 주로 사용된다.

    ```kotlin
    val person = Person("KyungHyeon")
    with(person) {
      	println(name)
      	println(age)
    }
    ```

  * #### also

    기존 객체를 수정하지 않고, 디버깅이나 로그 등 부가적인 작업을 할 때 주로 사용된다.

    ```kotlin
    val person = Person("KyungHyeon").also {
      	println(it.name)
    }
    ```

    ​
