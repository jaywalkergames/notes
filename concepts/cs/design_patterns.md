1. Automated setup
2. Portability among execution environments
3. Deploy to cloud
4. CI/CD
5. Production looks like Development and Staging
6. Scale up without changes to tooling or design

### Rules
- One codebase tracked with git, many deploys
- Explicitly declare dependencies
- Isolate dependencies
- Store config in environment
- Treat backing services as attached resources
- Separate build and run stages
- Execute app as stateless processes
- Export services via port binding
- Scale concurrency out via process model
- Fast startup
- Graceful shutdown
- Treat logs as event streams
- Run admin/management tasks as one-off processes

# Refactoring
a systematic process of improving code without creating new functionality that can transform a mess into clean code and simple design
- new functionality should not be created during refractoring
### Dirty Code
the result of inexperience multiplied by tight deadlines, mismanagement, and nasty shortcuts taken during the development process
### Clean Code
code that is easy to read, understand and maintain
- obvious what code does
- does not contain duplication
- passes all tests
### Code Smells
indicators of problems that can be addressed during refactoring
- long methods
- large classes
- too many primitives
- long parameter lists
- too much inheritance
- switch statements
- change preventers
- dead code
### Composing Methods
- Group similar code fragments together
- Call a function instead of using a temp variable
- 
### Moving Features Between Objects
- a method should be used most within its own class
- a field should be used most within its own class
- a class should have a single responsibility
- a class should not delegate to other objects within its methods
- 
### Organizing Data
X
### Simplifying Conditionals
X
### Simplifying Method Calls
X
### Dealing with Generalizations
X

# Design Patterns
## Creational
Object creation mechanisms that increase flexibility and reuse of existing code
### Factory Method
Interface for creating objects in a superclass
Allows subclasses to alter the type of objects that will be created
- replace direct object construction calls to a factory method (object returned are called products)
- Use the Factory Method when you don’t know beforehand the exact types and dependencies of the objects your code should work with.
### Singleton
Create a private constructor and a method that calls the constructor.
Call the method but only call the constructor within it if a new object is needed
## Structural
How to assemble objects and classes into larger structures, while keeping these structures flexible and efficient
## Behavioral
Assignment of responsibility between objects
