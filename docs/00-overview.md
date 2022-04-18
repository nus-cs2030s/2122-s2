# Unit 0. Overview

## Learning Outcomes

This unit provides an overview of the aims of CS2030/S and how the key concepts covered in CS2030/S are related to one another.

## What is This Module About?

CS2030/S is designed for students who have gone through a basic programming module and have learned about problem solving with simple programming constructs such as loops, conditions, and functions.  In a typical introductory programming module, such as CS1010 or its variants at NUS, students tend to write small programs (in the order of tens or hundreds of lines of code) to solve programming homework problems, working on their code alone before moving on to solve the next set of problems once the homework is done.

The first aim of CS2030/S is to change students' mindsets, teaching them to write software that will continue to evolve as software requirements change, and that will be read and modified by other programmers (including their future selves).

The second aim of CS2030/S is to level up the complexity of the programs that students will write, from hundreds of lines up to thousands of lines.  CS2030/S bridges students between writing "toy" programs to solve specific problems in CS1010 and writing larger real-world software in their later modules, such as CS2103 Software Engineering.

A programming language is the medium through which programmers can express their intentions and construct software, and is thus critical to supporting the aims above.  With the appropriate features and tools, one can tame the complexity of software, make one's written code friendlier for other programmers, and make it easier for the code to evolve.  The third aim of CS2030/S is thus to expand students' minds on different ways one can construct software and the principles behind some programming language constructs.  In particular, CS2030/S focuses on objects, types, and functions, as three key constructs towards building programmer-friendly software.  It covers both object-oriented and functional paradigms as two different approaches to constructing software, with a strong emphasis on type safety.

The final aim of CS2030/S is to introduce students to programming language concepts, to bridge them from introductory programming to advanced modules such as programming language design and implementation.  Part of CS2030/S introduces students to the design decisions behind some programming language constraints, and the workings behind programming language compilation and execution, giving them a glimpse into the programming systems that have mostly been treated as a black box in introductory modules so far.

## The Choice of Java

We decided to use a single programming language throughout this module.  This meant us having to pick a language that was strongly typed with static typing, and that supported both object-oriented and functional programming.  We chose Java for CS2030/S, considering multiple factors -- its popularity, syntax familiarity, and it allowing for smoother transitions to later modules in the NUS computing curriculum.

While Java is definitely not the most elegant programming language for expressing programs in functional style, our hope is for students to be able to learn the principles of functional programming and apply them to other programming languages nonetheless.  This choice was a trade-off to not have to switch languages in the middle of the module.

## What This Module is not About

This is not a module on Java programming.  We will not cover Java's syntax and features comprehensively, except those relevant to the concepts we teach.  In fact, we will avoid and even ban students from using certain Java features (such as `var`) for pedagogical purposes.

This is not a module on software engineering either.  Software engineering is a broad discipline on its own, deserving of a separate module.  Rather, this module is about the programming principles and constructs upon which programmers can design better software.  To highlight the importance of these principles and constructs, and see how they can be used, we will inevitably cover some software engineering design principles, such as Liskov's Substitution Principle (the L in SOLID), Tell-Don't-Ask, and Composition over Inheritance.  However, we will not go over object-oriented design or general software design in detail (e.g., we will not cover S,O,I,D in SOLID).

Lastly, CS2030/S is not a module that focuses on computational efficiency.  We have CS2040/S for that.  In CS2030/S, although reducing computational costs still plays a role, this is not the only cost that matters.  CS2030/S is also concerned with the human cost of debugging or maintaining software.  In striving for simpler software that is easier to maintain and extend, we may have to sacrifice computational efficiency.

## Taming Complexity in Software Development

An underlying theme of CS2030/S is taming complexity in software development.  There are objective metrics with which one can measure the complexity of software, but here, we will loosely define complexity as anything that increases the likelihood of bugs in a program.

Let's start by considering a simplified view of what a software program is.  One can view a software program as a collection of data variables and instructions on how to modify these variables.  A program is generally written to meet a specific requirement: given one or more input variables, the program should perform the computation needed to produce the output variables as per the requirement.  While doing so, the program often stores information in intermediate variables.

Having gone through an introductory programming module such as CS1010 or its variants, you should be familiar with the above scenario, and you should have had some experience writing programs to solve given computational problems.  The programs you have written for such introductory modules are mostly small "toy" programs -- ones consisting of no more than a few hundreds of lines with tens of variables.

Software development in the real world, however, is far more complex than what you would have experienced there.  A software program rarely solves a well-defined computational problem only.  It often requires multiple components, such as a user interface, data storage, and business rules, interacting with each other in an intricate manner to provide a set of functionalities.

As the requirements of software become more complex, the number of variables that need keeping track of increases; the logic of the computations the programmer needs for maintaining the variables becomes more complicated.  Furthermore, the variables are often interdependent.  For instance, updating a variable might require updating another; how a variable should be updated might depend on another variable.  In this way, having more variables increases the number of relationships between them that the programer has to keep track of.  Failure to correctly maintain these variables and their relationships will most likely lead to bugs.

Additionally, real-world software rarely remains static.  This property once again differs from what you would have experienced in an introductory programming module, where instructors rarely go back and change the requirements of programming homework once released.  In the real world, software evolves over time -- new features are added, business rules changes, better algorithms are deployed, etc.  The code gets updated accordingly, with new variables and computations added; the way variables are updated or depend on one another changes.  Updating the code of an already-complex software program to keep up with shifting requirements, if not managed properly, can also result in bugs.

Real-world software is often the product of multiple programmers' teamwork, where the software development process is unlike that of your individual homework in an introductory programming module.  When multiple programmers work together, interdependencies between states need to be communicated and handled both properly and consistently among the programmers.  One programmer's modifications to the code should not introduce bugs into another programmer's code.

Since software evolves over time, this notion of "multiple programmers" actually applies even to software developed by just a lone programmer over time.  Changing one's code should not introduce new bugs to other parts that one wrote some time ago.

## Strategies to Tame Complexity

### Good Software Development Practices

If you were taught well in your introductory programming module, you should already be familiar with some good programming practices that help to tame complexity and reduce the chance of bugs.  These practices include:

* Commenting your code: Doing so provides _in situ_ communication between you and other programmers on the team, as well as between you and your future self, on the non-obvious purposes of certain states and the relationships between them.  Such comments help in enhancing one's understanding of what the code is doing and in reminding one of the appropriateness of planned modifications when requirements change.

* Using a coding convention: Adhering to a coding convention helps improve code readability, reducing cognitive barriers when one programmer reads another programmer's code and allowing the reader to understand the code more easily and thoroughly.

CS2030/S will continue to enforce these good programming practices.

### Functions

You should also have been taught to always break your code down into functions, with each one performing a simple, specific task.  Those functions can then be composed to complete larger and more complex tasks.  Functions are an important programming structure in taming code complexity, allowing programmers to (i) compartmentalize computations and their effects, reducing interactions to a few well-defined ones (through arguments and return values); (ii) hide implementation details so that they can be changed later without affecting other parts of the code; (iii) reuse computations and thus write code that is more succinct and easier to understand/change.

In CS2030/S, not only will you be continuing to break your computations into functions, but we will also be kicking it up several notches.  A major part of CS2030/S is introducing you to more programming paradigms and language tools that will allow you to compartmentalize computations, hide details, and reduce repetition.

### The Abstraction Principle

The last point above about why it is important to code in small, reusable functions, follows what is called the _Abstraction Principle_[^1].  The principle states that:

[^1]: This principle is formulated by Benjamin C. Pierce in his book "Types and Programming Languages."

> "Each significant piece of functionality in a program should be implemented in just one place in the source code. Where similar functions are carried out by distinct pieces of code, it is generally beneficial to combine them into one by abstracting out the varying parts."

This principle is something that we will visit over and over again in CS2030/S, applying it to different sections of programs that have varying parts.  In the case of functions, the "varying parts" are the values on which we wish to perform computations.  We will also apply this principle to (i) types, abstracting them out as parameterized types or subtypes, and (ii) sub-computations, abstracting them out as first-class functions.  Generics, subtypes, and first-class functions are concepts that underlie most of the content of CS2030/S.

### Erecting an Abstraction Barrier

Another important strategy for taming complexity is the _abstraction barrier_.  In the context of writing functions, let's separate the role of a programmer into two: the _implementer_, who implements the function, and the _client_, who calls the function.  The implementer should compartmentalize the internal variables and the implementation of the function, hiding them behind an abstraction barrier, while exposing its parameters and return values as the only communication gateways across the barrier.

This abstraction barrier is another thing that we will refer to repeatedly in CS2030/S.  We will see how to maintain this barrier not only in the context of functions, but also for variables alongside the computations on them, by encapsulating them as _objects_, and hiding details from the client through _access modifiers_.  These ideas form two of the four core principles of _object-oriented programming_: _encapsulation_ and _abstraction_.

### Code for Change

The abstraction barrier, if erected and maintained properly, reduces code complexity.  It, however, also reduces flexibility as software evolves.  If the client wishes to modify a computation protected by an abstraction barrier, they will need the help of the implementer.  In CS2030/S, we will see two ways in which we can modify the computations done behind the abstraction barrier, _without changing the code behind the barrier_.

First, we will introduce the concepts of _inheritance_ and _polymorphism_, the other two core principles of object-oriented programming.  These object-oriented mechanisms allow programmers to easily extend or modify the behavior of existing code.

Second, we will introduce _closures_, abstractions of computations and their environments, that we can pass into the functions behind the abstraction barrier to perform computations.  This idea, if carried to the extreme in terms of flexibility, leads to the concept of _monads_ in the functional programming paradigm.  A monad is a computational structure that allows objects to be composed and manipulated in a succinct and powerful way.

### Types

Allowing a programmer to change the behavior of existing code without changing the code itself could lead to bugs, if not managed properly.  To prevent this, both the programming language system, and the programmers, have to adhere to certain rules when extending or modifying the behavior of existing code.  Java and many other typed languages have _type systems_ -- a set of rules that governs how variables, expressions, and functions interact with one another.  You will be learning about subtyping and the Liskov Substitution Principle, two notions that are important to constraining how inheritance and polymorphism should be used, in order to avoid bugs.

A type system is also an important tool for reducing the complexity of software development.  By constraining the interactions between variables, expressions, and functions, the interdependence possible between these programming constructs is reduced.  Furthermore, any attempts by programmers to break the constraints can be caught automatically.  By utilizing type systems properly, we can detect potential bugs before they manifest themselves.

A reason CS2030/S chooses to use Java is due to its type system.  CS2030/S will introduce the concepts of types, subtypes, compile-time vs. run-time types, variants of types, parameterized types, and type inferences, in the context of Java.  We will see how we can define our own types (using _classes_ and _interfaces_) and the relationships between them, as well as parameterized types and generic functions that take in types as parameters.  These concepts are applicable to many other programming languages.

### Eliminating Side Effects

We have discussed how functions can compartmentalize computations and isolate their complexity within their bodies.  For this approach to be effective, each function must not have any side effects, like updating a variable that is not within the function.  Such functions, called _pure functions_, are one of the key principles of the functional programming paradigm, and are something that we will explore to kick off the section on this paradigm in CS2030/S.

A related idea in object-oriented programming that we will cover in CS2030/S is _immutability_ -- that an object cannot be changed once created.  If we wish to update such an object, we instead need to create a new one.  With immutability and pure functions, we can guarantee that the same function invoked on the same objects will always return the same value.  This certainty can help in understanding and reasoning about the behavior of code.
