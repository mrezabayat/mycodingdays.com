---
title: "Object Oriented Modelling - Part 1: Abstraction and Encapsulation"
date: 2023-02-04
description: "In this article, we’ll examine common modelling problems and how programming languages have evolved towards object orientation. And we’ll explore abstraction and encapsulation. We'll discuss each topics with code examples in C++ and UML diagrams."
tags: ["Object-oriented modelling", "Abstraction", "Encapsulation", "Decomposition", "Generalization", "Programming languages", "C++", "UML", "Design principles", "Software development"]
categories: ["Design and Architecture"]
author: <author_id>
media_subpath:  /assets/img/posts/005
image:
    path: banner.png
---

In this article, we'll dive deeper into the world of object-oriented modelling. We'll start by examining common modelling problems and how programming languages have evolved towards object orientation. **Abstraction**, **encapsulation**, **decomposition**, and **generalization** are four major design principles that are essential for problem-solving and lead to software that is flexible, reusable, and easy to maintain. In this article, we'll explore **abstraction** and **encapsulation**. Following these principles is critical for developing well-designed software.

We'll also discuss how to express design structure in C++ code and UML class diagrams using the principles of abstraction and encapsulation.

By the end of this article, you'll have a solid understanding of **abstraction** and **encapsulation** concepts of object-oriented modelling and be well-equipped to create software that is both effective and efficient. So, let's dive in and explore these design principles in-depth!

## Designing Effective Software Models

When embarking on a software development project, it's important not to dive right into writing code. Instead, taking the time to understand the full requirements of the product and using good design practices is crucial. Designing falls between understanding the requirements and building the product, dealing with both the problem and solution spaces. Effective design should present and describe concepts in a way that both users and developers can understand, using common terms.

There are many approaches to making the design process easier, with some strategies and programming languages developed for specific kinds of problems. One popular approach is the object-oriented approach, which allows concepts in the problem and solution spaces to be described as objects that can be understood by both users and developers. This shared understanding facilitates discussions around complex problems, and object-oriented programming with object-oriented languages is an effective means of solving complex problems.

![Software Architecture](software-architecture.jpg)

Object-oriented design involves conceptual design, which uses object-oriented analysis to identify key objects and break down the problem into manageable pieces, and technical design, which uses object-oriented design to refine object details, including attributes and behaviors, making them clear enough for developers to implement as working software. These design activities happen iteratively and continuously, with the goal of constructing and refining models of all software objects.

Software models are essential for understanding and organizing the design process, and design principles and guidelines are applied to simplify objects and look for commonalities that can be handled consistently. Models should be continuously evaluated to ensure the original problem is addressed, and qualities such as reusability, flexibility, and maintainability are satisfied. Models also serve as design documentation and are often mapped to skeletal source code, especially in object-oriented languages like Java.

Software models are typically expressed in a visual notation called [Unified Modeling Language (UML)](https://en.wikipedia.org/wiki/Unified_Modeling_Language), with different kinds of UML diagrams used to focus on different software issues (for more information on various UML diagrams see [this post](https://www.mycodingdays.com/uml_modeling_with_plantuml_a_comprehensive_guide_with_examples/)). Structural models can describe what objects do and how they relate, similar to a scale model of a building in architecture.

Understanding the role of models in design and their relationship to coding languages is crucial. In the next section, we'll review the history of programming languages.

## The Evolution of Programming Languages: Adapting to Changing Needs

Languages are constantly evolving to effectively communicate thoughts and ideas between people. Programming languages are no exception to this rule and have undergone significant changes over time. These changes have been driven by the need to find more effective solutions to existing problems, and to address new data structures. Programming languages and paradigms have also evolved, leading to shifts in programming techniques.

![Evolution of Programming Languages](evolution.jpg)

As a **software developer**, it is essential to have a thorough understanding of the history of programming paradigms. Some systems may still use older languages and design paradigms, and it may be more efficient to use a different paradigm for specific problems. Additionally, new programming languages may only modify existing structures rather than introducing entirely new ones. Therefore, having knowledge of the past can be a significant advantage in the field of software development.

Top-down programming is an example of a programming language and design strategy that is suited for solving data-processing problems. This design involves mapping processes in the problem to routines to be called, starting with the "top" process. This design is often represented by a tree of routines and implemented in a programming language that supports subroutines. Understanding such design strategies and programming languages that are specific to certain problems can be beneficial in solving complex software development issues.

![Programming Languages](evolution.png)

The table blew summarizes major programming paradigms throughout the history of programming languages.

| Programming Language            | Time Period      | Solutions Afforded                                                                                                                                                  | Unresolved Issues                                                                                                                                    |
| ------------------------------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
| **COBOL and Fortran**           | 1960s            | Introduced the imperative paradigm, dividing large programs into subroutines. Global data centralized variables for quicker access, optimizing performance.         | Alterations to global data could cause subroutines to encounter unexpected results, highlighting a need for improved data management.                |
| **Algol 68 and Pascal**         | Early 1970s      | Introduced scopes and local variables for subroutines, reducing global data issues. Enabled abstract data types for better organization and data integrity.         | Rising complexity of software and reduced cost of computer time made managing larger programs in a single file impractical, requiring new paradigms. |
| **C and Modula-2**              | Mid-1970s        | Allowed code organization across multiple files, enhancing maintainability. Introduced header files and unique instances of abstract data types for better control. | Inheritance of abstract data types remained a challenge, limiting design flexibility.                                                                |
| **Object-Oriented Programming** | 1980s to present | Classes enabled inheritance, better real-world representation, and improved compartmentalization. Supported by popular languages like Java, C++, and Python.        | Object-oriented paradigms improved scalability and organization but still face challenges with complexity and evolving system requirements.          |

## Mastering the Four Key Principles of Object-Oriented Programming

In object-oriented programming, creating models of object representation is made possible. However, it's important to understand the major design principles that make object-oriented programming work. These principles include abstraction, encapsulation, decomposition, and generalization. By mastering these principles, you can develop a strong foundation for creating effective and efficient object-oriented programs. Read on to learn more about these key design principles and how they can help you create better programs.

### Abstraction

**Abstraction** is a crucial design principle in object-oriented programming that simplifies complex ideas. By reducing a concept to its essentials and ignoring extraneous details, abstraction helps developers to focus on the critical elements needed to solve a problem within a given context. As one of the four primary design principles, abstraction is essential for creating clear and concise class designs that are easy to understand and modify. Whether you're building a gaming app or a running exercise app, abstraction enables you to create an appropriate software development context that suits the purpose of the application.

![Complex Idea](complex-idea.jpg)

To create an effective abstraction, it's important to follow the rule of least astonishment. This means that the essential attributes and behaviors should be clearly defined without any unexpected surprises or irrelevant details that go beyond its scope. By doing so, the abstraction will make sense and serve its intended purpose.

Programming concepts comprise various elements, such as functions, classes, methods, and enumerations. In object-oriented modeling, the principle of abstraction is closely related to the concept of a class. By using abstraction to determine the fundamental details of a concept, these details may be defined within a class. Every object that is created from a class includes the essential details to represent an instance of the concept, but it may also have unique characteristics. Consider a cookie cutter used to create gingerbread men. Each gingerbread man cookie belongs to the "gingerbread men" class and shares important features such as a head, arms, and legs, despite being decorated differently.

When creating an abstraction, it's crucial to consider the context or perspective as it can impact the essential characteristics of a concept. For example, think of the essential characteristics of a person. Without context, it can be challenging to understand. But, in a gaming app, the essential characteristics of a person would be in the context of a gamer. In contrast, in a running exercise app, it would be in the context of an athlete. So, it's essential to choose the most appropriate abstraction for the context of software development. Understanding the context before creating an abstraction is crucial for success.

Understanding the essential characteristics of an abstraction can be done in two ways: by examining its fundamental **attributes** and by analyzing its core **behaviors** or responsibilities.

In software development, basic attributes are fixed characteristics that do not disappear over time. These attributes may have changing values, but the attributes themselves remain constant. For instance, the concept of a tiger may have an age attribute, and although the tiger's age value may vary, the age attribute remains an essential basic attribute of the tiger concept.

When forming an abstraction, it's essential to consider not only the basic attributes but also the basic behaviors or responsibilities of a concept. For example, a tiger abstraction not only has attributes such as age, but also behaviors such as hunting, eating, and sleeping that are essential for its survival. These behaviors are considered responsibilities of the tiger abstraction for its purpose in the ecosystem.

When forming an abstraction, it's important to only include a concept's essential attributes and behaviors. The appropriate abstraction can be determined by considering the context. For instance, when dealing with a lion in a hunting context, it's unnecessary to consider its preferred sleeping position. If the context shifts, the correct abstraction may also shift accordingly.

Abstraction is a powerful tool in software design that offers many benefits. By simplifying class designs and emphasizing essential attributes and behaviors, abstractions can make code more focused, clear, and easy to understand for other developers. However, context and perspective are critical factors that must be taken into account to create effective abstractions. It is also essential to review and modify abstractions as necessary when the system's purpose or problem changes.

In C++, abstraction is implemented using classes and access modifiers. Through abstraction, programmers can simplify the use of complex systems, reduce code duplication, and enhance the maintainability of software. In this example, we will explore how abstraction can be used in C++ to create a basic bank account system.

```cpp
#include <iostream>
#include <string>
#include <utility>

class BankAccount {
   private:
    std::string m_name;
    int m_accountNumber;
    double m_balance;

   public:
    BankAccount(std::string name, int accountNumber, double balance)
        : m_name(std::move(name)),
          m_accountNumber(accountNumber),
          m_balance(balance) {}

    void deposit(const double amount) {
        m_balance += amount;
        std::cout << "Deposit successful. New balance: $" << m_balance
                  << std::endl;
    }

    void withdraw(const double amount) {
        if (m_balance - amount >= 0) {
            m_balance -= amount;
            std::cout << "Withdrawal successful. New balance: $" << m_balance
                      << std::endl;
            return;
        }
        std::cout << "Withdrawal failed. Insufficient balance." << std::endl;
    }

    void display() {
        std::cout << "Name: " << m_name << std::endl;
        std::cout << "Account Number: " << m_accountNumber << std::endl;
        std::cout << "Balance: $" << m_balance << std::endl;
    }
};

int main() {
    BankAccount account("John Doe", 12345, 1000);
    account.display();
    account.deposit(500);
    account.withdraw(2000);
    account.withdraw(500);
    account.display();

    return 0;
}
```

Output:

```bash
Name: John Doe
Account Number: 12345
Balance: $1000
Deposit successful. New balance: $1500
Withdrawal failed. Insufficient balance.
Withdrawal successful. New balance: $1000
Name: John Doe
Account Number: 12345
Balance: $1000
```

In this example, the `BankAccount` class is an abstraction of a real-world bank account. It represents the essential features and behaviors of a bank account, such as the ability to deposit and withdraw funds, and to display the account details. The implementation of these features is hidden from the user of the `BankAccount` class (in the `main` function), who only needs to know how to interact with the object through its public methods. This allows for easy and safe manipulation of the bank account object without exposing its underlying implementation details.

In a class diagram, each concept or class is depicted with a box, just like the one shown blew. This box is divided into three sections, the class name, properties, and operations.

<p>
  <img src="BackAccount.svg" alt="class diagram of the bank account">
</p>

- The class name is the same as the name of the corresponding class in code. 
- The properties section is equivalent to the member variables in code, and it defines the attributes of the abstraction using a standard template for the variable name and type:

  `<variable name>:<variable type>`

  The variable types can be primitive types or classes.
- The operations section is equivalent to methods in code and defines the behaviors of the abstraction using a standard template for the operation name, parameter list, and return type.

  `<name>( <parameter list> ) : <return type>`

### Encapsulation

**Encapsulation** is a crucial design principle that involves the concept of containing something in a capsule. It has three essential ideas that make it useful for programming. First, it enables bundling attribute values and behaviors into an object. Second, it allows for exposing certain data and functions through an interface that can be accessed from other objects. Third, it restricts access to certain data and functions to only within the object, ensuring privacy and security. Encapsulation is a vital aspect of object-oriented programming that helps create organized, efficient, and secure code.

![Encapsulation](Encapsulation.png)

Encapsulation is a crucial design principle that involves the concept of containing something in a capsule. It has three essential ideas that make it useful for programming.

- First, it enables bundling attribute values and behaviors into an object.
- Second, it allows for exposing certain data and functions through an interface that can be accessed from other objects.
- Third, it restricts access to certain data and functions to only within the object, ensuring privacy and security. Encapsulation is a vital aspect of object-oriented programming that helps create organized, efficient, and secure code.

When designing a software system, it's important to consider how to organize related data and functionality into cohesive units. The design principle of encapsulation helps achieve this by bundling data and behavior into a self-contained object, allowing for better organization and control over access to the data. This makes it easier to program and maintain code, as everything related to a specific object is located in one place.

Encapsulation is a crucial programming concept that enables objects created from a class to have their own data values for attributes and exhibit behaviors. This simplifies programming by keeping data and the code that manipulates it together in one place, making it easier to maintain and update.

To achieve effective encapsulation, an object's data should only include what is relevant for its purpose. For instance, a lion object would only contain information about the food it hunts and not details about animals on a different continent. This ensures that a class only has knowledge of the attributes or data that are relevant to its function, promoting effective encapsulation.

In addition to defining the attributes or data relevant to an object, a class also defines its behaviors through methods. These methods manipulate the attribute values or data to achieve the desired behaviors. However, not all methods are made accessible to other objects. Only certain methods, which are designed to be exposed or accessed from outside the class, are made available to other objects. This provides an interface to other objects to use the class.

#### Integrity and Security

Encapsulation, one of the key principles of object-oriented design, not only enables the bundling of attributes and behaviors into self-contained objects, but it also plays an important role in ensuring data integrity and protecting sensitive information. By restricting access to certain data and functions within an object, encapsulation provides a level of security that prevents unauthorized access and manipulation of sensitive data. This is particularly important in applications that handle sensitive information such as financial data, personal information, and medical records.

![security](security.jpg)

By restricting access to certain attributes and methods of an object, encapsulation can help maintain data integrity and prevent sensitive information from being tampered with. This approach also ensures that the data within an object cannot be changed through variable assignments, thereby preventing any assumptions or dependencies from breaking.

Encapsulation helps maintain data privacy by restricting access to sensitive information. This prevents the data from being accessed or changed through means other than specific methods, ensuring that the data remains secure and confidential. It also prevents sensitive information from being revealed through queries that rely on this data.

#### Changeable Implementation

Encapsulation is a powerful tool for software development, especially when it comes to implementing changes. The ability to separate the exposure of data from the actual bundle of attributes allows for flexibility in implementation while maintaining a consistent interface. This means that even if the underlying code changes, users can still access the same information using the same interface, without needing to understand the details of how the implementation works.

#### Black box

The principle of encapsulation supports the concept of changeable implementation and is closely tied to black box thinking. The beauty of encapsulation is that the details of the internal workings of a class are hidden from other classes, allowing for the implementation of attributes and methods to change without affecting the accessible interface of the class. This black box thinking means that as long as a class can access the interface, it does not need to know the specifics of the computations happening within the class. In essence, a class acts like a black box, allowing inputs and producing outputs through its methods without revealing its internal workings.

By implementing encapsulation and black box thinking, an abstraction barrier is created where the inner workings of a class become irrelevant to the outside world. As a result, the abstraction significantly reduces complexity for users accessing the class, making the system more manageable and easier to understand.

Encapsulation not only simplifies complexity, but also increases reusability through black box thinking. Other classes only need to know which methods to call, what inputs to provide, and what outputs to expect. This makes software modular and easy to work with, as classes can be managed independently without exposing their internal behavior to other classes. Encapsulation ensures that the implementation details of a class remain hidden, as long as the interface is maintained, making software development more efficient and streamlined.

Encapsulation, a fundamental principle in object-oriented programming, involves bundling data and their related functions into a self-contained object. This creates a boundary between the object and the rest of the program, controlling the access to the object's data and functions. Encapsulation allows for data to be exposed and made accessible from other objects or restricted to within the object, as needed. By encapsulating data and functions within an object, developers can write cleaner, more modular code that is easier to maintain and debug.

In UML class diagrams, encapsulation is represented by defining all of the relevant data of an object in the attributes section of the class, and by providing specific methods to access and modify those attributes. This approach ensures that the object's data and methods are bundled together in a self-contained entity and can be exposed or restricted as needed, promoting data security and reducing complexity in the code.

In UML class diagrams, we use symbols to indicate the access modifiers of class members.

- Private members are denoted with a minus sign (-).
- Protected members are denoted with a hash symbol (#).
- Public members are denoted with a plus sign (+).

For example, if we have a private member variable called "age" in a class, we would represent it in UML as follows:

```text
- age: int
```

If we have a public method called "setName" that takes a string parameter and returns void, we would represent it in UML as follows:

```text
+ setName(name: string): void
```

Similarly, a protected member variable called "count" would be represented as:

```text
# count: int
```

Two common methods used to maintain data integrity are getters and setters.

- Getters are used to retrieve data and are usually named in the format of `get<attribute name>`. They are often used to retrieve private data.
- Setters are often used to set a private attribute in a safe manner. Setters are used to change data and are named in the format of `set<attribute name>`.

Both types of methods help ensure that data is accessed and modified in an authorized way.

Here's an example of encapsulation in C++:

```cpp
#include <iostream>
#include <string>

class Person {
   private:
    std::string m_name;
    int m_age;

   public:
    void setName(std::string name) { m_name = name; }
    std::string getName() { return m_name; }
    void setAge(int age) { m_age = age; }
    int getAge() { return m_age; }
};

int main() {
    Person p1;
    p1.setName("John Doe");
    p1.setAge(30);
    std::cout << p1.getName() << " is " << p1.getAge() << " years old."
              << std::endl;
    return 0;
}
```

In this example, the `Person` class has two private data members: `m_name` and `m_age`. These data members are not directly accessible from outside the class. Instead, public member functions are used to set and get the values of these data members. The `setName` and `setAge` functions are used to set the values of name and age, respectively. The `getName` and `getAge` functions are used to retrieve the values of name and age, respectively.

This encapsulation ensures that the name and age data members are not directly accessible from outside the class. This helps to prevent accidental or intentional modification of these data members by other parts of the program. It also makes the code more maintainable, as any changes to the implementation of the Person class can be made without affecting the rest of the program.

The UML class diagram for `Person` class looks like this

<p>
  <img src="Person.svg" alt="the uml diagram of the Person class">
</p>

In conclusion, object-oriented modelling is a fundamental concept in software design that allows developers to create efficient and effective software. The four key principles of object-oriented programming - abstraction, encapsulation, decomposition, and generalization - are essential for creating well-designed software models.

Abstraction allows developers to focus on the essential features of a system while ignoring the irrelevant details. Encapsulation protects the internal workings of a system from external interference, providing security and integrity. Decomposition breaks down complex systems into smaller, more manageable parts, making maintenance and updating easier. Generalization allows for code reuse and flexibility in designing and modifying a system.

By following these principles, developers can create software that is flexible, reusable, and easy to maintain, leading to more efficient and effective software development. The evolution of programming languages towards object orientation has allowed developers to implement these principles more easily, resulting in more powerful and sophisticated software systems.

In the next part of this series, we will explore the principles of decomposition and generalization in more depth, and show how to express them in C++ code and UML class diagrams. By mastering these four principles, developers can design software models that are robust, efficient, and secure, and meet the needs of modern software development.
