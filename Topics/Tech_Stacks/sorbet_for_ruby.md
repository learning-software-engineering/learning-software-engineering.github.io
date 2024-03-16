# Pros and Cons of Sorbet for Ruby

## Introduction
Languages like JavaScript, Python, and Ruby are powerful in the fact they offer dynamic typing, which eases the speed of development. Dynamically typed languages offer no type checking, and allows for some interesting lines of code such as referencing non-existent variables and changing the type of a variable on the fly. In recent years however, there has been a trend of adding a type system on top of dynamically typed languages; Sorbet adds a type system on top of Ruby. Originally developped by Stripe Inc. Sorbet is used at a number of large companies such as Shopify, InstaCart, and CoinBase to name a few. 
## Pros
The big advantage of using Sorbet is without a doubt the strict typing provided for an otherwise dynamically typed language. Furthermore, code written using Sorbet offers enhanced readability for both the outhor, as well as reviewers. Engineers know exactly what type every method inputs and outputs,while errors are thrown if an engineer tries to input the wrong type or use the output incorrectly. As such, errors that would normally be caught at run time in these dynamic languaes are caught before hand, saving companies countless hours of wrok when things go wrong in production. Furthermore, Sorbet is backwards compatible with regular Ruby code, therefore you can add Sorbet to your project gradually or even omit it all together to begin with and add it later on as things grow (although this would resulkt in some serious tech debt!).
## Cons
Interestingly, the same thing that makes Sorbet attractive to some programmers is one of it's cons. Although a type system is nice, it begs the question, why not just use a strongly typed language like Java instead? Furthermore, dynamic languages with a type system on top can still end up doing wacky things, just in a different way. David Heinemeier Hanssen, famously the creator of Rails, describes these wacky events as "type gymnastics", where an engineer has to write increasingly complex type annotations on an otherwise acceptable line of code in order to eliminate the errors. Here's an example of type gymnastics:
````{verbatim, lang = "markdown"}
type IntTuple<X extends string, Acc extends number[] = []> =
`${Acc['length']}` extends `${X}` ? Acc : IntTuple<X, [...Acc, Acc['length']]>
````
## Is Sorbet right for me?

