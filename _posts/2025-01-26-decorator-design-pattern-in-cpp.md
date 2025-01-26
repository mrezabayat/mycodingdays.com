---
title: "Decorator Design Pattern for Flexible and Dynamic Object Behavior in C++"
date: 2025-01-26
description: "In this post, we explore the Decorator Design Pattern, a powerful structural pattern that allows you to dynamically add behavior to objects without modifying their code. Through a practical example, we demonstrate how to use decorators to extend object functionality in a flexible and reusable way. This pattern promotes clean design principles like the Open/Closed Principle, ensuring that objects can be extended while keeping existing code intact. Learn how to implement decorators, manage complexity, and enhance your system's flexibility."
tags: ["Decorator Pattern", "Design Patterns", "Object-Oriented Design", "Software Architecture", "Flexibility", "Open/Closed Principle", "C++", "Dynamic Behavior", "Code Reusability"]
categories: ["Design Patterns", "Design and Architecture"]
author: mrbayat
media_subpath:  /assets/img/posts/009
image:
    path: banner.jpg
---

## Overview

The **Decorator Pattern** is a **structural design pattern** that allows behavior to be dynamically added to an individual object, either statically or dynamically, without altering the behavior of other objects from the same class. It is used to extend the functionalities of objects in a flexible and reusable way.

## Key Characteristics

1. **Dynamically Add Functionality**: The pattern provides an alternative to subclassing for extending functionality.
2. **Open/Closed Principle**: The pattern adheres to the Open/Closed Principle by allowing objects to be open for extension but closed for modification.
3. **Compositional Approach**: It uses composition instead of inheritance, where decorators "wrap" the original object to provide additional behavior.

## Structure

The pattern typically includes the following components:

1. **Component**: An interface or abstract class defining the base functionality.
2. **Concrete Component**: A class that implements the `Component` interface and provides the default behavior.
3. **Decorator**: An abstract class that implements the `Component` interface and has a reference to a `Component` object. It forwards requests to the wrapped object while adding new behavior.
4. **Concrete Decorator**: A class that extends the `Decorator` class and adds additional functionality.

### UML Representation

![decorator_uml_representation](decorator_uml_representation.png)

1. **`Component` Interface**:
   - Defines the base functionality.
   - Represented as an interface in UML.

2. **`ConcreteComponent` Class**:
   - Implements the `Component` interface.
   - Provides the core functionality.

3. **`Decorator` Abstract Class**:
   - Implements the `Component` interface.
   - Contains a reference to a `Component` object (composition).
   - Adds functionality by delegating calls to the wrapped component.

4. **Concrete Decorators (`ConcreteDecoratorA` and `ConcreteDecoratorB`)**:
   - Extend the `Decorator` class.
   - Add specific behavior while maintaining the base functionality.

The `o--` relationship between `Decorator` and `Component` indicates a composition, showing that the `Decorator` wraps a `Component` object.

### When to Use

- To dynamically and transparently add responsibilities to individual objects without impacting others.  
- When subclassing becomes impractical due to the need for numerous independent extensions or combinations of functionality.

The decorator pattern is widely used in UI frameworks, logging systems, and data formatting tasks. It provides a powerful tool for achieving clean and extensible designs.

### Advantages

- **Dynamic Flexibility**: You can add or remove responsibilities at runtime.  
- **Reusability**: Decorators can be applied to multiple objects, promoting code reuse.  
- **Adherence to Single Responsibility Principle**: Each decorator focuses on a specific concern, keeping functionality modular.
- **Simplified Class Hierarchies**: Reduces the need for a large number of subclasses.

### Disadvantages

- **Increased Complexity**: Managing many small decorator classes can make the design harder to read and understand.  
- **Performance Overhead**: Layering multiple decorators increases the number of objects and can impact performance.
- **Hard to Debug**: Debugging might be challenging when many decorators are chained. 

## Coffee Shop Example Using the Decorator Pattern

This example demonstrates how to design a flexible coffee shop application using the **Decorator Design Pattern**. The pattern is used to dynamically add condiments (like Milk, Mocha, and Soya) to various coffee types (Espresso, DarkRoast, and HouseBlend) without modifying the base classes.

### Design Components

1. **Component**
   - The `Beverage` abstract class defines the interface for all coffee types and condiments.

2. **Concrete Components**
   - `Espresso`, `DarkRoast`, and `HouseBlend` classes implement `Beverage` and provide specific coffee types.

3. **Decorator Base Class**
   - The `ICondimentDecorator` abstract class inherits from `Beverage` and contains a reference to a `Beverage` object it decorates.

4. **Concrete Decorators**
   - `Milk`, `Mocha`, and `Soya` extend `ICondimentDecorator`, adding specific behaviors and costs.
  
### Class Diagram

Below is the class diagram for the Coffee Shop example:

![class-diagram](class-diagram.png)

This diagram illustrates the relationships between the component (`Beverage`), the concrete components (`Espresso`, `DarkRoast`, `HouseBlend`), the decorator base class (`ICondimentDecorator`), and the concrete decorators (`Mocha`, `Milk`, `Soya`).

### Code Implementation

#### **1. Beverage Base Class**

Defines the interface for all beverages:

```cpp
#pragma once

#include <string>

namespace sb {
class Beverage {
public:
  virtual ~Beverage() = default;
  virtual std::string GetDescription() const { return m_description; }
  virtual double GetCost() const = 0;

protected:
  std::string m_description = "Unknown Beverage";
};
} // namespace sb
```

#### **2. Concrete Components**

Specific coffee types that extend `Beverage`:

**Espresso:**

```cpp
#pragma once

#include "beverage.hpp"

namespace sb {
class Espresso : public Beverage {
public:
  Espresso() { m_description = "Espresso"; }
  double GetCost() const override { return 1.99; }
};
} // namespace sb
```

**DarkRoast:**

```cpp
#pragma once

#include "beverage.hpp"

namespace sb {
class DarkRoast : public Beverage {
public:
  DarkRoast() { m_description = "Dark Roast Coffee"; }
  double GetCost() const override { return 1.99; }
};
} // namespace sb
```

**HouseBlend:**

```cpp
#pragma once

#include "beverage.hpp"

namespace sb {
class HouseBlend : public Beverage {
public:
  HouseBlend() { m_description = "House Blend Coffee"; }
  double GetCost() const override { return 1.89; }
};
} // namespace sb
```

#### **3. Decorator Base Class**

Defines the structure for all decorators:

```cpp
#pragma once

#include "beverage.hpp"
#include <memory>

namespace sb {
class ICondimentDecorator : public Beverage {
public:
  ICondimentDecorator(std::shared_ptr<Beverage> beverage) : m_beverage(std::move(beverage)) {}
  virtual ~ICondimentDecorator() = default;
  virtual std::string GetDescription() const = 0;

protected:
  std::shared_ptr<Beverage> m_beverage;
};
} // namespace sb
```

#### **4. Concrete Decorators**

Each condiment dynamically adds behavior and cost:

**Milk:**

```cpp
#pragma once

#include "icondiment_decorator.hpp"

namespace sb {
class Milk : public ICondimentDecorator {
public:
  Milk(std::shared_ptr<Beverage> beverage) : ICondimentDecorator(std::move(beverage)) {}

  std::string GetDescription() const override { return m_beverage->GetDescription() + m_description; }
  double GetCost() const override { return m_beverage->GetCost() + m_cost; }

private:
  std::string m_description = ", Milk";
  const double m_cost = 0.10;
};
}
```

**Mocha:**

```cpp
#pragma once

#include "icondiment_decorator.hpp"

namespace sb {
class Mocha : public ICondimentDecorator {
public:
  Mocha(std::shared_ptr<Beverage> beverage) : ICondimentDecorator(std::move(beverage)) {}

  std::string GetDescription() const override {
    return m_beverage->GetDescription() + m_description;
  }
  double GetCost() const override { return m_beverage->GetCost() + m_cost; }

private:
  std::string m_description = ", Mocha";
  const double m_cost = 0.20;
};
}
```

**Soya:**

```cpp
#pragma once

#include "icondiment_decorator.hpp"

namespace sb {
class Soya : public ICondimentDecorator {
public:
  Soya(std::shared_ptr<Beverage> beverage) : ICondimentDecorator(std::move(beverage)) {}

  std::string GetDescription() const override {
    return m_beverage->GetDescription() + m_description;
  }
  double GetCost() const override { return m_beverage->GetCost() + m_cost; }

private:
  std::string m_description = ", Soya";
  const double m_cost = 0.15;
};
} // namespace sb
```

#### **5. Main Program**

Demonstrates dynamically decorating beverages:

```cpp
#include "beverage.hpp"
#include "dark_roast.hpp"
#include "espresso.hpp"
#include "house_blend.hpp"
#include "milk.hpp"
#include "mocha.hpp"
#include "soya.hpp"

#include <iostream>
#include <memory>

int main() {
  using namespace sb;

  // Plain Espresso
  std::shared_ptr<Beverage> beverage = std::make_shared<Espresso>();
  std::cout << beverage->GetDescription() << " £" << beverage->GetCost() << std::endl;

  // Dark Roast with double Mocha and Milk
  std::shared_ptr<Beverage> beverage2 = std::make_shared<DarkRoast>();
  beverage2 = std::make_shared<Mocha>(beverage2);
  beverage2 = std::make_shared<Mocha>(beverage2);
  beverage2 = std::make_shared<Milk>(beverage2);
  std::cout << beverage2->GetDescription() << " £" << beverage2->GetCost() << std::endl;

  // House Blend with Soya, Mocha, and Milk
  std::shared_ptr<Beverage> beverage3 = std::make_shared<HouseBlend>();
  beverage3 = std::make_shared<Soya>(beverage3);
  beverage3 = std::make_shared<Mocha>(beverage3);
  beverage3 = std::make_shared<Milk>(beverage3);
  std::cout << beverage3->GetDescription() << " £" << beverage3->GetCost() << std::endl;

  return 0;
}
```

### Output

```text
Espresso £1.99
Dark Roast Coffee, Mocha, Mocha, Milk £2.49
House Blend Coffee, Soya, Mocha, Milk £2.34
```

This demonstrates how the **Decorator Pattern** enables dynamic extension of functionality without modifying existing code. Each condiment is a reusable, composable component.

## Conclusion

The **Decorator Design Pattern** is a powerful tool for extending the functionality of objects dynamically and transparently, without altering their structure or relying on an extensive inheritance hierarchy. In the **Coffee Shop example**, it allows us to dynamically add condiments like Milk, Mocha, and Soya to beverages such as Espresso, DarkRoast, and HouseBlend. This approach adheres to the **Open/Closed Principle**, ensuring that the system is open for extension but closed for modification.

By separating the core functionality (coffee types) from additional behaviors (condiments), the pattern promotes **flexibility**, **reusability**, and **modularity**. However, as demonstrated, the use of multiple decorators can introduce complexity, which should be carefully managed in larger systems.

Overall, the Decorator Pattern is ideal when you need a scalable and maintainable solution to dynamically combine behaviors, as it strikes a balance between flexibility and adherence to solid design principles.
