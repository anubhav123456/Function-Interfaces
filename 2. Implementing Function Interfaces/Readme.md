
---

# Functional Interface – Ways to Implement

## What is a Functional Interface?

A **Functional Interface** is an interface that contains **exactly one abstract method**.

* Introduced in **Java 8**
* Used as the **foundation for Lambda Expressions**
* Annotated with `@FunctionalInterface` (optional but recommended)

---

## Example Functional Interface

```java
@FunctionalInterface
interface Bird
{
    void canFly();
}
```

✔ Only **one abstract method** → valid functional interface
✔ Can have **default** or **static** methods (not shown here)

---

## Ways to Implement a Functional Interface

There are **three ways**:

---

## 1️⃣ Using `implements` Keyword (Normal Class)

### Code

```java
class Eagle implements Bird
{
    @Override
    public void canFly()
    {
        System.out.println("Eagle flies");
    }
}
```

### Usage

```java
Bird bird1 = new Eagle();
bird1.canFly();
```

### Output

```
Eagle flies
```

### Notes

* Traditional OOP approach
* Requires a **separate class**
* More boilerplate code
* Less preferred when behavior is small/simple

---

## 2️⃣ Using Anonymous Class

### Code

```java
Bird bird2 = new Bird()
{
    @Override
    public void canFly()
    {
        System.out.println("Bird flies in an anonymous class");
    }
};
```

### Usage

```java
bird2.canFly();
```

### Output

```
Bird flies in an anonymous class
```

### Notes

* No separate class needed
* Class is created **at runtime**
* Still verbose
* Common before Java 8

---

## 3️⃣ Using Lambda Expression (Java 8)

### Code

```java
Bird bird3 = () -> System.out.println("Bird flies using lambda expression");
```

### Usage

```java
bird3.canFly();
```

### Output

```
Bird flies using lambda expression
```

### Notes

* **Shortest and cleanest**
* No method name, no return type, no access modifier
* Best suited for **functional interfaces**
* Widely used in **Streams, Collections, and APIs**

---

## Complete Working Program

```java
@FunctionalInterface
interface Bird
{
    void canFly();
}

class Eagle implements Bird
{
    @Override
    public void canFly()
    {
        System.out.println("Eagle flies");
    }
}

public class Main
{
    public static void main(String[] args)
    {
        Bird bird1 = new Eagle();
        bird1.canFly();

        Bird bird2 = new Bird()
        {
            @Override
            public void canFly()
            {
                System.out.println("Bird flies in an anonymous class");
            }
        };
        bird2.canFly();

        Bird bird3 = () -> System.out.println("Bird flies using lambda expression");
        bird3.canFly();
    }
}
```

### Final Output

```
Eagle flies
Bird flies in an anonymous class
Bird flies using lambda expression
```

---

## Interview Comparison Summary

| Approach          | Code Length | Java Version | Interview Preference |
| ----------------- | ----------- | ------------ | -------------------- |
| implements        | Long        | All versions | ❌ Less preferred     |
| Anonymous Class   | Medium      | Java 7+      | ⚠️ OK                |
| Lambda Expression | Short       | Java 8+      | ✅ Highly preferred   |

---

### ⭐ Interview Tip

> **Lambda expressions work only with functional interfaces**
> If more than one abstract method exists → ❌ Lambda not allowed

---