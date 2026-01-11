
---
# Built-in Functional Interfaces
* Defined in package `java.util.function`

---

# 1️⃣ Consumer<T>

### 👉 Takes **one input**, returns **nothing**

```java
@FunctionalInterface
public interface Consumer<T> {
    void accept(T t);
}
```

### Example

```java
import java.util.function.Consumer;

public class ConsumerExample {
    public static void main(String[] args) {

        Consumer<String> printName = name -> 
                System.out.println("Name: " + name);

        printName.accept("Anubhav");
    }
}
```

---

# 2️⃣ BiConsumer<T, U>

### 👉 Takes **two inputs**, returns **nothing**

```java
@FunctionalInterface
public interface BiConsumer<T, U> {
    void accept(T t, U u);
}
```

### Example

```java
import java.util.function.BiConsumer;

public class BiConsumerExample {
    public static void main(String[] args) {

        BiConsumer<String, Integer> printDetails =
                (name, age) -> System.out.println(name + " is " + age + " years old");

        printDetails.accept("Anubhav", 30);
    }
}
```

---

# 3️⃣ Supplier<T>

### 👉 Takes **no input**, returns **something**

```java
@FunctionalInterface
public interface Supplier<T> {
    T get();
}
```

### Example

```java
import java.util.function.Supplier;

public class SupplierExample {
    public static void main(String[] args) {

        Supplier<Double> randomValue = () -> Math.random();

        System.out.println(randomValue.get());
    }
}
```

---

# 4️⃣ Function<T, R>

### 👉 Takes **one input**, returns **one output**

```java
@FunctionalInterface
public interface Function<T, R> {
    R apply(T t);
}
```

### Example

```java
import java.util.function.Function;

public class FunctionExample {
    public static void main(String[] args) {

        Function<String, Integer> lengthFinder = str -> str.length();

        System.out.println(lengthFinder.apply("Java"));
    }
}
```

---

# 5️⃣ BiFunction<T, U, R>

### 👉 Takes **two inputs**, returns **one output**

```java
@FunctionalInterface
public interface BiFunction<T, U, R> {
    R apply(T t, U u);
}
```

### Example

```java
import java.util.function.BiFunction;

public class BiFunctionExample {
    public static void main(String[] args) {

        BiFunction<Integer, Integer, Integer> sum =
                (a, b) -> a + b;

        System.out.println(sum.apply(10, 20));
    }
}
```

---

# 6️⃣ Predicate<T>

### 👉 Takes **one input**, returns **boolean**

```java
@FunctionalInterface
public interface Predicate<T> {
    boolean test(T t);
}
```

### Example

```java
import java.util.function.Predicate;

public class PredicateExample {
    public static void main(String[] args) {

        Predicate<Integer> isEven = n -> n % 2 == 0;

        System.out.println(isEven.test(10));
        System.out.println(isEven.test(7));
    }
}
```

---

# 7️⃣ BiPredicate<T, U>

### 👉 Takes **two inputs**, returns **boolean**

```java
@FunctionalInterface
public interface BiPredicate<T, U> {
    boolean test(T t, U u);
}
```

### Example

```java
import java.util.function.BiPredicate;

public class BiPredicateExample {
    public static void main(String[] args) {

        BiPredicate<Integer, Integer> isSumEven =
                (a, b) -> (a + b) % 2 == 0;

        System.out.println(isSumEven.test(10, 20));
    }
}
```

---

## 8️⃣ UnaryOperator<T>

### 👉 Takes **one input**, returns **same type output**

➡️ Special case of `Function<T, T>`

```java
@FunctionalInterface
public interface UnaryOperator<T> extends Function<T, T> {
}
```

### When to use?

✔ When **input type == output type**

### Example

```java
import java.util.function.UnaryOperator;

public class UnaryOperatorExample {
    public static void main(String[] args) {

        UnaryOperator<Integer> square = n -> n * n;

        System.out.println(square.apply(5)); // 25
    }
}
```
---
## 9️⃣ BinaryOperator<T>

### 👉 Takes **two inputs of same type**, returns **same type**

➡️ Special case of `BiFunction<T, T, T>`

```java
@FunctionalInterface
public interface BinaryOperator<T> extends BiFunction<T, T, T> {
}
```

### When to use?

✔ When **both inputs and output are of same type**

### Example

```java
import java.util.function.BinaryOperator;

public class BinaryOperatorExample {
    public static void main(String[] args) {

        BinaryOperator<Integer> sum = (a, b) -> a + b;

        System.out.println(sum.apply(10, 20)); // 30
    }
}
```
---

# 🔗 CHAINING CONCEPTS (Very Important)

---

## 1️⃣ Consumer Chaining (`andThen`)

👉 Executes **multiple Consumers sequentially**

```java
import java.util.function.Consumer;

public class ConsumerChaining {
    public static void main(String[] args) {

        Consumer<String> c1 = s -> System.out.println(s.toUpperCase());
        Consumer<String> c2 = s -> System.out.println(s.length());

        c1.andThen(c2).accept("java");
    }
}
```

📌 Output:

```
JAVA
4
```

---

## 2️⃣ BiConsumer Chaining (`andThen`)

```java
import java.util.function.BiConsumer;

public class BiConsumerChaining {
    public static void main(String[] args) {

        BiConsumer<String, Integer> c1 =
                (name, age) -> System.out.println(name);

        BiConsumer<String, Integer> c2 =
                (name, age) -> System.out.println(age);

        c1.andThen(c2).accept("Anubhav", 30);
    }
}
```

---

## 3️⃣ Function Chaining (`andThen`)

👉 First function executes → result goes to next

```java
import java.util.function.Function;

public class FunctionAndThen {
    public static void main(String[] args) {

        Function<Integer, Integer> multiply = n -> n * 2;
        Function<Integer, Integer> square = n -> n * n;

        System.out.println(multiply.andThen(square).apply(5));
    }
}
```

📌 Calculation:

```
5 → 10 → 100
```

---

## 4️⃣ Function Chaining (`compose`)

👉 **Reverse order** execution

```java
import java.util.function.Function;

public class FunctionCompose {
    public static void main(String[] args) {

        Function<Integer, Integer> multiply = n -> n * 2;
        Function<Integer, Integer> square = n -> n * n;

        System.out.println(multiply.compose(square).apply(5));
    }
}
```

📌 Calculation:

```
5 → 25 → 50
```

---

## 5️⃣ Predicate Chaining (`and`, `or`, `negate`)

```java
import java.util.function.Predicate;

public class PredicateChaining {
    public static void main(String[] args) {

        Predicate<Integer> isEven = n -> n % 2 == 0;
        Predicate<Integer> isGreaterThan10 = n -> n > 10;

        System.out.println(isEven.and(isGreaterThan10).test(12)); // true
        System.out.println(isEven.or(isGreaterThan10).test(9));   // false
        System.out.println(isEven.negate().test(7));             // true
    }
}
```

---

## 6️⃣ BiPredicate Chaining (`and`, `or`, `negate`)

```java
import java.util.function.BiPredicate;

public class BiPredicateChaining {
    public static void main(String[] args) {

        BiPredicate<Integer, Integer> isSumEven =
                (a, b) -> (a + b) % 2 == 0;

        BiPredicate<Integer, Integer> isSumGreaterThan20 =
                (a, b) -> (a + b) > 20;

        System.out.println(isSumEven.and(isSumGreaterThan20).test(10, 12));
        System.out.println(isSumEven.or(isSumGreaterThan20).test(5, 5));
    }
}
```

---

## 7️⃣ UnaryOperator Chaining (`andThen`)

👉 Executes **multiple UnaryOperators sequentially**
👉 Output of first becomes input of next

```java
import java.util.function.UnaryOperator;

public class UnaryOperatorChaining {
    public static void main(String[] args) {

        UnaryOperator<Integer> multiplyBy2 = n -> n * 2;
        UnaryOperator<Integer> add10 = n -> n + 10;

        System.out.println(multiplyBy2.andThen(add10).apply(5));
    }
}
```

📌 Calculation:

```
5 → 10 → 20
```

---

## 8️⃣ UnaryOperator Chaining (`compose`)

👉 **Reverse order execution**

```java
import java.util.function.UnaryOperator;

public class UnaryOperatorCompose {
    public static void main(String[] args) {

        UnaryOperator<Integer> multiplyBy2 = n -> n * 2;
        UnaryOperator<Integer> add10 = n -> n + 10;

        System.out.println(multiplyBy2.compose(add10).apply(5));
    }
}
```

📌 Calculation:

```
5 → 15 → 30
```

---

## 9️⃣ BinaryOperator Chaining (`andThen`)

👉 First `BinaryOperator` executes
👉 Result goes to a **Function** (not another BinaryOperator)

⚠ **Important Interview Point**
`BinaryOperator.andThen()` returns a **Function**, not a BinaryOperator.

```java
import java.util.function.BinaryOperator;
import java.util.function.Function;

public class BinaryOperatorChaining {
    public static void main(String[] args) {

        BinaryOperator<Integer> sum = (a, b) -> a + b;
        Function<Integer, Integer> square = n -> n * n;

        System.out.println(sum.andThen(square).apply(3, 4));
    }
}
```

📌 Calculation:

```
(3 + 4) = 7 → 49
```

---


# 🧠 Interview Summary

| Interface      | Input | Output    |
| -------------- | ----- | --------- |
| Consumer       | 1     | void      |
| BiConsumer     | 2     | void      |
| Supplier       | 0     | 1         |
| Function       | 1     | 1         |
| BiFunction     | 2     | 1         |
| UnaryOperator  | 1     | Same type |
| BinaryOperator | 2     | Same type |
| Predicate      | 1     | boolean   |
| BiPredicate    | 2     | boolean   |

---

## 🔥 INTERVIEW TIP

> **Supplier → gives**
> **Consumer → takes**
> **Predicate → checks**
> **Function → converts**
> **UnaryOperator → modifies**
> **BinaryOperator → combines**

---
