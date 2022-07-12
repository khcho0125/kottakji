# Kotlin part 2

* ### as 연산자

  ##### `as`는 지정된 타입으로 캐스트한다. 해당 타입으로 바꿀 수 없으면 ClassCastException이 발생한다. 해당 타입으로 변환 불가능할 경우 null을 반환하는 `as?` 연산자를 제공한다.  

  ```kotlin
  override fun equals(other: Any?): Boolean {
      val otherUser = other as? User ?: return false
      return otherUser.id == id
  }
  ```

* ### !! 연산자

  ##### null이 아닌 값은 코틀린에서 `!!` 을 사용하면 어떤 값이든 null이 될 수 없는 타입으로 바꿀 수 있다. 실제 null 값에 `!!` 을 적용하면 NullPointerException이 발생한다.

  ```kotlin
  fun test(user: User?) {
      var name = user!!.getId()
      print(name)
  }
  ```

* ### let 함수

  ##### null이 될 수 있는 식을 간단하게 사용할 수 있다. `?.` 와 함께 사용하여 null인지 검사한 후 그 값을 처리하는 경우다.	

  ```kotlin
  fun test(user: User?) {
      user?.let {  // null 일 때 실행 X
          print(user.getId());
      }
  }
  ```

* ### lateinit 제한자

  ##### `lateinit`  생성자 안에서 초기화 하지않고 나중에 초기화 되는 변수이다. `lateinit` 은 반드시 null이 될 일 없는 변수를 선언할 때 사용한다. `lateinit` 이 붙는 변수는 반드시 `var` 로 선언되어야 한다.

  ```kotlin
  class User {
      private lateinit var name: String

      fun setName(value: String) {
          name = value
      }
  }
  ```

  ​