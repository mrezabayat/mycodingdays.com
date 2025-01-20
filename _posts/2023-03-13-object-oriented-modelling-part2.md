---
title: "Object Oriented Modelling - Part 2: Decomposition and Generalization"
date: 2023-02-04
description: "This post explores two fundamental design principles in object-oriented modeling: decomposition and generalization. Decomposition involves breaking down complex systems into manageable parts, making them easier to understand, maintain, and scale, while generalization focuses on building hierarchical relationships between classes to promote reusability and extensibility. Using practical C++ examples and UML class diagrams, the post demonstrates how these principles can be applied to create modular, efficient, and maintainable software. From understanding relationships like association, aggregation, and composition to leveraging inheritance hierarchies, this article provides valuable insights and best practices for effective software design."
tags: ["object-oriented design", "software architecture", "C++ programming", "decomposition", "generalization", "UML diagrams", "software design principles", "inheritance", "class relationships", "modular programming"]
categories: ["Design and Architecture"]
author: mrbayat
media_subpath:  /assets/img/posts/006
image:
    path: banner.png
---
In this second part of our series on object-oriented modelling, we will explore two more fundamental design principles: decomposition and generalization. We will discuss how these principles help us to break down complex systems into manageable components and build relationships between them, ultimately leading to software that is modular, extensible, and easy to maintain.

We will examine how to apply decomposition and generalization to the design of classes and inheritance hierarchies in C++, as well as how to represent these structures using UML class diagrams.

Throughout the article, we will use practical examples and best practices to illustrate the benefits of decomposition and generalization in real-world scenarios. By the end of this article, you will have a deeper understanding of these essential design principles, and how to apply them effectively to your software design. So, let's dive in and continue our exploration of object-oriented modelling!

### Decomposition

**Decomposition** is a key design principle that involves breaking down a complex problem or system into smaller, more manageable parts. This can be done in two ways: by dividing a whole into smaller parts or by combining separate parts with different functionalities to create a cohesive whole. By breaking down a problem or system into smaller pieces, it becomes easier to understand and solve. This makes decomposition an essential tool in software design and development.

When using decomposition as a design principle, the focus is on breaking down a complex system into smaller, more manageable parts, each with its own specific responsibility. This can be achieved by identifying the distinct responsibilities of the system as a whole, and then creating separate objects from individual classes to represent each of these responsibilities. In essence, decomposition involves abstracting the key characteristics of a system and creating objects based on these abstractions. This is similar to the abstraction principle, which also involves breaking down a complex concept into simpler, more manageable parts.

Each component of a whole can correspond to a class, allowing for better organization and encapsulation. This means that each part can be handled independently and efficiently, with the class for the whole object relating to the classes for its individual parts.

![Decomposition](decomposition.jpg)

Objects can have different types of parts, which can have a fixed or dynamic number. For instance, a whole object may have a specific number of parts that is constant throughout its lifetime, such as an oven with four burners. On the other hand, some parts may vary in number, as is the case with items of food in a refrigerator object that can change from day to day. The nature of these parts and how they relate to the whole object depend on the design of the class.

Decomposition is not limited to dividing a whole into parts, as a part can also serve as a whole made up of further constituent parts. A great example of this is a kitchen, which is a part of a house, but can also be divided into parts such as an oven and a refrigerator. This approach enables us to create more modular and scalable systems that can be broken down into smaller, more manageable components. By decomposing complex systems into smaller parts, we can build systems that are easier to understand, maintain, and evolve over time.

In decomposition, it's important to consider the lifetimes of both the whole object and its constituent parts. Sometimes, the lifetime of a part is closely tied to the lifetime of the whole object, meaning one cannot exist without the other. This is the case with components like the temperature cooling gauge in a fridge. However, in other cases, the part and the whole can exist independently and have different lifetimes. For example, if an item of food goes bad in the fridge, the fridge itself will still function normally. Understanding the relationship between the lifetimes of the whole and its parts is essential for effective decomposition in software design.

In the process of decomposition, it's important to consider that a whole entity may include parts that are also shared with another whole simultaneously. However, in some cases, sharing a part may not be possible or intended.

There are three types of relationships in decomposition that define how the different parts of a system interact with each other. These relationships are **association**, **aggregation**, and **composition**, and each of them has its own unique uses and advantages.

#### Association

Association is a type of relationship where two classes are loosely linked to each other, meaning that they can exist independently of each other. This relationship is useful when there is no need for one class to depend on the other, but they still need to interact with each other in some way.

Here's an example of an association in C++:

```cpp
#include <iostream>
#include <memory>
#include <string>
#include <utility>
#include <vector>

class Student {
   private:
    int m_id;
    std::string m_name;

   public:
    Student(int studentId, std::string studentName)
        : m_id(studentId), m_name(std::move(studentName)) {}

    int getId() const { return m_id; }

    std::string getName() const { return m_name; }
};

class Course {
   private:
    std::string m_name;
    std::vector<std::shared_ptr<Student>> m_students;

   public:
    Course(std::string courseName) : m_name(std::move(courseName)) {}

    void enrollStudent(std::shared_ptr<Student> student) {
        m_students.push_back(student);
    }
    std::vector<std::shared_ptr<Student>> getStudents() const {
        return m_students;
    }
};

int main() {
    auto student1 = std::make_unique<Student>(1, "Alice");
    auto student2 = std::make_unique<Student>(2, "Bob");
    Course course = Course("Intro to Computer Science");
    course.enrollStudent(std::make_unique<Student>(1, "Alice"));
    course.enrollStudent(std::make_unique<Student>(2, "Bob"));
    auto students = course.getStudents();
    for (auto student : students) {
        std::cout << student->getName() << std::endl;
    }
    return 0;
}
```

In this code, two classes are defined: `Student` and `Course`. The `Student` class has two private data members: `m_id`, which is an integer representing the student's identification number, and `m_name`, which is a string representing the student's name. The `Course` class also has a private data member, `m_name`, which represents the name of the course, and a vector of smart pointers to `Student` objects, named `m_students`.

The `Course` class has two public member functions. The first one, `enrollStudent()`, takes a smart pointer to a `Student` object as an argument and adds it to the vector of enrolled students. The second function, `getStudents()`, returns a copy of the vector of enrolled students.

The `Course` class maintains a collection of students through a vector of shared pointers to `Student` objects. The `Course` class also provides methods to enroll a new `Student` and retrieve all the `Student` objects currently enrolled in the course. However, the `Student` objects themselves are not created or destroyed by the `Course` object. They exist independently and can be enrolled in multiple courses. Therefore, this is not an example of composition or aggregation.

Instead, the `Course` class and `Student` class are associated with each other through the concept of enrollment. A `Course` object enrolls one or more `Student` objects, and each `Student` object can be enrolled in one or more `Course` objects. This is a typical example of association, which models a relationship between two or more classes that does not imply ownership or containment.

The UML class diagram of the above code looks like this:

<p>
  <img src="association.svg" alt="UML class diagram of student and course example">
</p>

This diagram represents the two classes, `Student` and `Course`, and their association where a `Course` object enrolls 0 to many `Student` objects. The direction of the arrow indicates the direction of the association: a `Course` object enrolls `Student` objects, so the arrow points from `Course` to `Student`. The multiplicity notation `"0..*"` indicates that a `Course` object can enroll zero or more `Student` objects.

#### Aggregation

Aggregation is a more specific type of association, where one class is composed of one or more other classes, but those classes can still exist independently. This relationship is useful when there is a `"has-a"` relationship between the classes, where one class is made up of another class, but the two can still exist independently.

A real-life example of aggregation in C++ could be a university library system. The library system can be represented as a class, which consists of one or more `Book` objects. Each Book object can exist independently of the library system, but it is still part of the library system.

```cpp
#include <iostream>
#include <string>
#include <vector>

class Book {
   private:
    std::string m_title;
    std::string m_author;

   public:
    Book(std::string title, std::string author)
        : m_title(std::move(title)), m_author(std::move(author)) {}

    std::string getTitle() const { return m_title; }

    std::string getAuthor() const { return m_author; }
};

class LibrarySystem {
   private:
    std::vector<Book> m_books;

   public:
    LibrarySystem() {}

    void addBook(Book book) { m_books.push_back(book); }

    std::vector<Book> getBooks() const { return m_books; }
};

int main() {
    LibrarySystem myLibrary;
    myLibrary.addBook(Book("The Great Gatsby", "F. Scott Fitzgerald"));
    myLibrary.addBook(Book("To Kill a Mockingbird", "Harper Lee"));

    std::vector<Book> books = myLibrary.getBooks();
    for (const auto& book : books) {
        std::cout << book.getTitle() << " by " << book.getAuthor() << std::endl;
    }

    return 0;
}
```

In this implementation, the `Book` class has two private data members `m_title` and `m_author`, which store the title and author of a book, respectively. The Book class also has a constructor that takes two `std::string` arguments to initialize the `m_title` and `m_author` data members, as well as two member functions `getTitle()` and `getAuthor()` that return the title and author of the book, respectively.

The `LibrarySystem` class has one private data member `m_books`, which stores a vector of Book objects. The LibrarySystem class also has a constructor that initializes the `m_books` data member, an `addBook()` member function that takes a `Book` object and adds it to the `m_books` vector, and a `getBooks()` member function that returns the vector of `Book` objects.

The `LibrarySystem` class has a vector of `Book` objects, which it manages by adding or removing them from the vector. The `Book` objects themselves are not created or destroyed by the `LibrarySystem` object. They exist independently and can be part of other `LibrarySystem` objects or other collections of `Book` objects.

The `LibrarySystem` class does not own or contain the `Book` objects; rather, it aggregates them as part of its collection of books. The `Book` objects can exist and be used outside the context of the `LibrarySystem` object, and their lifetime is not tied to the lifetime of the LibrarySystem object.

Therefore, this is an example of aggregation, which models a `"has-a"` relationship between two classes, where one class (the aggregator) contains a collection of objects of another class (the aggregate). The aggregate objects can exist independently of the aggregator and can be part of other collections or relationships.

Let's take a look at the UML class diagram of the above system:

<p>
  <img src="aggregation.svg" alt="UML class diagram of above system">
</p>

This UML class diagram shows aggregation between two classes: A `LibrarySystem` has zero or more (shown by `0..*`) `Book`, and a `Book` is aggregated with zero or more `LibrarySystem` (at a time).

#### Composition

Composition is the strongest type of relationship, where one class is composed of one or more other classes, and those classes cannot exist independently. This relationship is useful when there is a "part-of" relationship between the classes, where one class is made up of another class and cannot exist without it.

Understanding these three types of relationships is essential for effective software design, as they help to define how different parts of a system interact with each other and ensure that the system is both maintainable and scalable. By carefully choosing the appropriate type of relationship for each part of a system, software designers can create systems that are both powerful and flexible.

#### How to differentiate aggregation and association?

Aggregation and association are both types of relationships between classes in object-oriented programming, but they represent different kinds of relationships.

Association is a relationship between two or more classes, where objects of one class are connected to objects of another class. In an association, the objects of one class use or interact with the objects of another class, but they do not own or compose those objects. For example, a university has many students and professors, but the students and professors can exist independently of the university.

Aggregation is a specific type of association, where one class is composed of one or more other classes. In an aggregation, the composed objects are part of the whole object, but they can still exist independently of it. For example, a car is composed of an engine, wheels, and other parts, but the engine, wheels, and parts can exist independently of the car.

Here are some key differences between aggregation and association:

Ownership: In aggregation, the composed objects are part of the whole object and are owned by it, while in association, the objects are not owned by each other.

Multiplicity: In aggregation, a class can be composed of one or more instances of another class, while in association, the relationship can be one-to-one, one-to-many, or many-to-many.

Dependency: In aggregation, the whole object depends on the composed objects, while in association, the objects are not dependent on each other.

To summarize, association is a general term for a relationship between two or more classes, while aggregation is a specific type of association where one class is composed of one or more other classes.

### Generalization

In software design, **generalization** is a powerful principle that eliminates redundancy and optimizes problem-solving. This principle is not exclusive to software development and is widely used in various disciplines.

In programming, methods are frequently used to model algorithmic behaviors. By defining a method, a programmer can generalize a behavior and apply it to various input data, reducing the need for duplicate code throughout the program.

Object-oriented modelling utilizes generalization as a primary design principle to reduce redundancy through class inheritance. By identifying shared characteristics between multiple classes and factoring them out into another class, object-oriented modelling achieves generalization beyond the creation of a method that can be applied to different data.

Object-oriented programming uses inheritance to achieve generalization, which allows for the creation of parent and child classes. Child classes inherit attributes and behaviors from their parent class, which helps to eliminate redundancy in code. By factoring out repeated or common characteristics into a parent class, the resulting code becomes more efficient and easier to manage. Parent classes are designed to capture general ideas and have broader applications, making them a valuable tool for developers.

In object-oriented programming, a single parent class can have multiple child classes that inherit its common attributes and behaviors. While each child class may also have unique attributes and behaviors, they all share the same general characteristics from the parent class. This allows for efficient and organized coding, with the ability to easily add specialized features to each child class.

In the world of object-oriented programming, a superclass is the term used for a parent class, while a subclass refers to the child class. By inheriting attributes and behaviors from its parent class, a subclass can specialize and become more focused in its functionality. This process of inheritance allows for the creation of a generalization at the superclass level.

Using parent classes in object-oriented programming can greatly increase the efficiency and accuracy of your code. By creating a general template that can be inherited by multiple child classes, you save time and reduce the risk of errors. Additionally, parent classes make your code more flexible, maintainable, and reusable.

<!-- markdownlint-capture -->
<!-- markdownlint-disable -->
> Choosing appropriate names for superclasses and subclasses is an important aspect of object-oriented modelling. While you can name your classes however you like, it is recommended to name them after the real-world objects or concepts they represent. This not only makes the code easier to understand but also helps with the overall organization and maintenance of the codebase.
{: .prompt-tip }
<!-- markdownlint-restore -->

Generalization offers numerous benefits in object-oriented modelling. Inheriting attributes and behaviors from a superclass to subclasses allows for easy maintenance of common code, resulting in robust software. Changes made in the superclass are automatically reflected in all subclasses, making software more manageable. Furthermore, subclasses can be easily added without having to recreate common attributes and behaviors, enabling software to expand seamlessly. As a result, generalization facilitates reusable code and ensures that identical code blocks can be used for multiple classes, leading to more efficient software solutions.

<!-- markdownlint-capture -->
<!-- markdownlint-disable -->
> The **"Don't Repeat Yourself"** rule, or **D.R.Y.**, is a key principle in coding, and it is exemplified through both methods and inheritance. By reusing code, developers can write less code overall, reducing repetition and making maintenance easier. In other words, generalization through methods and inheritance allows for more efficient and sustainable coding practices.
{: .prompt-info }
<!-- markdownlint-restore -->

#### Real-life example

Let's consider a real-life example of generalization in C++ using a simple scenario of shapes. Imagine you want to write a program that deals with various shapes like circles, squares, and triangles. Each shape has common properties like area and perimeter, but they also have their unique attributes and methods.

To achieve generalization, you can create an abstract base class called "Shape" that defines the common properties and methods that all shapes share. This class will serve as a blueprint for all specific shapes.

Here's an example implementation:

```cpp
#include <iostream>

class Shape {
public:
    virtual double getArea() = 0;
    virtual double getPerimeter() = 0;
};

class Circle : public Shape {
private:
    double radius;

public:
    Circle(double r) : radius(r) {}

    double getArea() {
        return 3.14159 * radius * radius;
    }

    double getPerimeter() {
        return 2 * 3.14159 * radius;
    }
};

class Square : public Shape {
private:
    double side;

public:
    Square(double s) : side(s) {}

    double getArea() {
        return side * side;
    }

    double getPerimeter() {
        return 4 * side;
    }
};

class Triangle : public Shape {
private:
    double base;
    double height;

public:
    Triangle(double b, double h) : base(b), height(h) {}

    double getArea() {
        return 0.5 * base * height;
    }

    double getPerimeter() {
        // Assuming it's an equilateral triangle for simplicity
        return 3 * base;
    }
};

int main() {
    Circle circle(5);
    std::cout << "Circle Area: " << circle.getArea() << std::endl;
    std::cout << "Circle Perimeter: " << circle.getPerimeter() << std::endl;

    Square square(4);
    std::cout << "Square Area: " << square.getArea() << std::endl;
    std::cout << "Square Perimeter: " << square.getPerimeter() << std::endl;

    Triangle triangle(3, 6);
    std::cout << "Triangle Area: " << triangle.getArea() << std::endl;
    std::cout << "Triangle Perimeter: " << triangle.getPerimeter() << std::endl;

    return 0;
}
```

In this example, the `Shape` class acts as a generalized representation of all shapes. It defines two pure virtual functions `getArea()` and `getPerimeter()`, which must be implemented by any derived class. The `Circle`, `Square`, and `Triangle` classes inherit from the `Shape` class and provide their own implementations of the area and perimeter calculations.

By using generalization, we can treat all shapes as instances of the `Shape` class, allowing us to write more flexible code that can work with different shapes interchangeably.

Here's the UML class diagram of the above example of shapes in C++:

<p>
  <img src="generalization.svg" alt="UML class diagram, demonstrating the generaliztion.">
</p>

### Conclusion

In this article, we explored two fundamental design principles in object-oriented programming: decomposition and generalization. We learned how decomposition allows us to break down complex systems into manageable components, enabling modular and scalable software. By identifying distinct responsibilities and creating objects based on these abstractions, we achieve code organization and maintainability.

Generalization, on the other hand, helps us eliminate redundancy and optimize problem-solving through class inheritance. By factoring out common attributes and behaviors into a superclass, we create a general template that can be inherited by multiple subclasses. This approach promotes code reuse, flexibility, and scalability, while maintaining a clear hierarchy and enhancing code efficiency.

Throughout the article, we covered various real-life examples and practical implementations in C++, along with corresponding UML class diagrams. By understanding and applying decomposition and generalization effectively, we can design software systems that are modular, extensible, and easy to maintain.

By incorporating these principles into our object-oriented modelling practices, we can build robust and flexible software solutions, reducing code duplication and improving code organization. Whether we are developing small-scale applications or large-scale systems, decomposition and generalization play vital roles in creating efficient, reusable, and maintainable codebases.
