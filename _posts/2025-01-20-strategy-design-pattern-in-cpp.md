---
title: "Strategy Pattern in C++: A Flexible Approach to Dynamic Behaviors with Smart Pointers"
date: 2025-01-20
description: "This article demonstrates how to implement the Strategy Pattern in C++, using a simple example of ducks with different flying and quacking behaviors. It highlights the flexibility and reusability of the pattern and shows how smart pointers can be used to manage memory safely and prevent leaks."
tags: ["Strategy Pattern", "C++", "Design Patterns", "Smart Pointers", "Memory Management", "Object-Oriented Programming", "Behavioral Patterns", "C++ Best Practices", "Software Design", "Dynamic Behaviors"]
categories: ["Design Patterns", "Design and Architecture"]
author: <author_id>
media_subpath:  /assets/img/posts/007
image:
    path: banner.jpg
---

## Strategy Design Pattern

### Overview

The Strategy design pattern is a **behavioral** design pattern that enables selecting an algorithm's behavior at runtime. It defines a family of algorithms, encapsulates each one in a separate class, and makes them interchangeable without altering the client code. This pattern promotes the *Open-Closed Principle*, allowing the addition of new strategies without modifying existing ones. It typically consists of three main components: the **Context**, which uses a Strategy object; the **Strategy interface**, which defines a common contract for all algorithms; and the **Concrete Strategies**, which implement specific variations of the algorithm. The Strategy pattern is particularly useful when a class must support multiple behaviors that can vary independently of the clients using them.

### Key Components

![key-component-uml-class-diagram](key_components_uml_class_diagram.png)

1. **Context**
   a. **Role**: Acts as the primary class that interacts with clients and uses a Strategy object to perform specific behaviors.
   b. **Responsibility**: Maintains a reference to a Strategy object and delegates the algorithm's execution to it.
   c. **Flexibility**: Can switch between different Strategy objects at runtime, enabling dynamic behavior changes.

2. **Strategy Interface**
   a. **Role**: Serves as a common contract for all concrete strategy implementations.
   b. **Responsibility**: Declares a method (or methods) that all concrete strategies must implement.
   c. **Purpose**: Ensures consistency and allows the Context to work with any Strategy implementation interchangeably.

3. **Concrete Strategies**
   a. **Role**: Provide specific implementations of the algorithm defined in the Strategy interface.
   b. **Responsibility**: Implement different variations of the algorithm, encapsulating their details.
   c. **Purpose**: Allow easy addition of new behaviors without modifying the Context or other strategies, adhering to the Open-Closed Principle.

### Example

Let’s consider an example to understand the Strategy design pattern in action. We have a `Duck` class that needs to perform different behaviors, such as flying and quacking. Instead of hardcoding these behaviors into the class, they are abstracted into two separate interfaces: `iFlyBehavior` and `iQuackBehavior`. These interfaces define the contracts for flying and quacking actions. Various concrete implementations, such as `FlyWithWings` or `FlyNoWay` for flying and `Quack` or `MuteQuack` for quacking, encapsulate specific behaviors. This approach allows the `Duck` class to dynamically use different behaviors at runtime by composing appropriate strategy objects, ensuring flexibility and adherence to the Open-Closed Principle. New behaviors can be easily introduced without modifying the existing code.

![class diagram](duck-class-diagram.png)

#### Duck Class

```cpp
#pragma once

#include "ifly_behavior.hpp"
#include "iquack_behavior.hpp"

#include <iostream>
#include <memory>

namespace duck {

class Duck {
public:
  virtual ~Duck() = default;
  Duck(const Duck &) = delete;
  Duck(Duck &&other) noexcept 
    : m_flyBehavior(std::move(other.m_flyBehavior))
    , m_quackBehavior(std::move(other.m_quackBehavior)) {}
  Duck &operator=(const Duck &) = delete;
  Duck &operator=(Duck &&other) noexcept {
    if (this != &other) {
        m_flyBehavior = std::move(other.m_flyBehavior);
        m_quackBehavior = std::move(other.m_quackBehavior);
    }
    return *this;
  }

  void swim() const { std::cout << "I'm swimming.\n"; }
  virtual void display() = 0 ;

  void performQuack() { m_quackBehavior->quack(); }
  void performFly() { m_flyBehavior->fly(); }

  void setFlyBehavior(std::unique_ptr<iFlyBehavior> flyBehavior) {
    m_flyBehavior = std::move(flyBehavior);
  }
  void setQuackBehavior(std::unique_ptr<iQuackBehavior> quackBehavior) {
    m_quackBehavior = std::move(quackBehavior);
  }

protected:
  Duck() = default;

  std::unique_ptr<iFlyBehavior> m_flyBehavior;
  std::unique_ptr<iQuackBehavior> m_quackBehavior;
};

}
```

#### Fly Behavior Interface

```cpp
#pragma once

class iFlyBehavior {
public:
  virtual ~iFlyBehavior() = default;
  virtual void fly() = 0;
};
```

#### Quack Behavior Interface

```cpp
#pragma once

class iQuackBehavior {
public:
  virtual ~iQuackBehavior() = default;
  virtual void quack() = 0;
};
```

#### Concrete Fly Behaviors

```cpp
#include "ifly_behavior.hpp"
#include <iostream>

class FlyWithWings : public iFlyBehavior {
public:
  void fly() override {
    std::cout << "I'm flying with wings!\n";
  }
};

class FlyNoWay : public iFlyBehavior {
public:
  void fly() override {
    std::cout << "I can't fly.\n";
  }
};
```

#### Concrete Quack Behaviors

```cpp
#include "iquack_behavior.hpp"
#include <iostream>

class Quack : public iQuackBehavior {
public:
  void quack() override {
    std::cout << "Quack!\n";
  }
};

class MuteQuack : public iQuackBehavior {
public:
  void quack() override {
    std::cout << "...\n";
  }
};
```

### Conclusion

The Strategy Pattern provides an elegant solution for managing algorithms and behaviors in a flexible, reusable, and maintainable way. By encapsulating behaviors in separate classes and leveraging composition, we can easily extend or modify an object's behavior without altering its underlying code. In this example, we showcased how ducks can have different flying and quacking behaviors, demonstrating the versatility of the pattern. Additionally, we utilized smart pointers to manage the dynamic allocation of strategy objects, ensuring memory safety and preventing potential memory leaks. This approach highlights how modern C++ features can enhance traditional design patterns.
