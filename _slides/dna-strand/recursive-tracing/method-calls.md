---
title: Method calls
nav_order: 3
---

A key learning objective for this lesson is to trace the execution of recursive algorithms, which requires an understanding of how to evaluate method calls. In Java, a **method** is a procedure that runs the code defined in its body. For example, consider this example program.

```java
public static void main(String[] args) {
    boolean x = false;
    System.out.println("x = " + x + " at main start");
    methodExample(x);
    System.out.println("x = " + x + " at main end");
}

public static void methodExample(boolean x) {
    System.out.println("x = " + x + " at method start");
    x = true;
    System.out.println("x = " + x + "  at method end");
}
```

Calling the `main` method results in the following output.

```
x = false at main start
x = false at method start
x = true  at method end
x = false at main end
```

There are two important principles that are necessary for understanding how recursion works.

Control flow
: Anytime a method is called, the program temporarily pauses evaluation to evaluate the called method. Only after returning from the called method does the original program pick up where it left off.

Variable scope
: Every variable has its own scope, the localized parts of the program that can access or change the variable. Variables declared inside a `for` loop, for example, are scoped to the `for` loop. Parameters are variables scoped over the entire method.
