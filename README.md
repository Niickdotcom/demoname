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
2) This mechanism automatically configures Spring application based on the dependencies in the class path and the beans define by
by developer
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

