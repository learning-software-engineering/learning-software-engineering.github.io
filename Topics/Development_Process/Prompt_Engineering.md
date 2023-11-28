## Introduction to Prompt Engineering

Prompt engineering is the art and science of designing input queries (prompts) to generate the desired output from language models like PaLM2 and GPT. The quality of the output is directly influenced by how well the prompt is structured, making this skill vital for those utilizing language models in their applications.

When structuring prompts, it is crucial to consider clarity, context, and specificity. A well-engineered prompt should be clear and concise, providing enough context to guide the model towards the intended output without being overly specific, which may limit the model's creativity or lead to biased responses.


## Steps for Structuring Highly-Effective Prompts

1. Understand Your Model: Know the capabilities and limitations of your model to set realistic expectations for its output​​.

2. Define the Input: Clearly state what you want the model to respond to. This can be a direct question, a task you want the model to perform, an entity to operate on, or a completion of a given text​​.

3. Provide Context: Offer additional information and instructions that specify how the model should behave or what information it should consider when generating a response​​.

4. Use Examples: Include input-output pairs to demonstrate the format or style of response you're looking for. This can help the model understand the pattern it should follow​​.

5. Clear Instructions: Tell the model exactly what to do in a straightforward manner. Clarity is key to preventing misinterpretation by the model​​.

6. Partial Inputs: Let the model complete a thought or statement. This method leverages the model's predictive capabilities and can be especially powerful when combined with examples and context​​.

7. Contextual Information: Provide all necessary information within the prompt, especially if the task requires specific knowledge or constraints​​.

8. Prefixes: Use prefixes to indicate different sections or types of content within your prompt, helping the model understand and categorize the information more effectively​​.

9. Adjust Parameters: Experiment with parameters like max output tokens, temperature, top-K, and top-P to fine-tune the creativity and randomness of the responses​​.

10. Iterative Design: Prompt engineering is rarely perfect on the first try. Iterate on your prompt based on the responses you get, refining until you achieve the desired output​​.


## Writing Prompts - A Sample Scenario

Suppose you are an educator and you want the llm to generate 5 MCQ's for you based on certain text that you provide. You want the output in json format
This is how a good prompt is structured:

"Context: You are a teacher who wants to create multiple-choice questions based on readings given to the students.

 Example Text: The Tinder Fire was a wildfire that burned 16,309 acres (66.00 km2) of the Coconino National Forest in the U.S. state of Arizona during April and May 2018. 

 Example output: "{\"Question\": \"When did the Tinder Fire occur\", \"Answer\": \"A\", \"A\": \"April and May 2018\", \"B\": \"April and May 2019\", \"C\": \"May and June 2018\", \"D\": \"Jan and Feb 2018\"}"

 Using the following information and nothing else, generate 5 Multiple Choice questions based on the information above and return them in JSON format.
 Exactly follow the JSON format of the example question below. Each question should be separated by "&&" and nothing else.
 
 Actual Text: {text you want to provide}"


The provided prompt is well-structured for the following reasons:

1. Clarity of Task: It clearly defines the context and role of the user, in this case, an educator, setting a clear purpose for the language model's task of generating multiple-choice questions.

2. Specific Example: By including an example of the desired output in JSON format, the prompt sets explicit expectations for the structure and content of the language model's responses, reducing ambiguity.

3. Precise Instructions: The prompt specifies the exact number of questions, the separation character, and the information to be used, guiding the model to produce a well-organized and focused output.

For the similar scenario, this is one example of a bad prompt:

"Context: You are a teacher who wants to create multiple-choice questions based on readings given to the students.
 Using the following information and nothing else, generate 5 Multiple Choice questions based on the information above and return them in JSON format.
 Text:{text you want to provide} "


The provided prompt is not well-structured for the following reasons:

1. Lack of Example Text: Unlike the good prompt, the bad prompt does not include example text to demonstrate the type of content from which the questions should be derived. This omission can lead to confusion about the scope and nature of the content being tested.

2. Absence of Output Format Description: The bad prompt fails to specify how the JSON format should be structured, unlike the good prompt which includes a detailed example. This lack of clarity can result in varied and potentially incorrect output formats.

3. Vagueness in Instruction: The second prompt is vague in its instructions, missing out on details such as the level of difficulty of the questions or the specific areas of the text to focus on, which could lead to a mismatch in expectations and actual output.


## What LLM should you choose?

Here are few popular LLM's you can make use of:

1. LLaMA-2: This model, developed by Meta, is known for its efficiency and scalability, making it suitable for research and development in language understanding and generation. LLaMA-2 is designed to be adaptable to various computational settings, from large-scale servers to smaller, more constrained environments.

2. PaLM-2 (Pathways Language Model): Developed by Google, PaLM-2 is recognized for its advanced capabilities in language understanding, reasoning, and generation. It's particularly adept at handling complex natural language processing tasks, making it suitable for applications requiring deep linguistic analysis and nuanced language generation.

3. GPT (OpenAI): Known for powering ChatGPT, GPT models like GPT-3.5 and GPT-4 are versatile, handling complex reasoning, understanding, and coding tasks. GPT-4, in particular, is multimodal, capable of processing both text and images, making it suitable for a wide range of general-purpose applications​​.

4. BLOOM: An open-access, multilingual language model optimized for text generation and exploring language characteristics. It can generate text in 13 programming languages and 46 natural languages, suitable for multilingual text generation and language studies​​.

5. Claude: Developed by Anthropic, this model is designed for high-reliability text processing tasks including text summarization, creative writing, coding, and search. It offers variations like "Claude Instant" for faster performance​​.

6. Cohere: Created by former Google Brain team members, Cohere offers a range of models for different use cases. Its Cohere Command model is notable for its robustness and accuracy, making it suitable for diverse applications, from content creation to business analytics​​.

7. Falcon: A series of open-source LLMs known for exceptional performance in reasoning and language tasks. The Falcon models, including Falcon 180B, are suitable for applications requiring high-performance language understanding and reasoning​


## Additional Resources

1. How to Talk to an LLM: LLM Prompt Engineering for Beginners - UC Today : (https://www.uctoday.com/unified-communications/how-to-talk-to-an-llm-llm-prompt-engineering-for-beginners/#:~:text=,depth%20task%20descriptions)

2. Master Prompt Engineering: Demystifying Prompting Through a Structured Approach : (https://promptengineering.org/master-prompt-engineering-demystifying-prompting-through-a-structured-approach/#:~:text=,can%20quickly%20grasp%20your%20intent) 

3. A guide to prompting LlaMA2 : (https://replicate.com/blog/how-to-prompt-llama) 

Here are resources for the LLM's discusses above:

4. BLOOM: https://bigscience.huggingface.co/blog/bloom 

5. Claude: https://bigscience.huggingface.co/blog/bloom

6. Cohere: https://cohere.com/

7. GPT: https://openai.com/blog/chatgpt/

8. LlaMA2: https://ai.meta.com/llama/

9. PaLM2: https://ai.google/discover/palm2