# Pros and Cons of Sorbet for Ruby

## Introduction
Languages like JavaScript, Python, and Ruby are powerful in the fact they offer dynamic typing, which eases the speed of development. Dynamically typed languages offer no type checking, and allows for some interesting lines of code such as referencing non-existent variables and changing the type of a variable on the fly. In recent years however, there has been a trend of adding a type system on top of dynamically typed languages; Sorbet adds a type system on top of Ruby. Originally developped by Stripe Inc. Sorbet is used at a number of large companies such as Shopify, InstaCart, and CoinBase to name a few. 

Below is an example of a simple function with and without Sorbet.

Without Sorbet:
````{verbatim, lang="markdown"}
def sayHello(name)
  puts "Hello, #{name}!"
end

sayHello("Sorbet") # ok!
sayHello()   # error at run time
sayHelo("")  # error at runtime
````

With Sorbet:
````{verbatim, lang="markdown"}
# typed: true
extend T::Sig

sig {params(name: String).returns(NilClass)}
def sayHello(name)
  puts "Hello, #{name}!"
end

sayHello("Sorbet") # ok!
sayHello()   # error: Not enough arguments provided
sayHelo("")  # error: Method `sayHelo` does not exist
````

## Pros
* Strict typing provided for an otherwise dynamically typed languageFurthermore
* Enhanced readability for both the outhor, as well as reviewers
* Engineers know exactly what type every method inputs and outputs, where errors are thrown if types used are invalid
* errors that would normally be caught at run time in these dynamic languaes are caught before hand
* Sorbet is backwards compatible with regular Ruby code
  
## Cons
* Adding a type system to a dynamic language avoids the advantages of a dynamically typed language
* Type gymnastics to make the 'compiler' happy about the type you used.

Here's an example of type gymnastics in TypeScript, that occur when trying to define a type for url parameters of an api call using ````fetch()````:
````{verbatim, lang = "markdown"}
type paramsType = string | URLSearchParams | string[][] | Record<string, string> | undefined | null
````

## Is Sorbet right for me?

As I'm sure you can imagine, the answer to this question is, it depends. The advantages of Ruby on Rails is the fact it's a batteries included framework; everything is pretty much ready to go once you've initialized your project. This allows an engineer to develop their app very quickly, with scalability already accounted for. However, adding strict typing to Ruby on Rails will ultimately slow down one's development process, foregoing the advantages of a framework like Rails. If your project is intended to remain small, there's not really a reason to add Sorbet on top, there will be a manageable amount of code so the error tracing advantages aren't as drastic and you shorten the amount of time to a minimum viable product. If you plan on creating a monolith, Sorbet is definitely advantageous. The development timeline on a monolith is more stretched out so engineers can afford to spend a bit of time using Sorbet in order to avoid run time errors in the future (although this might result in some seriopus tech debt!). 

You can try Sorbet at https://sorbet.run/

## Sources:
https://sorbet.org/
https://world.hey.com/dhh/turbo-8-is-dropping-typescript-70165c01
https://youtube.com/watch?v=5ChkQKUzDCs
https://www.youtube.com/watch?v=zQnBQ4tB3ZA
