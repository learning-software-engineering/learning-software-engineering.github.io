# Introduction to the OpenAI API in Python

OpenAI has emerged as the global leader in Large Language Models (LLMs), and has productionized such models into hits like ChatGPT, GitHub Copilot, and more. They've released an API that developers can use to query its sophisticated models using Curl, Node.js, or Python. This tutorial is for the Python version.

Let's dive in.


_Note that the API's credits are not free! You get 3 months of free credit upon creation of an OpenAI account, but after you must pay. Visit their [pricing](https://openai.com/pricing) page for detailed pricing_

## Set-up
- First, make sure you are setup with Python 3.7.1 or newer (necessary), and have a basic environment manager like conda set up (reccomended). 

- You can very easily install the openai library via a simple pip install: 

    ```bash
    pip install --upgrade openai
    ```

    Or conda install: 
    ```bash
    conda install -c conda-forge openai
    ```

## Setting up API key
- Head to the [API Keys](https://platform.openai.com/api-keys) page and create a new key. Note that as soon as you see the key on screen, this is the last time you will see it! So be sure to copy it to a safe place on your machine.

- Head to your project and create a .env file. _Make sure you add .env to your .gitignore as we will put your API key in this file!_ Add the following line to your .env: 

    ```
    OPENAI_API_KEY=your_key
    ```
    where 'your_key' is replaced by the string provided on the API Keys page.

- In the .py file you'd like to use the API in, run the following: 

    ```python
    from openai import OpenAI

    client = OpenAI()
    ```

- If you get this error: 

    ```
    openai.OpenAIError: The api_key client option must be set either by passing api_key to the client or by setting the OPENAI_API_KEY environment variable
    ```

    Then this means your Python is not able to access your environment variables properly. To force this, we can add the following lines: 

    ```python
    from openai import OpenAI
    from dotenv import load_dotenv # import dotenv
    load_dotenv() # loads the environment variables from .env file
    client = OpenAI()
    ```


## Prompting OpenAI models via the API

- The GPT models work by providing the sequence of characters most likely to come after the prompt. So when you ask ChatGPT a question, its not 'answering the question', its 'finishing the prompt'. With that in mind, we can do some simple prompt completion: 

    ```python
    completion = client.chat.completions.create(
    model="gpt-3.5-turbo", # OpenAI's current standard model. Fast and cheap!
    messages=[
        {"role": "user", "content": "Come up with a name for my new strawberry ice cream flavor!"}
    ]
    )

    print(completion.choices[0].message.content)

    ```

    The output I get is 

    ```
    "Berry Bliss"
    ```

- You can play around with the model to understand its behvaior. One cool feature is you can feed in a full conversation. A great example from the OpenAI API Documentation is: 

    ```python
    response = client.chat.completions.create(
    model="gpt-3.5-turbo",
    messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {"role": "user", "content": "Who won the world series in 2020?"},
        {"role": "assistant", "content": "The Los Angeles Dodgers won the World Series in 2020."},
        {"role": "user", "content": "Where was it played?"}
    ]
    )
    ```

    What this allows you to do is feed in a full conversation. Each input has an associated 'role'. "system" is for giving the model instructions on how to behave. E.g. "Be a useful assistant" or "Be a detailed explainer of all things math". "user" prompts are those that come from the user. So in this example, the user has already fed the system a request regarding the world series. The "assistant" role is for providing previous model answers! So the model answered saying the LA Dodgers won. The user follows up with a new question, and then this whole conversation is fed into the model to respond. Pretty cool right? 




## Conclusion


These are just some of the things you can do with the OpenAI API. They have other models that are more sophisticated, and even ones that can process images. Just be sure to check out the pricing page to ensure you don't over spend. Luckily, the prices are fairly low, at fractions of a cent per prompt, and the lowest credit buy in is just $5 USD. 



## Resources

https://platform.openai.com/docs/guides/text-generation/chat-completions-api
https://openai.com/pricing
https://www.youtube.com/watch?v=uRQH2CFvedY