# Using the VertexAI SDK

In this page we will go over what VertexAI is and how to get started with using it in python to use generative AI in your projects.

## What is VertexAI

VertexAI is a platform offered by Google Cloud Protocols that allows users to seamlessly integrate generative AI into their applications.
The platform allows users to access PALM2, which is Google's state of the art large language model (LLM), train their own models, and deploy their own models for production use.

You can read more at their own website. [VertexAI](https://cloud.google.com/vertex-ai?hl=en)

## Getting started with VertexAI

In this article we will provide a quick start guide to using Google's PALM2 model in python.

### Creating a Google Cloud Account

To use VertexAI we must first create a Google Cloud Account. When you first sign up everyone gets a certain amount of free credits for you to use. Visit The following site and sign up for free using an existing or a new Google account. [Create your Account](https://cloud.google.com/)

### Accessing VertexAI

To navigate to the VertexAI page, visit the Products and Solutions page found in the Navigation menu on the top left corner of your console. In the Products and Solutions page, scroll to the section on Artificial Intelligence and click on VertexAI. Alternitavely, you can search for VertexAI in the search bar or you can visit the following link [VertexAI](https://console.cloud.google.com/vertex-ai).

### Using VertexAI Online

For this section we will focus on using generative AI. VertexAI offers 3 types of generative AI, text, vision, and speech. To try out the generative AI online visit the generative AI studio on the left hand side. Here you can choose which generative AI you want to use, but we will focus on using text generation so click on Language. Here you can choose to checkout their premade prompts, or you can create your own prompts by clicking text prompts at the top of the page. Here you can test out different prompts, different models, and different parameters. Their are 2 options for creating prompts, freeform or structured, you can make your selection on the top right corner. Any prompts that you make can also be saved in the top right corner for you to look back on.

### Using the VertexAI SDK in Python

#### Setup

To use the VertexAI SDK have Python installed with version above 3.7. You can install install Python [here](https://www.python.org/downloads/).

Next, activate all required API's on your dashboard of the VertexAI Page, this will require you to link billing to your account.

Now install the VertexAI library using pip. you may choose to do this step in a Virtual Environment.

```
pip install google-cloud-aiplatform
```

To use the VertexSDK we must first authenticate ourselves using credentials. We will do this by creating a service account. You can find the instructions [here](https://developers.google.com/workspace/guides/create-credentials). In short, create a service account in your google cloud console and assign it permissions to access API's, then create a key for it and select to save it as a JSON and download the created _credentials.json_ file into your working directory.

#### Usage

First, we will import the required packages

```python
import vertexai
from vertexai.language_models import TextGenerationModel
from google.oauth2 import service_account
```

Next, we will initialize the SDK and authenticate ourselves. You can find the project name and location by going to the VertexAI page, visiting the [generative studio](https://console.cloud.google.com/vertex-ai/generative/language/create/text), and using one of the models. In the top right corner there should be a button, view code. In the code you can find the project name and location. Now initialize your self with the following code snippet.

```py
vertexai.init(project="project", location="location", credentials=service_account.Credentials.from_service_account_file('credentials.json'))
```

Now you can use PALM2 with the following code. Change the parameters and prompt to be your own!

```py
parameters = {
    "candidate_count": 1,
    "max_output_tokens": 1024,
    "temperature": 0.2,
    "top_p": 0.8,
    "top_k": 40
}
model = TextGenerationModel.from_pretrained("text-bison")
response = model.predict(
    """Write your prompt here!

    """,
    **parameters
)
print(f"Response from Model: {response.text}")
```

### Conclusion

This article was guide for getting started with using the VertexAI SDK for the purpose of integrating generative AI into your applications. The provided instructions and code snippets showed how to use the generative AI studio by Google and how to use the VertexAI SDK in python to use PALM2 in python. Hopefully, you were able to learn how to get started with integrating PALM2 into your applications. Below are further readings that can help you use the other features that VertexAI offers and more in-depth guides.

### Articles and Resources

[More information on VertexAI](https://cloud.google.com/vertex-ai/docs/start/introduction-unified-platform)  
[VertexAI SDK Documentation](https://cloud.google.com/python/docs/reference/aiplatform/latest/index.html)  
[Creating Access Credentials](https://developers.google.com/workspace/guides/create-credentials)
