---
layout: post
title: Kotlin Basics and Installation Guide using Android Studio
date: '2017-08-13 01:26:45'
tags:
- android
- kotlin
---

What is Kotlin?
Kotlin is JVM language. It is based on both object oriented and functional language.

- Can create classes, objects, Methods and also instances like object oriented language.
- As a Functional language supports creating higher order functions, collection of functions, passing function as parameter in other functions, returns functions in some functions.
- No need to write classes, declare variables and getters or setter methods.
- Less coding than Java for equivalent result.

####Installation steps:
In Android Studio ---> select preferences from menu options ----> select plugins ---> Install JetBrains Plugin and then click on kotlin plugin.

File Extension is .kt
kotlin compiler creates class when we run the app
- Kotlin function starts with 'fun' keyword.
```
fun main(args: Array<String>){
println("Hello world")
}
```
- It supports immutablity.
'val' is immutable (once assigned with value will not allow reassigning any other values)
'var' is mutable (can reassign to some values any time you want)
- String templates or interpolation 
```
var str:String = "kotlin programming"
println("Welcome to $str")
```
- Can use 'if' statement as an expression
```
val result = if(5 > 3){
"correct answer"
}else{
"wrong answer"
}
println(result)
```
####Functions:
Much easier to use functions.
Can use default and named parameters.
Can create extension functions.
Can create infix functions.
It supports overloading operators.
Supports tail recursion. (Avoids stack overflow error in case of heavy recursive logics)

####Interface:
Interface in kotlin is pretty much similar to Java.
By default interface is public, no need to declare it explicitly. There is no such 'implements' keyword.

####Class:
Kotlin classes are by default public and final. final classes and methods cannot be overridden. To allow overriding can use open keyword for either classes or methods.

####Sealed Classes:
- Used to restrict the class hierarchies.
- Value can have one of the types from a limited set, but cannot have any other types.
- Extension of enum classes.

####Constructors:
- Constructors part of class definition.
- It takes default parameters.

####Data classes:
- Provides a convenient way to override equals, hashCode and toString.
- Typically immutable classes
- Kotlin also generates 'copy' methods.







