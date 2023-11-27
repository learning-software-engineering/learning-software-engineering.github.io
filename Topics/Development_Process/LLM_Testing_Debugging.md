# Large Language Model (LLM) for testing and debugging

## Attention!
It is important to have background knowledge of standard testing methodologies before reading this content. 
LLM can be a strong tool for testing, but it will NOT replace standard testing methodologies. 

See the following links for learning more standard testing techniques: 
- [Automated Testing](Automated_Testing.md)
- [QA Testing](QA_testing.md)

In addition, if you are planning to use LLM for your coursework, it is important for you to check the course guidelines on the usage of generative AI. 

## Motivation
Have you had any experience of being stuck on the code for an enormous amount of time,  only to find that the issue was a simple logic error or typo? 
It is not uncommon for programmers to overlook these seemingly trivial mistakes, especially when you are spending too much time on the same part of the code, making you biased on your code.
When you have a friend near you, it might be easy to ask for help to identify any of these errors. 
However, this might not always be true. As a replacement for your friend who goes on vacation while you are programming in a dark room, you can have LLM!

LLM, like ChatGPT, can become your strong tool for testing & debugging when you use it correctly. 

## Debugging 
A simple example of the usage of LLM for debugging can be as follows: 
```
Provide a step-by-step description of the code below.

def fibonacci(n):
    if n == 1: 
        return 1
    return fibonacci(n-1) + fibonacci(n-2)
```
The above simple example can help you understand your code better, allowing you to debug it efficiently.
It is important for you to make the prompt as clear and organized as possible to improve the accuracy of the LLM's response. 
When your prompt is difficult to understand, LLM can misinterpret or may not respond accurately.

If you have some context about the code, you should always include them in your prompt. This will include:

- Error obtained from the code
- Sample inputs and outputs 
- Purpose of the code

LLM can perform significantly better with more contextual information, even if that seems unrelated to the specifics of your code. 

Given this, we further use the following prompt to debug the code: 
```
You are a Python programmer. 
You are trying to debug the following Python code for computing the n-th Fibonacci number.

Code: 

def fibonacci(n):
    if n == 1: 
        return 1
    return fibonacci(n-1) + fibonacci(n-2)

Sample inputs and outputs: 

Input: n = 1, Output: 1
Input: n = 2, Output: RecursionError: maximum recursion depth exceeded in comparison
Input: n = 8, Output: RecursionError: maximum recursion depth exceeded in comparison

Identify and describe the parts of the code that are wrong.  
```

In addition to the LLM's helpful response, the process of identifying the context and forming the prompt itself can lead you to have a better understanding of your code. 

## Testing
In addition to debugging, LLM can be used to generate test cases to make sure your code is correct. 
When you are working on a single problem for so long, you might get biased on some aspects, 
which may cause you to overlook some edge cases for your problem. 
This can potentially be captured by LLM-generated test cases. 


### Generating test cases directly
You can generate test cases directly as follows: 
```
You are working on the following Python code: 

<your code>

Precondition: ...
Postcondition: ...

Generate test cases using <your testing framework> that covers all cases. 
```
However, it is important to note that you should also create test cases manually to make sure you have the correct understanding of your code. 
Even though LLM can be great for reducing the chance of missing some edge cases, it is always important for you to take steps to generate test cases. 

### Generating Test Data
Instead of generating test cases directly as some programming language, you can also ask LLM to create test data in specific formats (e.g. JSON, CSV).

Here are an interesting blog that tries to create JSON payloads for API request: [Using LLMs for test data generation](https://blog.dkwr.de/development/llm-for-test-data-generation/?utm_source=hnblogs.substack.com)

Even though the data it can generate is limited because LLM has limits on the number of tokens that it can output, you can make those data your starting point. 
You might also want to do validation on your generated data since it can generate incorrect data.

### Generating Personas
Persona-based testing is an important technique you can use for quality assurance. 
You can create a fictional character called a persona that represents a specific user group to guide you through your testing processes (and the development process in general). 
LLM is also a great tool for generating personas. 

The following blog has a number of examples for generating buyer personas for various types of industries: [Creating Buyer Personas with Chat GPT + Template Prompts
](https://medium.com/@ferdian_ariff/creating-buyer-personas-with-chat-gpt-template-prompts-ad78f98e7e3e)

One example from the above blog is:  

```
Create a buyer persona for a tech enthusiast who enjoys gaming and virtual reality experiences.
```

One interesting thing you can do is interact with the persona generated by LLM. 
LLM is also good at role-play, so you can ask LLM to act like the generated persona, 
to deepen your understanding of your software's user group. 

## Advantages and disadvantages
Here are the advantages and disadvantages you should know if you are using LLM for testing and debugging. 

**Advantages:**

- Saves time: LLM can generate test cases / feedback on your code 
- Increase test coverage: LLM can create test cases that are not biased, allowing it to create test cases that cover some edge cases that you missed. 
- Deepens your understanding of your code: If you prompt properly for testing and debugging purposes, your steps for making the prompt itself can allow you to understand more about your code. In addition, you can talk with LLM in an interactive manner, which can lead you to find problems that you might have overlooked. 

**Disadvantages:**

- Over-reliance: If you rely too much on LLM to work on your code, you might lose control over your code, which can cause critical mistakes. 
- Incorrect answer: LLM is not perfect. It can generate incorrect answers. You should always validate output from LLM manually to avoid having problems with LLM's output.
- Limits on output tokens: LLM usually has limits on output tokens that it can generate. You can split up into multiple prompts to avoid this issue. 

## Going further: Few-shot
One advanced technique you can use for testing & debugging with LLM is few-shot learning. 
In short, few-shot learning is a technique that can improve LLM's response by providing example inputs & outputs. 
For example, in the context of testing, you can provide example(s) of test cases that you created in your prompt to let 
LLM understands what you are looking for. 
You can see [here](https://blog.andrewcantino.com/blog/2021/04/21/prompt-engineering-tips-and-tricks/) for more detailed example for few-shot learning. 

## Recommended LLMs 
There are a number of LLMs that are accessible. I will list some LLMs that I recommend as a reference. 
- **ChatGPT (GPT3.5)**: LLM created by OpenAI. It's probably one of the most commonly used LLMs right now. It should be suitable for most use cases. 
- **GPT4**: Improved version of GPT3.5. It supports image as an input, so it may be suitable when you want to debug styling issues with your UI. As of 2023 November 17, you can pay USD $20/month to get an upgrade on your ChatGPT account to get access to GPT4. (You can also pay per token if you use OpenAI API)
- **Llama 2**: LLM released by Meta AI. It can be used for research and commercial use, and you can even download the model if you get access. It offers 7B, 13B, and 70B model sizes, so you might be able to run on your local machine if you have good hardware. If you are interested in fine-tuning LLM to make a model specifically good for generating tests or debugging, this model can be a great option. 

Other options include BARD, Falcon, and PALM. 

## Conclusion 
When LLM, like ChatGPT, is used correctly, it can provide strong support for your software engineering experiences. 
However, LLM must be used carefully to avoid potential risks, as shown [above](#advantages-and-disadvantages). 
In addition, it is always important to have knowledge of more standard testing methodologies to not over rely on the power of LLM 
to make sure that you always have full control over your software. 

When used correctly, LLM can become a strong friend that supports your journey for your software career. 

## References / Additional Resources
- [Software Testing and LLM- are we heading in the right direction?](https://www.linkedin.com/pulse/software-testing-llm-we-heading-right-direction-nstarx/)
- [ChatGPT-4 Code Debug](https://www.w3schools.com/gen_ai/chatgpt-4/chatgpt-4_code_debug.php)
- [A Beginner's Guide to ChatGPT Prompt Engineering](https://www.datacamp.com/tutorial/a-beginners-guide-to-chatgpt-prompt-engineering)
- [How to Debug Code Using ChatGPT](https://rajvivan11.medium.com/how-to-debug-code-using-chatgpt-7b75d2615b8c)
- [Persona Based Testing](https://medium.com/@ChamalAsela/persona-based-testing-de6e1396c23c)
- [Can LLM help SWE write test cases?](https://medium.com/@taiyuanz/can-llm-help-swe-write-test-cases-4d1cd3b51b3e)
- [Using LLMs for test data generation](https://blog.dkwr.de/development/llm-for-test-data-generation/?utm_source=hnblogs.substack.com)
- [Creating Buyer Personas with Chat GPT + Template Prompts](https://medium.com/@ferdian_ariff/creating-buyer-personas-with-chat-gpt-template-prompts-ad78f98e7e3e)
- [Prompt Engineering Tips and Tricks with GPT-3](https://blog.andrewcantino.com/blog/2021/04/21/prompt-engineering-tips-and-tricks/)
- [Prompt Engineering Guide](https://www.promptingguide.ai/)