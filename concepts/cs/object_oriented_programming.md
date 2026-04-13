# Object-Oriented Programming

### The Four Pillars of OOP

**Abstraction**

Hide internal implementation details and expose only the needed functionality for each object.

**Encapsulation**

Objects keep state private. Other objects can only access the object’s public members.

**Inheritance**

Classes can reuse functionality of other classes.

**Polymorphism**

Classes that inherit functionality from other classes can change that functionality.

### SOLID Principles

Single Responsibility Principle: each module should do one thing really well

Open-Closed Principle: objects should be open for extension but closed for modification

Liskov Substitution Principle: every subclass or derived class should be substitutable for their base or parent class

Interface Segregation Principle: a client should never be forced to implement an interface that it doesn’t use

Dependency Inversion Principle: entities must depend on abstractions, not on concretions

### Modularity

Cohesion:

Coupling:

Connotation: ?

# Functional Programming

### X

Y

### X

Y

# Deployment

### Monolith

X

### Microservices

X

### Serverless

X

# Workflow

### JIRA

X

### Artifactory

X

# Security

### Secure Development

1. Design with security in mind
    1. Define security requirements
    2. Consider data protections
    3. Generate test cases
    4. Keep designs simple
2. Parameterize Queries
    1. Specify placeholders for parameters
    2. Use ORMs
3. Protect Data
    1. UNIX commands, JS hex encoding, HTML entity encoding
    2. Monitor how JS and HTML populate user input
    3. Encrypt stored data and data in transit (use crypto libs)
    4. Don't make sensitive data accessible in memory or temp storage
    5. Use transport security layer (TLS) to encrypt data in transit
4. Validate Inputs
    1. Confirm data is correct type
    2. Confirm data is correct range
    3. Only validate on the server side
5. Implement Auth
    1. Confirm user IDs
    2. Multifactor auth
    3. Timeouts
    4. Monitor suspicious IP addresses and machine IDs
    5. Implement access controls (default permission is deny)
6. Implement Logging and Intrusion Detections
    1. Keep audit and transaction logs separate
    2. Log timestamp, source IP, user ID
    3. Don't log opt-out data, session IDs, or hash value of passwords
    4. Disable logging for production mobile applications
7. Use existing frameworks when available
    1. Keep libraries and build tools up to date
    2. Build in extra security controls as needed
8. Handle All Errors
    1. Verify all unexpected behavior is correctly handled
    2. Confirm error messages sent to users do not contain sensitive data
    3. Use pen testing, fuzzing, fault injection
9. Static Code Analysis
    1. Identify memory leaks, access violations, arithmetic errors, array overruns
    2. Compile code with highest warnings

# Design Patterns

X

# Application Design

### Reliability

Tolerating hardware & software faults

Human error

### Scalability

Measuring load & performance

Latency percentiles & throughput

What operation are performed the most often

What operations take the most time

### Maintainability

Operability

Simplicity

Evolvability

- make reversible technology decisions

Loose Coupling:

- separate systems based on hardware capabilities (elasticity)
- only allow communication between systems through services
- each component is released separately
- internal changes of a component do not effect other components

### Security

On-premise requirements

Networking, VPC

### Cost

Time to develop

Money

# Data Encoding

### Format

JSON: schemaless, slow serialization, universal, web support

Protobuf: schema, compact, universal

- keep a database of schema changes allows for compatibility
- type checking at compile time for statically typed programming languages

### Dataflow

The process that writes to the database encodes the data

The process that reads from the database decodes the data

REST (JSON):

gRPC (Protobuf):

Message Broker: buffer, guaranteed delivery, IP security, decouples sender and recipient

# Legal

[Legal](https://www.notion.so/Legal-cac156f76ab145dd834e716bb2bf686c?pvs=21)
