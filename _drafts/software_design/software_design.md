---
layout: post
title: "Software Design"
category: jekyll update
---

- See what Wikipedia says about Software design 
- There is an ACM/IEEE Software Engineering Curriculum Guideline [check here](https://www.acm.org/education/curricula-recommendations) 
- A handnote from linkedIn

Software Design →  looks at lower-level aspects
Software Architecture →  looks at higher-level aspects

## Object Oriented Design
### Object Oriented Modeling

Design a Software: Requirements (user stories) > Conceptual design (mockups) > Technical design (diagrams)

#### Conceptual design
- Components → Responsibility
- Components → Connections ← Components

#### Technical Design
Breaking Components to lower level and determine responsibility specification. For technical design components can be broken into class, function etc.

#### Quality Trade-offs
Which quality too focus on ← Context
- Functional (purpose) 
- Non-functional Requirements (Security, Convenience, Performance Re-usability, Flexibility, Maintainability etc.)

#### Class Responsibility Collaborator (CRC)
For Conceptual design

|Class Name|
|:--------:|
|Responsibility|Collaborator|

### Creating Models
#### Design Principles
- Abstraction ← Rule of Least Astonishment. (omit the details Attributes & Behaviors and keep specifics regarding context perspective)
- Encapsulation ← Bundle data, functions that manipulate data, and self-contained objects. Restrict access to some Attribute & Method and thus provide data integrity. Black Box thinking. Achieve Abstraction Barrier. 
- Decomposition ← Dividing a Components into Parts with separate Responsibilities. Fixed and Dynamic parts. Problem is lifetime of Whole object and Part object. Sharing Parts between Components is possible.
- Generalization (Inheritance, Polymorphism) ← Generalizing the common parts. Implements DRY.

#### Technical Diagram (UML)

|Class Name|
|----------|
|Properties<br>`<-/+/#> <variable name>:<variable types`>|
|Operations<br>`<-/+/#> <name> (<parameter list>): <return type>`|

- Encapsulation: Getter & Setter.
- Decomposition: Association (loose partnership between objects. Example - Cat:Ball; Lines), Aggregation (weak has-a relationship - Whole object has parts that belong to it but parts. can exist independently. Example - PetStore:Pets; Empty Diamond), Composition (strong has-a relationship - Whole cannot exist without its Parts and vice versa. Example - Human:Brain; Filled Diamond)
- Inheritance: extends Implementation (SuperClass can have multiple SubClass but SubClass can only have one SuperClass) Multiple (SubClass can have multiple SuperClass, Java do not have this but C++ does) Arrow.
- Interfaces: implements Can be used to implement polymorphism. Interface can have multiple inheritance Dotted Arrow.

|<< interface >><br>Interface Name|
|---------------------------------|
||
|...|

#### Design Principles
- Measuring Design Complexity: (A Module (class or method) should not have complexity level greater than 7). 
- Loose Coupling ←  Needs to be Loosely Coupled rather than Strongly Coupled. The degree should be small. Ease and Flexibility to connect one module to other module.
- High Cohesion ← One Responsibility
- Separation of Concern ← Abstract an idea and Encapsulate it then Decompose and Generalize 
- Information Hiding ← Encapsulation. Access Modifier (Public, Private, Protected, and Default)
- Conceptual Integrity ← Communication, Code Review

##### Generalization Principle
Inheritance Issues ← If SubClass is not adding anything additional to SuperClass then inheritance is misused. Breaking Liskov’s Substitution Principle.

##### Modeling Behavior
UML Sequence Diagram: Box (Object), lifeline (time), arrows (message), rectangle (active time)

UML State Diagram: Illustrate single object as it behaves in response to series of events. The state of an Object defined by values of its Attributes. State name, State variable, and State Activity (Entry, Exit, and Do) can describe a State. Transition take Object from one state to another. Transition can be described by Event, Condition, and Action. Filled circle (start), rounded rectangle (State), arrows (Transition), circle with filled circle (termination)

##### Model Checking
3 Phases → Modelling phase, Running phase, Analysis phase

### Design Patterns
- 23 patterns → “Design Pattern: Elements of Reusable Object-Oriented Software”
- Pattern Language ← Creational Pattern, Structural Pattern, Behavioral Pattern

#### Creational Pattern
- Singleton Pattern: Only one Object of a Class. The Object is generally globally available. Lazy creation ← the object is not created until it is needed. But it has drawback in case of concurrent running process trying to access it simultaneously.

{% highlight Java %}
class Singleton {
  Singleton* uniqueInstance = NULL;
  Singleton () {
      printf("Private Constructor\n");
  };
  
  public:
    Singleton* getInstance (){
      if (uniqueInstance == NULL){
        uniqueInstance = new Singleton;
      }
      return uniqueInstance;
    }
};
{% endhighlight %}

- Factory Object Pattern: Factory type Classes that instantiate object of a Class that has different SubClasses. It helps when multiple client tries to create the instance of the same set of Classes (SubClasses). It’s base is on Concrete Implementation. Factory Method Pattern is related pattern that separates out the Object creation part and uses Coding to an Interface not to Implementation.

#### Structural Pattern

- Facade pattern: Facade Class is a wrapper Class that hides the subsystem complexity by encapsulating it ← act as entry point.
- Adapter Pattern: Adapter Class use an target interface to make two incompatible subsystem talk to each other. It wraps the adaptee by converting the request from the client to a format that the adaptee can understand.
- Composite Pattern: The Composite design pattern use to solve the problem of building a tree like structure with Objects and treating each object in the tree structure uniformly. It uses Polymorphism by Interface (or, abstract SuperClass) and Recursive Composition to make Component to be composed of other Components.
- Proxy Pattern: Proxy Subject Class wraps the Real Subject Class to provide lightweight version of resource-intensive Real Subject Object, to provide a secured layer in front of the Real Subject Class, or providing a local representation in place of a remote Real Subject Object.
- Decorator Pattern: Adding behavior to an Object at run-time using Aggregation instead of pure Inheritance.

#### Behavioral Pattern
- Template Method Pattern: 
- Chain of Responsibility Pattern:
- State Pattern: 
- Command Pattern:
- Mediator Pattern:
- Observer Patter:

#### MVC Pattern

#### Design Principles underlying Design Pattern
- L Liskov’s Substitution Principle 
- O Open/Closed Principle: Class should be close to be edited after development but open to extension. Open ← Inheritance or Abstract/Polymorphism
- D Dependency Inversion Principle: High level Modules should depend upon high level resources (Abstract or Interfaces).
- Composing Object Principle: Use Aggregation rather than Inheritance to achieve loose coupling. Composite or Decorator Design pattern use this principle.
- I Interface Segregation Principle:
- Principle of Least Knowledge: Law of Demeter.

#### Code Smells
- Refactoring: Improving the Design of Existing Code
- Comment
- Duplicated Code
- Long Method
- Large Class
- Data Class
- Data Clamps
- Long Parameter List
- Divergent Change
- Shotgun Surgery
- Feature Envy
- Inappropriate Intimacy
- Message Chain
- Primitive Obsession 
- Switch Statement
- Speculative Generality 
- Refuse Bequest 

### Design Diagrams
- Data Flow Diagram (DFD)
 - (ERD)
 - (HLD)
 - (DLD)
