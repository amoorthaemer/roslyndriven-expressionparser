# Roslyn Driven Expression Parser

I started this project because I needed an expression parser that could generate an expression tree from not only single line, but also multiline C# code. The expression parsers found on NuGet where not sufficient to fullfill my needs (except for `CSharpScript`, but that one generates an assembly which is loaded into memory and never gets unloaded) 

So I took a deep dive into Roslyn and with a lot of debugging and sparse documentation I gpt enough basis to get started. This project is the result of these efforts.

# What's included?

In essence the parser can handle any C# code that leads to a lambda function (e.g. an `Expression<TDelegate>`, where `TDelegate` is either a `Func<...>`, an `Action` or an `Action<...>`). Which automatically excludes any class/record/struct/interface declaration and it's containing code. If you need such functionality use Roslyn itself to handle that for you.

Also the parser is based on C# language version 9, so you have all of the nifty C# syntactic sugar at your disposal. NOTE: pattern expressions are not (yet) supported.

## So how about async/await?

That's a totally different cookie to crack. Async/await is currently not supported by the `Expression` class, although there is a library that has at least support for an 'await' expression and I'm looking into this to support at least some basic functionality

## LINQ expressions

To be able to use the expression parts to generate LINQ expressions and using them in for example as a filter, you're just as limited in your toolset as the C# editor subscribes. Which means: single line only and no methods that returns a `ref` or `out` parameter.

# Documentation

(TODO)
