---
date: 2019-02-24T09:05:25+02:00
title: "Building a RESTful WebApi with F# and NetCore"
description: In this article, we build a simple WebApi with F# and NetCore. Target is C# developers who want to know more about functional languages and F# in particular.
slug: building-a-restful-webapi-with-fsharp-and-netcore
share: false
---
It is a common misconception that F# is just for data science, machine
learning, and quantitative finance; in the .NET eco-system you turn to C#
for enterprise and web development and, eventually, you'll look at F# for
serious number crunching.

While it is undoubtedly true that functional languages are ideally suited for
solving numerical problems, some of them - and F# in particular - are
perfectly fine for tackling so many different domains other than scientific
ones. F# is a cross-platform, functional-first, general purpose language.
Stress on functional-first and general purpose. Line-of-business applications
are almost always perfect candidates for F# development. On this topic, I
recommend you take a look at Scott Wlaschin's "[Why F# is the best enterprise
language][1]"

On my part I am going to show you how easily we can build a RESTful WebAPI
with F# on NetCore, taking no compromises on its C# counterpart.

## Create, build, run

Open up your terminal and type the following:

    $ dotnet new webapi -o MyWebApi -lang f#
    The template "ASP.NET Core Web API" was created successfully.

The command above creates the `MyWebApi` directory and initializes an F#
WebApi project in it, which you can build right away:

    $ cd MyWebApi && dotnet build
    Microsoft (R) Build Engine version 15.9.20+g88f5fadfbe for .NET Core
    Copyright (C) Microsoft Corporation. All rights reserved.

    Build succeeded.
        0 Warning(s)
        0 Error(s)

And while we are at it, let's launch it:

    $ dotnet bin/Debug/<dotnetcoreapp_version>/MyWebApi.dll
    Now listening on: http://localhost:5000
    Now listening on: https://localhost:5001
    Application started. Press Ctrl+C to shut down.

Our WebApi is up and running, ready for us to play with it:

    $ curl -k https://localhost:5001/api/values
    ["value1","value2"]

The `-k` option tells `curl` to skip certificate verification on the https
connection to localhost. Alternatively, you can open the same URL from your
browser.

We did not write a single line of code, and yet we have a web API up and
running. Yes, this is the same experience we get when we create a C# WebApi
project. If you want to see that, try launching the same `dotnet new`
command, minus the `-lang` option.

## Show me the code

These days I use Visual Studio Code and the Unix (MacOS) terminal for most of
my development, be it Python, JavaScript, C#, or F#. If you are on Visual
Studio, you should still be able to follow along.

Let's fire up VSCode:

    code .

The F# development experience in VSCode is excellent thanks to the [Ionide
project][2], an open source cross-platform package for F# development. It
brings IntelliSense, tooltips, document formatting, syntax checking, error
highlighting, and more to VSCode. Just go to the Extensions tab and search
for Ionide. Once you install and activate the extension, a brand new F# tab
appears in VSCode. Click it. This tab lets you look at the project from the
F# perspective.

In F#, the file order matters. That's a consequence of another important
rule: in F#, the order in we define types does matter. Files at the bottom of
the project can access types and values defined above them, but not the other
way around. In the F# tab, stuff is ordered for you by dependency. You can
add new files, or move them up and down the hierarchy as needed.

Click on `Contollers/ValuesControllers.fs`, so we can view its code. It
begins like this:

    namespace MyWebApi.Controllers

    open Microsoft.AspNetCore.Mvc

F# namespaces work like C# ones. They allow you to organize data types and
modules (not functions!) and yes, you can nest them in a hierarchy. The
`open` statement, you guessed it, is F# flavor of C#'s `using`.

But! Where are the curly braces? Well, the thing is, in F# we don't need
curly braces. Don't run away now; we'll get back to this. 

Let's go on with the code review:

    [<Route("api/[controller]")>]
    [<ApiController>]
    type ValuesController () =
        inherit ControllerBase()

We decorate the `ValuesController` type (think C# classes) with two
attributes. First one defines the general route to the controller endpoints
(`/api/values/`); the second one informs .NET that `ValuesController` is, in
fact, a controller.

Finally, we get to look at one of the controller members:

    [<HttpGet>]
    member this.Get() =
        let values = [|"value1"; "value2"|]
        ActionResult<string[]>(values)

Again, very much like with C#, we have an attribute binding an HTTP method to
this member (`Get`). Every time a GET request hits the controller route,
`Get` executes. What's more interesting here, however, is the member scope.

For starters, no curly braces. F#, like Python and others, is a
whitespace-significant language: we indent code to tell the compiler that
we're in a nested scope. At first, coming from other .NET languages, this
might come as a shock. It sure was for me, although I had to make this jump
way back when I got first into Python.

Secondly, the `values` assignment has no type declaration what-so-ever. It
looks like we're dealing with a dynamic language like JavaScript or, again,
Python. Only, F# is static. In F# you rarely have to specify types, and
that's thanks to its powerful type inference system. If you hover your mouse
over the `values` word, you'll see that good old IntelliSense is on duty, as
usual, reporting `values` as an array of strings.

F# type inference is so robust that sometimes can feel like magic, but it is
not. It follows a set of precedence rules that drive the compiler. The result
is that you get the best of both worlds: a language that is concise as a
dynamic one, yet it is strongly typed and compiled, as a static one. By the
way: thanks of type inference, F# functions are implicitly generic.

Combined with the removal of noise, such as curly braces and semicolons, you
will find that the type inference system makes writing, reading and, more
importantly, reasoning about code a pleasant experience.

So why do we have to declare `ActionResult` type on the following line?
Because that's a .NET BCL type, not an F# type. Type inference won't work as
well when applied to the BCL. Fortunately, the compiler (IntelliSense) will
let you know when an explicit type is needed.

Notice that on the last line there is no `return`. In F#, `return` is
implicit. I should probably mention immutability. That `values` array over
there, is immutable like all F# types are unless they are explicitly made
mutable with the `mutable` keyword. Immutability is a *big* deal in
functional languages.

Let's assume that we want to replace this template code with something more
meaningful. Maybe we have a repository object that allows us to retrieve data
from a backend. This repository an external C# package and it has this nice
`Find(Expression<Func<T, bool>>)` method that we want to leverage, to enable
filtering on our API endpoint.

1. The client can use a query string (`?name=john`);
2. If included, parse the query into a lambda expression (`x => x.Name==john`);
3. Pass the lambda to repository's `Find` method;
4. Return lookup results to the client.

For simplicity, we don't want to support multiple query keys, or various
values for the same key;

We want to achieve this:

    [<HttpGet>]
    member this.Get() =
        let filter = getFilter this.Request.Query
        let result = repository.Find<License>(filter).Result;

        ActionResult<License List>(result)

On the first line, we pass the query to the `getFilter` helper function. In
F# there's no notion of wrapping function arguments with parenthesis. Again,
succinctness. `getFilter` will return either `null` if there is no query
string or a lambda filter.

On the second line, we invoke the `Find` method, passing our filter to it. We
then send back the results to the client. Notice that we are returning a
`List<Value>` or, in F# syntax, a `Value List`. We do not have to update the
`Get` signature. Type inference quietly takes note.

With the general business logic out of our way, let's get to the only
remaining piece of the puzzle, the `getFilter` function. For this, it is
probably a good idea to add a `Helpers.fs` file, with a `Helpers` module in
it.

    namespace MyWebApi

    open Microsoft.AspNetCore.Http
    open System.Linq.Expressions
    open System

    module private Helpers =

        let getFilter (query:IQueryCollection)  =

            let expr (key:string, value) =
                let entity=Expression.Parameter(typeof<'T>)
                let body= Expression.Equal(Expression.Property(entity, key), Expression.Constant(value))
                Expression.Lambda<Func<'T, bool>>(body, entity)

            match query.Count with
            | 0 -> null
            | _ ->
                query
                |> Seq.head
                |> fun kvp -> (kvp.Key, kvp.Value |> Seq.head)
                |> expr

Now, this is interesting. We briefly touched on the fact that namespaces
can't hold functions. You use modules for that (F# modules can also store
types, however, like namespaces.). Here we define a `Helpers` module, with
one function `getFilter` in it. To use this module in `ValueController`, we
will need to `open MyWebApi.Helpers` there. Alternatively, we could decorate
the module with the `[<AutoOpen>]` attribute, so that adopters do not need to
open it explicitly. `AutoOpen` is a nice feature, but please don't overuse
it.

Let's look at `getFilter` implementation. First, we define an inner function
`expr`. It takes a key-value tuple (one argument, not two!), does its magic,
and, returns a lambda expression with the required signature of `Func<'T,
bool>`. This code is not particularly interesting; you would do something
similar in C#. Notice, however, that we are forced to declare the type one of
the tuple values. That's because the compiler needs to know which of the (way
too many) overloads of `Expression.Property` we want to use. We could
strongly type the second argument instead; it would be the same. Also, take
note of how we declare a generic type in F#. The convention is not to use
uppercase as we do here, you typically use `'a` for example, but `'T` is also
ok. I tend to use ``T` when I am working on the boundaries between the BCL
and F#, like in here.

The `match...with` block is the heart of `getFilter`.

            match query.Count with
            | 0 -> null
            | _ -> ...

It matches `query.Count` value with some alternatives.

- if no items are in the query, then return null;
- any other value (`_` is a catchall), do something else.

Pattern matching is super interesting in F#. You can think of `match...with`
as a `switch/case` on steroids. Here, let's stress one of its many features:
exhaustive checking. We used the catchall `_` symbol on the second branch.
Had we used a specific value instead, the compiler would throw an "incomplete
pattern matching" error. Think of how many subtle bugs this feature alone
cuts out.

Let's now consider the second and last branch in our pattern matching code.
All the time in our code, no matter the language, we call a sequence of
methods. In this concatenation, the output of one method serves as the input
for the next. In these situations we have two options: either we use a
temporary variable to hold the result of one method call, then we pass said
variable to the next, or, if the call sequence is not too long, we nest one
method call within the other. In both cases, code quickly becomes hard to
read and, what's worse, it becomes difficult to grasp its intentions. F#
*forward pipe* operator aims to solve this problem. Let's look back at our
pipeline:

    query |> Seq.head |> fun kvp -> (kvp.Key, kvp.Value |> Seq.head) |> expr

In his book [Get Programming with F#][5], Isaac Abraham provides us with what
I think is the best explanation of what the forward pipe operator means:

> Take the value on the left-hand side of the pipe and flip it over to the
right-hand side as the last argument to the function. [...] The beauty of
this is that as long as the output of one function matches the input of the
next one, any function can be chained with another one.

Once it clicks, you'll love it.

We start with `query`, our input argument, which is pipelined (passed) to the
`Seq.head` function. This function returns the first element (head) of the
input sequence. Now, `query` is an `IQueryCollection`, which happens to
implement `IEnumerable` which, in turn, is an alias for F# `seq<'T>` so yes,
`query` is a sequence. Here we don't want to support multiple keys, so we
only take the first one. Next up in the pipeline we have an inline function
or lambda. This one accepts the `kvp` argument (a `KeyValuePair`) and returns
a tuple with `kvp` key and the value. The lambda is interesting because it
comes with a nested pipeline. Querystrings can come with multiple values for
the same key (i.e. `?name=john&name=mike`), so `kvp.Value` is itself a
sequence of strings. Again, we don't support multiple key values, so we keep
the first one. The last step in our pipeline is, of course, the call to our
`expr` function, which will take the tuple as input, and return the
corresponding expression filter.

One last thing. Remember that explicit type declaration we had to add to
`expr`'s input tuple? That one was weird, although it did have a reason.
Let's refactor our code to be more compact, so we inline `expr` into the
pipeline:

    let getFilter (query:IQueryCollection)  =

        match query.Count with
        | 0 -> null
        | _ ->
            query
            |> Seq.head
            |> fun kvp -> (kvp.Key, kvp.Value |> Seq.head)
            |> fun (key, value) ->
                let entity=Expression.Parameter(typeof<'T>)
                let body= Expression.Equal(Expression.Property(entity, key), Expression.Constant(value))
                Expression.Lambda<Func<'T, bool>>(body, entity)

See? Now we don't need to declare `key` type. It is inferred from the input
function (the left-hand side of the pipe!)

## Wrapping up

Building and running a RESTful API with F# is simple. Sure, the template code
above does not look very functional, and it isn't. Once you get more
confident with F#, you should probably move to functional web frameworks,
like [Giraffe][3]. The takeaway point I am trying to make, however, is that
F# with pure NetCore delivers. Functional purists may shiver, but my advice
is that you begin doing F# right away, solving problems that you are already
familiar with.

I learned about F# back in 2010-11 when it was very new, and I immediately
fell in love with it. Then I spent years and years waiting for the right
project, the one with a perfect "functional fit" that would allow me to use
F# in the real world. Guess what? It never happened. Either we had a good
candidate but we were in a hurry, so no time for learning, or we got
"less-than-ideal-for-functional" projects (in our mind) to work on.

Then I was tasked to write yet another RESTful web service. We have plenty
scattered around, both in Python and C#. RESTful services have been my bread
and butter for such a long time; I even went around to release a Python REST
framework called [Eve][4].

This time, I thought, I am going to do it differently. This time, I am going
down the F# rabbit hole. What I found at the bottom of it was pure joy.

---
PS: That fictional repository we've been using, well, that's a concrete
thing, an open source project I have been working on called Boxroom. When it
is ready for prime time, I will post about it here on my site. Interested?
Join the newsletter; a link is right down here.

*Join the [newsletter][nl] to get an email alert when a new post surfaces on
this site. If you want to get in touch, I am @[nicolaiarocci][tw] on twitter.*

 [tw]: http://twitter.com/nicolaiarocci
 [nl]: http://eepurl.com/b-_Pzz
 [1]: https://fsharpforfunandprofit.com/posts/fsharp-is-the-best-enterprise-language/
 [2]: http://ionide.io/
 [3]: https://github.com/giraffe-fsharp/Giraffe
 [4]: https://github.com/pyeve/eve/
 [5]: https://manning.com/books/get-programming-with-f-sharp