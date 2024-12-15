## Handle multilingual data
### Database
Use a Translation Table: 
``` sql
CREATE TABLE translation ( 
id INT AUTO_INCREMENT PRIMARY KEY, 
entity_type VARCHAR(50), -- Type of entity (e.g., 'celebrity', 'event') 
entity_id INT NOT NULL, -- ID of the entity being translated 
language_code VARCHAR(10) NOT NULL, -- Language code (e.g., 'en', 'zh') 
field_name VARCHAR(50), -- Field name being translated (e.g., 'name', 'description') 
field_value TEXT NOT NULL -- Translated content );
```
## What is a `Bean`?
A **bean** is an **object** that is managed by the Spring **Inversion of Control (IoC) container**. Beans are the building blocks of a Spring application, and the IoC container is responsible for creating, managing, and wiring these beans.
Imagine you’re building something with **Lego blocks**. Each Lego block is like a **bean** in a Spring application. Beans are just **objects** (pieces of code) that work together to create a full application.
- An **object** is a concrete entity created from a class. Example: A `Car` object has fields like `color`, `model`, and methods like `drive()`.
- Every object is an **instance** of a class, but "instance" emphasizes the fact that it was created from that specific class.
## What is `IoC container`?
Instead of you (the developer) manually creating and wiring objects together, a framework like Spring takes care of it for you.
The **IoC (Inversion of Control) container** is a **special program inside Spring** that creates and connects all these beans (objects) for you. It manages **how beans are created** and **how they talk to each other**.
- Instead of you creating objects using `new`, the IoC container automatically creates them for you.
## About `@Autowired`
The `@Autowired` annotation in Spring is used for **Dependency Injection (DI)**. Spring will automatically find and inject an instance of `CelebrityRepository` into `CelebrityServiceImpl` at runtime.
### Field injection:
```java
@Service
public class CelebrityServiceImpl implements CelebrityService {

    @Autowired  // This is field injection
    private CelebrityRepository celebrityRepository;

    @Override
    public Celebrity getCelebrityById(int id) {
        return null;
    }
}
```
This is called **field injection** because the dependency (in this case, `CelebrityRepository`) is injected directly ==**into** the **field**== without using a constructor or setter. It has limitations (harder to test, less clear, not flexible).
### Constructor injection:
```java
@Service
public class CelebrityServiceImpl {

    private final CelebrityRepository celebrityRepository; // Declared as a final field

    @Autowired
    public CelebrityServiceImpl(CelebrityRepository celebrityRepository) { // Constructor injection
        this.celebrityRepository = celebrityRepository; // Injected dependency
    }
}
```
Constructor injection doesn’t mean we initialize dependencies ourselves; instead, it’s about **specifying dependencies explicitly via the constructor** and letting Spring provide them when creating the object.