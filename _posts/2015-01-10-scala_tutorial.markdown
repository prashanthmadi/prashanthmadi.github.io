---
layout: post
title: Scala Tutorial
date: '2015-01-10 17:29:00'
tags:
- scala
---

What is Scala ?

* Functional Programming (treats computation as the evaluation of mathematical functions and avoids state and mutable data)
* Pure Object oriented
* Supports Java Library / Framework Ecosystem
* It cuts down on boilerplate, so programmers can concentrate on the logic of their problems. 
To get data from url : `Source.fromURL(url, "UTF-8").mkString`
* It adds expressiveness, by tightly fusing object-oriented and functional programming concepts in one language.[Functional vs Object Oriented Programming](http://stackoverflow.com/questions/2078978/functional-programming-vs-object-oriented-programming)
* It protects existing investments by running on the Java Virtual Machine and interoperating seamlessly with Java.

**apply** : Function is an Object with an apply method

```
Object Hello { 
def apply(s:String) = "Hello" + world} 
println (Hello("world"))
```

**named** : normal way of creating functions

```
def sum(x:Int,y:Int):Int = { x+y }
```
**literal** : Functions can be assigned to variable

```
val add_one = (x:Int) => x+1 

add_one(3) // 4 
// Turning existing functions into literals 

val p = print _  // _ is something like we dont actually whatsoever value is 
p("Hi") 
// if you want to restrict your params 

val add_one:(Int) => Int = (x) => x + 1  // defines that it takes int and returns Int 
```

**Partial functions** : not all parameters info is provided

```
val add_one = sum(1,_:Int) 
add_one(5) // gives 6
```

**curried functions** [http://en.wikipedia.org/wiki/Currying](http://en.wikipedia.org/wiki/Currying)

```
vall addition = (sum _).curried // applies arguments in a sequence 
addition(5)(1)
```

**Higher-order functions** : functions that take functions as parameter[http://en.wikipedia.org/wiki/Higher-order_function](http://en.wikipedia.org/wiki/Higher-order_function)

```
// twice(f, 7) = f(f(7)) = (7 + 3) + 3. 
def f(x): 

return x + 3 

def twice(function, x): 

return function(function(x)) 

print(twice(f, 7)) 
```

####Pattern Matching :

```
def matchTest(x: Int): String = x match { 
case 1 => "one" 
case 2 => "two" 
case _ => "many" 
} 
```
whats the big deal ? . we can do the same with switch in java 

http://docs.oracle.com/javase/tutorial/java/nutsandbolts/switch.html</pre>

**Match on Class Instances**

```
var play = sport("cricket") 

play match{ 

case sport("football") => println("im playing football") 

case sport("cricket") => println("im playing cricket") 

case sport(_) => println("im unsure") 
}
```

**Match on Regular Expressions**

```
// val vs var 

val cricket ="^c.*" 
val football = "^f.*" 

val sport = "cricket" 

sport match{ 

case cricket : pl("playing cricket") 

case football : pl("playing football") 

case _ : pl ("xxx") 
}
```

[http://kerflyn.wordpress.com/2011/02/14/playing-with-scalas-pattern-matching/](http://kerflyn.wordpress.com/2011/02/14/playing-with-scalas-pattern-matching/)

Scala Closures [http://www.tutorialspoint.com/scala/scala_closures.htm](http://www.tutorialspoint.com/scala/scala_closures.htm) 

**Object** : object in scala is like the static portion of class in java.
[https://code.google.com/p/moviehub/source/browse/src/com/prashanth/test/MovieTesting.scala](https://code.google.com/p/moviehub/source/browse/src/com/prashanth/test/MovieTesting.scala)

**Class**
[http://www.tutorialspoint.com/scala/scala_classes_objects.htm](http://www.tutorialspoint.com/scala/scala_classes_objects.htm)

**Generics**:

```
class Stack[T] 
{ 
private val list = new List [T] 
def pop : T ={ } 
def peek : T = { } 
} 
Covariant +T   (Accepts any type that is sub class of T) 
Contravariant -T (Accepts any type that is super class of T)
```