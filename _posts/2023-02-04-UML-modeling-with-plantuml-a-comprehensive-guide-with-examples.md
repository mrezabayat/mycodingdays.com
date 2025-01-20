---
title: "UML Modeling with PlantUML: A Comprehensive Guide with Examples"
date: 2023-02-04
description: "Master UML for effective software design with this comprehensive guide. Learn about structure & behavior diagrams, use case, class, state machine, sequence & activity diagrams. Explore real-life examples and discover the power of inheritance, composition, polymorphism and more. Enhance your software design process with UML."
tags: ["UML", "Software Design", "Structure Diagrams", "Behavior Diagrams", "Use Case Diagrams", "Class Diagrams", "State Machine Diagrams", "Sequence Diagrams", "Activity Diagrams", "Inheritance", "Composition", "Polymorphism"]
categories: ["Design and Architecture"]
author: mrbayat
media_subpath:  /assets/img/posts/004
image:
    path: banner.png
---

[UML (Unified Modeling Language)](https://en.wikipedia.org/wiki/Unified_Modeling_Language) is a standardized modeling language that is widely used to visualize, document and communicate the architecture, design and artifacts of a software system. It provides a graphical representation of the system’s structure, behavior, and components. The language enables software engineers to communicate complex designs and concepts to stakeholders who may not have a technical background.

UML is a widely adopted modeling language that is supported by several tools and platforms. One of these tools is [PlantUML](https://plantuml.com/), which is an open-source tool that allows you to create UML diagrams using a simple text-based language. With PlantUML, you can generate diagrams for a wide range of UML diagrams, including class diagrams, sequence diagrams, activity diagrams, use case diagrams, and state diagrams, among others.

## PlantUML in Visual Studio Code

To get started with PlantUML in [Visual Studio Code](https://code.visualstudio.com/), you first need to install the [PlantUML extension](https://marketplace.visualstudio.com/items?itemName=jebbs.plantuml) in the Visual Studio Code marketplace. To do this, follow these steps:

1. Open Visual Studio Code
2. Click on the Extensions icon in the Activity Bar on the side of the editor
3. Search for "PlantUML" in the extensions marketplace
4. Install the PlantUML extension
5. Restart Visual Studio Code if necessary
6. Once you have installed the PlantUML extension, you are ready to start using PlantUML in Visual Studio Code.

Using PlantUML in Visual Studio Code is straightforward. To create a new PlantUML diagram, simply create a new file with a .puml extension and start writing PlantUML syntax. For example:

```text
@startuml
class Car {
  +String brand
  +String model
  +String color
  +int year
  +int speed
}
@enduml
```

As you type the PlantUML syntax, you will see a live preview of your diagram in the editor (press `Alt` + `D` to start PlantUML preview). You can also use the Preview UML Diagram command to open a live preview in a separate window.

Additionally, the PlantUML extension for Visual Studio Code also provides several other features, such as:

Syntax highlighting for PlantUML syntax
Auto-completion for PlantUML syntax
Ability to generate UML diagrams as PNG, SVG, or ASCII art files
Ability to render PlantUML diagrams from .puml files in Markdown previews
These features make it easier to use PlantUML in Visual Studio Code, and they can help you create UML diagrams more quickly and efficiently.

## Class diagram

A Class Diagram in Unified Modeling Language (UML) is a type of static structure diagram that provides a graphical representation of a system's classes, interfaces, objects, and their relationships to each other. It is a fundamental modeling tool used to describe the structure of an object-oriented system, including the objects, attributes, and operations that the system comprises.

A class is a blueprint or a template for creating objects, and in UML, a class is represented as a rectangle with three sections: the top section for the class name, the middle section for the class attributes, and the bottom section for the class operations. In UML, classes can be connected through various relationships, including inheritance, association, aggregation, and composition.

Inheritance is a relationship between two classes, where one class is a subclass of another, and the subclass inherits all the attributes and operations of the superclass. This relationship is indicated by an arrow pointing from the subclass to the superclass, with an open triangle at the arrowhead.

Association is a relationship between two classes, where one class uses the services of another class. This relationship is indicated by a line connecting the two classes, with an optional arrowhead indicating the direction of navigation. The association can be further classified into unidirectional and bidirectional, depending on the direction of navigation.

Aggregation is a relationship between two classes, where one class is a whole and the other is a part. This relationship is indicated by a diamond shape at the end of the line connecting the two classes, near the whole class.

Composition is a relationship between two classes, where one class is the owner of the other class and has a strong ownership relationship. This relationship is similar to aggregation, but with a filled diamond shape, indicating that the part class cannot exist without the whole class.

In addition to the relationships between classes, class diagrams can also show the visibility of attributes and operations, indicated by symbols such as + for public, - for private, and # for protected.

Class diagrams provide a clear and concise representation of the structure of an object-oriented system, and are used to communicate the system design to stakeholders, validate design decisions, and identify any potential design problems. They are an essential tool for any software development process and play a crucial role in the modeling and analysis of object-oriented systems.

Here is an example of a class diagram in PlantUML:

```text
@startuml Class Diagram Example
class Animal {
  int id
  String name

  +int getId()
  +String getName()
  +void makeSound()
}

class Dog extends Animal {
  String breed

  +String getBreed()
  +void makeSound()
}

class Cat extends Animal {
  String furColor

  +String getFurColor()
  +void makeSound()
}

class Owner {
  int id
  String name
  List<Animal> pets

  +int getId()
  +String getName()
  +List<Animal> getPets()
  +void addPet(Animal pet)
}

Animal "1" *-- "0..*" Owner : has
Owner "1" o-- "0..*" Animal : owns
@enduml
```

Rendering the above code with PlantUML produces the below diagram

<p>
  <img src="class-diagram.svg" alt="an example of a class diagram in PlantUML">
</p>

In this diagram, the inheritance relationship between `Animal`, `Dog`, and `Cat` is shown by the arrow pointing from `Dog` and `Cat` to `Animal`. The composition relationship between `Owner` and `Animal` is shown by the diamond shape on the side of the `Owner` class, indicating that `Animal` objects are composed within `Owner` objects.

## Sequence Diagram

A Sequence Diagram in Unified Modeling Language (UML) is a type of interaction diagram that shows how objects or components interact with each other in a sequential manner, over time. It is a valuable tool for modeling the behavior of an object-oriented system and provides a graphical representation of the interactions between objects or components, along with the sequence in which these interactions occur.

In a sequence diagram, objects or components are represented as vertical lifelines, and interactions between these objects are represented as horizontal arrows that connect the lifelines. Each interaction is represented by a message, which is an arrow pointing from the sender object to the receiver object, with the name of the message written above the arrow.

A sequence diagram models the interactions between objects or components in a specific scenario, and can show the flow of messages between objects, including the order and timing of these messages. It can also show the flow of control between objects, such as decisions, loops, and branches.

Sequence diagrams are useful for modeling the dynamic behavior of an object-oriented system, and can help to identify any potential issues with the system's design, such as communication problems or synchronization issues. They are also used to validate design decisions and to communicate the system behavior to stakeholders.

Sequence diagrams can also show the creation of objects and the destruction of objects, represented as messages with the keyword `new` or `delete`, respectively. In addition, they can show the activation and deactivation of objects, represented as rectangular boxes around the interactions with the object.

Overall, sequence diagrams provide a clear and concise representation of the interactions between objects or components in a system, and play an important role in the modeling and analysis of object-oriented systems. They are a valuable tool for understanding the behavior of a system and for identifying potential design issues early in the software development process.

The following is an example of a simple sequence diagram in PlantUML:

```text

@startuml Sequence Diagram Example
hide footbox
participant User
participant CustomerService
participant OrderService
participant PaymentService
participant InventoryService

User -> CustomerService : Request customer information
CustomerService -> User : Send customer information
User -> OrderService : Request to place order
OrderService -> PaymentService : Request payment
PaymentService -> User : Request payment information
User -> PaymentService : Provide payment information
PaymentService -> OrderService : Confirm payment
OrderService -> InventoryService : Request inventory check
InventoryService -> OrderService : Confirm inventory availability
OrderService -> User : Confirm order placement
@enduml
```

Rendering the above code with PlantUML gives us the below diagram

<p>
  <img src="Sequence-Diagram.svg" alt="an example of a simple sequence diagram in PlantUML">
</p>

## Activity Diagram

An Activity Diagram in Unified Modeling Language (UML) is a type of flowchart that displays the steps of a process or a workflow, including the order and flow of activities, as well as the decisions that must be made along the way. The activity diagram is used to model the behavior of a system, by showing the flow of control from one activity to another, and the decisions that control that flow.

Activity diagrams are particularly useful for modeling the flow of control in a business process, a software development process, or any other process that involves multiple steps and decisions. They are also used to represent the flow of control in a use case, and can help to model the flow of control within an individual object.

In an activity diagram, activities are represented as rounded rectangles, and arrows are used to show the flow of control between activities. Activities can also be connected by decision nodes, which represent decisions that must be made in order to determine which path the flow of control should take.

Activity diagrams can also show the flow of control in a parallel or concurrent manner, by using swim lanes. Swim lanes are horizontal divisions within an activity diagram that show the flow of control between objects or components in parallel.

Activity diagrams can also show the creation and destruction of objects, represented by messages with the keywords `new` or `delete`. In addition, they can show the activation and deactivation of objects, represented by a rectangular box around the activities related to the object.

Another important aspect of activity diagrams is the use of action states, which represent a single, atomic step in the process. Action states are represented as a square with a black circle inside, and can also have an associated action that is performed during that state.

Overall, activity diagrams provide a clear and concise representation of the flow of control in a process or a workflow, and play an important role in the modeling and analysis of systems and processes. They are widely used in software development, business process modeling, and other fields, and are a valuable tool for understanding the behavior of a system and for identifying potential problems early in the development process.

```text
@startuml Activity diagram example

title "Online Shopping Process"

start
:Customer Login;
:View Products;
:Add to Cart;
:Checkout;
note right
This is an example of a note.
end note
:Payment;
:Order Confirmation;
stop

@enduml
```

Let's compile this with PlantUML,

<p>
  <img src="activity-diagram.svg" alt="an example of activity diagram generated by PlantUML">
</p>

This activity diagram models the flow of control in an online shopping process. The process starts with the customer logging into the system, and continues with the customer viewing the products, adding items to the cart, checking out, and making the payment. The process ends with the order confirmation.

The diagram also includes decision points, represented by diamond shapes, where the flow of control can take different paths depending on the outcome of a decision. For example, if the customer enters the wrong login credentials, they will be taken back to the customer login step. If the payment fails, the customer will be taken back to the payment step to try again.

This activity diagram provides a clear and concise representation of the flow of control in the online shopping process, and can be used to identify potential problems or inefficiencies in the process. By modeling the flow of control in this way, it's possible to understand the behavior of the system and make improvements to optimize the process.

## Use case diagram

A use case diagram in Unified Modeling Language (UML) is a visual representation of the relationships between actors and the actions they perform in a system. It provides a high-level view of the system's functionalities and the requirements that it must fulfill to achieve its goals.

A use case diagram is used to model the interactions between a system and its external actors, such as users or other systems. It helps to identify the functionalities that the system must provide and the actors who are involved in the system.

In a use case diagram, the system is represented by a rectangle, while the actors are represented by stick figures. The interactions between the actors and the system are represented by arrows connecting the actors to the use cases they interact with.

Each use case represents a specific functionality of the system, such as creating an account, making a purchase, or updating personal information. The use case is written in natural language, making it easy for stakeholders to understand and communicate the system's requirements.

The use case diagram is an important tool for requirements gathering and analysis, as it provides a clear and concise representation of the system's functionalities and the actors involved. This information can then be used to design the system and to create test cases to validate the requirements.

Another important aspect of use case diagrams is their ability to model scenarios and alternative paths through the system. This allows for a more comprehensive view of the system, including edge cases and error handling.

The use case diagram is an essential tool for software development, as it provides a clear understanding of the system's requirements and the interactions between the actors and the system. This results in more efficient development and reduced risks, as the requirements are clear and understood by all stakeholders.

Use case diagrams are particularly useful in Agile development methodologies, as they provide a high-level view of the system's requirements and can be easily updated as the requirements change during the development process.

In summary, a use case diagram in UML is a powerful tool for modeling the functionalities of a system and the interactions between the actors and the system. It provides a clear and concise representation of the system's requirements, allowing for more efficient development and reduced risks.

```text
@startuml Use Case Diagram Example - Online Shopping System

package CustomerActions {
  actor Customer
  usecase Login
  usecase ViewProducts
  usecase AddToCart
  usecase Checkout
  usecase TrackOrder
  usecase LeaveFeedback
}

package AdminActions {
  actor Admin
  usecase AdminLogin
  usecase ManageProducts
  usecase ManageOrders
  usecase ManageCustomerFeedback
}

Customer --> Login
Customer --> ViewProducts
Customer --> AddToCart
Customer --> Checkout
Customer --> TrackOrder
Customer --> LeaveFeedback

Admin --> AdminLogin
Admin --> ManageProducts
Admin --> ManageOrders
Admin --> ManageCustomerFeedback


' This is a hack to make diagrams vertically aligned.
Login -[hidden]-> AdminActions

@enduml
```

Here is the diagram generated by PlantUML:

<p>
  <img src="use-case.svg" alt="an example of use case diagram generated by PlantUML>
</p>

In this example, the use case diagram models the interactions between two actors in the online shopping system: the customer and the admin. The customer can perform actions such as login, view products, add items to their cart, checkout, track their order, and leave feedback. The admin, on the other hand, can perform actions such as login, manage products, manage orders, and manage customer feedback.

This use case diagram provides a high-level view of the system's functionalities and the actors involved, making it easier to understand the system's requirements and design the system accordingly.

## State Diagram

A state diagram, also known as a state machine diagram or statechart, is a type of behavioral diagram in the Unified Modeling Language (UML) that describes the behavior of an object or a system over time. It models the dynamic behavior of a system by representing the different states that an object can be in, the events that trigger transitions between those states, and the actions that are performed as a result of these transitions.

State diagrams are widely used in software engineering and other fields to model the behavior of real-world systems, such as computer programs, electronic devices, and business processes. They are particularly useful for modeling the behavior of systems with multiple states and complex interactions, as they provide a clear and concise representation of the system's behavior.

A state diagram consists of states, transitions, events, and actions. States represent the different conditions or phases that an object can be in, and transitions represent the changes that occur as the object moves from one state to another in response to events. Events are external stimuli that trigger a transition, and actions are the operations that are performed as a result of a transition.

An example of a state diagram using PlantUML can be shown as follows:

```text
@startuml Order state diagram

state Order {
  [*] --> NewOrder
  NewOrder --> PaymentVerification : Payment Verification
  PaymentVerification --> Approved : Payment Approved
  PaymentVerification --> Declined : Payment Declined
  Approved --> AvailabilityCheck : Item Availability Check
  AvailabilityCheck --> InStock : Item In Stock
  AvailabilityCheck --> OutOfStock : Item Out of Stock
  InStock --> ShippingAddressVerification : Shipping Address Verification
  ShippingAddressVerification --> Verified : Address Verified
  ShippingAddressVerification --> AddressDeclined : Address Declined
  Verified --> ConfirmOrder : Order Confirmation
  ConfirmOrder --> Shipped : Order Shipped
  AddressDeclined --> CancelOrder : Order Cancelled
  OutOfStock --> CancelOrder :Order Cancelled
  Declined --> CancelOrder : Order Cancelled
  CancelOrder --> [*] : Canceled
  Shipped --> [*] : Shipped
}

@enduml
```

Compiling the above code with PlantUML generates the below diagram:

<p>
  <img src="state-diagram.svg" alt="an example of state diagram generated by PlantUML">
</p>

In this example, the state diagram models the lifecycle of an order. The order starts in the "NewOrder" state and goes through several states such as "PaymentVerification", "Approved", "AvailabilityCheck", "ShippingAddressVerification", "Verified", "ConfirmOrder", and "Shipped". Depending on various conditions, the order may also go to states such as "Declined", "OutOfStock", "AddressDeclined", or "CancelOrder". The use of arrows and square brackets show the transitions between states and the conditions that trigger those transitions. The asterisks denote the start and end states of the diagram.

## Conclusion

In conclusion, the Unified Modeling Language (UML) is a powerful tool for modeling and communicating software designs. The various diagrams within UML such as structure diagrams, behavior diagrams, use case diagrams, class diagrams, state machine diagrams, sequence diagrams, and activity diagrams, provide a comprehensive way to model different aspects of software systems. PlantUML is a popular open-source tool that provides an easy-to-use syntax for creating UML diagrams.

In this article, we have covered some of these diagrams briefly, and provided practical examples of each of them using PlantUML. By understanding UML and PlantUML, software developers can communicate their designs effectively, leading to better collaboration and more efficient development processes. Whether you are a beginner or an experienced developer, we hope that this article has been informative and helpful in your understanding of UML and PlantUML.
