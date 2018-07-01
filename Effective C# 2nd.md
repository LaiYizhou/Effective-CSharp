# Chapter 1: C\# Language Idioms



## 1. Use Properties Instead of Accessible Data Members 

- is far easier to change
- multithreaded
- can be virtual
- can define a property in an interface, and *Field* can't
- different accessibility
- *indexer*
  - multidemensional indexer
  - use an indexer for sequences or dictionaries



## 2. Prefer *readonly* to *const*

- *runtime constants*: slower and correct
- *compile-time constants*: faster but maybe broken program
- Prefer *runtime constants* To *compile-time constants*
- *runtime constants*: more flexibility and can be any type



## 3. Prefer the *is* or *as* Operators to Casts

- safer
- more efficient at runtime



## 4. Use Conditional Attributes Instead of *#if* 

- must have a return type of *void*
- more efficient
- only use at function level, which forces you to better structure your code



## 5. Always Provide *ToString()* 

- also can create different forms of string output 



## 6. Understand the Relationships Among the Many Different Concepts of Equality    

- C# provides four different functions:
  - public static bool **ReferenceEquals** (object left, object right);
  - public static bool **Equals** (object left, object right);
  - public virtual bool **Equals**(object right);
  - public static bool operator **==** (MyClass left, MyClass right);
- never redefine *Object.ReferenceEquals()*
  - *ReferenceEquals()* always returns false when you use it to test equality for *value types*. 
  - Even when you compare a value type to itself, *ReferenceEquals()* returns false. This is due to **boxing**
- never redefine *Object.Equals()* 
  - *Object.Equals (object left, object right)* Invokes *Equals (object right)*
- override instance *Equals()* and *operator==()* for *value types* to provide better performance. 
- override instance *Equals()* for *reference types*



## 7. Understand the Pitfalls of *GetHashCode()*

- the only one that should **avoid** writing

- For reference types, it works but is inefficient.

  For value types, the base class version is often incorrect.     

- **if** overload *GetHashCode()*, must follow :

  - If two objects are equal (as defined by operator==), they must generate the same hash value.
  - For any object A, A.GetHashCode() must always return the same value.
  - The hash function should generate a random distribution **among all integers for all inputs**.    



## 8. Prefer Query Syntax to Loops    

- move your program logic from a more *imperative model* to a *declarative model*.

- can execute those queries in parallel using the *.AsParallel()* method.    



## 9. Avoid Conversion Operators in Your APIs    

- If you want to convert another type into your type, use a constructor.    



## 10. Use Optional Parameters to Minimize Method Overloads    

- use *optional paramerters* and *named parameters*
- simpler
- more readable



## 11. Understand the Attraction of Small Functions

- Smaller and simpler functions make it easier for the JIT compiler

- A smaller function is more likely to contain fewer local variables

- Smaller methods are better candidates for *inlining*. 

  （But remember that even small functions that are virtual or that contain try/catch blocks cannot be inlined.）



# Chapter2 : Resource Management



## 12. Prefer Member Initializers to Assignment Statements

- Just initialize the variable when you declare it
- move initialization into the body of a constructor



## 13. Use Proper Initialization for Static Class Members

- use static initializers, can catch the exceptions yourself
- use static initializers and **static constructors** to initialize static class members    



## 14. Minimize Duplicate Initialization Logic

- if multiple constructors contain the same logic, factor that logic into a common constructor instead.
- use **default parameters** （C# 4.0） to minimize the duplicated code in constructors.    
- makes overloaded constructors more resilient
- DO NOT invoke another common function in different constructor
- Use *this()*  for constructor chaining : one constructor invoke another constructor
- In general, prefer *default values* to overloaded constructors.     



## 15. Utilize *using* and *try*/*finally* for Resource Cleanup

- if any exceptions, the *Dispose()* never happen
- can't use the *using* statement with a variable of a type that does not support the *IDisposable* interface
- if allocate multiple objects, can prefer to *try/finally* 



## 16. Avoid Creating Unnecessary Objects

- promote often-used local variables to member variables
- Infrequently called is unnecessary
- try to avoid creating the same objects repeatedly
- provide a class that stores singleton objects, like *System.String* (is immutable type)
- consider creating mutable builder classes for immutable types



## 17. Implement the Standard Dispose Pattern

