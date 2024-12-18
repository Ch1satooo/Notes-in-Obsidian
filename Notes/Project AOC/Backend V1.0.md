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
### Field injection (not recommended):
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
### Constructor injection (better):
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
## About `getter() setter()`
### JSON:
Many JSON parsing libraries like **Jackson** and **Gson** rely on getter and setter methods to map JSON keys to Java objects.
- When JSON `{ "name": "John" }` is deserialized into a Java object, the library automatically calls `setName("John")`.
- When serializing a Java object to JSON, the library calls `getName()` to retrieve the value.
### Flexibility for Future Changes:
```java
// Changing how 'fullName' is stored 
public String getFullName() { 
	return firstName + " " + lastName; // Combines two fields dynamically. 
	}
```
### Validation and Control:
Setters allow to validate input or execute extra logic when modifying a field, ensuring the object remains in a valid state.
```java
public void setSalary(double salary) { 
	if (salary < 0) { 
		throw new IllegalArgumentException("Salary cannot be negative"); 
		} 
	this.salary = salary; 
}
```
## `static` in Java
Class includes **method**, **static method** directly belongs to whole class, it can be called by: 
```java
className.methodName()
```
**Non-static method** (instance method) corresponds specific **instance**, it can be called by: 
```java
className instanceName = new className();
instanceNmae.methodName();
```
Most of the time, we do not use static method, but for utility methods, using static methods are appropriate.
## Generics in Java
### Genetic classes: 
Used when multiple methods share the same `<T>`.
```java
public class Printer<T, K>{
	T content;
	K secondContent;
	// Constuctor
	
	public void print(){
		System.out.println(content, secondContent);
	}
}
```
`<T>` allows the class to work with **different types**. It also can be extended using: 
`<T extends className/interfaceName`.
**Call**: 
```java
Printer<Integer> printer = new Printer<>(123);
printer.print();
```
#### Generic methods: 
Used when type flexibility is needed for one method.
```java
private static <T> void print(T content){
	System.out.println(content);
}
```
T here is a wildcard(data type). By **adding a `<T>` before return value type**, it tells Java that this is a generis type. Same way, `<T>` also can be extended using: 
`<T extends className/interfaceName`.
**Call**: 
```java
print("Anything");
print(123);
print(new Car());
// etc.
```
If want use generics in method, must declare it in method header: 
```java
public <T> void example(){
	Optional<T> optional = Optional.empty();
	System.out.println(optional.isEmpty());
}
```
## int and Integer
In Java, `int` is a **primitive data type**, while `Integer` is a **wrapper class** for the `int` primitive type.
- `Integer` is an **object**, which means it can be null. It allows to use additional methods like `Integer.parseInt()` and `Integer.toString()`.
- `Integer` can be `null`.
## About Constructor
A constructor is **unnecessary** when static methods or setters can handle initialization more flexibly, especially when creating objects with varying configurations or providing clearer intent for object creation.
## Why Not Use `void` for POST Requests?
- RESTful APIs recommend returning the resource's location or identifier after creation. It aligns with the HTTP standard for `POST`:
	- **Client Sends**: Data for resource creation.
	- **Server Responds**: Resource ID and `201 Created` status.
- For Confirmation of Successful Processing.
## Optional
`Optional<T>` is a **container object** (`Opthinal<String/Object/...>`) that may or may not contain a non-null value. It’s used to **avoid null pointer exceptions**.
It's a type class, just like **Integer**, which has other methods of it can be called.
```java
public Optional<User> findUserByName(String name, List<User> user) {
	for(User user : user) {
		if(user.getName().equals(name)) {
			return Optional.of(user);
		}
	}
	return Optional.empty();
}
```
## How `findById` Works in a Repository?
The `findById` method in a Spring Data JPA repository explicitly returns an `Optional<Celebrity>`. Then, must explicitly handle the `Optional` to retrieve the underlying `Celebrity` object  in service layer.
==But==, other derived query methods return `List<Celebrity>` or `Celebrity` type.
## `CollectionUtils.isEmpty` and `List.isEmpty`
`CollectionUtils.isEmpty` (from Spring Framework) and `List.isEmpty` (a method of the Java `List` interface) both check if a collection is empty.
- `CollectionUtils.isEmpty(collection)` returns a **boolean value**. When the collection is null, it returns true.
- But, `List.isEmpty()` throws a `NullPointerException` if the collection is `null`.