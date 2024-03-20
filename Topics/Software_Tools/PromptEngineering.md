# Introduction to Prompt Engineering

# Table of Contents
- [Introduction to Prompt Engineering](#introduction-and-understanding)
  - [Understanding Large Language Models (LLMs)](#understanding-large-language-models-llms)
  - [How does it work](#how)
- [Technical Techniques](#techinical-techniques)
  - [Zero-shot Learning](#zero-shot-learning)
  - [Few-shot Learning](#few-shot-learning)
  - [Chain-of-thought Prompting](#chain-prompting)
- [Application](#application)
  - [Function Calling](#function-calling)
  - [Code Generation with LLM](#codegeneration)
  - [Code Generation with Large Language Models](#code-generation-with-large-language-models)
- [Citations](#citations)


<a id="introduction-and-understanding"></a>
# Introduction and Understanding

## Understanding Large Language Models (LLMs)

<a id="understanding-large-language-models-llms"></a>
### Introduction to LLMs:

Large Language Models (LLMs) are at the forefront of artificial intelligence, driving innovations in natural language processing and beyond. These powerful models are trained on extensive datasets composed of diverse text from the internet, enabling them to grasp the complexities, subtleties, and varied patterns of human language. As a result, LLMs can generate text that's not only coherent and contextually relevant but also remarkably human-like in its composition. Most Common examples include Chatgpt, Copilot, etc.

<a id="how"></a>
### How does it work?

#### Pre-training:
This foundational stage involves training the LLM on a vast corpus of text data. During pre-training, the model learns the general rules of language, including grammar, syntax, and semantics, without any specific task in mind. This broad understanding of language equips the model to tackle a wide range of text-based tasks.

#### Fine-tuning:
After pre-training, LLMs can undergo fine-tuning on smaller, task-specific datasets. This process tailors the model's responses to perform well on particular tasks or understand the nuances of specialized domains, such as legal documents or medical literature.

### Generative Capabilities:
LLMs are not just passive observers of language; they are active creators. Given a prompt or a start of a sentence, these models can generate text that follows logically and engagingly. This generative capability makes them invaluable for applications like content creation, where they can produce original articles, stories, and even poetry that mimics human writing styles.


### Examples and Demonstrations:
Imagine prompting an LLM with the sentence "The sunset over the ocean was a breathtaking sight," and the model continues with "as the hues of pink and orange painted a masterpiece in the sky, reflecting the day's end with a promise of renewal." This example showcases the model's ability to continue the narrative in a way that's contextually appropriate and stylistically coherent.

<img width="375" alt="Screenshot 2024-03-17 at 8 49 34 PM" src="https://github.com/Adrianhui123/learning-software-engineering.github.io/assets/97869438/955c38ed-bbc6-43a2-848e-f23d7c27f019">


<a id="techinical-techniques"></a>
# Technical Techniques
## Techniques in Prompt Engineering

<a id="zero-shot-learning"></a>
### 1. Zero-shot Learning: Learn Without Examples

Imagine asking your friend to do something they've never done before, but they use their smarts to figure it out anyway. That's zero-shot learning for AI - you ask the AI to do a task it wasn't specifically trained for, and it tries to make sense of it using what it knows.

Example: Let's say you want the AI to write a poem about the ocean, but it was never specifically trained to write poems. You simply ask, "Write a poem about the ocean." The AI uses its general understanding of language and poems to create one for you.

<img width="200" alt="Screenshot 2024-03-17 205057" src="https://github.com/csc301-2024-s/learning-software-engineering.github.io/assets/75962325/8176099c-30f2-4347-aa2d-9cde47285402">

#### Application Tips:
- Be clear and precise in your prompt. Since the model has no examples to learn from in this context, clarity in task description is crucial.
- Incorporate relevant keywords or concepts related to the task to help the model understand the context.

<a id="few-shot-learning"></a>
### 2. Few-shot Learning: Learning with a Few Examples

This is like showing your friend a few pictures of cakes you like before asking them to bake one for you. By giving the AI a few examples of what you want, you help it understand exactly what you're looking for.

Example: If you want the AI to generate customer service responses, you could start by showing it a couple of examples:

Customer Complaint: "My order arrived late."
Service Response: "We're so sorry for the delay. We'll look into it and ensure it doesn't happen again."

You then ask the AI to respond to a new complaint, "I received the wrong item," guiding it to generate a similar style of response.

#### Application Tips:
- Select your examples carefully. They should be representative of the task and closely match the desired output format or context.
- Limit the number of examples to avoid overwhelming the model or biasing the response too heavily towards the examples given.

<a id="chain-prompting"></a>
### 3. Chain-of-thought Prompting: Solving Step by Step

Think of a time when you solved a problem by talking through it step by step. Chain-of-thought prompting is when you guide the AI through a task by breaking it down into smaller, manageable steps. It helps the AI think through complex issues more clearly.

Example: Let's say you want the AI to calculate the total cost of a shopping list. Instead of asking directly, you guide it:

"First, list the prices of apples, bread, and milk."
"Then, add the prices together."

This method helps the AI understand and tackle each part of the problem, leading to a clearer and more accurate answer.

<img width="200" alt="Screenshot 2024-03-17 205109" src="https://github.com/csc301-2024-s/learning-software-engineering.github.io/assets/75962325/86813ee5-69a8-46b3-baa9-c904d37085a9">

In each of these techniques, the key is to communicate effectively with the AI, guiding it to understand and perform tasks it wasn't directly trained to do. Whether you're giving it a brand new challenge, showing it a few examples, or walking it through a problem step by step, these methods enhance how well the AI can assist you.

#### Application Tips:
- Break down the task into smaller, manageable steps that the model can logically follow.
- Encourage the model to explicitly state its reasoning at each step, which not only clarifies the thought process but also helps in identifying any logical errors.
- Adjust the complexity of the steps based on the task's difficulty and the model's capabilities.

<a id="function-calling"></a>
## Function Calling
### Function Calling with LLMs

Function calling in Large Language Models (LLMs) is a groundbreaking feature that fundamentally transforms how AI interacts with the digital world. It empowers LLMs to go beyond mere text generation, enabling them to perform specific actions, interact with external APIs, and utilize tools to fetch real-time data or execute tasks. This capability is crucial for developing intelligent applications that require up-to-date information or complex computations, marking a significant leap towards more versatile and practical AI systems.

At its core, function calling acts as a bridge between the AI's understanding of natural language and the execution of digital functions. This means that LLMs can now understand a user's request in natural language, determine the necessary actions to fulfill that request, and execute those actions through predefined functions. It's a vital advancement that enhances the AI's utility, allowing it to provide more accurate, contextually relevant, and timely responses.

### Code Demo for Function Calling

Let's make this concept clearer with a code example. Imagine you want to develop a feature that allows users to ask for the current time in any timezone, so the user can ask a message like 
“What is the current time in New York?” in your own application. You have a function that has all the time zones. To achieve this you will need a LLM that can extract the key messages out and plug into a parameter.

To achieve this, you'd set up a function that the LLM can call to perform the translation. 

```
tools = [
    {
        "type": "function",
        "function": {
            "name": "get_current_time",
            "description": "Get the current time in a specified timezone",
            "parameters": {
                "type": "object",
                "properties": {
                    "timezone": {
                        "type": "string",
                        "description": "The timezone to get the current time for",
                    }
                },
                "required": ["timezone"]
            },
        }
    }
]
```

tools provide a  get_current_time function outline, which tells the LLM what information it needs to collect. LLM will then help to extract needed parameters from the message, for example the timezone,  and fill it into the function call based on natural language input..

When the user ask for the current time in a specific timezone, you will have a json like this:
```
messages = [
    {
        "role": "user",
        "content": "What is the current time in New York?"
    }
]
```

The get_competion function below specifies the necessary parameter we want to define the model we will use. And we will call it by providing the message and the tools.
```
def get_completion(messages, model="gpt-3.5-turbo-1106", temperature=0, max_tokens=300, tools=None):
    response = openai.chat.completions.create(
        model=model,
        messages=messages,
        temperature=temperature,
        max_tokens=max_tokens,
        tools=tools
    )
    return response.choices[0].message

response = get_completion(messages, tools=tools)
```

After processing the user's inquiry, the LLM prepares a structured response that outlines the parameters required for the get_current_time function. This includes identifying and organizing the relevant timezone from the user's message.

Function calling is very important as it opens up new possibilities for AI applications providing dynamic content generation, personalized assistance, sophisticated data analysis and real-time decision-making. By integrating LLMs with external tools and APIs, developers can create more responsive, intelligent, and capable systems that cater to a wide range of needs and industries.

<a id="application"></a>
# Application

<a id="codegeneration"></a>
## Code Generation with Large Language Models

### Setting the Stage:
To guide the model, we use a System Message that sets the context: "You are a helpful code assistant that can teach a junior developer how to code. Your language of choice is Python. Don't explain the code, just generate the code block itself."

### Basic Code Generation:
When tasked with generating basic code, such as creating a Python script to greet a user by name, LLMs analyze the structure and semantics of the prompt to construct a suitable code block. The model draws on patterns and examples it has learned during training to produce syntactically correct and functionally appropriate Python code that matches the task described in the prompt.

<img width="375" alt="Screenshot 2024-03-17 at 8 57 21 PM" src="https://github.com/Adrianhui123/learning-software-engineering.github.io/assets/97869438/840d3761-d7f0-4366-8e12-d341eb44e9a0">


### Completing Functions:
For completing partial functions, LLMs rely on their understanding of coding patterns and the specific requirements outlined in the prompt. Given the start of a function, the model predicts the most likely continuation based on its training, which includes analyzing countless code examples. This capability is akin to predicting the next word in a sentence but applied to the syntax and structure of code.

### Code Explanation:
Explaining code involves the model interpreting the logic and function of a given code block and then describing its purpose and operation in natural language. This process requires the LLM to reverse-engineer the code, applying its understanding of programming concepts and language semantics to provide a clear and accurate explanation.

### Debugging and Editing:
The potential for LLMs to assist in debugging and editing code lies in their ability to analyze code for syntactical and logical errors, drawing on examples and patterns from their training data. The model can suggest corrections or improvements by identifying inconsistencies or errors in the code and comparing them with known correct implementations. This capability is particularly valuable for identifying common mistakes and proposing optimized solutions.

<a id="citation"></a>
## Citations
- [Prompting Guide](https://www.promptingguide.ai/)
- [McKinsey Explainers: What is Prompt Engineering?](https://www.mckinsey.com/featured-insights/mckinsey-explainers/what-is-prompt-engineering)
