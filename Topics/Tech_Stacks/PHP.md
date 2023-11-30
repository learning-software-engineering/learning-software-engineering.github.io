# Learning PHP

## Table of contents
### [Introduction](#introduction-1)
### [Why use PHP](#why-use-php-1)
### [Setup](#setup-1)
### [PHP Basics](#php-basics-1)
### [Additional Resources](#additional-resources-1)


## Introduction
PHP stands for Hypertext Preprocessor, and it is a server-side scripting language designed for web development. This makes it different from client-side languages such as JavaScript, which is executed on the client's browser rather than the web server. PHP is embedded within HTML code and is widely used to create dynamic and interactive web pages. It can be used to perform various tasks such as collecting form data, generating dynamic page content, managing databases, handling cookies and sessions, and more.

Before continuing to learn PHP it is recommended to have a basic understanding of the commmon web development languages:
- HTML
- CSS
- JavaScript

## Why use PHP
You may have heard PHP reffered to as a "dying language", but it is still widely used in web development. In fact, it is estimated that over 75% of [websites](https://w3techs.com/technologies/details/pl-php) use PHP in some way. PHP is a great choice for web development because it is easy to learn and use, as well as being free and open-source.

Additional advantages of PHP include:
- It's cross-platform and flexbility, meaning it can run on any operating system and can be used to create a wide variety of web applications.
- It's fast and efficient, and it is supported by most web hosting services. (It's estimated to be 3 times faster than Python!) This makes PHP sites load faster and use less server resources.
- It has a large community of developers and users that can provide support and resources.
- It's scalable, and it can be used to create large-scale applications.

You can learn more about the advantages and disadvantages of PHP [here](https://anywhere.epam.com/business/pros-and-cons-of-php).
## Setup
To set up PHP on your machine, you will need:
- A web server
- A database
- PHP

The official PHP website provides a [guide](https://www.php.net/manual/en/install.php) on how to install PHP on your machine. Additionaly, you can find a video tutorial on how to install PHP on Windows [here](https://www.youtube.com/watch?v=DTy57Hg1jCk).

## PHP Basics
You can write PHP scripts at any point in an HTML document. The syntax for PHP scripts is as follows:
```php
<?php
    // PHP code goes here
?>
```
As we can see the script starts with `<?php` and ends with `?>`. Any code in between these tags will be executed by the PHP engine.

To demonstrate how PHP works, let's create a simple "Hello World" static web page. First, create a new file called `index.php` and add the following code:
```php
<!DOCTYPE html>
<html>
<body>

<h1>My first PHP page</h1>

<?php
echo "Hello World!";
?>

</body>
</html>
```
In the above example, we have a simple HTML document with a heading and a PHP script that prints "Hello World!". If we open this file in a browser, we will see the following output:
```
My first PHP page
Hello World!
```
As we can see, the PHP script is embedded directly within the HTML code. By using echo, we can output text to the browser. 

## Additional Resources
- Much of the information in this guide was taken from [this tutorial](https://www.w3schools.com/php/default.asp) by W3Schools. You can find more information about PHP as well as a step-by-step tutorial on how to get started with PHP on their website.
- For a great and indepth way of getting started with PHP, check out [this YouTube course by FreeCodeCamp](https://www.youtube.com/watch?v=OK_JCtrrv-c&ab_channel=freeCodeCamp.org).
