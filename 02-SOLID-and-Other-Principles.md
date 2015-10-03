# SOLID and Other Principles
## Table of Contents
* SOLID Principles
  * SRP – Single Responsibility Principle
  * OCP – Open/Closed Principle
  * LSP – Liskov Substitution Principle
  * ISP – Interface Segregation Principle
  * DIP – Dependency Inversion Principle
* Other Principles
  * DRY – Don't Repeat Yourself
  * YAGNI – You Aren't Gonna Need It
  * KISS – Keep It Simple, Stupid


## Single Responsibility Principle
* The Single Responsibility Principle states that every object should have a single responsibility, and that responsibility should be entirely encapsulated by the class.
* Cohesion
  * Relation of responsibilities
  * Focused on one task
* Coupling
  * Dependency on other modules
  * Relationship between modules
* Ideal - low coupling / strong cohesion
* Responsibilities
* "A reason to change"
  * Mapped to project requirements
  * More requirements – more possible changes
  * More responsibilities – more changes in code
  * Multiple responsibilities in one class – coupling
  * More coupling – more errors on change
* Classic violations
  * Objects that can print/draw themselves
  * Objects that can save/restore themselves
* Classic solution
  * Separate printer
  * Separate saver (or memento)
* Solution
  * Multiple small interfaces (ISP)
  * Many small classes
  * Distinct responsibilities
* Result
  * Flexible design
  * Lower coupling
  * Higher cohesion

## Open/Closed Principle
* The Open / Closed Principle states that software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification.
* Open to Extension 
  * New behavior can be added in the future 
* Closed to Modification 
  * Changes to source or binary code are not required 
* Change behavior without changing code?!
  * Rely on abstractions, not implementations
  * Do not limit the variety of implementations
* In .NET
  * Interfaces
  * Abstract Classes
* In procedural code
  * Use parameters
* Classic violations
  * Each change requires re-testing (possible bugs)
  * Cascading changes through modules
  * Logic depends on conditional statements
* Classic solution
  * New classes (nothing depends on them yet)
  * New classes (no legacy coupling)
* Three approaches to achieve OCP
  * Parameters
    * Pass delegates / callbacks
  * Inheritance / Template Method pattern
    * Child types override behavior of a base class
  * Composition / Strategy pattern
    * Client code depends on abstraction
    * "Plug in" model
* When to apply OCP?
  * Experience tell you
  * "Fool me once, shame on you" 
    * Don't apply OCP at first
    * If module changes once, accept it
    * If it changes a second time, refactor for OCP
* OCP add complexity to design
* No design can be closed against all changes

## Liskov Substitution Principle
* The Liskov Substitution Principle states that Subtypes must be substitutable for their base types.
* Substitutability – child classes must not
  * Remove base class behavior
  * Violate base class invariants
* The problem
  * Polymorphism break
  * Client code expectations
  * "Fixing" by adding if-then – nightmare (OCP)
* Classic violations
  * Type checking for different methods
  * Not implemented overridden methods
  * Virtual methods in constructor
* Solutions
  * "Tell, Don't Ask"
    * Don’t ask for types
    * Tell the object what to do
  * Refactoring to base class
    * Common functionality
    * Introduce third class

## Interface Segregation Principle
* The Interface Segregation Principle states that Clients should not be forced to depend on methods they do not use.
* Interface is:
  * The interface type
  * All public members of a class
* Having "fat" interfaces leads to:
  * Classes having methods they do not need
  * Increasing coupling
  * Reduced flexibility
  * Reduced maintainability
* Classic violations
  * Unimplemented methods (also in LSP)
  * Use of only small portion of a class
* When to fix?
  * Once there is pain! Do not fix, if is not broken!
  * If the "fat" interface is yours, separate it to smaller ones
  * If the "fat" interface is not yours, use "Adapter" pattern
* Solutions
  * Small interfaces
  * Cohesive interfaces
  * Focused interfaces
  * Let the client define interfaces
  * Package interfaces with their implementation

## Dependency Inversion Principle
* High-level modules should not depend on low-level modules. Both should depend on abstractions.
* Abstractions should not depend on details. Details should depend on abstractions.
* How it should be
  * Classes should declare what they need
  * Constructors should require dependencies
  * Hidden dependencies should be shown
  * Dependencies should be abstractions
* How to do it
  * Dependency Injection
  * The Hollywood principle "Don't call us, we'll call you!"
* Inversion of Control container (IoC)
  * Responsible for object instantiation
  * Initiated at application start-up
  * Interfaces are registered into the container
  * Dependencies on interfaces are resolved

## Other Principles
* Don't Repeat Yourself (DRY)
  * Variations include: 
    * Once and Only Once 
    * Duplication Is Evil (DIE) 
  * Classic violations
    * Magic Strings/Values 
    * Duplicate logic in multiple locations 
    * Repeated if-then logic 
    * Conditionals instead of polymorphism 
    * Repeated Execution Patterns 
    * Lots of duplicate, probably copy-pasted, code 
    * Only manual tests 
    * Static methods everywhere 
* You Ain't Gonna Need It (YAGNI)
  * Time for adding, testing, improving
  * Debugging, documented, supported
  * Difficult for requirements
  * Larger and complicate software
  * May lead to adding even more features
  * May be not know to clients
* Keep It Simple, Stupid (KISS)

## Domain Driven Development (DDD)
* A standardization of the best implementations of layered architecture
* Primary focus to Domain layer
* Base complex designs on a model of the domain
* Initiate a creative collaboration between  technical and domain experts to iteratively refine a conceptual model that addresses particular domain problems
* Clean Architecture

![Clean Architecture](https://github.com/huytrongnguyen/aspnet5/blob/master/css/imgs/clean-architecture.jpg)

* Onion Architecture

![Onion Architecture](https://github.com/huytrongnguyen/aspnet5/blob/master/css/imgs/onion-architecture.jpg)

* We used BDD (Behavior Driven Development) as a collaboration tool
  * Feature: ATM cash withdrawal
    * **As** a bank customer
    * **I want** to withdraw cash from an ATM
    * **So** that I can get money off-hours
  * Scenario: Enough money in the account
    * **Given** the customer has $100 in her account
    * **When** she withdraws $60 through the ATM
    * **Then** she has $40 in her account
    * **And** the ATM dispenses $60
    * **And** the ATM prints a receipt
