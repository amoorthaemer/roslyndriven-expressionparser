# Roslyn Driven Expression Parser

I started this project because I needed an expression parser that could generate an expression tree from not only single line, but also multiline C# code. The expression parsers found on NuGet where not sufficient to fullfill my needs (except for `CSharpScript`, but that one generates an assembly which is loaded into memory and never gets unloaded) 

So I took a deep dive into Roslyn and with a lot of debugging and sparse documentation I gpt enough basis to get started. This project is the result of these efforts.

# What's included?

In essence the parser can handle any C# code that leads to a lambda function (e.g. an `Expression<TDelegate>`, where `TDelegate` is either a `Func<...>`, an `Action` or an `Action<...>`). Which automatically excludes any class/record/struct/interface declaration and it's containing code. If you need such functionality use Roslyn itself to handle that for you.

## Supported features

The following language features are fully supported:
* block syntax ({...})
* return <value>
* if/else
* while
* do/while
* for
* foreach
* switch/case/default
* try/catch
* try/finally
* try/catch/finally
* local functions
* inline lambda functions  (e.g. `var f = () => { ... }`)
* typeof, nameof, sizeof
* new
* with
* checked

NOTE: The parser is based on C# language version 9, so you have most of the nifty C# syntactic sugar at your disposal.

The following language features are not (yet) supported
* pattern expressions
* unsafe operations (e.g. pointers, `ref` locals (e.g. `return ref` or `readonly ref`)


## So how about async/await?

That's a totally different cookie to crack. Async/await is currently not supported by the `Expression` class, although there is a library that has at least support for an 'await' expression and I'm looking into this to support at least some basic functionality

## LINQ expressions

To be able to use the expression parts to generate LINQ expressions and using them in for example as a filter, you're just as limited in your toolset as the C# editor subscribes. Which means: single line only, no control flow statements and no methods that returns a `ref` or `out` parameter.

For example: `customer => customer.Name == "John"` 

# Documentation

(TODO)
