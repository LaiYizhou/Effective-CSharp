# Chapter 1: C\# Language Idioms



## 1. Use *Properties* Instead of Accessible Data Members 

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













