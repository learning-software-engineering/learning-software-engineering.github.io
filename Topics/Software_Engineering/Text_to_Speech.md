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



### Google Cloud TTS:



## Comparison Between the Three Models



## Reference

* [Text to Speech Explained](https://speechify.com/blog/text-to-speech-explained-a-comprehensive-guide/)

* [gTTS](https://pypi.org/project/gTTS/)
