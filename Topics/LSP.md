
# The Liskov Substitution Principle
​
## 1. Motivation for The Liskov Substitution Principle (LSP)
You may know of the LSP from the SOLID principles, which roughly says that instances of a subclass should be able to be substituted for an instance of its superclass without breaking the program. This is a powerful idea; but in fact, the LSP proposes a stronger notion of subtyping:

_Subtype Requirement_: Let ![{\displaystyle \phi (x)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/546b660b2f3cfb5f34be7b3ed8371d54f5c74227) be a property provable about objects ![{\displaystyle x}](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4) of type T. Then ![{\displaystyle \phi (y)}](https://wikimedia.org/api/rest_v1/media/math/render/svg/db7ffe2f7daf9bae8d3f2711b2fd67348aceb3dc) should be true for objects ![{\displaystyle y}](https://wikimedia.org/api/rest_v1/media/math/render/svg/b8a6208ec717213d4317e666f1ae872e00620a0d) of type S where S is a subtype of T.

If the subtype requirement is satisfied, then not only is the correctness of our program preserved when substituting objects for sub-objects, but also any *provable* property! What is means for a property to be provable is perhaps unclear, so let's just assume for simplicity our own intuitive notions of provability.

## 2. The Principles in The LSP
The subtype requirement is an incredibly powerful tool for reasoning about our programs, but how does the LSP help us guide our programming to satsify it? The LSP imposes requirements[^1] on method signatures common across many typed languages:

 1. **Contravariance of parameter types in the subtype** – if parameters **P** are permissible in method ***f*** of a type, then **P** is also be permissible in ***f*** of any subtype. Equivalently:
	- If it "works" for a method in a type, then it "works" for the same method in any subtype.
	- The space of permissible parameters of the subtype is a **superset** of the space of permissible parameters of the type.
2. **Covariance of return types in the subtype** – a requirement symmetric to the first:
	- The return type of a method in the subtype should "work" as a return type to the same method in the type.
	- The space of permissible return values of the subtype is a **subset** of the space of permissible return values of the type.
3. **New exceptions cannot be thrown by the methods in the subtype, except if they are subtypes of exceptions thrown by the methods of the supertype**

but also imposes additional behavioural requirements[^1]:

4. **Preconditions cannot be strengthened in the subtype.**
5. **Postconditions cannot be weakened in the subtype.**
6. **Invariants cannot be weaked in the subtype.**
7. **History Constraint:** subtypes should not modify state defined in the type in a manner that is not expected by the type.

Requirements 1 to 6 are straightforward, so we won't discuss them. But the reader should convince themself that they are important, and necessary to satisfy the subtype requirement. We'll discuss requirement 7 as it's the novel requirment introduced in the LSP, and has important implications on how subtyping/inheritance should be used. The Wikipedia article illustrates a nice example of a violation of the History Constraint in the case of subtyping between mutable and immutable objects, but we'll illustrate a scenario that is simpler and probably more relatable.

If you've learnt about OOP, you may have been told that the use of mutable public instance variables in a class is generally not a good idea, and that you should instead create getter and setter methods for it. Whether or not you agree with this practice, using mutable public instance variables is problematic in the context of the LSP and using subtyping/inheritance: not only is it possible to freely mutate the state of the object, hence violating the History Constraint, but you may also break invariants which are assumed by the implementation of the methods in the supertype, causing catastrophic failure of your program! On the contrary, if all your mutable instance variables are private (meaning state can only be modified through exposed methods of the supertype), then its *impossible* for the History Constraint to be violated. Note that this does not mean that one *must* declare all their instance variables this way to satisfy the History Constraint, it's just that its a very simple and easy way to ensure that they do. Of course, one could be incredibly disciplined and meticulous in their programming, but at that point they may as well avoid subtyping/inheritance as they'll shoulder all the associated complexity and gain little to none of the benefits.

A side note: the satisfaction of the subtype requirement is undecidable, meaning no computer program, hence no compiler or linter or any static analysis tool, can figure out whether or not its violated in general.

## 3. Conclusion
We discussed the notion of subtyping proposed by the LSP and its utility for reasoning about our programs. We discussed the actual principles/requirements imposed by the LSP to guide our programming to satisfy the subtyping requirement. And finally, we looked at an example of how the novel History Constraint introduced by the LSP impacts how we do object-oriented programming. Hopefully this writeup gave a little bit more insight into the implications of the LSP and motivated its ideas for some readers. Of course, there's much more to learn about the LSP than what we've discussed here. The Wikipedia article and the original paper[^2] by Liskov and Wing are good places to go next.



[^1]: Wikipedia contributors. "Liskov substitution principle." _Wikipedia, The Free Encyclopedia_. Wikipedia, The Free Encyclopedia, 9 Mar. 2024. Web. 17 Mar. 2024. https://en.wikipedia.org/w/index.php?title=Liskov_substitution_principle&oldid=1212676939

[^2]: Barbara H. Liskov and Jeannette M. Wing. 1994. A behavioral notion of subtyping. ACM Trans. Program. Lang. Syst. 16, 6 (Nov. 1994), 1811–1841. https://doi.org/10.1145/197320.197383
