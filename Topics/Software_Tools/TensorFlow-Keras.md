# Introduction to AI Frameworks in Software Engineering

## Table of Contents:
- ### [Introduction](#Introduction)
- ### [AI Tools for Software Engineers](#AI-Tools-for-Software-Engineers)
- ### [Frameworks to Build Your Own Models](#Frameworks-to-Build-Your-Own-Models)
- ### [The Purpose of Different Models](#The-Purpose-of-Different-Models)
- ### [Additional Resources](#Additional-Resources)
---

## Introduction
This page will introduce the topic of Artificial Intelligence in Software Engineering, specifically, AI tools for developers to use, popular frameworks for building AI models, and the purpose of different types of AI models. 

Over the last several years, AI has exploded in terms of its capabilities, and as the years continue to progress, AI will continue to improve and become more and more a part of our everyday lives.

Understanding what tools we, as people aspiring to join the technology industry, have at our disposal and what these tools can be used for is becoming increasingly important. 

Being able to utilize the AI models which already exist and building your own AI models for your own purposes are both incredibly vital concepts we must understand in order to implement these tools to the best of their abilities. 

Please note that the following sections are not comprehensive as there are a plethora of different AI tools, frameworks, and model types. This page will only cover the surface of these numerous concepts, focusing on what are the most popular tools, frameworks, and model types currently used by software engineers. 

## AI Tools for Software Engineers

AI tools are becoming increasingly popular to use by programmers as they allow programmers to finish their work at a faster pace and allow for a deeper understanding in concepts programmers may not have as much knowledge on.

Here are some of the most popular AI-based tools used by programmers today:

### [GitHub Copilot](https://github.com/features/copilot):
- GitHub Copilot is a widely used extension-based tool that directly provides contextualized assistance throughout the software development lifecycle.
- Basically, this tool can help with completing your code as well as respond to any questions regarding your code by utilizing the GitHub Copilot Chat extension.
- This tool is supported by almost every major IDE and platform, such as Visual Studio Code, JetBrains IDEs, and Vim.
- Depending on how much information the tool has regarding a specific coding language, you can get immense help. For example:
  - JavaScript is supported incredibly well because of how much information the AI model was able to be trained on.

### [ChatGPT](https://openai.com):
- ChatGPT is by far the most popular AI-based tool, not just for programmers, but for everybody in the world.
- As a chat-based AI tool, you can input any questions, code, or prompts you have in mind and in return, receive a fairly comprehensive explanation/response.
  - However, due to the vast amount of data this AI model has been trained on, it is not able to provide the best answers specifically for code based questions.
- ChatGPT also has an API you can adapt to your own specifications through [transfer learning](https://builtin.com/data-science/transfer-learning#).
- This AI model is able to provide responses to a plethora of input prompts, such as writing basic code, critiquing short stories/essays, and even helping pick out an outfit.

### [Tabnine](https://www.tabnine.com):
- Tabnine is a lesser known AI-based tool for autocompleting code, however, it is still fairly powerful and it has its own strong points.
- This AI model has been fully trained on open-source respositories, meaning that it does not invasively utilize your data for training.
- It can be locally adapted to your codebase and knowledge base without stealing any information, allowing it to combine the universal data the it was trained on with the specificities of your work.
- You can also run this model completely locally, meaning that none of your information is relayed to the company's main database for training or selling.
- It is similar to GitHub Copilot in the sense that it is an extension-based tool which is available on most major IDEs and platforms, and is able to provide assistance with most major programming languages.
- The only real issue with this AI model is that it is only for programmers, it is not able to help with anything outside of code, unlike ChatGPT.

## Frameworks to Build Your Own Models

The AI tools described above are incredibly useful in a majority of scenarios, however, if you need a model to do a very specific task, these AI tools are not going to provide what you need.

In these cases, you can build your own AI model. It sounds incredibly difficult, and for a long time, it was an arduous task which exhausted many resources, but nowadays, you are able to use frameworks to build and train your own custimizable AI model in less than 100 lines.

Here are some of the most popular frameworks used by programmers to build AI models:

### [PyTorch](https://pytorch.org): 
- Pytorch is one of the first frameworks many programmers learn to use in order to build AI models.
- It is one of the simplest frameworks to understand and allows for incredible speed, optimization, and functionality in C++ runtime environments.
- It has a full C++ front-end which allows for programmers procient in C++ to hit the ground running with building their AI model(s).
- TorchServe, which is a tool used in combination with PyTorch, allows programmers to deploy their custom models with incredible ease and makes application integration a breeze.
  - However, when compared to TensorFlow and Keras, PyTorch is more commonly used for research tasks rather than deployment for production.
- As it is one of the most widely used frameworks, there is an incredible amount of guides and information online that can help you learn and debug your PyTorch code.
- It is also available on most major operating systems, specifically Linux, Mac, and Windows, and you can build your model in either Python or C++/Java.

### [TensorFlow](https://www.tensorflow.org):
- TensorFlow is probably the most widely used framework for building and training AI models in the world right now.
- In comparison to PyTorch, it is even simpler to build and train your own AI models and is better at deploying models in production to build AI products.
- This framework provides a tool called [TensorBoard](https://www.tensorflow.org/tensorboard) which graphically displays the data for easy debugging.
- TensorFlow can be used with most popular programming languages. For example:
  - It has a stable API for Python.
  - It has APIs without a backward compatability guarantee for Javascript, C++, and Java.
  - It even has third-party language binding packages for C#, Haskell, Julia, MATLAB, R, Scala, Rust, OCaml, and Crystal.
- This framework also has incredible scalability, meaning that users can develop models using the framework and have it work the same on every device.
- It is completely open source, allowing any user to employ the TensorFlow module whenever and wherever they want without spending any money.
- Two of the issues with this framework is that it lags behind other frameworks, such as PyTorch, in terms of computation speed, and because it is so widely used, the framework is updated very frequently.

### [Keras](https://keras.io):
- Out of the three frameworks listed, Keras is by far the simplest to learn and utilize.
- It has incredible backend support, as it is built on top of Microsoft CNTK, Theano, and TensorFlow, meaning it encourages the employment of backends when building a model.
- Keras has a plethora of pre-trained models, and with a fairly simple and quick use of [transfer learning](https://builtin.com/data-science/transfer-learning#), users do not even need to build and train a model from scratch, saving on time and resources.
- This framework is a high-level API, meaning it is fairly abstracted and more generic, allowing for users to build and train models in quite literally just a few lines of code.
- As it is an incredibly popular framework and is an open-source platform, Keras has a massive community of active users and researchers who constantly help one another and improve the framework.
- However, this framework does have its own set of cons as well. For example:
  - Compared to other frameworks like PyTorch and TensorFlow, Keras just does not have as much features, such as dynamic chart creation.
  - The Keras library's error messages are incredibly ineffective, meaning that it is more difficult to debug your code and understand what exactly went wrong.
  - As Keras is a high-level API, users do not have as much control over manipulating functions.

## The Purpose of Different Models

Utilizing frameworks makes building custom AI models incredibly simple, however, frameworks do not tell you what kind of model you should build for your specific task.

There are so many possible types of models users can implement depending on what they are building the model for, so it is important to understand what the purpose of different models are and where each of them excel.

Before understanding which models to use, it is important to understand how AI models are trained. 

There are three possible ways an AI model can be trained:
- Supervised Learning: the AI model learns from **labeled data**, where each data point is associated with a known output or target value.
- Unsupervised Learning: the AI model learns from **unlabeled data**, where no predefined output or target value exists for each data point. The model autonomously seeks patterns or structures within the data without explicit guidance.
- Reinforcement Learning: the AI model learns from **its interactions with the environment**, receiving feedback based on its actions. The objective is to optimize rewards or minimize penalties by exploring various actions and their resulting outcomes and picking the best option out of all of them. 

Now, we can actually discuss different types of AI models and when they are used.

Here are some of the most popular AI model types used by programmers to build AI models:

### [Linear Regression](https://www.analyticsvidhya.com/blog/2021/10/everything-you-need-to-know-about-linear-regression/):
- Linear regression models are one of the most common AI model types used.
- It employs a simple mathematical function to establish a linear relationship, mapping the input data to the output data.
- These models are usually trained in a supervised manner.
- A linear regression model should be used when the programmer can assume that there is a linear relationship between the input and the output. For example:
  - An AI model that predicts house prices might use a linear function that takes into account factors (inputs) such as size, location, change in house price over the years, etc.
- In general, linear regression models should be used when you need to predict a numeric outcome, like sales, temperature, or scores, but it can also be used when you need to predict the class of an input.

### [Deep Neural Networks](https://www.bmc.com/blogs/deep-neural-network/):
- Neural networks are one of the most popular implementations of AI models.
- It consists of several layers of interconnected nodes (or neurons) organized into an input layer, one or more hidden layers, and an output layer.
- The design of this AI model type is actually based on the human brain's neural network, which is why the internal nodes of a neural network are also called neurons.
- These models are usually trained in a supervised manner, however, there are variations of neural networks designed for unsupervised learning and reinforcement learning. For example:
  - Autoencoders and certain types of generative models are variations of neural networks designed for unsupervised learning.
  - Deep Q-networks are a variation of neural networks designed for reinforcement learning.
- Neural networks are used for an incredible number of tasks, such as speech recognition, image recognition/classification, and natural language processing.

### [Decision Trees](https://www.analyticsvidhya.com/blog/2021/08/decision-tree-algorithm/):
- Decision trees are one of the most basic yet effective ways models make predictions, sometimes even beating out neural networks and other more advanced AI models.
- Decision trees represent a flowchart-like structure where each internal node represents a decision based on an attribute, each branch represents an outcome of that decision, and each leaf node represents the final prediction or classification.
- These models are usually trained in a supervised manner, however, they can also be used in unsupervised learning scenarios, such as clustering.
- Decision trees are typically used for simpler tasks such as classification of inputs.

## Additional Resources
- [5 AI Tools Every Software Developer Should Be Using In 2023](https://medium.com/geekculture/5-ai-tools-every-software-developer-should-be-using-in-2022-afc4fb149c60)
- [TensorFlow vs PyTorch: Deep Learning Frameworks \[2023\]](https://www.knowledgehut.com/blog/data-science/pytorch-vs-tensorflow#)
- [PyTorch vs Tensorflow vs Keras](https://www.datacamp.com/tutorial/pytorch-vs-tensorflow-vs-keras#)
- [Best AI Models: Types and How to Choose Them](https://dataconomy.com/2023/04/04/best-ai-models-types-how-to-choose-what-is/)
