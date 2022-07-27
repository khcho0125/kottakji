# Kotlin part 6

* ## Singleton

  싱글톤은 어떤 클래스가 최초 한번만 메모리를 할당하고 그 메모리에 만든 객체를 계속 사용하는 디자인 패턴입니다.

  자바에서의 싱글톤은 보통 아래 코드와 같은 방식입니다.

  ```java
  public class Example {
    	private static Example instance;
    
    	private Example() {}
    
   	public static Example getInstance() {
        	if(instance != null) {
          	instance = new Example();
        	}
        	return instance;
    	}
  }
  ```

  하지만 코틀린이라면...?

  ```kotlin
  object Example {
  }
  ```

  네 이게 다입니다.

  `object` 키워드는 한 번만 생성되는 클래스의 인스턴스로 내부 모든 값들이 한 번만 생성됩니다.

  이런 object 키워드에도 문제점이 있는데
  프로세스 실행시 인스턴스가 실행되 클래스를 사용하지 않아도 메모리를 잡아 먹는다는 것입니다.

  #### 때문에 object가 호출될 때 초기화 되도록 만듭니다.

  object가 프로세스 실행시 메모리에 올라가는 것을 막을 수는 없지만, 내부 변수들을 지연 생성해 호출될 때 초기화 될 수 있도록 합니다.

  ```kotlin
  object Example {
    	val simple by lazy { "simple" }
  }
  ```

  이 방식을 통해 Singleton 내부에 메모리를 크게 잡아먹는 변수들을 지연 생성해 메모리 최적화를 노려볼 수 있습니다.

  ​