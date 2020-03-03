# NestJs

## entities
- controller
- module
- main

## routing
- not managed centrally (unlike angular)
- determined in the controllers

## controller
- handle http requests and delegate complex tasks to providers
- registered in module controllers
- DTO: data transfer object
  - define data received at server side
- features
  - auto serialize returned JSON object
  - auto resolve async return value

## provider
- a class with @Injectable decorator
- registered in module provider
- has module scope
- examples
  - services
  - repositories
  - factories
  - helpers
- inject dependency
  - to make wiring up entity relationships can be handled by framework runtime
  - constructor-based injection
  - property-based injection

## services
- responsible for data storage & retrieval

## module
- class annotated with @module decorator
- singleton by default
- types of modules
  - application module
  - feature modules
  - shared module
  - dynamic module
- configurable properties
  - providers
    - providers to be instantiated by nest, and shared across the module
  - controllers
  - imports
    - modules that exports providers required in this module
  - exports
    - providers should be available to other modules that import this module

## Aspect oriented programming
- solve cross-cutting concerns
- related features
  - middlewares
  - interceptors (beforem stream manipulation)
  - guards
  - interceptors (after stream manipulation)
  - exception filters


## middleware
- functions called before route handlers
- a function implementing NestMiddleware interface
- have access to request and response objects
- features of middlewares
  - execute any code
  - change req, res
  - end req, res cycle
  - call next() to pass control if not ending req, res cycle
- functional middleware
  - a function and requires no dependency

## exception filters
- extends HttpException
- default global exception filter will catch all HttpException

## pipe
- two use cases
  - transformation: input => output
  - validation: throw exception if invalid
- operate on arguments processed by controller route handler
- no controller method is executed if exception is thrown
- built-in pipes
  - ValidationPipe
  - ParseIntPipe
  - ParseUUIDPipe

## guard
- determines if a given request should be handled by the route handler
  - depending on permission, roles, ACLs, etc.
- implement CanActivate interface
- executed after each middleware, before interceptor or pipe
- guard vs middleware
  - middleware suitable for authentication
  - guard more suitable for authorization, as it's aware of what will be executed next

## interceptors
- implement NestInterceptor interface
- bind extra login before/after function execution
  - transform returned ressult
  - transform exception thrown

## oop
- patterns
  - IOC: inversion of control
  - SOC: 
- decoupling
  - inversion of control
	
## DTO
- exist between network transfer boundaries
- should not contain business logic
- internal consistency check
- basic validation

## ORM
- data access layer (like dao layer in Java)
- transaction (事物)
  - should be ACID: atomic, consistent, isolation, durability
    - atomic: transaction cannot be divded futher, execute all or nothing
    - consistent: tranform db from one consistent state to another consistent state
    - isolated: conccurent transactions cannot affect each other
    - durable: onece effective, effect is permanent

## CLI
- project init
  - nest new project_name
- file generators
  - nest g controller courses
  - nest g service courses


## authentication vs authorization
- authentication
  - decides if user is what he claims to be
  - method
    - login form
    - HTTP authentication
    - http digest
    - x.509 certificates
- authorization
  - decides if user allows to do something
  - method
    - access controls for URLs
    - secure objects and methods
    - access control lists (ACLs)

## authentication using passport
- steps
  - authenticate user by verifying password, jwt
  - manage authenticated state
    - issue a JWT token
    - or create express session
  - attach authenticated user info to Request object for use in route handlers
- not logged in user
  - restrict protected routes
  - trigger local passport strategy on auth/login route
- logged in user
  - restrict protected routes
