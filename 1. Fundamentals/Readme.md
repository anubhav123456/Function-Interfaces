## Functional Interface (Java 8)

### 1. What is a Functional Interface?

A **Functional Interface** is an interface that contains **exactly one abstract method**.

* Also known as **SAM Interface (Single Abstract Method)**
* Introduced in **Java 8**
* Used heavily with **Lambda Expressions** and **Streams**

---

### 2. What a Functional Interface Can Have

A functional interface **can have only one abstract method**, but it **can also include**:

1. **Default methods**
2. **Static methods**
3. **Methods inherited from `Object` class**

   * `toString()`
   * `equals()`
   * `hashCode()`

These **do NOT count** toward the abstract method count.

---

### 3. Example of a Functional Interface

```java
@FunctionalInterface
interface Bird {
    void canFly(); // abstract method (only one allowed)

    default void eat() {
        System.out.println("Bird is eating");
    }

    static void breathe() {
        System.out.println("Bird is breathing");
    }

    // Object class methods allowed
    String toString();
}
```

---

### 4. Why Object Class Methods Are Allowed

Methods like `toString()`, `equals()`, and `hashCode()` are **not counted as abstract methods** because:

* Every Java class **implicitly extends `Object`**
* These methods are already available to all classes
* Hence, they **do not violate** the single abstract method rule

---

### 5. @FunctionalInterface Annotation

* The `@FunctionalInterface` annotation is **optional**
* It is used for **compile-time safety**

#### With Annotation

```java
@FunctionalInterface
interface Bird {
    void canFly();
}
```

#### Without Annotation (Still Valid)

```java
interface Bird {
    void canFly();
}
```

---

### 6. Why Use @FunctionalInterface?

Using `@FunctionalInterface` helps because:

* Ensures **only one abstract method** exists
* Causes **compile-time error** if another abstract method is added accidentally
* Improves **readability and intent** of the interface

#### Compilation Error Example

```java
@FunctionalInterface
interface Bird {
    void canFly();
    void eat(); // ❌ Compilation Error
}
```

---

### 7. Key Points to Remember

* ✔ Only **one abstract method** allowed
* ✔ Can have **default methods**
* ✔ Can have **static methods**
* ✔ Can include **Object class methods**
* ✔ Annotation is **optional but recommended**
* ✔ Backbone of **Lambda Expressions**

---

### Interview Tip 🔥

> If an interface has exactly one abstract method, it **IS a functional interface**, even without `@FunctionalInterface` annotation.

---
