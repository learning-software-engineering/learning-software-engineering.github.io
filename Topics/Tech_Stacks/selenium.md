# Webscraping and Automation Using Selenium with Python

## What is Selenium?
Selenium is an open-source browser automation framework that can be used within many different programming languages, including Python. From the [official documentation](https://www.selenium.dev/documentation/) this is a list compiled of languages and their support of Selenium. 

| Programming Language | Selenium Support                             |
|----------------------|----------------------------------------------|
| **Java**              | Main language for Selenium. Officially supported with Selenium WebDriver. |
| **Python**            | Widely used for Selenium scripting. Supported with Selenium WebDriver. |
| **C#**                | Supported with Selenium WebDriver. Often used in combination with the .NET framework. |
| **JavaScript**        | Supported for browser automation with Selenium WebDriver. Popular for frontend testing using tools like Protractor. |
| **Ruby**              | Has Selenium support through libraries like Watir and Capybara. |
| **Kotlin**            | Interoperable with Java, can use Java Selenium bindings. |
| **Groovy**            | Compatible with Java, often used with Selenium. |
| **PHP**               | Selenium bindings available for PHP. |
| **Perl**              | Selenium bindings available for Perl. |
| **Swift**             | Selenium bindings available for Swift. |
| **Objective-C**       | Selenium bindings available for Objective-C. |
| **R**                 | Selenium bindings available for R. |
| **C++**               | Limited support through third-party libraries. |
| **Go**                | Limited support through third-party libraries. |

However, for the purposes of this introduction, we will refer to Selenium usage in **Python**.

## What can I do with Selenium?
Selenium has uses within automating browser interactivity, such as extracting information from the web and interacting with elements such as buttons and forms. It is an important tool used in automation to execute a plethora of different test cases you may want to perform on a website you are developing. If you are interested in learning more about using Selenium for testing purposes, you can check out [this guide](https://www.simplilearn.com/tutorials/python-tutorial/selenium-with-python#:~:text=Selenium%20with%20Python%20is%20used,skimming%20the%20entire%20site%2C%20etc.).

## Getting started
1. **Install Selenium bindings**

    The easiest way to install Selenium is with the `pip package manager`. With Python and pip installed, simply run the following command to get the latest version.
    
    ```bash
    pip install selenium
    ```
    
    You can then run the following command to see if you successfully installed Selenium.
    
    ```bash
    pip show selenium
    ```
    
    If the installation was successful, the output should be similar to the following.
    
    ```bash
    Name: selenium
    Version: 4.15.2
    Summary: 
    Home-page: https://www.selenium.dev
    Author: 
    Author-email: 
    License: Apache 2.0
    Location: /Users/john/CSC301/venv/lib/python3.11/site-packages
    Requires: certifi, trio, trio-websocket, urllib3
    Required-by: 
    ```
2. **Install Chrome WebDriver**

    Now, download the appropriate Chrome WebDriver version matching your Chrome browser version and place it in the project directory.

3. **Start Writing Code**

    At this point, you are ready to start using Selenium. Now you can import the specific functionality you want within Selenium with the import statement `from selenium import [specific module]` to fit your specific use cases.

## Headless drivers

If you are running your scripts from a headless terminal (with no GUI), or don't want the browser actions to be visible, you can use selenium with a headless WebDriver. This is useful if your testing environment is a server that you are connected to with SSH. 

With Python, you can accomplish this by using `pyvirtualdisplay`. Before your Selenium interaction, initiate your virtual display using:
```python
display = Display(visible=0, size=(800, 600))
display.start()
```

Then, after the interaction runs, close your virtual display.
```python
display.close()
```
Typically, you would use a _try, except, finally_ statement to execute the code, and you would instantiate the display at the top of the `try` block, and close it at the end of the `finally `block.

## Automation

The Selenium WebDriver can be used for many purposes, including logging in to websites, filling out forms, and clicking buttons. For example, if there is a particular task that you need to do every day that requires you to login to a website, and then navigate to a certian page this is a simple task in Selenium. You can then automate this script to run at a given time interval on a linux server using `cron`. For example, you could include this following line your _crontab_ to schedule the script to run at midnight everyday:

```bash
0 0 * * * python3 /path/to/selenium/script.py
```

You can learn more about what the numbers and wildcards mean [here](https://crontab.guru/once-a-day), or you can check out the [linux man page](https://man7.org/linux/man-pages/man5/crontab.5.html) to learn more about cron.

## Acknowledgements:
- **Selenium**: Selenium is an open-source framework for automating browser interactions. To learn more about Selenium and its capabilities, please visit the official Selenium website: [Selenium Documentation](https://www.selenium.dev/documentation/en/)
- **Chrome WebDriver**: The Chrome WebDriver is a tool provided by Selenium for automating interactions with the Chrome browser. For detailed documentation and instructions on using Chrome WebDriver, please refer to the official ChromeDriver documentation: [ChromeDriver Documentation](https://sites.google.com/a/chromium.org/chromedriver/)

