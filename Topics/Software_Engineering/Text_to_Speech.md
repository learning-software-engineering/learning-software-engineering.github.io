# Text to Speech Using Python

## Introduction

Text to Speech (TTS) is a type of assistive technology that reads digital text aloud. Utilizing a combination of natural language processing and digital signal processing, TTS systems convert words from a document or other sources into audible speech. TTS technology is widely used to assist individuals with visual impairments or reading disabilities, improve user engagement, and provide hands-free computing.

In software engineering, TTS can serve multiple purposes across various domains:
- Accessibility: Enhancing the accessibility of applications for users with visual impairments or reading difficulties.
- User Interface: Providing auditory feedback or guidance in applications, improving user experience.
- Multimedia Applications: Generating voiceovers for videos and presentations automatically.
- Virtual Assistants and Chatbots: Enabling conversational interfaces to communicate with users in a more natural, human-like manner.

## TTS Models and Their Set Up

We will introduce three popular TTS models for python. 

### gTTS:

gTTS is a Python library and CLI tool to interface with Google Translate's text-to-speech API. 

Price: Free!

Voice Choices: Only the default voice, but supports most of languages.

Available Functions: Only contain basic text-to-speech conversions.

**Set-up**

- You can very easily install the gTTS library via pip install: 

    ```bash
    pip install gTTS
    ```

**Quickstart**

- Using Command Line:
    ```bash
    gtts-cli 'hello' --output hello.mp3
    ```

- Using Module:
    ```bash
    from gtts import gTTS
    tts = gTTS('hello')
    tts.save('hello.mp3')
    ```

### OpenAI TTS:


OpenAI's text-to-speech (TTS) technology refers to a suite of artificial intelligence models and tools developed to convert written text into spoken words. This technology is built on advanced machine learning and deep learning principles, making it possible to generate highly realistic and natural-sounding voice outputs. OpenAI's TTS systems are designed to understand the nuances of language, including intonation, emotion, and context, allowing them to produce speech that closely mimics human-like articulation and expressiveness.


**Price**: 	$15.00 / 1M characters

**Voice choices**: There are 6 voices to choose from (alloy, echo, fable, onyx, nova, and shimmer)

**Supported output formats**: Opus, AAC, FLAC, WAV, PCM

**Available Functions**: Have two different models: 1. tts-1(optimized for speed) 2. tts-1-hd(optimized for quality)


**Set-up**

- You can easily get the openAPI library via pip install: 

    ```bash
    pip install --upgrade openai
    ```

**Quickstart**

- Set environment:
First, create a local **.env** file in your project folder with the following content:
    ```bash
    # Once you add your API key below, make sure to not share it with anyone! The API key should remain private.
    OPENAI_API_KEY=abc123
    ```

- Import Module:
    ```bash
    from pathlib import Path
    from openai import OpenAI
    ```

- Use Module:
    ```bash
    client = OpenAI()

    speech_file_path = Path(__file__).parent / "speech.mp3"
    response = client.audio.speech.create(
    model="tts-1",
    voice="alloy",
    input="Today is a wonderful day to build something people love!"
    )

    response.stream_to_file(speech_file_path)
    ```
By changing output file name, the output can be configured to any of supported formats. By changing input model name("tts-1", "tts-1-hd"), voice name("alloy", "echo", "fable", "onyx", "nova", and "shimmer"), you can get different output quality and voice.

- Stream real time audio
    ```bash
    client = OpenAI()

    response = client.audio.speech.create(
        model="tts-1",
        voice="alloy",
        input="Hello world! This is a streaming test.",
    )

    response.stream_to_file("output.mp3")
    ```
By using this code, the audio will be able to be played before the full file has been generated and made accessible.



### Google Cloud TTS:



## Comparison Between the Three Models



## Reference

* [Text to Speech Explained](https://speechify.com/blog/text-to-speech-explained-a-comprehensive-guide/)

* [gTTS](https://pypi.org/project/gTTS/)
