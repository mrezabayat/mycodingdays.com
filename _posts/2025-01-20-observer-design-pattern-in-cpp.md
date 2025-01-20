---
title: "The Observer Design Pattern: A Weather Station Example in C++"
date: 2025-01-20
description: "This article provides a comprehensive guide to understanding and implementing the **Observer Design Pattern** using a weather station example in C++. It explains how to establish a one-to-many relationship between a subject and its observers, enabling dynamic updates whenever the subject's state changes. Through clear explanations, detailed code examples, and a class diagram, you'll learn how to design a loosely coupled, extensible system suitable for real-time updates. Whether you're a beginner or an experienced developer, this article will help you master the Observer Design Pattern and apply it effectively in your software projects."
tags: ["Observer Design Pattern", "C++ Design Patterns", "Weather Station Example", "Software Architecture", "Behavioral Patterns", "Real-Time Systems", "Event-Driven Programming", "Loosely Coupled Systems", "Object-Oriented Design", "C++ Tutorials"]
categories: ["Design Patterns", "Design and Architecture"]
author: mrbayat
media_subpath:  /assets/img/posts/008
image:
    path: banner.jpg
---

## Observer Design Pattern

The **Observer Design Pattern** is a behavioral design pattern used to establish a one-to-many dependency between objects. It allows one object, called the **subject**, to notify multiple dependent objects, called **observers**, about any changes in its state automatically, without the subject needing to know the details of the observers.

### Key Features

1. **Decoupling**: The subject and observers are loosely coupled. The subject only knows that it has observers, but not their specific implementation.
2. **Dynamic Relationships**: Observers can be added or removed at runtime, allowing flexibility in managing dependencies.
3. **Push or Pull Communication**:
   - In the **push model**, the subject sends specific details about changes to observers.
   - In the **pull model**, the observer queries the subject for state updates.

### Components

1. **Subject**:
   - Maintains a list of observers.
   - Provides methods for attaching, detaching, and notifying observers.

2. **Observers**:
   - Define an interface for receiving updates from the subject.

3. **Concrete Subject**:
   - Implements the subject's methods and maintains its state.
   - Notifies observers of changes to its state.

4. **Concrete Observers**:
   - Implement the observer interface.
   - Define the specific reaction to updates received from the subject.

![observer-design-pattern-uml-class-diagram](observer-design-pattern-uml-class-diagram.png)

### How It Works

1. Observers register themselves with the subject using an `attach` method.
2. When the subject's state changes, it invokes the `notify` method.
3. The subject iterates through its list of observers and calls their `update` method.
4. Observers take appropriate actions based on the notifications they receive.

### Advantages

- **Promotes Reusability**: Subjects and observers can be reused independently.
- **Supports Open/Closed Principle**: Adding new observers doesn’t require modifying the subject.
- **Simplifies Event Handling**: Centralizes the logic for notifying changes.

### Disadvantages

- **Potential Performance Impact**: Notifying a large number of observers can be time-consuming.
- **Memory Leaks**: If observers are not detached properly, it can lead to memory issues.
- **Unpredictable Order**: The order of notification to observers is often undefined, which might lead to inconsistencies.

## Observer Pattern

The Observer Pattern is a behavioral design pattern that allows an object, known as the subject, to maintain a list of its dependents, called observers, and notify them of any state changes, usually by calling one of their methods.

### When to Use

- When a change to one object requires changing others, and you don't know how many objects need to be changed.
- When an object should be able to notify other objects without making assumptions about who those objects are.

### Weather Station Example Using the Observer Design Pattern

The **Observer Design Pattern** enables a one-to-many dependency, where a subject notifies its observers of any state changes. This example demonstrates how a weather station (`WeatherData`) can broadcast changes in weather data (temperature, humidity, pressure) to multiple displays.

We use:

- `WeatherData` as the **subject** that stores weather measurements.
- `CurrentConditionDisplay`, `StatisticsDisplay`, and `ForecastDisplay` as the **observers** that respond to updates and display relevant data.
- Interfaces (`IObserver`, `ISubject`, `IDisplayElement`) to ensure a loosely coupled design.

Here is how it works:

1. **Subject (WeatherData)**: Maintains a list of observers, provides methods to register/remove them, and notifies them of state changes.
2. **Observers**: Implement `IObserver` to receive updates. Each observer updates its state and displays information based on the data.
3. **Client**: Creates the subject and observers, registers observers with the subject, and updates the subject's state.

#### Code Implementation

We define abstract interfaces to enforce contracts for the subject, observer, and display elements.

##### `IObserver` Interface

Defines the `update()` method, called by the subject when notifying observers.

```cpp
#pragma once
namespace ws {
class IObserver {
public:
  virtual ~IObserver() = default;
  virtual void update(double temperature, double humidity, double pressure) = 0;
};
} // namespace ws
```

##### `ISubject` Interface

Defines methods for managing and notifying observers.

```cpp
#pragma once
#include <memory>

namespace ws {
class IObserver;

class ISubject {
public:
  virtual ~ISubject() = default;
  virtual void registerObserver(std::shared_ptr<IObserver> observer) = 0;
  virtual void removeObserver(std::shared_ptr<IObserver> observer) = 0;
  virtual void notifyObservers() = 0;
};
} // namespace ws
```

##### `IDisplayElement` Interface

Defines the `display()` method for visualizing data.

```cpp
#pragma once
namespace ws {
class IDisplayElement {
public:
  virtual ~IDisplayElement() = default;
  virtual void display() = 0;
};
} // namespace ws
```

##### Concrete Subject

`WeatherData` Implements the `ISubject` interface and stores weather measurements. When data changes, it notifies observers by calling their `update()` methods.

```cpp
#pragma once
#include "isubject.hpp"
#include "iobserver.hpp"
#include <list>

namespace ws {
class WeatherData : public ISubject {
public:
  void registerObserver(std::shared_ptr<IObserver> observer) override {
    observers.push_back(observer);
  }

  void removeObserver(std::shared_ptr<IObserver> observer) override {
    observers.remove(observer);
  }

  void notifyObservers() override {
    for (auto &observer : observers) {
      observer->update(m_temperature, m_humidity, m_pressure);
    }
  }

  void setMeasurements(double temperature, double humidity, double pressure) {
    m_temperature = temperature;
    m_humidity = humidity;
    m_pressure = pressure;
    notifyObservers();
  }

private:
  std::list<std::shared_ptr<IObserver>> observers;
  double m_temperature{};
  double m_humidity{};
  double m_pressure{};
};
} // namespace ws
```



#### Concrete Observers

`CurrentConditionDisplay` displays the current temperature and humidity.

```cpp
#pragma once
#include "iobserver.hpp"
#include "idisplay_element.hpp"
#include <iostream>

namespace ws {
class CurrentConditionDisplay : public IObserver, public IDisplayElement {
public:
  void update(double temperature, double humidity, double pressure) override {
    m_temperature = temperature;
    m_humidity = humidity;
    display();
  }

  void display() override {
    std::cout << "Current conditions: " << m_temperature
              << "F degrees and " << m_humidity << "% humidity" << std::endl;
  }

private:
  double m_temperature{};
  double m_humidity{};
};
} // namespace ws
```

`StatisticsDisplay` displays the average, maximum, and minimum temperatures.

```cpp
#pragma once
#include "iobserver.hpp"
#include "idisplay_element.hpp"
#include <iostream>
#include <limits>

namespace ws {
class StatisticsDisplay : public IObserver, public IDisplayElement {
public:
  void update(double temperature, double humidity, double pressure) override {
    ++m_numberOfReadings;
    m_avgTemperature = (m_avgTemperature * (m_numberOfReadings - 1) + temperature) / m_numberOfReadings;
    m_maxTemperature = std::max(m_maxTemperature, temperature);
    m_minTemperature = std::min(m_minTemperature, temperature);
    display();
  }

  void display() override {
    std::cout << "Avg/Max/Min temperature = " << m_avgTemperature << "/"
              << m_maxTemperature << "/" << m_minTemperature << std::endl;
  }

private:
  int m_numberOfReadings{};
  double m_maxTemperature = std::numeric_limits<double>::min();
  double m_minTemperature = std::numeric_limits<double>::max();
  double m_avgTemperature{};
};
} // namespace ws
```

`ForecastDisplay` predicts weather changes based on pressure differences.

```cpp
#pragma once
#include "iobserver.hpp"
#include "idisplay_element.hpp"
#include <iostream>

namespace ws {
class ForecastDisplay : public IObserver, public IDisplayElement {
public:
  void update(double temperature, double humidity, double pressure) override {
    m_lastPressure = m_currentPressure;
    m_currentPressure = pressure;
    display();
  }

  void display() override {
    std::cout << "Forecast: ";
    if (m_currentPressure > m_lastPressure) {
      std::cout << "Improving weather on the way!" << std::endl;
    } else if (m_currentPressure == m_lastPressure) {
      std::cout << "Same weather ahead!" << std::endl;
    } else {
      std::cout << "Cooler, rainy weather ahead!" << std::endl;
    }
  }

private:
  double m_currentPressure = 29.92;
  double m_lastPressure{};
};
} // namespace ws
```

#### Client Code

The `main()` function demonstrates the interaction between the subject and observers.

```cpp
#include "weather_data.hpp"
#include "current_condition_display.hpp"
#include "statistics_display.hpp"
#include "forecast_display.hpp"
#include <memory>

int main() {
    auto currentConditionDisplay = std::make_shared<ws::CurrentConditionDisplay>();
    auto statisticsDisplay = std::make_shared<ws::StatisticsDisplay>();
    auto forecastDisplay = std::make_shared<ws::ForecastDisplay>();

    ws::WeatherData weatherData;

    weatherData.registerObserver(currentConditionDisplay);
    weatherData.registerObserver(statisticsDisplay);
    weatherData.registerObserver(forecastDisplay);

    weatherData.setMeasurements(80, 65, 30.4);
    weatherData.setMeasurements(82, 70, 29.2);
    weatherData.setMeasurements(78, 90, 29.2);

    return 0;
}
```

The Client Code:

1. Create `WeatherData` as the subject.
2. Create observers (`CurrentConditionDisplay`, `StatisticsDisplay`, `ForecastDisplay`) and register them with `WeatherData`.
3. Call `setMeasurements()` on `WeatherData` to update weather data, which triggers notifications to all observers.

This implementation demonstrates how the Observer Design Pattern allows dynamic updates and maintains a loosely coupled system.

Here is the class diagram of this example:

![weather-station-class-diagram](weather-station-class-diagram.png)

### Conclusion

The **Observer Design Pattern** provides an elegant solution for implementing a one-to-many dependency, ensuring that when a subject's state changes, all its observers are automatically updated. In this example, the **Weather Station** showcases the pattern's real-world application by allowing multiple display elements to observe and react to changes in weather data. 

This design promotes **loose coupling**, as the subject and observers interact through interfaces, making the system highly extensible. For instance, adding a new display element is as simple as creating a new observer class and registering it with the subject, without modifying existing code. This aligns with the **Open/Closed Principle**, a cornerstone of software design.

By leveraging interfaces and dynamic relationships between components, the Observer Design Pattern is ideal for event-driven systems, real-time updates, and scenarios where the subject's state changes frequently. While it can introduce complexity with a large number of observers or notification delays, its benefits in maintainability and scalability often outweigh these challenges.

For developers, mastering this pattern is essential for building robust, modular, and easily extensible applications. Whether it's a weather station, stock market ticker, or GUI framework, the Observer Design Pattern remains a cornerstone of software design.
