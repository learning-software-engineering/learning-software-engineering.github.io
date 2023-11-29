# Clean coding: coding and comment styling!


### Why care about coding and commenting style?

Code isn't good just cause it works. As we become more experienced in software engineering we soon realize that there is so much to consider other than the fact that it works. In fact, functioning code is the bare minimum. For example, most of us have learned that we need to consider time and space efficiency. If we didn't we'd constantly have to wait for the results we want. This can pose a big problem if those results are dependent on other results that are also not time efficient. We also have to think about scalability. We don't want to have to rewrite code just to add one feature. However, what's so important about coding and commenting style? How does that affect users? If I understand it is that not good enough? In short, no.

First, we should consider the event of inconsistent styling. This can mean not using naming conventions, inconsitent documentation/ commenting, and inconsistent spacing. In this case, while you might understand what is going on as you are writing it, future will most likey get confused (especially if you haven't worked with the same language in a while). For example, consistent naming conventions can serve as a hint of the purpose of whatever it is you're naming. For example, specific naming conventions can tell you what type of function you are looking at (for example, a unit test function vs. a use case function), what type of variable (different scopes), etc. Consistent commenting and spacing also add to the readability of your code. Therefore, future you will thank you greatly for giving them hints on how to understand your code. Not just future you but other developers that will have to work with your code.

### How to choose which style is best for me?

Now that we know how important coding style is important, how do we choose one? Luckily you don't have to invent this yourself. There are different guides to styling depending on factors such as coding language. Below, I'll highlight common naming conventions and commenting styles.

#### Naming conventions
There are many different naming conventions which you can learn [here](https://www.freecodecamp.org/news/programming-naming-conventions-explained/). However, I'll below popular naming conventions for python and java:

|               | Constants | Variables | 	Types (Structures) | 	Functions | Modules |
| ------------- | --------- |--------- |--------- |--------- |--------- |
| Python        | lower_case|lower_case | CamelCase|lower_case|lowercase|
| Java  | 	UPPER_CASE|CamelCase | CamelCase|mixedCase|lowercase|

#### Commenting

When commenting, you want to consider a few things:
- Redundancy. If the code is self-explanatory, it most likely does not need a comment attached to it. Your comments should not add noise to your code.
- Usefulness. Commenting should add value to your code. It should either explain logic, or add extra information you might not get from the code itself.
- Descriptive. TODO comments should properly outline what needs to be done. It should not be too vague.
  
### How do I enforce my styling decisions?

Other than remembering styling while working, depending on the language you are working with, you can find linters that will enforce specific coding standards (for example, spacing between functions, naming, etc.). Think of a linter as grammarly for coding!

### Resources to learn more.
- [Coding and Comment Style](https://mitcommlab.mit.edu/broad/commkit/coding-and-comment-style/#:~:text=Your%20code%20will%20only%20be,be%20consistent%20with%20field%20conventions.)
- [How to choose the best code conventions for you and your team](https://www.freecodecamp.org/news/how-to-choose-the-best-code-conventions-for-you-and-your-team-992cc2cc7b83/)
- [What Is a Linter?](https://www.testim.io/blog/what-is-a-linter-heres-a-definition-and-quick-start-guide/)
- [Types of naming conventions](https://www.freecodecamp.org/news/programming-naming-conventions-explained/)
