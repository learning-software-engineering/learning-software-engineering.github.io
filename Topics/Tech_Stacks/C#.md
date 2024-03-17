# C#

## Introduction

C# is a multi-paradigm, object-oriented, imperative programming language. It has excellent support for concurrency and asynchronous programming, amazing integration with all components of the Microsoft tech stack and ecosystem. Despite having managed memory and being a garbage-collected language, it is suitable for both high and low-level applications through the use of unsafe contexts which permit manually managed memory.

One of the major differentiators between C# and other similar languages is the C# language’s commitment to excellent developer UX through providing syntactic sugar to simplify complex tasks and reduce the workload on developers when implementing common patterns and paradigms.

## Why Use C#

C# is an excellent choice for applications where cross-platform support is not a strong requirement, speed and memory efficiency are priorities, and especially when integrating with other components of Microsoft’s stack such as MSSQL Server.

### Cross-Platform Capabilities

While the .NET runtime is cross-platform and can be run on either Windows or Linux, the compatibility of different libraries and extensions to the language varies by platform. For small projects where few external dependencies will be brought in, it is likely ok to plan for cross-platform support, but for larger projects, it is probably better to pick a target platform and stick with it. With that said, either Windows or Linux are suitable host operating systems as the runtime is compatible with either, but once you have selected one, switching the host operating system can be challenging regardless of which you are using.

### Speed and Memory

C# is fast. As a language, C# is often thought of as Microsoft’s version of Java, but if you really compare the two, you will notice one is considerably faster than the other. Both languages compile into their own platform-independent, intermediate bytecode and then run on their own runtimes (CLR vs JVM), and both make use of JITs to speed up execution considerably, but C# with the .NET runtime manages to be much faster than Java on the JVM ([source](https://benchmarksgame-team.pages.debian.net/benchmarksgame/fastest/csharp.html)).

When it comes to memory management, C# again offers a lot more than Java. Like Java, C# is garbage-collected and does not normally allow for the manual allocation of memory, nor for the use of pointers to manually access unmanaged memory. However, unlike Java, C# has a language feature called unsafe contexts. In an unsafe context, the developer can manually allocate unmanaged memory, make use of pointers, and perform a variety of other low-level memory operations that make C# suitable for performance-critical applications that require very low-level memory management, provided these applications run on a platform fully capable of running the CLR.

### Microsoft Ecosystem

When working with the Microsoft ecosystem, C# is a no-brainer as a part of the stack. When working with MSSQL Server, for instance, C# provides better optimized and more efficient connection options through either the ADO .NET or Entity Framework libraries when compared to other languages that must connect through OLE DB. The extra levels of abstraction in OLE DB that permit it to be so widely used, also add overhead which slows the speed of operations when compared to ADO.NET or the Entity Framework.

C# provides similar advantages when working with Azure Cloud services, and all other things Microsoft.

### Developer Experience

C# is just generally a joy to program in. The vast array of syntactic sugar and language features means that there
is a slick, clean way to do basicallly anything you need. Furthermore, this is all done within the confines of a 
static type system that leaves most code in great shape for static analysis. The garbage collection removes the
messy overhead of manual memory management, and even though it's not as low level as something like C++,
it is stil a blazingly fast language.

## Language Features

### Asynchronous Programming and Concurrency

C# was actually the first major language to use the now ubiquitous `async` and `await` keywords (which many mistakenly believe originated in JavaScript). The language has excellent support for both asynchronous and synchronous concurrency models. Many APIs are available with varying levels of customization exposed to the developer. These pieces of syntactic sugar provide the developer with many options for asynchronous concurrent programming.

For basic control over threads and synchronous threading, the `System.Threading` namespace is available. This namespace provides options to spawn and synchronize new threads, and also provides a variety of synchronization primitives like locks and monitors.

C# also has a variety of APIs for thread-safe collections, and pre-built abstractions implementing common synchronous threading patterns. For instance, the `Systems.Threading.Tasks.Parallel` class contains static methods for concurrently processing collections, and the System.Collections.Concurrent namespace contains classes such as `ConcurrentBag` — a thread safe implementation of a set data structure.

Read more about asynchronous programming in C# [here](https://learn.microsoft.com/en-us/dotnet/standard/asynchronous-programming-patterns/), threading [here](https://learn.microsoft.com/en-us/dotnet/standard/threading/managed-threading-basics), and parallel programming in C# [here](https://learn.microsoft.com/en-us/dotnet/standard/parallel-programming/).

### Properties

C# also has properties, a piece of syntactic sugar allowing language users to avoid the endless getter-setter boilerplate that plagues comparable object-oriented languages like Java. This language feature allows for easy read-only and write-only access to fields with simple syntax.

string readonlyString { get; } = “This is a readonly string”;

private string _S = null;

string writeOnlyString
{
	set {
		_S = value;
	}
}

You can read more about properties [here](https://learn.microsoft.com/en-us/dotnet/csharp/properties).

### Tuples

C# has an excellent piece of syntactic sugar to replicate tuples, a popular language feature from languages like Python that provides an easy to use, immutable collection of variables of multiple types. In C#, this is possible through the System.ValueTuple class, which provides a type accepting multiple generic type parameters that allow for specifying the contents of the tuple.

C# has many pieces of syntactic sugar to simplify declaring an instance of ValueTuple. Using a bracket-enclosed list of types as a type will be expanded to a corresponding ValueTuple type at compile time, and you can even use the var keyword to have the compiler infer the type of the tuple at compile-time.

(int, string) tuple = (1, “This is a string”);

var tuple = (1, “This is a string”);

You can read more about tuples [here](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/value-tuples).

### Reference and Value Types

Every type in C# falls into one of two categories: reference or value. A reference type is a type that is passed by reference, while a value type is passed by value. Value types include all primitives, any structs, any enums, and tuples. Everything else is a reference type.

You can read more about reference and value types [here](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/builtin-types/value-types).

### Dynamic Typing and Type Inference

C# is a statically-typed language, but it is one with excellent and comprehensive support for both dynamic typing and type inference. Variables are normally declared with a static type in C#. Through the var keyword, variables can be declared without explicitly declaring a type, allowing the compiler to infer the type of the variable at compilation time. For fully dynamically typed variables, the dynamic keyword allows the type of a variable to be determined at runtime. This allows for redefining the type of a variable at runtime, but doesn’t permit a lot of compile time error checking. 

Languages like TypeScript offer a similar level of flexibility between dynamic and static types, but C#’s system works better and requires fewer sketchy work-arounds as TypeScript is fundamentally trying to make a dynamically typed language statically typed while C# expands the language’s static type system to allow a single dynamic type. This means unless explicitly making use of the dynamic type, the language is statically typed, and works well as a statically typed language (which TypeScript occasionally does not).

You can read more about C#’s type inference [here](https://www.c-sharpcorner.com/UploadFile/mahesh/type-inference-in-C-Sharp/), or about dynamic typing [here](https://learn.microsoft.com/en-us/dotnet/csharp/advanced-topics/interop/using-type-dynamic).

### IDisposable Interface

For classes that make use of system resources, and that must then release those resources, C# provides the IDisposable interface. Classes that implement this resource can be used in using blocks which allow developers to automatically dispose and release consumed system resources at the end of the using scope.

using (var sw = File.CreateText(filePath))
{
sw.WriteLine("First Line");
sw.WriteLine("Second Line");

// StreamWriter is disposed of here
}

You can read more about the using keyword and the IDisposable interface [here](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/statements/using).

### String Interpolation

Like Python's f-strings, C# has easy syntactic sugar for string interpolation. In C# this is done by
prepending a \$ in front of the string, and inserting variable names between curly brackets.

For instance the Python f-string f'Hi {name}' would be

\$"Hi {name}"

in C#.

### Delegates

Like Java and most modern languages, C# has options for developers to make use of first-class functions through their delegate types. A delegate is a type representing a method in C#, similar to a single-method interface in Java. Like both Java’s lambda expressions and JavaScript’s arrow functions, C# has features that permit inline definition of delegate types through the => (lambda) operator. Delegate types can be declared from scratch with the delegate keyword, but are more commonly declared using the Action or Func generic classes. Action represents a delegate returning void while Func represents a delegate that returns a value. Either class can accept a list of arguments.

You can read more about delegates in C# [here](https://learn.microsoft.com/en-US/dotnet/csharp/programming-guide/delegates/).

### Null Coalescing

The null coalescing operator in C# allows developers to easily provide a ‘default value’ in cases when a nullable variable is null. This pairs well with the C# nullable type definition operator that allows making any type nullable. Consider the following example that makes use of the Color type, which is a value type and is normally not nullable.

// Declare a variable called c that uses the question mark after the type to indicate
// that it can be null
Color? c = null;

// Use the null coalescing operator (??) to print a ‘default value’ for
// the c variable
Console.WriteLine($“{c ?? new Color(0, 0, 0)}”);

You can read more about null coalescing in C# [here](https://www.geeksforgeeks.org/null-coalescing-operator-in-c-sharp/).

## C# For Web

C# offers two main ways of writing APIs and code for the web: the ASP.NET API and the MinimalAPI API.

### ASP .NET

ASP is the traditional way of writing HTTP APIs with C#. It provides a nice, object-oriented way of writing APIs. This is an older paradigm and is very familiar to many developers. There is also a wide range of documentation and examples available online.

You can read more about ASP .NET [here](https://learn.microsoft.com/en-us/aspnet/overview).

### MinimalAPI

The MinimalAPI paradigm, on the other hand, is a newer way of writing HTTP APIs with C#. Unlike ASP .NET, it follows a more functional approach, and allows developers to skip a lot of the boilerplate involved in writing for ASP .NET and for object-oriented code in general. As a newer technology, it is easier to use, but less mature and there may be fewer pieces of documentation and tutorials available.

You can read more about MinimalAPI [here](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/minimal-apis/overview?view=aspnetcore-8.0).

## C# For Databases

C# is a common choice of language when working with a Microsoft SQL Server (MSSQL Server) database. It provides two main ways to interact with the database, and some language features that dramatically improve the developer experience when interacting with the database.

### ADO .NET

ADO .NET provides data access objects for databases. It can be used to connect to a database with the Connection class, and to execute arbitrary queries on that database. In general, this is a great choice for applications that require a slightly higher level of control than what you get going through an ORM or similar technology (I.E. Entity Framework). If you need well-optimized queries and niche T-SQL language features, this is probably the best approach for you.

You can read more about ADO .NET [here](https://learn.microsoft.com/en-Us/dotnet/framework/data/adonet/).

### Entity Framework

The Entity Framework is C#’s baked in ORM. It offers the same features as any other ORM: mapping database entities to model classes, simplified data fetching, and easy data modification. All of this is at the expense of less control over the underlying queries, and as a result, a potentially less optimized data access layer.

You can read more about the Entity Framework [here](https://learn.microsoft.com/en-us/aspnet/entity-framework). 

### LINQ

LINQ stands for Language Integrated Queries. This is a language feature that allows for natively querying a data source from within the C# language. C# can convert these queries into SQL, REST API requests, or even other C# code depending on the data source being queried. This massively simplifies the process of fetching data from external sources, and provides a unified, source-agnostic interface when bringing any kind of external data into the application.

The LINQ documentation page provides the following example querying an in-memory array, but the process and syntax is identical regardless of the source of the data being queried.

// Specify the data source.
int[] scores = [97, 92, 81, 60];

// Define the query expression.
IEnumerable<int> scoreQuery =
    from score in scores
    where score > 80
    select score;

You can read more about LINQ [here](https://learn.microsoft.com/en-us/dotnet/csharp/linq/).

## Additional Resources

You can download the .NET SDK [here](https://dotnet.microsoft.com/en-us/download) to get started using this life-changing language that will make you understand how Microsoft earned its 3 trillion (as of 2024-03-17) market cap.
