# Coupling and Cohesion

## Learning Goals

- Define Coupling and Cohesion
- Explain tight coupling and loose coupling
- Explain high cohesion and low cohesion

## Introduction

When we create an application in Java, we want to make sure that it is easy
to maintain. Far too often do programmers spend more hours needed updating code.
In the late 1960s, Larry Constantine developed two concepts to help design
better software - coupling and cohesion. These concepts are now standard
terms in the software engineering community.

## Coupling

**Coupling** refers to the dependency two classes may have on each other.
Coupling can be measured based on the amount of relations between classes.
There are two different types of coupling that exist:

- Tight coupling.
- Loose coupling.

**Tight coupling** means the two classes are closely connected or dependent on
one another. If a developer needs to update a class but finds out another class
also needs to be updated due to the change, then those classes might be tightly
coupled. Let's look at an example of two classes that are tightly coupled:

```java
public class Book {
    private String title;
    private String author;
    private String genre;
    private Library library;    // refers to which library the book belongs to
}

public class Library {
    
    private String libraryName;
    private Book[] books;    // array of Book objects
}
```

The above example shows a `Book` and a `Library` class where both classes have
class members that refer to the other. We can say that these two classes are
**tightly coupled**. Tight coupling can lead to issues when maintaining code.

With our `Book` and `Library` class, the `Book` class has a reference to a
`Library` object, but is that really necessary? And can't a `Book` exist on its
own? What if we want our `Book` to end up in a store instead of a library? Or
maybe we own the book, and it lives on our e-reader. If we remove the `library`
property from the `Book` class then we would have this:

```java
public class Book {
    private String title;
    private String author;
    private String genre;
}

public class Library {
    
    private String libraryName;
    private Book[] books;    // array of Book objects
}
```

Now that we have removed one of the dependencies, we can say that these two
classes are **loosely coupled**. There is still a dependency in that a library
has an array of books, but they are mostly independent and the `Book` class can
now stand on its own or be implemented in other classes, like a `BookStore`
class.

## Cohesion

**Cohesion** refers to how closely related the contents inside a class are to
each other. Just like coupling, there are two measurements of cohesion we will
study:

- High cohesion.
- Low cohesion.

Let's say we have a `User` class and the `User` class has a name attribute and
an email attribute. We can also include a getter and a setter for each
attribute. A class with **low cohesion** is a class with unrelated
elements. So if our `User` class were to also have methods to validate an email
or even send an email, we could say that it then has low cohesion since those
two methods aren't related to the `User` itself. Maybe those methods could go in
a separate class, like `Email`. Low cohesion also means the class is taking on
too many responsibilities. Consider the following image to help demonstrate
cohesion:

![Cohesion](https://curriculum-content.s3.amazonaws.com/java-mod-2/coupling-cohesion/Cohesion.png)

[Reference: Difference Between Cohesion and Coupling](https://www.baeldung.com/cs/cohesion-vs-coupling)

If we were to remove the two methods that don't seem like they belong in the
`User` class, then we can say that all the attributes and methods in the class
are related and have **high cohesion**.

## Conclusion

When we are programming, it is best to say we want to develop code that has
high cohesion and low coupling to reflect a higher quality of software that is
easier to maintain.

## References

- [Reference: Difference Between Cohesion and Coupling](https://www.baeldung.com/cs/cohesion-vs-coupling)
