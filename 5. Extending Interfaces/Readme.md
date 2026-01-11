
---

# Extending Interfaces – Functional Interface (Java 8)

## 🔑 Key Rule (Very Important)

A **Functional Interface** can have **ONLY ONE abstract method**
(Default methods and static methods **do NOT count**.)

---

## ❌ Functional Interface Extending Non-Functional Interface

### ❌ Why Invalid?

If a functional interface extends another interface **that already has an abstract method**, and adds its own abstract method → **total abstract methods > 1** ❌

### Code

```java
interface LivingThing {
    void canBreathe();
}

@FunctionalInterface
interface Bird extends LivingThing {
    void canFly(); // ❌ Two abstract methods
}
```

### ❌ Abstract Methods Count

* `canBreathe()` → inherited
* `canFly()` → declared
  ➡ **2 abstract methods → NOT functional**

---

## ✅ Functional Interface Extending Interface with Default Method

### ✅ Why Valid?

Default methods **do not count** as abstract methods.

### Code

```java
interface LivingThing {
    default void canBreathe() {}
}

@FunctionalInterface
interface Bird extends LivingThing {
    void canFly(); // ✅ Only one abstract method
}
```

### ✅ Abstract Methods Count

* `canFly()` → only abstract method
  ➡ **Valid Functional Interface**

---

## ✅ Normal Interface Extending Functional Interface

### ✅ Why Valid?

Once you extend a functional interface **without `@FunctionalInterface`**, you are free to add more abstract methods.

### Code

```java
@FunctionalInterface
interface LivingThing {
    void canBreathe();
}

interface Bird extends LivingThing {
    void canFly(); // ✅ allowed
}
```

### 📝 Note

* `Bird` is **NOT** functional
* Multiple abstract methods allowed

---

## ❌ Functional Interface Extending Another Functional Interface (Different Methods)

### ❌ Why Invalid?

Both interfaces contribute **different abstract methods**, increasing the count.

### Code

```java
@FunctionalInterface
interface LivingThing {
    void canBreathe();
}

@FunctionalInterface
interface Bird extends LivingThing {
    void canFly(); // ❌ Two abstract methods
}
```

### ❌ Abstract Methods Count

* `canBreathe()`
* `canFly()`
  ➡ **2 abstract methods → Compilation error**

---

## ✅ Functional Interface Extending Functional Interface (Same Method)

### ✅ Why Valid?

If the child interface **overrides the same abstract method**, total abstract methods remain **1**.

### Code

```java
@FunctionalInterface
interface LivingThing {
    boolean canBreathe();
}

@FunctionalInterface
interface Bird extends LivingThing {
    boolean canBreathe(); // override
}
```

### ✅ Abstract Methods Count

* Only `canBreathe()`
  ➡ **Valid Functional Interface**

---

## ✅ Lambda Implementation Example

### Code

```java
Bird bird = () -> true;
System.out.println(bird.canBreathe());
```

### 🧠 Explanation

* Lambda implements the **single abstract method**
* No method name needed (SAM concept)
* Clean and concise

---

## 📌 Quick Interview Summary

| Scenario                                 | Allowed? |
| ---------------------------------------- | -------- |
| Functional FI extends non-FI             | ❌        |
| FI extends interface with default method | ✅        |
| Normal interface extends FI              | ✅        |
| FI extends FI (different methods)        | ❌        |
| FI extends FI (same method override)     | ✅        |

---
