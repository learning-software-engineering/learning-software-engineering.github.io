# Introduction to Prompt Engineering

# Table of Contents
- [Introduction to Prompt Engineering](#introduction-and-understanding)
  - [Understanding Large Language Models (LLMs)](#understanding-large-language-models-llms)
  - [How does it work](#how)
- [Application](#application)
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



