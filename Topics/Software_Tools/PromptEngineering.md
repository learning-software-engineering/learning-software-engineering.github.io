# Technical Techniques
## Techniques in Prompt Engineering

### 1. Zero-shot Learning: Learn Without Examples

Imagine asking your friend to do something they've never done before, but they use their smarts to figure it out anyway. That's zero-shot learning for AI - you ask the AI to do a task it wasn't specifically trained for, and it tries to make sense of it using what it knows.

Example: Let's say you want the AI to write a poem about the ocean, but it was never specifically trained to write poems. You simply ask, "Write a poem about the ocean." The AI uses its general understanding of language and poems to create one for you.

<img width="200" alt="Screenshot 2024-03-17 205057" src="https://github.com/csc301-2024-s/learning-software-engineering.github.io/assets/75962325/8176099c-30f2-4347-aa2d-9cde47285402">

### 2. Few-shot Learning: Learning with a Few Examples

This is like showing your friend a few pictures of cakes you like before asking them to bake one for you. By giving the AI a few examples of what you want, you help it understand exactly what you're looking for.

Example: If you want the AI to generate customer service responses, you could start by showing it a couple of examples:

Customer Complaint: "My order arrived late."
Service Response: "We're so sorry for the delay. We'll look into it and ensure it doesn't happen again."

You then ask the AI to respond to a new complaint, "I received the wrong item," guiding it to generate a similar style of response.


### 3. Chain-of-thought Prompting: Solving Step by Step

Think of a time when you solved a problem by talking through it step by step. Chain-of-thought prompting is when you guide the AI through a task by breaking it down into smaller, manageable steps. It helps the AI think through complex issues more clearly.

Example: Let's say you want the AI to calculate the total cost of a shopping list. Instead of asking directly, you guide it:

"First, list the prices of apples, bread, and milk."
"Then, add the prices together."

This method helps the AI understand and tackle each part of the problem, leading to a clearer and more accurate answer.

<img width="200" alt="Screenshot 2024-03-17 205109" src="https://github.com/csc301-2024-s/learning-software-engineering.github.io/assets/75962325/86813ee5-69a8-46b3-baa9-c904d37085a9">

In each of these techniques, the key is to communicate effectively with the AI, guiding it to understand and perform tasks it wasn't directly trained to do. Whether you're giving it a brand new challenge, showing it a few examples, or walking it through a problem step by step, these methods enhance how well the AI can assist you.

# Applications
## Function Calling with LLMs

Function calling in Large Language Models (LLMs) is a groundbreaking feature that fundamentally transforms how AI interacts with the digital world. It empowers LLMs to go beyond mere text generation, enabling them to perform specific actions, interact with external APIs, and utilize tools to fetch real-time data or execute tasks. This capability is crucial for developing intelligent applications that require up-to-date information or complex computations, marking a significant leap towards more versatile and practical AI systems.

At its core, function calling acts as a bridge between the AI's understanding of natural language and the execution of digital functions. This means that LLMs can now understand a user's request in natural language, determine the necessary actions to fulfill that request, and execute those actions through predefined functions. It's a vital advancement that enhances the AI's utility, allowing it to provide more accurate, contextually relevant, and timely responses.

## Code Demo for Function Calling

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


