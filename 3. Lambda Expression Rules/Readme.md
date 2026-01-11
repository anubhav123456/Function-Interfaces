
---

## Lambda Expression Rules (Java 8+)

### What is a Lambda Expression?

A **lambda expression** is a short block of code that takes in parameters and returns a value.
It is mainly used to implement **Functional Interfaces** (interfaces with **only one abstract method**).

**General Syntax**

```java
(parameters) -> expression
```

or

```java
(parameters) -> { statements }
```

---

## 1. No Parameters

* Used when the functional interface method does **not take any arguments**
* Empty parentheses `()` are **mandatory**

```java
() -> System.out.println("Hello")
```

✅ Example usage:

```java
Runnable r = () -> System.out.println("Hello");
r.run();
```

---

## 2. Single Parameter

* Parentheses are **optional** if there is **only one parameter**
* Java automatically infers the type

```java
(x) -> System.out.println(x)
```

or

```java
x -> System.out.println(x)
```

✅ Example usage:

```java
Consumer<Integer> c = x -> System.out.println(x);
c.accept(10);
```

---

## 3. Multiple Parameters

* Parentheses are **mandatory**
* Parameters are separated by commas
* Used when the lambda returns a value

```java
(x, y) -> x + y
```

✅ Example usage:

```java
BiFunction<Integer, Integer, Integer> sum = (x, y) -> x + y;
System.out.println(sum.apply(5, 3));
```

---

## 4. Multiple Statements

* Curly braces `{}` are **mandatory**
* `return` keyword is **required**
* Used when lambda body has more than one statement

```java
(x) -> 
{
    System.out.println(x);
    return x * 2;
}
```

✅ Example usage:

```java
Function<Integer, Integer> f = x -> {
    System.out.println(x);
    return x * 2;
};
System.out.println(f.apply(4));
```

---
