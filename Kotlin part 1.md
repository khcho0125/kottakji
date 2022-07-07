# Kotlin part 1

## Lombok 대신 data class을 사용하자

**data class**는 **데이터를 보관하는 목적으로 만든 클래스**를 말한다.

### data class의 특징

* 상속 받을 수 없다.
* **val 또는 var**으로 선언해야 한다.
* **abstract, open, sealed, inner** 을 붙일 수 없다.
* 1개 이상의 **property**를 가져야 한다.
* **hashcode(), equals(), toString(), copy()** 메소드를 자동으로 구성해준다.
  Override로 구현 가능

```kotlin
data class Food(val name: String, val price: Int)
```

이를 java code로 변환해보면 아래와 같다.

```java
public class Food {
    ...

    public Food(@NotNull String name, @NotNull Integer price) {
      ...
    }

    @NotNull
    public final Food copy(@NotNull String name, @NotNull Integer price) {
      return new Food(name, price);
    }

    @NotNull
    public String toString() {
        return "Food(name=" + this.name + ", price=" + this.price + ")";
    }

    public Integer hashCode() {
        return (this.name != null ? this.name.hashCode() : 0) * 31 + (this.price != null ? this.price.hashCode() : 0);
   }

   public boolean equals(@Nullable Object var1) {
      if (this != var1) {
         if (var1 instanceof Food) {
            Food var2 = (Food)var1;
            if (Intrinsics.areEqual(this.name, var2.name) && Intrinsics.areEqual(this.price, var2.price)) {
               return true;
            }
         }

         return false;
      } else {
         return true;
      }
   }
}

```

* ### 데이터 분해 및 대입 (Destructuring Declarations)

  객체 내부 변수를 다른 변수에 대입해야 할 때 보통 아래와 같이 대입한다.

  ```kotlin
  val food = Food("chicken", 15000)
  val foodname = food.name
  val foodprice = food.price
  ```

  하지만 data class는 Destructuring Declarations를 지원하기 때문에 아래와 같이 한줄로 표현 가능하다.

  ```kotlin
  val food = Food("chicken", 15000)
  val (foodname, foodprice) = food
  ```

  ​

