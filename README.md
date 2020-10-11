[TOC]

# 1. Getting Started

```scala
package playground
object ScalaPlayground extends App{
  prinln("Hello Scala")
}
```

- *extends APP* will automatically insert a main function for this object 



# 2. Values, Variables & Types

#### 2.1 values 

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

#### 2.2 Variables

```scala
var aVariable: Int = 4
aVariable = 5 // compiler will not complain
```

- Variables are mutable and can be reassigned
- Variables are used for in functional programming as side effects



# 3. Expressions

#### 3.1 Operators

`+`, `-`, `*`, `/` , `&`, `|` , `<<` , `>>`, 

`>>>`: right shift with zero extension

`==`, `!=`, `>`, `>=`, `<=`, `<`

`!`

`=`, `+=`, `-=`, ...(Changing a variable is called a side effect)

#### 3.2 Instructions VS Experssions

- Instructions: something that you tell the computer to do.

```
eg. Chaning a variable, print in the console...
```

- Expression: something that has a value and or a type

In functional programming, we'll think of expressions that is every single bit of your code will compute a value

##### 3.2.1 If Expression

```scala
// if expression
val aCondition = true
val aConditionValue = if (aCondition) 5 else 3
```

If expressions always return a result.

```scala
println(if (aCondition) 5 else 3)   // the result is 5
```

##### 3.2.2 loops

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

- **Side effects in Scala are actually expressions returning `unit`**

e.g. while loops, println(), reassig are side effects that also return a unit

##### 3.2.3 Code Blocks

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



# 4. Functions

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

### 4.2 Excerice

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



# 5. Type Inference

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



# 6. Recursion

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

- The tail recursion do not use enormours amount of memory to build up a large  indermediate expression

Recursion Order:

```
factHelper(n , a) = factHelper(n - 1, a * n)
First: computing (n - 1)
Second: computing (a * n)
Last: calling factHelper
```

- **The recursion is done at the LAST step**

The last expression of its code path is the facHelper. This allows Scala to preserve the same stack frame and not use additional stack frames for recursive.  

#### KEY: 

- **Use recursive call as the LAST expression.**
- **Use accumulators to turn a function into a tail recursive function**
- **The accumulators come from the base case**
- Accumulators store intermediate results rather than call the function recursively
- Once you made a tail recursion, add `@tailrec` before your function declaration, the compiler will check for you if the function respects the conditions for tail recursion, that way you are sure it will optimize the calls as expected.

### 6.3 Exercise

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



# 7. Call-By-Value and Call-By-Name

### 7.1 Intro

##### Call-By-Value

```scala
def calledByValue(x: Long): Unit = {
  println("by value:" + x)
  println("by value:" + x)
}
```

##### Call-By-Name

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



# 8. Default and Named Arguments

```scala
def facotial(n: Int, acc:Int = 1): Int = {
  if (n <= 1) acc
  else facotial(n - 1, n * acc)
}

// Call
facotial(10)
```

In this way, we acutally expose in a function in our API



# 9. Smart Operations on String

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



# 10. Object-Oriented Programming in Scala

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

# 11. Exercises for OOP in Scala

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



# 12. Syntactic Sugar: Method Notation

