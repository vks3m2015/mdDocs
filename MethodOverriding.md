
## Method Overriding in Java

When a subclass defines a **instance method** with **same name, number and type of parameters and return type** as an instance method in superclass then we call that method in subclass **override** the method in superclass.

An overriding method can also return a subtype of the type returned by the overridden method. This subtype is called a *covariant* return type.

If a subclass defines a **static method** with the same signature as a static method in the superclass, then the method in the subclass **hides** the one in the superclass.

A call to overridden method is resolved at runtime rather than compile time. This is called **runtime polymorphism**.

A superclass reference variable can refer to a subclass object. When an overridden method is called through a **superclass reference**, Java determines  which version of that method to execute based upon the **type of the object** being referred to at the time the call occurs

Here is the Example-

```sh



```