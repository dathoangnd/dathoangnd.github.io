---
layout: post
title:  "Design principles & Design patterns Cheatsheet"
---
This cheatsheet is archived for myself, and it is not easy to read. You can always find a better cheatsheet on Google.
## 1. Design principles
### 1.1. Single responsibility
Each class should be responsible for only one thing to change.
<img class="post-image" class="post-image" src="{{ '/assets/img/single-responsibility.png' | prepend: site.baseurl }}" />

### 1.2. Open / Closed
A class should be open for extension but closed for modification.
<img class="post-image" src="{{ '/assets/img/open-closed.png' | prepend: site.baseurl }}" />

### 1.3. Liskov substitution
When inheriting a class, ensure that the subclass can be used in place of the superclass without altering the logic of the code.
<img class="post-image" src="{{ '/assets/img/liskov-substitution.png' | prepend: site.baseurl }}" />

### 1.4. Interface segregation
A subclass should not be forced to implement methods of an interface that it does not use.
<img class="post-image" src="{{ '/assets/img/interface-segregation.png' | prepend: site.baseurl }}" />

### 1.5. Dependency inversion
High-level classes should not depend on low-level classes; both should depend on abstractions.
<img class="post-image" src="{{ '/assets/img/dependency-inversion.png' | prepend: site.baseurl }}" />


## 2. Design patterns
### 2.1. Creational patterns
Mnemonic: <b>A</b>braham <b>B</b>ecame <b>F</b>irst <b>P</b>resident of <b>S</b>tate.
#### 2.1.1. Abstract factory
Allows the creation of groups of related objects without specifying their exact class.
<img class="post-image" src="{{ '/assets/img/abstract-factory.png' | prepend: site.baseurl }}" />

#### 2.1.2. Builder
Allows the construction of complex objects step by step.
<img class="post-image" src="{{ '/assets/img/builder.png' | prepend: site.baseurl }}" />

#### 2.1.3. Factory method
Provides an interface for creating objects from a superclass, but lets subclasses decide which type of object to create.
<img class="post-image" src="{{ '/assets/img/factory-method.png' | prepend: site.baseurl }}" />

#### 2.1.4. Prototype
Allows the creation of objects that are identical to an existing object.
<img class="post-image" src="{{ '/assets/img/prototype.png' | prepend: site.baseurl }}" />

#### 2.1.5. Singleton
Ensures that only one instance of a class exists in the program.
<img class="post-image" src="{{ '/assets/img/singleton.png' | prepend: site.baseurl }}" />

### 2.2. Structural patterns
Mnemonic: <b>ABCDFFP</b>
#### 2.2.1. Adapter
Allows objects with incompatible interfaces to interact with each other.
<img class="post-image" src="{{ '/assets/img/adapter.png' | prepend: site.baseurl }}" />

#### 2.2.2. Bridge
Separates a set of related classes into two hierarchies: abstraction and implementation.
<img class="post-image" src="{{ '/assets/img/bridge.png' | prepend: site.baseurl }}" />

#### 2.2.3. Composite
Helps create a hierarchical structure of objects.
<img class="post-image" src="{{ '/assets/img/composite.png' | prepend: site.baseurl }}" />

#### 2.2.4. Decorator
Allows adding behavior to an object by wrapping it in another object.
<img class="post-image" src="{{ '/assets/img/decorator.png' | prepend: site.baseurl }}" />

#### 2.2.5. Facade
Creates a simple interface for using complex subsystems.
<img class="post-image" src="{{ '/assets/img/facade.png' | prepend: site.baseurl }}" />

#### 2.2.6. Flyweight
Allows the reuse of objects that share part of their state.
<img class="post-image" src="{{ '/assets/img/flyweight.png' | prepend: site.baseurl }}" />

#### 2.2.7. Proxy
Allows performing actions before or after invoking a method on an object.
<img class="post-image" src="{{ '/assets/img/proxy.png' | prepend: site.baseurl }}" />

### 2.3. Behavioral patterns
Mnemonic: <b>2 MICS O</b>n <b>TV</b>
#### 2.3.1. Mediator
Allows objects to communicate with each other through a mediator object.
<img class="post-image" src="{{ '/assets/img/mediator.png' | prepend: site.baseurl }}" />

#### 2.3.2. Memento
Allows saving and restoring the state of an object.
<img class="post-image" src="{{ '/assets/img/memento.png' | prepend: site.baseurl }}" />

#### 2.3.3. Iterator
Allows iterating over a collection of objects in a specific order.
<img class="post-image" src="{{ '/assets/img/iterator.png' | prepend: site.baseurl }}" />

#### 2.3.4. Intepretor
Defines how to interpret the grammar of a language and create objects that can handle that interpretation.
<img class="post-image" src="{{ '/assets/img/intepretor.png' | prepend: site.baseurl }}" />

#### 2.3.5. Chain of responsibility
Allows passing a request through a chain of handler objects.
<img class="post-image" src="{{ '/assets/img/chain-of-responsibility.png' | prepend: site.baseurl }}" />

#### 2.3.6. Command
Allows executing a request without knowing which object will handle it.
<img class="post-image" src="{{ '/assets/img/command.png' | prepend: site.baseurl }}" />

#### 2.3.7. State
Allows an object to change its behavior when its internal state changes, as if it were a different class.
<img class="post-image" src="{{ '/assets/img/state.png' | prepend: site.baseurl }}" />

#### 2.3.8. Strategy
Allows defining a family of algorithms, making them interchangeable within an object.
<img class="post-image" src="{{ '/assets/img/strategy.png' | prepend: site.baseurl }}" />

#### 2.3.9. Observer
Allows a group of objects to monitor changes to a single object and act upon those changes.
<img class="post-image" src="{{ '/assets/img/observer.png' | prepend: site.baseurl }}" />

#### 2.3.10. Template method
Defines the steps of an algorithm in the superclass and allows subclasses to change the behavior of some steps.
<img class="post-image" src="{{ '/assets/img/template-method.png' | prepend: site.baseurl }}" />

#### 2.3.11. Visitor
Separates an algorithm from the objects it operates on, allowing new algorithms to be added without modifying the objects.
<img class="post-image" src="{{ '/assets/img/visitor.png' | prepend: site.baseurl }}" />
