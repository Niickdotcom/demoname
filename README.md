How does @SpringBootApplication Internally work
1) Its a basic meta annotation which means its combine multiple annotation into one 
2) @SpringBootConfiguration, @EnableAutoConfiguration and @ComponentScan
3) its start using main method 
4) and main method is call run method i.e SpringApplication.run()
5) From this run mehtod the application context of IOC searches the class annotated with @Configuration annotation which calls
all the beans in the class path and initialize those classes 
6) Beans are stored in perticular spaces in JVM.
7) and the perticular space in call as IOC Container
8) after that all beans are created the request will go to the dispacter servlet and the dispatcher servlet will distribute 
all the request among the appropriate controller
9) also there are different layer like 
	presentation layer  --> Authentication & JOSN Translation 
	business layer --> Authorization, bussiness Logic and validation 
	persistence layer --> Storage logic 
	data base layer --> Actual Database

How does auto-configuration works in spring boot
1) one of the key feature of spring boot is auto-configuration .
2) This mechanism automatically configures Spring application based on the dependencies in the class path and the beans define by developer
its works as 
1) Spring Boot scans the classpath for libraries and annotations
2) it matches these against a predefined set of configuration (e.g if spring-boot-starter-web)
3) it will auto confiure a web application with an embedded tomcat server
4) the configurations are defined in @Configuration classes

Spring boot Dev tools
1) Spring Boot DevTools is designed to enhance the development experience by enabling features like
	automatic restart
	live reload
	configuration for faster development cycle.
2) how it works
	DevTools monitors the classpath for changes and automatically restarts the application when changes are detected
	it provide additional features like a separate cache, conditional bean, loading and optimization for development
	vs production environment

how java knows if an object is in use
1) Java doesn't directly "know" if an object is in use. 
Instead, it uses a technique called reachability analysis via its 
Garbage Collector (GC) to determine whether an object is still needed.
2) The Java Virtual Machine (JVM) determines if an object is in use by checking if it's reachable from any "GC roots
3) GC roots are special references that are always considered reachable.
	Local variables in stack frames (method call variables)
	Static variables (class-level fields)
	References from active threads
	JNI references

what is Generic in Java?
1) Generic means parameterized type.
2) the idea is to allow a type (like Integer, String etc or user-define types)
to be a parameter to method, classes and interfaces
3) Generic in java allows us to create classes, interfaces and method where the 
type of the data is specified as a parameter.

why use of generic?
1) before generics used object to store any type of data.
2) So these features lack type safety
3) for example adding an Integer to a list of String would not show an error until
runtime.
4) Generics add that type of safety feature.
5) Generics only works with Reference type
Type of Java Generics
1) Generic Mehtod -
2) Generic Classes -
for example
previously --> 
ArrayList a1 = new ArrayList();
a1.add("Nishith");
a1.add("Mehta");
a1.add(10); //This will allow us to add no complie time error
using generice -->
ArrayList<String> a1 = new ArrayList<String>();
a1.add("Nishtih");
a1.add("Mehta");
a1.add(10); // it will throw compile time error

Difference Bettwen Compiler and Interpreter

A compiler translates the entire source code of a 
program into machine code (or bytecode) before the 
program is executed, 
A interpreter translates and executes the source 
code line by line during runtime

Compiler created executable files. where as 
interpreters provide immediate feedback and are often more flexible for debugging

compiler is pre-execuation 
interpreter are during execuation

JIT Compiler

1) JIT -> Just in time Compiler
2) is a type of compiler that compiles code during the program executions also know as
dynamic compilation
How it works
1) Bytecode Translation
	JIT compiler typically take bytecode and translate it into native machine code
2) Dynamic Compilation
	compilation process happens during the programs execution
3) performance optimization
	compling a code at run time


Given permission only to the admin download document how we can do?

To restrict a document download endpoint to admin users in Spring Boot, 
I would use Spring Security with role-based access control. 
Specifically, I’d annotate the download method in the controller with @PreAuthorize("hasRole('ADMIN')") and enable method-level security 
using @EnableGlobalMethodSecurity(prePostEnabled = true). This ensures that only authenticated users with the ADMIN role can access that endpoint, 
while others receive a 403 Forbidden response.


How to Implement JWT Token provide Detail Explation?

JWT Token
a) jwt token is a compact, url safe taht is pass between two parties
b) JWT Token has 3 parts : Header, Payload and Signature.

Implementation of JWT Token
1) add the dependencies 
	io.jsonwebtoken
	jjwt
	spring-boot-starter-security
2) Create JwtUtil Utitlity Class
	in this we will add all 
	1) Secret-key
	2) Required methods such as generateToken, validate token, istokenexpired, 
	3) in generateToken will make check for all the details like setSubject, claims, setIssueDate, setExpiration,SignsWith
3) will Create JWT RequestFilter  classs
	1) and extends OncePerRequestFilter
	2) will override the method doFilterInternal
	3) will validate the userdetails
4) after that will create the SecurityConfig class 
	1) SecurityFilterChain  (will add details related to the securityConfig)
5) Create Authenticated Controller 
	1) will add the mapping request and related implemetation to generate control

implement JWT authentication in Spring Boot, I use a login endpoint that generates a signed JWT token using jjwt. 
I store user roles in the token, return it to the client, and require it in the Authorization header for protected requests. 
A filter (OncePerRequestFilter) intercepts each request, extracts the token, validates it, and sets the user in the security context if valid.


Functional Reference (Also know as Method Reference)
1) Compact Way to represent a lamda expression
2) Basically method reference is a process where it uses notation as :: to invoke the methods directly
3) Different type of method reference are
	a) Static method reference --> ContainingClass::staticMethodName
	b) Instance method reference of a perticular Object --> containingObject::instanceMethodName
	c) Instance method reference of an arbitrary object of a particular type --> ContainingType::methodName
	d) Constructor reference --> ClassName::news

how to read spring environment variable?
basically reading application properties files we can do using multiple ways 
	1) using @Value annotation
	2) Using Environment Object
	3) access system variable directly System.getenv();


What is concurent Modification Exception
	ConcurrentModificationException is a runtime exception in Java 
 	that occurs when a collection is modified while it is being iterated over. 
  	This typically happens when multiple threads are accessing and modifying the same collection concurrently, 
   	but it can also occur in a single-threaded environment if the collection is modified directly while using an iterator.


Shallow Copy and Deep Copy
	Shallow Copy -	
 		A shallow copy will simply copy the values of the fields of the original object into the new object. 
 		In shallow copy, if the original object has any references to other class objects, then only the reference of that object is cloned. 
  		Therefore, any changes in this referenced object will be reflected in both the original and the cloned object. 
    	Deep Copy -
     		However, a deep copy creates a new object, including all referenced objects, and any changes made to the cloned object will not affect the original object.

Who is responsible to perform action on Jwt Token once it is generated?
	The server is responsible for acting upon a generated JWT. It does this by verifying the token's signature and claims to authenticate and authorize users. The server can then grant access to protected resources based on the JWT's contents. 
Here's a more detailed breakdown:
	1. Token Verification:
		The server receives a JWT (usually in an HTTP header) from the client. It then verifies the token's signature to ensure it hasn't been tampered with and that it was issued by a trusted source. 
	2. Claim Validation:
		The server checks the claims (data) within the JWT, such as the user's ID, roles, and permissions. 
	3. Authorization Decision:
		Based on the verified claims and the server's authorization rules, the server decides whether to grant the user access to the requested resource. 
	4. Access Granted or Denied:
		If the JWT is valid and the user has permission, the server grants access and proceeds with the request. Otherwise, the server denies access and returns an appropriate error code (e.g., 401 Unauthorized). 


Explain bean life cycle in spring boot?
In Spring Boot, the bean lifecycle is managed by the Spring IoC container, which controls how beans are created, initialized, and destroyed. It starts with instantiation, where the container creates the bean either through a constructor or a factory method. Once the bean is created, Spring performs dependency injection—injecting any required dependencies using annotations like @Autowired.
After injection, the bean enters the initialization phase. At this point, we can hook into the lifecycle using annotations like @PostConstruct, or by implementing the InitializingBean interface and overriding the afterPropertiesSet() method. This is where we typically perform setup tasks like opening connections or initializing resources.
Once initialized, the bean is ready for use throughout the application. Finally, when the application context shuts down, Spring triggers the destruction phase. We can define cleanup logic using @PreDestroy, or by implementing the DisposableBean interface and overriding the destroy() method. This is useful for releasing resources, closing connections, or stopping background tasks.

How many Objects are created
Java has a String pool—a special memory area where string literals are stored to optimize memory usage. When you use a string literal, Java checks if that value already exists in the pool. If it does, it reuses the reference. If not, it adds it.
🔍 Line-by-Line Breakdown
1️⃣ String str = new String("Hello");
- Creates 2 objects:
- One String literal "Hello" in the String pool (if not already present).
- One new String object in the heap, which is a copy of the literal.
2️⃣ String str2 = "Hello";
- Reuses the "Hello" literal from the String pool.
- No new object is created.
3️⃣ String str3 = "Hello";
- Again, reuses the same "Hello" from the pool.
- No new object is created.

what is saga pattern 

In a microservices architecture, one of the biggest challenges we face is managing distributed transactions—especially when a business process spans multiple services and databases. Traditional approaches like two-phase commit (2PC) don’t scale well in distributed systems due to their blocking nature and single point of failure. That’s where the Saga Pattern comes in.
The Saga Pattern is a design pattern used to manage long-running, distributed transactions by breaking them into a series of smaller, local transactions. Each of these transactions is handled by a separate microservice, and after completing its part, the service either triggers the next step or publishes an event. If any step fails, the system executes a compensating transaction to undo the previous steps and maintain consistency.
There are two main types of saga implementations: choreography and orchestration.
In choreography-based sagas, each service listens for events and reacts accordingly. For example, in an e-commerce system, when an order is placed, the Order Service publishes an event. The Payment Service listens to it and processes the payment. If successful, it publishes another event that the Inventory Service listens to, and so on. This approach is decentralized and works well for simpler workflows, but it can become hard to manage as the number of services grows.
On the other hand, orchestration-based sagas use a central orchestrator that controls the flow of the saga. The orchestrator calls each service in sequence and handles failures by invoking compensating actions. This makes the flow easier to visualize and debug, especially in complex business processes.
Let me give you a real-world example from a project I worked on. We were building a loan approval system where the process involved multiple services: customer verification, credit scoring, document validation, and final approval. Each service had its own database and logic. We implemented the Saga Pattern using orchestration. The orchestrator would initiate the saga, call each service, and if any service failed—for example, if the credit score was too low—it would trigger compensating actions like canceling the loan application and notifying the user.
One of the key benefits of the Saga Pattern is that it provides eventual consistency rather than strong consistency, which is more realistic in distributed systems. It also improves fault tolerance and scalability. However, it does come with challenges like handling retries, ensuring idempotency, and managing complex rollback logic.


What is Pagination?
Pagination is the process of breaking down large result sets into smaller, manageable chunks—called pages. Instead of loading thousands of records into memory, which can be inefficient and slow, we fetch a limited number of records per request. This improves performance, reduces memory usage, and enhances user experience, especially in APIs and UI-driven applications.
In Spring Data JPA, pagination is seamlessly supported through the JpaRepository interface, which extends PagingAndSortingRepository. This gives us access to methods like findAll(Pageable pageable) and findAll(Sort sort). The Pageable interface allows us to define the page number, size, and sorting criteria.
For example, in a book application, if I want to fetch books 10 at a time, I can use:
Pageable pageable = PageRequest.of(0, 10, Sort.by("title").ascending());
Page<Book> booksPage = bookRepository.findAll(pageable);
This will return the first 10 books sorted by title. The Page object also gives metadata like total pages, total elements, and whether it’s the last page—very useful for building paginated APIs.
Now, regarding JpaRepository, it’s a core interface in Spring Data JPA that abstracts away boilerplate code for CRUD operations. It provides methods like save(), findById(), delete(), and more. What’s powerful is that it supports query derivation, meaning I can define methods like findByAuthor(String author) and Spring will automatically generate the query.
In real-world projects, I’ve used JpaRepository to build scalable, maintainable data access layers. Combined with pagination, it helps us handle performance-sensitive endpoints, especially in admin dashboards, reporting modules, and search features.
To sum up: pagination helps us manage large data efficiently, and JpaRepository simplifies data access with powerful abstractions. Together, they’re essential tools in any Spring Boot developer’s toolkit.





