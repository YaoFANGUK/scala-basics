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

`=`, `+=`, `-=`, ...(Chaning a variable is called a side effect)

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

- **side effects in Scala are actually expressions returning unit**

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

- Stack Recuesion is **Inefficient**

```scala
def factorial(n: Int): Int = 
	if (n <= 1) 1
	else x * factorial(n - 1)
```

Example:

<img src="./images/recur1.jpeg" width="500">

Recursion Order:

```
  factorial(n) 
= n * factorial(n -1)
First: computing (n - 1)
Second: calling factorial
Last: computing mutiply (n * (...))
```

- Stack Recursion uses too much memory, which may leadt to stack overflow.

<img src="./images/recur2.png" width="500">

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



# 7. Call-By-Name and Call-By-Value

