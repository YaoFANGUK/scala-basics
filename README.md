[TOC]

# Section 1: Scala Basics



## 1. Getting Started

```scala
package playground
object ScalaPlayground extends App{
  prinln("Hello Scala")
}
```

- *extends APP* will automatically insert a main function for this object 



## 2. Values, Variables & Types

### 2.1 values 

```scala
object ValuesVariablesTypes extends App {
  val x: Int = 42
  print(x)
  x = 2 //report an error 
}
```

- vals are immutable and cannot be reassigned

```scala
object ValuesVariablesTypes extends App {
  val x = 42
  print(x)
}
```

- **the types of vals are optional** (since the compiler can infer the type of vals)

##### 2.1.1 Int (4 Bytes)

```scala
val x: Int = 21
// val x = 21
```

##### 2.1.2 String

```scala
val aString: String = "Hello"
// val aString = "Hello"
```

##### 2.1.3 Boolean

```scala
val aBoolean: Boolean = false
// val aBoolean = true
```

##### 2.1.3 Char

```scala
val aChar: Char = 'a'
// val aChar = 'a'
```

##### 2.1.4 Short (2 Bytes)

```scala
val aShort: Short = 4612
// val aShort = 4612432423  will report an error (Int doese not math Short)
```

##### 2.1.5 Long (8 Bytes)

```scala
val aLong: Long = 12314345345345345L
```

To mark that a number should be represented as Long, we should put it a captital `L` at the end.

##### 2.1.6 Floats

```scala
val aFloat: Float = 2.0f
```

##### 2.1.7 Double

```scala
val aDouble: Double = 3.14
```

### 2.2 Variables

```scala
var aVariable: Int = 4
aVariable = 5 // compiler will not complain
```

- Variables are mutable and can be reassigned
- Variables are used for in functional programming as side effects



## 3. Expressions

### 3.1 Operators

`+`, `-`, `*`, `/` , `&`, `|` , `<<` , `>>`, 

`>>>`: right shift with zero extension

`==`, `!=`, `>`, `>=`, `<=`, `<`

`!`

`=`, `+=`, `-=`, ...(Changing a variable is called a side effect)

### 3.2 Instructions VS Experssions

- Instructions: something that you tell the computer to do.

```
eg. Chaning a variable, print in the console...
```

- Expression: something that has a value and or a type

In functional programming, we'll think of expressions that is every single bit of your code will compute a value

#### 3.2.1 If Expression

```scala
// if expression
val aCondition = true
val aConditionValue = if (aCondition) 5 else 3
```

If expressions always return a result.

```scala
println(if (aCondition) 5 else 3)   // the result is 5
```

#### 3.2.2 loops

- Instructions with side effects

```scala
// Never write this again
var i = 0
while(i< 10)
{
  println(i)
  i++
}
```

- Everything in scala is an expression

```scala
var aVariable = 4
val aWeirdValue = (aVariable = 3)
println(aWeirdValue)
```

-  The type of  `(aVariable = 3)` is a `Unit` , `Unit` is a special type in Scala is equivalent to void in other languages.  

-  **Side effects in Scala are actually expressions returning `unit`**

e.g. while loops, println(), reassig are side effects that also return a unit

#### 3.2.3 Code Blocks

Code blocks are special kind of expressins because they have some special properties.

```scala
val aCodeBlock = {
  val y = 2
  val z = y + 1
  if (z > 2) "Hello" else "GoodBye"
}
```

- Code blocks are expression. The value of the block is the value of its last expression.
- Code blocks can have their own definition of values and variables.

### 3.3 Questions

1. What is the value of someValue?

```scala
val someValue = {
  2 < 3
}
```

ANS: true

2. What is the value of someOtherValue?

```scala
val someOtherValue = {
  if(someValue) 239 else 986
  42
}
```

ANS: 42



## 4. Functions

### 4.1 Defining a function

```scala
def aFunction(a: String, b: Int): Strig = {
  a + " " + b
}

// call
aFunction("Hello", 3)
```

Parameterless Function:

```scala
def aParameterlessFunction(): Int = 42

// call
aParameterlessFunction
// or 
aParameterlessFunction()
```

```scala
def aRepeatedFunction(aString: String, n: Int): String = {
  if (n == 1) aString
  else aString + aRepeatedFunction(aString, n-1)
}
```

**When you need loops, use recursion ! **

```scala
def aFunctionWithSideEffect(aString: String): Unit = println(aString)
```

```scala
def aBigFunction(n: Int): Int = {
  def aSmallerFunction(a: Int, b: Int): Int = a + b
  aSmallerFunction(n, n-1)
}
```

### 4.2 Exerices

1. A greeting function

```scala
def greeting(name: String, age: Int) = "Hi, my name is " + name + " and I am " + age + " yeas old"
```

2. Factorial function

```scala
def factorial(n: Int): Int = if(n == 0) 1 else n * factorial(n-1)
```

3. Fibonacci function

```scala
def fibonacci(n: Int): Int = {
  if(n<=2) 1
  else fibonacci(n-1) + fibonacci(n-2)
}
```

4. Test if a number is prime

```scala
def isPrime(n: Int): Boolean = {
  def isPrimeUntil(t: Int): Boolean = {
    if (t <= 1) true
    else n % t != 0 && isPrimeUntil(t-1)
  }
  
  isPrimeUntil(n - 1)
  // or isPrimeUntil(n / 2)
}
```



## 5. Type Inference

### 5.1 What the compiler knows

- Case 1:

```scala
val message = "Hello, World!"

// The compiler infers the type from right hand side
// val message: String = "Hello, World!"
```

- Case 2:

```scala
val x = 2
val y = x + "items"

// the compiler can progressively determine thetype of each 
// the right side of x is an Int, so x is an Int
// the right side of y is Int + String = String, so y is a String
```

- Case 3:

```scala
def succ(x: Int) = x +1

// the compiler is able to look at the implementation to figure out the resulting expression
//def succ(x: Int): Int = x +1
```

### 5.2 What the compiler do NOT know

- Recursion

```scala
def factorial(n: Int) = 
	if (n<=0) 1
	else n * factorial(n - 1)
```

This case is an expression which has two branches so the compiler has to analyze both. The frist branch returns an integer which is fine. But the compiler can infer the type from the other branch.



## 6. Recursion

### 6.1 Stack Recursion

<a href="https://www.youtube.com/watch?v=_JtPhF8MshA&t=523s">Video Explaination</a>

- Stack Recuesion is **inefficient**

```scala
def factorial(n: Int): Int = 
	if (n <= 1) 1
	else x * factorial(n - 1)
```

Example:

<img src="https://s1.ax1x.com/2020/10/09/0D1anI.jpg" width="500">

Recursion Order:

```
  factorial(n) 
= n * factorial(n -1)
First: computing (n - 1)
Second: calling factorial
Last: computing mutiply (n * (...))
```

- Stack Recursion uses too much memory, which may lead to stack overflow.

<img src="https://s1.ax1x.com/2020/10/09/0D1y9g.png" width="500">

When calculating a larger number, it has to build up a very large intermediate expression, counting down from a million down to one, building up all the multiplications in the middle before we actually get to the end and start collapsing this whole thing down.

To fix this problem, we use tail recursion.

### 6.2 Tail Recursion

- Tail Recursion is **Efficient**

Redefine the factorial function:

```scala
def factorial(n: Int): Int = {
  def factHelper(x: Int, accumulator: Int): Int = {
	  if (x <= 1) accumulator
  	else factHelper(x - 1, x * accumulator)
  }
  factHelper(n, 1)
}
```

or 

```scala
def factHelper(x: Int, accumulator: Int): Int = {
	  if (x <= 1) accumulator
  	else factHelper(x - 1, x * accumulator)
}

def factorial(n: Int): Int = factHelper(n, 1)
```

Deduction:

```
  factorial(10) 
= factHelper(10, 1)
= factHelper(10 - 1, 10 * 1)
= factHelper(9, 10)
= factHelper(9 - 1, 9 * 10)
= factHelper(8, 90)
= factHelper(8 - 1, 8 * 90)
= factHelper(7, 720)
= factHelper(7 - 1, 7 * 720)
= ...
= 3628800
```

- The tail recursion do not use enormours amount of memory to build up a large indermediate expression

Recursion Order:

```
factHelper(n , a) = factHelper(n - 1, a * n)
First: computing (n - 1)
Second: computing (a * n)
Last: calling factHelper
```

- **The recursion is done at the LAST step**

The last expression of its code path is the facHelper. This allows Scala to preserve the same stack frame and not use additional stack frames for recursive.  

### 6.3 KEY: 

- **Use recursive call as the LAST expression.**
- **Use accumulators to turn a function into a tail recursive function**
- **The accumulators come from the base case**
- Accumulators store intermediate results rather than call the function recursively
- Once you made a tail recursion, add `@tailrec` before your function declaration, the compiler will check for you if the function respects the conditions for tail recursion, that way you are sure it will optimize the calls as expected.

### 6.4 Exapmle

| Stack Recursion                 | Tail Recursion       |
| :------------------------------ | -------------------- |
| pow(5, 4)                       | pow(5, 4)            |
| 5 * pow(5, 3)                   | pow_accum(5, 4, 1)   |
| 5 * (5 * pow(5, 2))             | pow_accum(5, 3, 5)   |
| 5 * (5 * (5 * pow(5, 1)))       | pow_accum(5, 2, 25)  |
| 5 * (5 * (5 * (5 * pow(5, 0)))) | pow_accum(5, 1, 125) |
| 5 * (5 * (5 * (5 * 1)))         | pow_accum(5, 0, 625) |
| 625                             | 625                  |

Notice that **the function on the left must store in its stack `exp` number of integers**, which will be multiplied when the recursion terminates and the function returns 1. In contrast, **the function at the right must only store 3 integers at any time**, and computes an intermediary result which is passed to its following invocation. **As no other information outside of the current function invocation must be stored**, a **tail-recursion optimizer can "drop" the prior stack frames**, eliminating the possibility of a stack overflow.

### 6.5 Exercise

1. Concatenate a string n times, using tail recursion

```scala
@tailrec
def concatString(aString: String, times: Int, accumulator: String): String = {
  if (times <= 0) accumulator
  else concatString(aString, times - 1, aString + accumulator)
}

// call
concatString("hello", 5, "")
```

2. Create a isPrime function, using tail recursion

```scala
def isPrime(n: Int): Boolean = {
  @tailrec
  def isPrimeUntil(t: Int, accumulator: Boolean): Boolean = {
    if (t <= 1) accumulator
    else isPrimeUntil(t - 1, accumulator && n % t != 0)
  }
  isPrimeUntil(n-1, true)
}

// call
isPrime(37)
```

3. Create a Fibonacci function, using tail recursion

- Basic idea:

```haskell
fib n = fibHelper n (0, 1)
fibHelper 0 (a, b) = a
fibHelper 1 (a, b) = b
fibHelper n (a, b) = fibHelper (n - 1) (b, a + b)
// we move a little window along one
```

- Recursion Order:

```
First: computing (n - 1)
Second computing (b, a + b)
Last: call fibHelper
```

- Answer:

```scala
def fibonacci(n : Int): Int = {
  @tailrec
  def fibonacciHelper(t: Int, accumulator_a: Int, accumulator_b: Int): Int = {
    if(t <= 1) accumulator_b
    else fibonacciHelper(t - 1, accumulator_b, accumulator_a + accumulator_b)
  }
  fibonacciHelper(n, 0, 1)
}

// call
fibonacci(10)
```

As we can see the accumulators come from the base case of recursion.



## 7. Call-By-Value and Call-By-Name

### 7.1 Intro

#### 7.1.1 Call-By-Value

```scala
def calledByValue(x: Long): Unit = {
  println("by value:" + x)
  println("by value:" + x)
}
```

#### 7.1.2 Call-By-Name

- Use `=>` to  tell the compiler that the parameter will be called by name

```scala
def calledByName(x: => Long): Unit = {
  println("by name:" + x)
  println("by name:" + x)
}
```

##### Comparision

Tesing:

```scala
calledByValue(System.nanoTime())
calledByName(System.nanoTime())
```

Results:

```shell
by value:134817818230063
by value:134817818230063
by name:134817890556063
by name:134817890628091
```

##### Explanation

- In the By Value Call: the exact avlue of this expression is computed before the function evaluates
- In the By name Call: this expression is passed literally as is. 

```scala
def calledByValue(x: Long): Unit = {
  println("by value:" + 134817818230063)
  println("by value:" + 134817818230063)
}


def calledByName(x: => Long): Unit = {
  println("by name:" + System.nanoTime())
  println("by name:" + System.nanoTime())
}
```

### 7.2 Examples

```scala
def infinite(): Int = 1 + infinite()
def printFirst(x: Int, y: => Int) = println(x)
```

Case 1:

```scala
printFirst(infinite(), 34)
```

Case 2:

```scala
printFirst(34, infinite())
```

Case 1 will crash with a stack overflow error, while Case 2 runs well.

##### Explanation

**The by name parameter delays the evaluation of the expression passed here until it's used.** In case 2, since the parameter y is not used, infinite() is never actually evaluated.

### 7.3 Summary

- Call By Value:
  - Value is computed before call
  - same value used everywhere
- Call By Name:
  - expression is passed literally
  - expression is evaluated at every use within



## 8. Default and Named Arguments

```scala
def facotial(n: Int, acc:Int = 1): Int = {
  if (n <= 1) acc
  else facotial(n - 1, n * acc)
}

// Call
facotial(10)
```

In this way, we acutally expose in a function in our API



## 9. Smart Operations on String

```scala
val str: String = "Hello, I am learning Scala"

str.charAt(2)  //l

str.substring(7,11)   //I am

str.split(" ").toList //List(Hello, I, am, learning, Scala)

str.startWith("Hello") //true

str.replace(" ","-")  //Hello,-I-am-learning-Scala

str.tolowerCase()

str.length
```

### 9.1 Scala method:

- Prepending

```scala
val aNumberString = "45"
println('a' +: aNumberString :+ 'z')
```

Result:

 ```
a2z
 ```

- Reverse

```scala
str.reverse
```

- take

```scala
str.take(2)
```

### 9.2 Scala Specific: String Interpolators

##### 1. S-interpolators

```scala
val name = "David"
val = 21
val greeting = s"Hello, my name is $name and I am $age eyas old"
```

- use `$`

##### 2. F-interpolators

```scala
val speed = 1.2f
val myth = f"$name can eat $speed$2.2f"
```

Result:

```
David can eat 1.20 burgers per minute
```

<img src="https://s1.ax1x.com/2020/10/09/0DBuGR.png" width="500">

##### 3. Raw-interpolators

```scala
println(raw"This is a \n newline")
```

Result:

```
This is a \n newline
```

However:

```scala
val escaped = "This is a \n newlline"
println(raw"$escaped")
```

Result:

```
This is a
 newline
```

The raw interpolator of  the strings ignores escaped characters inside raw characters in the string.



# Section 2: Object-Oriented Programming in Scala



## 10. Object-Oriented Basics

### 10.1 Class and Instance

- A class organises data and behaviour. That is code
- Instantitaion means concrete realisations and memory that is actual memory spaces that comform to the code and the data structure that the class describes.

```scala
class Person(name: String, age: Int) // Constructor

object OOBasics extends App{
  val person = new Person("Join", 26)
  println()
}
```

age is a class parameter but it's not a class member that you can access with.

```scala
println(person.age) // this is wrong, the compiler will complain
```

- **Class parameters are NOT FIELDS**

The way to convert a class parameter to a field would be to add the `val` or  `var` keyword

```scala
class Person(name: String, val age: Int) // Constructor
```

Now the compiler is happy:

```scala
println(person.age) // the compiler will NOT complain
```

To define a class

```scala
class Person(name: String, val age: Int) {
  //Body
  val x = 2   // var definition
  println(1 + 2)  //expression
  
  def greet(name: String): Unit = println(s"$name says: Hi, $name")
}
```

The Block of code inside can have basically everything, including:

- `val` and `var` definitions
- `function` definitions, which is called methods
- `expressions`
- other definitions (e.g., packages and other classes)

```scala
class Person(name: String, val age: Int) {
  //Body
  val x = 2   // var definition
  println(1 + 2)  //expression
  
  def greet(name: String): Unit = println(s"$name says: Hi, $name")
}

val person = new Person("John", 26)
person.greet("Daniel")
```

Result:

```
Daniel says: Hi, Daniel
```

##### `this` keyword:

```scala
class Person(name: String, val age: Int) {
  //Body
  val x = 2   // var definition
  println(1 + 2)  //expression
  
  def greet(name: String): Unit = println(s"$(this.name) says: Hi, $name")
}

val person = new Person("John", 26)
person.greet("Daniel")
```

the `name` is not a class field but it's still available within the class definition. `this.name` will refer to the name parameter of class `person` whther the `name` is actually a field or not.

Result:

```
John says: Hi, Daniel
```

- Overloading: defining method with the same name but different signatures. Different signature means different number of parameters or paramaters of different types coupled with possibly different return type at the end.

### 10.2 Mutilple Constructors 

(or overloading constructors)

In Scala, we use `def this`for building mutiple constructors:

```scala
def this(name: String) = this(name, 0)
```

```scala
def this() = this("John Doe")
```



### 11. Object-Oriented Basics Exercises

##### 1. Implement a novel and a writer class

```scala
/* Novel and Writer
 * writer: firstname, surname, year
 *   - method: fullname
 * novel: name, year of release, author
 *.  - method: authorAge, isWrittenBy(author), 
 *             copy(new year of relase) renturn new instance of novel
 */

class Writer(firstname: String, surname: String, val year:Int) {
  def fullname(): String = firstname + " " + surname
}

class Novel(val name: String, yearOfRelase: Int, val author: Writer){
  // no parameter passed into authorAge, so this is no need to add parentheses
  def authorAge: Int = yearOfRelase - author.year
  def isWrittenBy(author: Writer): Boolean = author == this.author
  def copy(newYear: Int): Novel = new Novel(this.name, newYear, this.author)
}

val author = new Writer("Chries", "Dickens", 1812)
val imposter = new Writer("Chries", "Dickens", 1812)
val novel = new Novel("Great Expectation", 1861, author)

println(novel.authorAge)
println(novel.isWrittenBy(imposter))
println(novel)
println(novel.copy(2008))
```

##### 2. Implement a counter class

```scala
/* receives a int value
* method: - current count
*         - method to increment/decrement => new counter
*         - overload inc/dec to receive an amount
*/
class Counter(val count: Int = 0){
  def currentCount = n
  def increment = new Counter(count + 1)  // immutability
  def decrement = new Counter(count - 1)  // immutability
  // Overload
  // recursively
  def increment(n : Int): Counter = {
    if (n <= 0 ) this
    else increment.increment(n - 1)
  }
  // def decrement(n : Int) = new COunter(count - n)
  // recursively
  def decrement(n : Int): Counter  = {
	  if (n <= 0 ) this
    else decrement.decrement(n - 1)
  }
}
```

<img src="https://s1.ax1x.com/2020/10/11/0cuHc4.png" width="500">



## 12. Syntactic Sugar: Method Notation

```scala
object MethodNotations extends App{
  class Person(val name: String, favriteMovie: String) {
    def likes(movie: String): Boolean = movive == favoriteMoive
  }
  val mary = new Person("Mary", "Inception")
  println(mary.likes("Inception"))
}
```

Result:

```
true
```

### Syntactic Sugar 1: infix notation / operator notaion

Instead of:

```scala
println(mary.likes("Inception"))
```

We can write:

```scala
println(mary likes "Inception")
```

**This only works with methods which have only one parameter**.

- Object.methid with a single parameter can be replaced with the repression object method parameter.

The `like` method is like a operator which yields a string, while `mary` and `"inception"` are operands

```scala
def hangoutWith(person: Person): String = s"$(this.name) is hanging out with $(person.name)" 

val tom = new Person("Tom", "Fight Club")
println(mary hangoutWith tom)
```

Result:

```
Mary is hanging out with Tom
```

This is also **valid**:

```scala
def +(person: Person): String = s"$(this.name) is hanging out with $(person.name)" 

val tom = new Person("Tom", "Fight Club")
println(mary + tom)
// which equals to println(mary.+(tom))

```

- On the other hand: **All operators are methods**

### Syntactic Sugar 2: prefix notation

- Prefix notation is all about unary operators

```scala
val x = -1
```

this `-` (negative sign ) is a unary operator;

unary operators are also methods.

```scala
val y = 1.unary_- // equivalent with val y = -1
```

- `unary_` prefix only works with a few operators:
  - `-`
  - `+`
  - `~`
  - `!`

Example:

```scala
def unary_! : String = s"name, What the heck?!"
```

notice there is a whitespace after the `!`

```scala
println(!mary) // equivalent with mary.unary_!
```

Result:

```
Mary, What the heck?!
```

### Syntactic Sugar 3: postfix notation

```scala
def isAlive: Boolean = true
```

Instead of:

```scala
println(mary.isAlive)
```

We can write:

```scala
println(mary isAlive)
```

However, in practice we often use the dot `.` notation, because the space notaion (i.e., the postfix notation) can introduce potential ambiguities when reading the code for human.

- **Postfix notaion is only avaiable to method without parameters.**

### Special Method: `apply`

`apply` has special property in Scala

```scala
def apply(): String = s"Hi, my name is $name and I like $favoriteMoive"
```

The implementation is not significant but the method signature. The method signature is Bloody impory not so much its return type but the **method name** and **method parameters**

Instead of:

```scala
println(mary.apply())
```

We can write:

```scala
println(mary())   // equivalent with println(mary.apply())
```

This `apply` breaks that barrier between object oriented programming and functional programming.



## 13. Method Notation Excerises

### 13.1 Overload the `+` operator

```scala
// receive a string and return a new person with a nickname
// mary + "the rockstart" =>  new person "Mary (the rockstar)"
def +(nickName: String): Person = new Person(s"$name ($nickName)", favoriteMovie)

println((mary + "the Rockstar").apply())
```

### 13.2 Add an age to the Person class

```scala
//add a unary + operator => new person with the age + 1
// +mary => mary with the age incremented

def unary_+ :Person = new Person(name,favoriteMovie,age + 1)

// call
println((+mary).age)
```

### 13.3 Add a "learns" method in the Person class

```scala
// add a learnScala method, calls learns method with "Scala"
// use it in postfix notation
def learns(thing: String): String = s"$name leans $thing"
def learnsScala: String = this learns "Scala"

// call
println(mary learnsScala)
```

### 13.4 Overload the apply method

```scala
// mary.apply(2) => "Mary watched her favorite movie Inception 2 times"
def apply(): String = s"Hi, my name is $name and I like $favoriteMovie"
def apply(n: Int): String = s"$name watched her favorite movie $favoriteMovie $n times"

// call
println(mary learnsScala)
println(mary(10))
```

ANSWER:

```scala
package playground
import scala.language.postfixOps

object ScalaPlayground extends App {

  class Person(val name: String, favoriteMovie: String, val age: Int = 0){

    def like(movie: String): Boolean = movie == favoriteMovie
    def +(nickName: String): Person = new Person(s"$name ($nickName)", favoriteMovie)
    def unary_+ :Person = new Person(name,favoriteMovie,age + 1)  //prefix notation sugar
    def learns(thing: String): String = s"$name leans $thing"
    def learnsScala: String = this learns "Scala" //infix notation sugar
    def apply(): String = s"Hi, my name is $name and I like $favoriteMovie"
    def apply(n: Int): String = s"$name watched her favorite movie $favoriteMovie $n times"

  }

  val mary = new Person("Mary", "Inception")
  println((mary + "the Rockstar").apply())
  // println((mary + "the Rockstar")())
  println((+mary).age)
  println(mary learnsScala) // postfix notation sugar
  println(mary(10))
}
```

Result:

```
Hi, my name is Mary (the Rockstar) and I like Inception
1
Mary leans Scala
Mary watched her favorite movie Inception 10 times
```

<img src="https://s1.ax1x.com/2020/10/11/0cNpX6.png" width="500">



## 14. Scala Objects

- Objects in Scala are a dedicated (专用的) concept. 

In Java:

```java
public class JavaPlayground{
  public static void main(String args[]){
    // access by
    System.out.println(Person.N_EYES);
  }
}

class Person{
  public static final int N_EYES = 2;
}
```

>  We would access the `N_EYES` field from the class `Person` not from an instance of person. This is called **class level** functionality.

- Scala **DOES NOT** have class-level functionality (e.g., "static")

An object can actually have this knid of static-like functionality.

In Scala:

```scala
object Object extends App{
  object Person{    // type + its only instance
    // "static/"class" level functionality
    val N_EYES = 2
  }
  
  // access by
  println(Person.N_EYES)
}
```

An object can have `vals` or `vars` and can also have method definitions.

Objects can be defined in a similar way that classes can with the exception that objects do not receive parameters.

We can define the vals and vars and methods **inside objects** and we can access them as we would in a class level setting.

1. **In Scala, we use an `object` as a singleton instance**.

when we defined the object person, we basically not only define its type but also define its only instance. 

```scala
val mary = Person 
val john = Person
```

 this `Person` is the instance of the person type, which is the only instance that this person type can have. 

```scala
println(mary == john)
```

Result:

```
true
```

There are singleton instances by definition without any other code needed from us.

2. A pattern used often in practice is that we write objects and classes with the same name

```scala
class Person(val name: String){
  // Instance level functionality
  
}
```

This pattern of writing classes and objects with the same name in the same scope is called companions.

3. Factory method

```scala
object Object extends App{
  object Person{  
    
    // ...
    //factory method
    def from(mother: Person, father: Pseron): Person = new Person("Bobbie")
  }
}
```

The sole purpose is to build persons given some parameters.

```scala
val bobbie = Person.from(mary, john)
```

Often we rename `from` to `apply`

```scala
object Object extends App{
  object Person{  
    
    // ...
    //factory method
    def apply(mother: Person, father: Pseron): Person = new Person("Bobbie")
  }
}
```

So instead of from, we call apply or delete the apply

```scala
val bobbie = Person(mary, john)
// val bobbie = Person.apply(mary, john)
```

4. Scala Application

- a Scala application is  `a Scala object` wich a very important and particular method called `main`

```scala
def main(args: Array(String)): Unit
```

Scala application are turned into Java Virtual Machine applications whose entry point have to be static public static void main with an array of string as a parameter.

**Takeaways**

- Scala doesn't have "static" values/method

- Scala objects

  - are in their own class

  - are the only instance

  - singleton pattern in one line!

    - ```scala
      object Person{
        val N_EYES = 2
        def canFly: Boolean = false
      }
      ```

- Scala companions

  - ```scala
    class Person
    object Person
    ```

  - can access each other's private members

  - Scala is more OO than Java

- Scala application

  - ```scala
    def main(args: Array[String]): Unit
    ```

  - ```scala
    object MyApp extends App
    ```



## 15. Inheritance - Part I

### 15.1 single class inheritance

```scala
object InheritanceAndTraits extends App{
  class Animal {
    def eat = println("nomnom")
  }
  
  class Cat extends Animal
  
  val cat = new Cat
  cat.eat // valid expression
}
```

- Scala uses **single class inheritance**, which means to only extend one class at a time. While **Intricate inheritance** models are offered in `traits`

- A subclass only inherits non-private member of the superclass

```scala
object InheritanceAndTraits extends App{
  class Animal {
    private def eat = println("nomnom")
  }
  
  class Cat extends Animal
  
  val cat = new Cat
  cat.eat // invalid expression, eat is inaccessable
}
```

- `protected` keyword marks this method/property are only usable within this class and within subclasses only.

```scala
object InheritanceAndTraits extends App{
  class Animal {
    protected def eat = println("nomnom")
  }
  
  class Cat extends Animal{
    def crunch = {
      eat  // valid expression (within subclass)
      println("Crunch Crunch")
    }
  }
  
  val cat = new Cat
  cat.eat // invalid expression (without subclass)
  cat.crunch // valid expression
}
```

### 15.2 Constructors

```scala
class Person(name: String, age: Int)
class Adult(name: String, age: Int, idCard: String) extends Person // invalid expression, the compiler will complain that we have unspecified value paramters name and age.
```

Defining class like this with the class signature also defines its constructor. 

When we instantiate a derived class (in this case adult), the JVM will need to call an constructor from a parent class first (in this case person).  

```scala
class Person(name: String, age: Int)
class Adult(name: String, age: Int, idCard: String) extends Person(name, age) // this is valid
```

Or use Auxiliary function as constructor

```scala
class Person(name: String, age: Int){
  def this(name: String) = this(name, 0)
}
class Adult(name: String, age: Int, idCard: String) extends Person(name) // this is valid
```

### 15.3 Overriding

```scala
class Dog extends Animal{
  override def eat = println("crunch crunch")
}

val dog = new Dog
dog.eat
```

**overriding works for method as well as vals and vars**

```scala
class Animal {
  val creatureType = "wild"
  protected def eat = println("nomnom")
}

class Dog extends Animal{
  override val creatureType = "domestic"
  override def eat = println("crunch crunch")
}
val dog = new Dog
println(dog.creatureType)
```

Or:

```scala
class Dog(override val creatureType: String) extends Animal{
  override def eat = println("crunch crunch")
}

val dog = new Dog("K9")
```

Or:

```scala
class Dog(dogType: String) extends Animal{
  override val creatureType = dogType
}

val dog = new Dog("K9")
```

### 15.4 Type substitution

```scala
val unknownAnimal: Animal = new Dog("K9")
unknownAnimal.eat
```

- **This is a broad sense called polymorphism** (为不同数据类型的实体提供统一的接口)
- A method call will always go to the most overridden version whenever possible.

- `super` is used when you want to reference a method or a field from parent class.

### 15.5 Preventing overrides

#### 15.5.1 Use keyword `final` on `<method>`

```scala
class Animal {
  val creatureType = "wild"
  final def eat = println("nomnom")
}

class Dog extends Animal{
  override def eat = println("crunch crunch")  // invalid expression (Method 'eat' cannot override final member)
}
```

This prevernts the method to be overridden.

#### 15.5.2 Use keyword `final` on `<class>`

```scala
final class Animal {
  val creatureType = "wild"
  final def eat = println("nomnom")
}
```

This prevents the whole class from being extended.

```scala
class Animal {
  val creatureType = "wild"
  final def eat = println("nomnom")
}

class Dog extends Animal{ // invalid expression (Illegal inheritance from final class Animal)
  // ...
}
```

#### 15.5.3 Seal the class by  `sealed`

- Sealling the class is a software restriction in that you can extend the classes in ths file only, but prevents extension in other files.

In file xx1.scala

```scala
sealed class Animal {
  val creatureType = "wild"
  final def eat = println("nomnom")
}
```

In file xx1.scala

```scala
class Dog extends Animal{   // valid expression
  //...
}
class Cat extends Animal{   // valid expression
  //...
}
```

In file xx2.scala

```scala
class Dog extends Animal{   // invalid expression
  //...
}
class Cat extends Animal{   // invalid expression
  //...
}
```



## 16. Inheritance - Part II

### 16.1 Abstract

```scala
object AbstractDataTypes extends App{
  
  //abstract
  abstract class Animal {
    val creatureType: String
    def eat: Unit
  
}
```

There are situations where you need to leave some fields or methods blank or unimplemented. These are called **abstract** members. Classes which contain unimplemented or abstract fields or methods are called abstract classes and they are defined by the keyword `abstract`.

- Abstract classes can not be instantiated.

```scala
class Dog extends Animal {
  override val creatureType: String = "Canine"
  override def eat: Unit = println("Crunch crunch")
}
```

To extend abstract classes, the `override` keyword can be simplified:

```scala
class Dog extends Animal {
  val creatureType: String = "Canine"
  def eat: Unit = println("Crunch crunch")
}
```

### 16.2 Traits

#### 16.2.1 Definition

Traits are the ultimate abstract data types in Scala.

```scala
trait Carnivore{
  def eat(animal: Animal): Unit
}

trait ColdBlooded
```

```scala
class Crocodile extends Animal with Carnivore with ColdBlooded{
  val creatureType: String = "Croc"
  def eat: Unit = println("nomnomnom")
  def eat(animal: Animal): Unit = println(s"I'm a croc and I'm eating )$(animal.creatureType)"
}

val dog = new Dog
val croc = new Crocodile
croc.eat(dog)

```

Result:

```
I'm a croc and I'm eating Canine
```

####  16.2.2 Difference between `trait` and `abstract`

- Similarity:

Both `Abstract`  and `trait` classes can have abstract and non-abstract types

```scala
abstract class Animal {
    val creatureType: String = "wild"
    def eat: Unit
}
```

```scala
trait Carnivore{
  def eata(animal: Animal): Unit
  val preferredMeal: String = "fresh meat"
}
```

- Difference:

  - **traits** cannot have constructor parameters

  - ```scala
    trait Carnivore(name: String){      // invalid expression
      def eata(animal: Animal): Unit
      val preferredMeal: String = "fresh meat"
    }
    ```

  - **multiple traits may be inherited by the same class**: you can only extend one class but you can mix in multiple traits.

  - **trait - behavior**: We choose a **trait** when describe a type of behaviour

  - abstract class is a type of thing: e.g., animal describe animals but traits describe what they do.

### 16.3 Scala's Type Hierarchy

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20190401170602/ScalaTypeHierarchy.png">



## 17. Inheritance Exercises

#### Implementing our own collection

```scala
abstract class MyList{
  /*
  head = first element of the list
  tail = remainder of the list
  isEmpty = is the list empty
  add(Int) => new list with this element added
  toString => a String representation of the list
  */
  def head: Int
  def tail: MyList
  def isEmpty: Boolean
  def add(element: Int): MyList
  def toString: String
}
```

Extend by two subclasses: the empty list and non-empty list

- The empty list is an object

```scala
object Empty extends MyList {
  def head: Int = ???
  def tail: MyList = ???
  def isEmpty: Boolean = ???
  def add(element: Int): MyList = ???
}
```

The `???` returns nothing, when this method is called, it will throw a not implemented error.

- The Non empty list is a class with two parameters

```scala
class Cons(h: Int, t: MyList) extends MyList {
  def head: Int = ???
  def tail: MyList = ???
  def isEmpty: Boolean = ???
  def add(element: Int): MyList = ???
}
```

`Cons` will actually compose a value with some other list, which is what a linked list actually means. It is composed of an element and the rest of the list.

```scala
object Empty extends MyList {
  def head: Int = throw new NoSuchElementException
  // throw expression are expressions which return nothing (nothing type)
  def tail: MyList = throw new NoSuchElementException
  def isEmpty: Boolean = true
  def add(element: Int): MyList = new Cons(element, Empty)
}
```

```scala
class Cons(h: Int, t: MyList) extends MyList {
  def head: Int = h
  def tail: MyList = t
  def isEmpty: Boolean = false
  def add(element: Int): MyList = new Cons(element, this)
}
```

Test 1:

```scala
object ListTest extends App{
  val list = new Cons(1, Empty)
  println(list.head)
}
```

Result:

```
1
```

Test 2:

```scala
object ListTest extends App{
  val list = new Cons(1, new Cons(2, new Cons(3, Empty)))
  println(list.tail.head)
  println(list.add(4).head)
  println(list.isEmpty)
}
```

Result:

```
2
4
false
```

- To implement `toString` method

```scala
abstract class MyList{
  def head: Int
  def tail: MyList
  def isEmpty: Boolean
  def add(element: Int): MyList
  // Just prints the elements in order with the space in between them
  def printElements: String 
  // printElement will actually delegate to the subclasses implementation
  override def toString: String = "[" + printElements + "]"
}

object Empty extends MyList {
  def head: Int = throw new NoSuchElementException
  def tail: MyList = throw new NoSuchElementException
  def isEmpty: Boolean = true
  def add(element: Int): MyList = new Cons(element, Empty)
  def printElements: String = ""
}

class Cons(h: Int, t: MyList) extends MyList {
  def head: Int = h
  def tail: MyList = t
  def isEmpty: Boolean = false
  def add(element: Int): MyList = new Cons(element, this)
  def printElements: String = 
  	if (t.isEmpty) "" + h
  	else h + " " + t.printElements
  // this is a recursive method which lists every single element in this non empty list by calling printElements recursively on the tail
}

```

Test:

```scala
object ListTest extends App{
  val list = new Cons(1, new Cons(2, new Cons(3, Empty)))
  // polymorphic call
  println(list.toString)
}
```

Result:

```scala
[1 2 3]
```

- Why add `override` before `def toString`?

`toString` and `equals` and `hashCode` are methods that are present in the `anyref` class

<img src="https://s1.ax1x.com/2020/10/12/0WlVPA.md.png" width="500">



## 18. Generics

### 18.1 Generics Implementation

- Single type parameters:

```scala
object Generics extends App{
  // Generic class
  class MyList[A] {
    // use the type A inside the definition
  }
  
  val listOfIntegers = new MyList[Int]
  val listOfString = new MyList[String]
}
```

- Multiple type parameters:

```scala
class MyMap[key,value] {
  //
}
val mapOfIntString = new MyMap[Int, String]
```

- This also works for `trait`:

```scala
trait MyMap[key,value] {
  //
}
val mapOfIntString = new MyMap[Int, String]
```

-  Generic Methods

```scala
object MyList {
  def empty[A]: MyList[A] = ???
  
 //...
  val emptyListOfIntegers = MyList.empty[Int]
}
```

### 18.2 Variance Problem

```scala
class Animal
class Cat extends Animal
class Dog extends Animal
```

If Cat extends Animal, does a list of Cat also extend the list of Animal ?

- Option 1: 

- > Yes, List[Cat] extends List[Animal] = COVARIANCE

  This behaviour is called **covariance** and the way that you declare a covariant list is to:

  ```scala
  class CovariantList[+A]
  val animal: Animal = new Cat
  val animalList: CovariantList[Animal] = new CovariantList[Cat]
  ```

  `+A` means that this is a covariant list

  - Is animalList.add(new Dog) OK ?

  - > To answer this qustion, we have to lean **bounded type**

    If I add a new Dog into a list of cats, that will turn this new list into a list of animal basically. Because I have cats and a dog which makes the whole list a list of generic animals.

    **Adding a dog to a list of cats would actually turn it into something more generic**

- Option 2:

- > No, List[Animal] and List[Cat] are two separate things
  >
  > NO = INVARIANCE

- This is called **invariance** and the way you declare a invariant list is to:

  ```scala
  class InvariantList[A]
  val invariantAnimalList: InvariantList[Animal] = new InvariantList[Cat]   // invalid expression
  ```

- Option 3: (counter-intuitive)

- >  Hell, No!

- This is called **Contravariance**

  ```scala
  class ContravariantList[-A]
  val contravariantList: ContravariantList[Cat] = new ContravariantList[Animal]
  ```

  We can replace a list of animals with a list of cats because cats are animals. In the contravariant case, I'm replacing a list of cats with a list of animals even though cat is a subtype of animal. The relationship is exactly opposite.

  ```scala
  class Trainer[-A]
  val contravariantList: Trainer[Cat] = new Trainer[Animal]
  ```

  Now the semantics of it will change because if I want a trainer of cat but I am supplying a trainer of animal. the trainer of animal on the right hand side is better. Because a trainer of animal can also train a dog or cat, dinosaur...

### 18.3 Bounded types

Bounded types allow you to use your generic classes **only for centain types** that are either a **subclass** `<:`of a different type or a **superclass **`>:` of a different type.

- `<:`

```scala
class Cage[A <: Animal](animal: A)
val cage = new Cage(new Dog))
```

In this case, class Cage only accepts type parameters which are subtype of animal

```scala
class Car
val newCage = new Cage(new Car) // Invalid expression
```

that is because `Car` does not a class `Animal`

- `>:`

```scala
class Cage[A >: Animal](animal: A)
val cage = new Cage(new Dog))
```

In this case, class Cage only accpet type parameters which are supertypes of animal

- Bounded types solves variance problem

a natural method to add in MyList type would be an add method

```scala
class MyList[A] {
  def add(element: A): MyList[A] = ???
}
```

this `add` method signature now does not work, even through MyList is covariant and it's generic. The error that the compiler tells us is: 

```
Covariant type A occurs in contravariant problem in type A of value element
```

The right way:

```scala
def add[B >: A](element: B): MyList[B] = ???
/*
 A = Cat
 B = Animal
*/
```

**This means: if I put in a B which is a supertype of A into a list of A, then this list will trun into a MyList of B not into MyList of A.**

### 18.4 Expand MyList to be Generic

```scala
abstract class MyList[+A]{
  def head: A
  def tail: MyList[A]
  def isEmpty: Boolean
  def add[B >: A](element: B): MyList[B]
  // Just prints the elements in order with the space in between them
  def printElements: String 
  // printElement will actually delegate to the subclasses implementation
  override def toString: String = "[" + printElements + "]"
}

object Empty extends MyList[Nothing] {
  def head: Nothing = throw new NoSuchElementException
  def tail: MyList[Nothing] = throw new NoSuchElementException
  def isEmpty: Boolean = true
  def add[B >: Nothing](element: B): MyList[B] = new Cons(element, Empty)
  def printElements: String = ""
}

class Cons[+A](h: A, t: MyList[A]) extends MyList[A] {
  def head: A = h
  def tail: MyList[A] = t
  def isEmpty: Boolean = false
  def add[B >: A](element: B): MyList[B] = new Cons(element, this)
  def printElements: String = 
  	if (t.isEmpty) "" + h
  	else h + " " + t.printElements
  // this is a recursive method which lists every single element in this non empty list by calling printElements recursively on the tail
}

```

```scala
object ListTest extends App {
  // val listOfInt: MyList[Int] = Empty
  // val listOfString: MyList[String] = Empty
  val listOfInt: MyList[Int] = new Cons(1, new Cons(2, new Cons(3, Empty)))
  val listOfString: MyList[String] = new Cons("Hello", new Cons("Scala", Empty))
  println(listOfInt)
  println(listOfString)
}
```

Result:

```
[1 2 3]
[Hello Scala]
```

<img src="https://s1.ax1x.com/2020/10/13/0hNGuj.md.png" width="500">

<img src="https://s1.ax1x.com/2020/10/13/0hN7qA.png" width="500">



## 19. Anonymous Classes

Example:

```scala
object AnoymousClasses extends App {
  abstract class Animal {
    def eat: Unit
  }
  
  // anonymous class
  val funnyAnimal: Animal = new Animal {
    override def eat: Unit = println("ahahahahaha")
  }
  
  prinln(funnyAnimal.getClass)
}
```

Result:

```
class playground.AnoymousClasses$$anon$1
```

What acutally happen when we wrote this is that the compiler created a class with a name called `playground.AnoymousClassses$$anon$1`

and actually instantiated it later and assigned it to `funnyAnimal`

- Steps of compiler doing this

First:

```scala
class AnoymousClasses$$anon$1 extends Animal
```

Second:

```scala
val funnyAnimal: Animal = new AnoymousClasses$$anon$1
```

Another example: 

```scala
class Person(name: String){
  def sayHi: Unit = println(s"Hi, my name is $name, how can I help?")
}
val jim = new Person("Jim"){
  override def sayHi: Unit = println("Hi, my name is Jim, now can I be of service?")
}
```

<img src="https://s1.ax1x.com/2020/10/13/0hwEJP.md.png" width="500">



## 20. OO Exercises: Expanding Our Collection

1. Generic trait MyPredicate[-T]

It will have a small method to test whether a value of type T passes a condition. It returns a Boolean. Every subclass of MyPredicate[T] will actually have a different implemmentation of that little method.

> Example:
>
> ```scala
> class EvenPredicate extends MyPredicate[Int]
> ```

```scala
trait MyPredicate[-T] {
  def test(elem: T): Boolean
}
```

2. Generic trait MyTransformer[-A, B]

It will take two parameters A and B. It will have a method called `transform(a: A): B` to convert a value of type A into a value of type B. Every subclass of my transformaer will have a different implementation of that method.

> Example:
>
> ```scala
> class StringToIntTransformer extends MyTransformer[String, Int]
> ```

```scala
trait MyTransformer[-A, B] {
  def transform(elem: A): B
}
```

3. MyList functions

- **map**: which takes MyTranformer and returns a new list of a different type

  > Example:
  >
  > ```pseudocode
  > [1,2,3].map(n * 2) = [2, 4, 6]
  > ```

```Scala
def map[B](transformer: MyTransformer[A, B]): MyList[B]
```

- **filter**: which takes MyPredicate and returns MyList

  > Example:
  >
  > ```pseudocode
  > [1,2,3,4].filter(n % 2) = [2, 4]
  > ```

```scala
def filter(predicate: MyPredicate[A]): MyList[A]
```

- **flatMap**: which takes a transformer from  A to MyList[B] and it returns on MyList[B]

  > Example
  >
  > ```pseudocode
  > [1,2,3].flatMap(n => [n,n+1]) => [1,2,2,3,3,4]
  > ```

```scala
def flatMap[B](tansformer: MyTransformer[A, MyList[B]]): MyList[B]
```

> In order to implement flatMap, we need a concatenation function

- ++ (concatenation function)

```scala
def ++[B :> A](list: MyList[B]): MyList[B]
```

\[**Answer**\]:

```scala
abstract class MyList[+A] {
  def head: A
  def tail: MyList[A]
  def add[B >: A](element: B): Mylist[B]
  def printElements: String
  override def toString: String = "[" + printElements + "]"
  def map[B](transformer: MyTransformer[A, B]): MyList[B]
  def flatMap[B](tansformer: MyTransformer[A, MyList[B]]): MyList[B]
  def filter(predicate: MyPredicate[A]): MyList[A]
}
```

```scala
object Empty extends MyList[Nothing] {
  def head: Nothing = throw new NoSuchElementException
  def tail: MyList[Nothing] = throw new NoSuchElementException
  def isEmpty: Boolean = true
  def add[B >: Nothing](element: B): MyList[B] = new Cons(element, Empty)
  def printElements: String = ""
  
  def map[B](transformer: MyTransformer[Nothing, B]): MyList[B] = Empty
  def filter(predicate: MyPredicate[Nothing]): MyList[Nothing] = Empty
  def ++[B :> Nothing](list: MyList[B]): MyList[B] = list
  def flatMap[B](tansformer: MyTransformer[Nothing, MyList[B]]): MyList[B] = Empty
}
```

```scala
class Cons[+A](h: A, t: MyList[A]) extends MyList[A] {
  def head: A = h
  def tail: MyList[A] = t
  def isEmpty: Boolean = false
  def add[B >: A](element: B): MyList[B] = new Cons(element, this)
  def printElements: String = 
  	if (t.isEmpty) "" + h
  	else h + " " + t.printElements
  
  def filter(predicate: MyPredicate[A]): MyList[A] = 
  	if (predicate.test(h)) new Cons(h, t.filter(predicate))
  	else t.filter(predicate)
  def map[B](transformer: MyTransformer[A, B]): MyList[B] = 
  	new Cons(transformer.transform(h), t.map(transformer))
  def ++[B :> A](list: MyList[B]): MyList[B] = new Cons(h, t ++ list)
  def flatMap[B](tansformer: MyTransformer[A, MyList[B]]): MyList[B] = transformer.transform(h) ++ t.flatMap(transformer) 
}
```

\[**Testing**\]:

```scala
val listOfIntegers: MyList[Int] = new Cons(1, new Cons(2, new Cons(3, Empty)))

val anotherListOfIntegers: MyList[Int] = new Cons(4, new Cons(5, Empty)))
```

- map

```scala
println(listOfIntegers.map(new MyTransformer[Int, Int]{
  override def transform(elem: Int): Int = elem * 2
}).toString)
```

Result:

```shell
[2 4 6]
```

Explanation:

```pseudocode
[1,2,3].map(n * 2)
= new Cons(2,[2,3].map(n * 2))
= new Cons(2, new Cons(4, [3].map(n * 2))
= new Cons(2, new Cons(4, new Cons(6, Empty.map(n * 2))))
= new Cons(2, new Cons(4, new Cons(6, Empty)))
```

- filter

```scala
println(listOfIntegers.filter(new MyPredicate[Int]: Boolean {
  override def test(elem: Int) = elem % 2 == 0
})
```

Result:

```shell
[2]
```

Explanation:

```pseudocode
[1,2,3].filter(n % 2 == 0)
= [2,3].filter(n % 2 == 0)
= new Cons(2,[3].filter(n % 2 == 0))
= new Cons(2,Empty.filter(n % 2 == 0))
= new Cons(2,Empty)
```

- ++

```scala
println(listOfIntegers ++ anotherListOfIntegers).toString)
```

Result:

```shell
[1,2,3,4,5]
```

Explanation:

```pseudocode
[1,2,3] ++ [4,5]
= new Cons(1, [2,3] ++ [4,5])
= new Cons(1, new Cons(2, [3] ++ [4,5])))
= new Cons(1, new Cons(2, new Cons(3, Empty ++ [4,5])))
= new Cons(1, new Cons(2, new Cons(3, [4,5]))
= new Cons(1, new Cons(2, new Cons(3, new Cons(4, new Cons(5, Empty)))))
```

- flatMap

```scala
println(listOfIntegers.flatMap(new MyTransformer[Int, MyList[Int]] {
  override def transform(elem: Int): MyList[Int] = new Cons(elem, Cons(elmen + 1, Empty))
}).toString)
```

Result:

```
[1 2 2 3 3 4]
```

Explanation:

```pseudocode
[1,2].flatMap(n => [n,n + 1])
= transformer.transform(1) ++ [2].flatMap(n => [n,n + 1])
// transformer: n => [n, n + 1]
// 1 => [1,2]
= [1, 2] ++ [2].flatMap(n => [n,n + 1])
= [1,2] ++ [2,3] ++ Empty.flatMap(n => [n,n + 1])
= [1,2] ++ [2,3] ++ Empty
= [1,2,2,3]
```



## 21. Case Classes

### 21.1 Case Classes

There is a problem that for lightweight data structure (like class person), we need to reimplement all sorts of boilerplate like `companion objects`, `standard methods ` for serialising and for `toString`, `equals`, `hasCode`

Case classes are an ideal solution to this problem. 

```scala
case class Person(name: String, age: Int)
```

The `case` keyword does the following things:

1. **class parameters are promoted to fields**

默认为主构造函数参数列表的所有参数前加 val

```scala
case class Person(name: String, age: Int)
val jim = new Person("Jim", 34)
println(jim.name)  //valid expression
```

>  Instead:
>
> ```scala
> class Person(name: String, age: Int)
> val jim = new Person("Jim", 34)
> println(jim.name)  //invalid expression
> ```

2. **sensible toString**

```scala
case class Person(name: String, age: Int)
val jim = new Person("Jim", 34)
println(jim.toString)
```

Result:

```
Person(Jim,34)
```

> Instead:
>
> ```scala
> class Person(name: String, age: Int)
> val jim = new Person("Jim", 34)
> println(jim.toString)
> ```
>
> Result:
>
> ```
> ScalaPlayground.Person@7b69c6ba
> ```

- Syntactic Sugar:  

```
println(jim.toString) 
// equals to
println(jim)
```

println(instance) = println(instance.toString)

3. **`equals` and `hashCode` implemented out of the box**

添加天然的 hashCode、equals 和 toString 方法。由于 == 在 Scala 中总是代表 equals，所以 case class 实例总是可比较的

```scala
val jim2 = new Person("Jim", 34)
prinln(jim == jim2)
```

Result:

```
true
```

4. **Case classes have handy copy methods**

生成一个 `copy` 方法以支持从实例 a 生成另一个实例 b，实例 b 可以指定构造函数参数与 a 一致或不一致

```scala
val jim3 = jim.copy(age = 45)
println(jim3)
```

Result:

```
Person(Jim, 45)
```

5. **Case classes have companion objects**

创建 case class 和它的伴生 object

```scala
val thePerson = Person
```

It delegates to the Person's `apply` method. The companion object's apply method does the same thing  as the constructor. So in practice, we don't need to use the keywork new when instantiating a case class

实现了 apply 方法让你不需要通过 new 来创建类实例

```scala
val mary = Person("Mary", 23)
```

6. **Case classes are serialisable**

It makes classes especially useful when dealing with distributed systems. We can send instances of case classes through the network and in between JVM.

7. **Case classes have extractor patters**

This means case classes can be used in pattern matching

### 21. 2 Case Objects

```scala
case object UnitedKindom {
  def name: String = "The UK of GB and NI"
}
```

Case objects have the same property as case classes except they don't get companion objects because they are their own companion objects.

### 21.3 Exercise

Expand MyList using case classes and case objects

```scala
abstract class MyList[+A] {
  def head: A
  def tail: MyList[A]
  def add[B >: A](element: B): Mylist[B]
  def printElements: String
  override def toString: String = "[" + printElements + "]"
  def map[B](transformer: MyTransformer[A, B]): MyList[B]
  def flatMap[B](tansformer: MyTransformer[A, MyList[B]]): MyList[B]
  def filter(predicate: MyPredicate[A]): MyList[A]
}

case object Empty extends MyList[Nothing] {
  def head: Nothing = throw new NoSuchElementException
  def tail: MyList[Nothing] = throw new NoSuchElementException
  def isEmpty: Boolean = true
  def add[B >: Nothing](element: B): MyList[B] = new Cons(element, Empty)
  def printElements: String = ""
  
  def map[B](transformer: MyTransformer[Nothing, B]): MyList[B] = Empty
  def filter(predicate: MyPredicate[Nothing]): MyList[Nothing] = Empty
  def ++[B :> Nothing](list: MyList[B]): MyList[B] = list
  def flatMap[B](tansformer: MyTransformer[Nothing, MyList[B]]): MyList[B] = Empty
}

case class Cons[+A](h: A, t: MyList[A]) extends MyList[A] {
  def head: A = h
  def tail: MyList[A] = t
  def isEmpty: Boolean = false
  def add[B >: A](element: B): MyList[B] = new Cons(element, this)
  def printElements: String = 
  	if (t.isEmpty) "" + h
  	else h + " " + t.printElements
  
  def filter(predicate: MyPredicate[A]): MyList[A] = 
  	if (predicate.test(h)) new Cons(h, t.filter(predicate))
  	else t.filter(predicate)
  def map[B](transformer: MyTransformer[A, B]): MyList[B] = 
  	new Cons(transformer.transform(h), t.map(transformer))
  def ++[B :> A](list: MyList[B]): MyList[B] = new Cons(h, t ++ list)
  def flatMap[B](tansformer: MyTransformer[A, MyList[B]]): MyList[B] = transformer.transform(h) ++ t.flatMap(transformer) 
}
```

Testing:

```scala
val listOfIntegers: MyList[Int] = new Cons(1, new Cons(2, new Cons(3, Empty)))
val cloneListOfIntegers: MyList[Int] = new Cons(1, new Cons(2, new Cons(3, Empty)))
```

```scala
println(cloneListOfIntegers == listOfIntegers)
```

Result:

```
true
```

<img src="https://s1.ax1x.com/2020/10/14/05VKa9.png" width="500">



## 22. Exceptions

Example:

```scala
val x:String = null
println(x.length)
// this will crash with a NullPointerException
```

### 22.1 Throw an Exception

- Use `throw` keyword

```scala
throw new NullPointerException
```

It returns a `Nothing`

```scala
val aWeirdValue = throw new NullPointerException
```

```scala
val aWeirdValue: String = throw new NullPointerException
// also valid because Nothing is a valid substitute for any other type.
```

### 22.2 `throwable` class

- throwable classes extend the Throwable class

- `Exception` and `Error` are the major Throwable subtypes

> Both exceptions and errors will crash JVM, but exceptions and errors are different in their semantics
>
> - `Exceptions` denote something that went wrong with the program. (e.g., null pointer exception)
> - `Errors` denote something that happened wrong with the system. (e.g., Stack overflow error)

### 22.3 Catch an Exception

```scala
def getInt(withExceptions: Boolean):Int = 
	if (withExceptions) throw new RuntimeException("No Int for you")
	else 42

try {
  // code that might throw
  getInt(true)
} 
catch {
	case e: RuntimeException => println("caught a Runtime exception")  
}
finally {
  // code that will get executed no matter what
  println("Finally")
}
```

`getInt` with the parameter `true` tries to throw a runtime exception, and it got caught in the `catch` block. The case `e` runtime exception is a pattern for the exception that got thrown. The `=> println("caught a Runtime exception")  ` expression got evaluated which had the side effect of printing to the console

```scala
def getInt(withExceptions: Boolean):Int = 
	if (withExceptions) throw new RuntimeException("No Int for you")
	else 42
```

```scala
try {
  // code that might throw
  getInt(true)
} 
catch {
	case e: NullPointerException => println("caught a Runtime exception")  
}
finally {
  // code that will get executed no matter what
  println("Finally")
}
```

Now `e` catches Null pointerException, and this programming will crash.

- `finally ` block is optioanl and also **`finally` does not influence the return type of the `try/catch`expression**

```scala
val potentialFail = try {
  getInt(true)
} 
catch {
	case e: RuntimeException => 43
}
finally {
  println("Finally")
}

println(potentialFail)
```

Result:

```shell
43
```

The `try` returns an `Int` and `catch` also returns an `Int`, so the type of `potentialFail` is `Int`

```scala
val potentialFail = try {
  getInt(true)
} 
catch {
	case e: RuntimeException => println("caught a Runtime exception")
}
finally {
  println("Finally")
}

println(potentialFail)
```

Result:

```shell
caught a Runtime exception
Finally
()
```

The `try` returns a `Int` and `catch` returns an `unit`, so the compiler tries to unify `int` and `unit`. Thus, the type of `potentialFail` is `AnyVal`

- Use `finally` only for side effects

  > E.g. loging sth. to a file

### 22.4 Define Our Own Exceptions

Exceptions are instances of special classes that derive from `Exception` or `Error`

```scala
class MyException extends Exception
val exception = new MyException

throw exception
```

1. Crash your program with an OutOfMemoryError (OOM)

```scala
val array = Array.ofDim(Int.MaxValue)
```

2. Crash with StackOverflowError (SO)

```scala
def infinite: Int = 1 + infinite
```

3. PocketCalculator

- add(x,y)

- subtract(x,y)

- multiply(x,y)

- devide(x,y)

  >  Throw:
  >
  > - OverflowException if add(x,y) exceeds Int.MAX_VALUE
  > - UnderflowException if subtract(x,y) exceeds Int.MIN_VALUE
  > - MathCalculationException for division by 0

```scala
class OverflowException extends RuntimeException
class UnderflowException extends RuntimeException
class MathCalculationException extends RuntimeException("Division by 0")

object PocketCalculator {
  def add(x: Int, y: Int) {
    val result = x + y
    // a positive value puls a positive value giving a negative value means that overflown integer
    if (x > 0 && y > 0 && result < 0) throw new OverflowException
    else if (x < 0 && y < 0 && result > 0) throw new UnferflowException
    else result
  }
  
  def subtract(x: Int, y: Int) = {
    val result = x - y
    if (x > 0 && y < 0 && result < 0) throw new OverflowException
    else if (x < 0 && y > 0 && result > 0) throw new UnferflowException
    else result
  }
  
  def multiply(x: Int, y: Int) = {
    val result = x - y
    if (x > 0 && y > 0 && result < 0)throw new OverflowException
    else if (x < 0 && y < 0 && result > 0)throw new OverflowException
    else if (x > 0 && y < 0 && result > 0)throw new underflowException 
    else if (x < 0 && y > 0 && result > 0)throw new underflowException
    else result
  }
  
  def divide(x: Int, y: Int) = {
    if (y == 0) throw new MathCalculationException
    else x / y
  }
  
  println(PocketCalculator.add(Int.MaxValue, 10))
  println(PocketCalculator.divide(2, 0))
}
```

<img src="https://s1.ax1x.com/2020/10/14/05RHdx.png" width="500">



## 23. Packaging and Imports

### 23.1 what is a package

- A package is basically just a bunch of definitions grouped under the same name. In 99% of the time, this matches directory structure.

- Members within a package are visible/accessible by using their symbol name.

For example, the project structure is as follows:

```scala
.
├── rock-the-jvm-scala-beginners.iml
├── scala-beginners.iml
└── src
    ├── lectures
    │   └── part2oop
    │       └──CaseClasses.scala
    └── playground
        └── ScalaPlayground.scala

```

In `CaseClasses.scala`

```scala
package lectures.part2oop
//...
object CaseClasses extends App {
  // ...
  case object UnitedKingdom {
    def name: String = "The UK of GB and NI"
  }
}
```

In `ScalaPlayground.scala`

```scala
package playground
import lectures.part2oop.CaseClasses.UnitedKingdom

val country = UnitedKingdom
```

We have to `import` a package that we want to use

If we don't want  `import`, we have to use `fully qualified name`

- Fully Quanlified name:

```scala
package playground

val country = lectures.part2oop.CaseClasses.UnitedKingdom
```

- Packages are ordered hierarchically

The hierarchy is given by this dot `.` notation .

E.g. The `part2oop` package is a sub-package of `lectures` package

### 23.2 Package Object

We can now only write classes and traits and objects and we can only access values or methods or constants from them. Nut we might need to have some kind of universal constants or universal methods that reside outside classes/traits/.. so we don't need to resort to classes to access them. Package Objects are created for this purpose.

```scala
package lectures


package object part2oop {
  def sayHello: Unit = println("Hello, Scala")
  val SPEED_OF_LIGHT = 299792458
}
```

- **Package objects can only be one per package**

- The naming convention of package objects file is `package.scala`

Inside this package object, we can define method or constants and use them by their name throughout the entire rest of the package.

In `CaseClasses.scala`

```scala
sayHello
val speed = SPEED_OF_LIGHT
```

### 23.3 Import Package

1. Import two or more package

```scala
import playground.{PrinceCharming, Cinderella}
```

2. Import all sub-package

```scala
import playground._
```

Only use underscore`_` if you actually need it.

3. Name aliasing at imports

```scala
import playground.{PrinceCharming, Cinderella => Princess}

val princess = new Princess
```

This feature is useful if for some reason you need to import more than one class with the same name from different packages. This aliasing will solve naming conflicts. 

```scala
import java.util.Date
import java.sql.Date
val d = new Date // compiler will assume this is the first import
```

To fix it:

- use full qualified name

```scala
val date = new Date
val sqlDate = new java.sql.Date(2018,5,4) 
```

- use aliasing

```scala
import java.util.Date
import java.sql.[Date => SqlDate]

val date = new Date
val sqlDate = new sqlDate(2018,5,4) 
```

4. Default imports

Default imports are packages that are automatically imported without any intentional import from your side. 

Some examples includes:

- `java.lang`: String, Object, Exception etc.
- `scala`: Int, Nothing, Function etc.
- `scala.Predef`: println, ??? etc.



# Section 3: Functional Programming in Scala



## 24. What's a Function?

#### 24.1 Intro

The whole purpose of the functional programming section is to use and work with **functions as first class elements**.

However, the problem is we come from an Object Oriented world. So basically everything is an object that means its an instance of some kind of class. This is how the JVM was originally designed. **So the only way we could simulate functional programming was to use classes in instances of those**

```scala
trait MyFunction[A, B] {
  def apply(element: A):B 
}

val doubler = new Myfunction[Int, Int] {
  override def apply(element: Int): Int = element * 2
}

println(doubler(2))
```

Result:

```
4
```

So far, `doubler` is an instance of a function like class which can be called like a function.

Scala supports these function types out of box:

- `function types`are `Function1` or `Function2`...`Function22`

```scala
val stringToIntConverter = new Function1[Strinbg: Int] {
  override def apply(string: String): Int = String.toInt
}

println(stringToIntConverter("3") + 4)
```

Result:

```scala
7
```

**Scala supports these function types up to 22 parameters**

```scala
val adder: Function2[Int,Int,Int] = new Function2[Int, Int, Int] {
  override def apply(a: Int, b: Int): Int = a + b
}
```

#### 24.2 Syntactic Sugar:

- Function types `Function2[A, B, R]`  can be written as `(A,B) => R`

```scala
val adder: (Int,Int) => Int = new Function2[Int, Int, Int] {
  override def apply(a: Int, b: Int): Int = a + b
}
```

**All Scala functions are objects or instances of classes deriving from Function1, ..., Function22**

Exercise:

1. a function which takes 2 strings and concatenates them

```scala
val concatenator: (String,String) => String = new Function2[String, String, String] {
  override def apply(a: InStringt, b: String): String = a + b
}
```

2. transform the MyPredicate and MyTransformer into function types

```scala
//trait MyPredicate[-T] {
//  def test(elem: T): Boolean
//}

//trait MyTransformer[-A, B] {
//  def transform(elem: A):B
//}
```

- `MyPredicate` is basically a funtion type from T => Boolean
- `MyTransformer` is basically a funtion type from A => B

The `MyPredicate` and `MyTransformer` types do not make sense any more, because we now have `Function` types. So we can safely delete them.

```scala
abstract class MyList[+A] {
  def head: A
  def tail: MyList[A]
  def add[B >: A](element: B): Mylist[B]
  def printElements: String
  override def toString: String = "[" + printElements + "]"
  def map[B](transformer: (A => B): MyList[B]
  def flatMap[B](tansformer: (A => MyList[B]): MyList[B]
  def filter(predicate: A => Boolean): MyList[A]
}

case object Empty extends MyList[Nothing] {
  def head: Nothing = throw new NoSuchElementException
  def tail: MyList[Nothing] = throw new NoSuchElementException
  def isEmpty: Boolean = true
  def add[B >: Nothing](element: B): MyList[B] = new Cons(element, Empty)
  def printElements: String = ""
  
  def map[B](transformer: Nothing => B): MyList[B] = Empty
  def filter(predicate: Nothing => Boolean): MyList[Nothing] = Empty
  def ++[B :> Nothing](list: MyList[B]): MyList[B] = list
  def flatMap[B](tansformer: Nothing => MyList[B]): MyList[B] = Empty
}

case class Cons[+A](h: A, t: MyList[A]) extends MyList[A] {
  def head: A = h
  def tail: MyList[A] = t
  def isEmpty: Boolean = false
  def add[B >: A](element: B): MyList[B] = new Cons(element, this)
  def printElements: String = 
  	if (t.isEmpty) "" + h
  	else h + " " + t.printElements
  
  def filter(predicate: A => Boolean): MyList[A] = 
  	if (predicate(h)) new Cons(h, t.filter(predicate))
  	else t.filter(predicate)
  def map[B](transformer: A => B): MyList[B] = 
  	new Cons(transformer(h), t.map(transformer))
  def ++[B :> A](list: MyList[B]): MyList[B] = new Cons(h, t ++ list)
  def flatMap[B](tansformer: A => MyList[B]): MyList[B] = transformer(h) ++ t.flatMap(transformer) 
}
```

**Higer order functions**: either receive functions as parameters or return other functions as result.

3. define a function which takes an argument Int returns another function which takes an Int and returns an Int

   - What's the type of this function

     > Function1[Int, Function1[Int, Int]]

   - how to do it

```scala
val superAdder: Function1[Int, Function1[Int, Int]] = new Function1[Int, Function1[Int, Int]] {
  override def apply(x: Int): Function1[Int, Int] = new Function1[Int, Int] {
    override def apply(y: Int): Int = x + y
  }
}
```

```scala
val adder3 = superAdder(3)

println(adder3(4))
println(superAdder(3)(4))  // curried function
```

Result:

```
7
7
```

- **Curried function have the property that they can be called with multiple parameter lists** 

- A curried function receives some kind of parameter and returns another function which receives parameters.

<img src="https://s1.ax1x.com/2020/10/15/07CPne.png" width="500">



## 25. Anonymous Functions

### 25.1 Lambda

#### 25.1.1 Intro

Object Oriented way of defining an anonymous function and instantiating it on the spot:

```scala
val doubler = new Function1[Int, Int] {
  override def apply(x: Int) = x * 2
}
```

In Scala, we can simply write this way:

```scala
val doubler = (x: Int) => x * 2
```

Its called **anonymous function** or **a lambda**. The name lambda comes from the term lambda calculus, which is the mathematical representation of functional programming.

the lambda thing `(x: Int) => x * 2` is a value which is an instance of Funtion1

- Single Parameter

```scala
// we can also define this way 
val doubler: Int => Int = x => x * 2
```

- Multiple Parameter

```scala
val adder: (Int, Int) => Int = (a: Int, b: Int) => a + b
```

- No Paramter

```scala
val justDoSomething: ()=> Int = () => 3
```

```scala
// careful
println(justDoSomething)  //function itself
println(justDoSomething()) // actual call
```

Result:

```
playground.ScalaPlayground$$$Lambda$17/0x00000008000c0c40@76a3e297
3
```

**In OOP, we can call no-paramter methods without `()`, but when it comes to lambdas, we must  call them with `()`**

#### 25.1.2 Curly brace with lambda

```scala
val stringToInt = {
  (str: String) => Str.toInt
}
```

### 25.2 Syntactic Sugar

#### 25.2.1 `=>` 

As the most simplified answer, you can substitute whatever is on the left-hand side of `=>` with the word "LEFT" and whatever is on the right-hand side with the word "RIGHT".

Then, the meaning of "**LEFT => RIGHT**" becomes:

**Take LEFT then do RIGHT.**

This means that if you have a "()=>" that you can take nothing (that is, no parameters) and then do whatever is on the right-hand side.

#### 25.2.2 `_` 

**`_` underscore stands for a different parameter.**

- Increment

```scala
val niceIncrement: Int => Int = _ + 1 // equivalent to x => x + 1 
```

- Add

```scala
val niceAdder:(Int, Int) => Int = _ + _ // equivalent to (a,b) => a + b 
```

### 25.3 Exercises

1. MyList: replace all FunctionX calls with lambdas

   > ```scala
   > println(listOfIntegers.map(new MyTransformer[Int, Int]{
   >   override def transform(elem: Int): Int = elem * 2
   > }).toString)
   > 
   > println(listOfIntegers.filter(new MyPredicate[Int]: Boolean {
   >   override def test(elem: Int) = elem % 2 == 0
   > })
   >         
   > println(listOfIntegers.flatMap(new MyTransformer[Int, MyList[Int]] {
   >   override def transform(elem: Int): MyList[Int] = new Cons(elem, Cons[elmen + 1, Empty])
   > }).toString)
   > ```

```scala
println(listOfIntegers.map(elem => elem * 2).toString)
// println(listOfIntegers.map(_ * 2).toString)
println(listOfIntegers.filter(elem => elem % 2 == 0)
// println(listOfIntegers.filter(_ % 2 == 0)
println(listOfIntegers.flatMap(elem: Int => new Cons(elem, Cons(elmen + 1, Empty))).toString)
```

2. Rewrite the "special" adder as an anonymous function

   > ```scala
   > val superAdder: Function1[Int, Function1[Int, Int]] = new Function1[Int, Function1[Int, Int]] {
   >   override def apply(x: Int): Function1[Int, Int] = new Function1[Int, Int] {
   >     override def apply(y: Int): Int = x + y
   >   }
   > }
   > ```

```scala
val superAdder = (x: Int) => (y: Int) => x + y
```

<img src="https://s1.ax1x.com/2020/10/15/07epcR.png" width="500">



## 26. Higer-Order-Functions and Curries

```scala
object HOFsCurries extends App{
  val superFunction: (Int, (String, (Int => Boolean)) => Int) => (Int => Int) = ???
}
```

### 26.1 Higer-Order-Functions (HOFs)

Function that applies a function n times over a value x:

```scala
//nTimes(f, n, x)
//nTimes(f, 3, x) = f(f(f(x))) = nTimes(f, 2, f(x))
//nTimes(f, n, x) = f(f(...f(x))) = nTimes(f, n-1, f(x))
def nTimes(f: Int => Int, n:Int ,x: Int): Int = {
  if (n <= 0) x
  else nTimes(f, n - 1, f(x))
}
```

Testing:

```scala
val plusOne = (x: Int) => x + 1
println(nTimes(plusOne, 10, 1))
```

Result:

```
11
```

Better:

```scala
// nTimesBetter = x => f(f(f...f(x)))
// increment10 = nTimesBetter(plusOne, 10) = x => plusOne(plues(One)...(x))
def nTimesBetter(f: Int => Int, n: Int): (Int => Int) = 
	if (n<=0) (x: Int) => x
	else (x: Int) => nTimesBetter(f, n-1)(f(x))
```

Testing:

```scala
val plus10 = nTimesBetter(plusOne,10)
println(plus10(1))
```

Result:

```
11
```

### 26.2 Curried Functions

```scala
val superAdder:Int => (Int => Int) = (x: Int) => (y: Int) => x + y
```

Testing:

```scala
val add3 = superAdder(3) // y => 3 + y
println(add3(10))
```

Result:

```
13
```

- Functions with multiple parameter lists

```scala
def curriedFormatter(c: String)(x: Double): String = c.format(x)
```

Testing:

```scala
val standardFormat: (Double => String) = curriedFormatter("%4.2f")
val preciseFormat: (Double => String) = curriedFormatter("%10.8f")

println(standardFormat(Math.PI))
println(preciseFormat(Math.PI))
```

Result:

```
3.14
3.14159265
```

