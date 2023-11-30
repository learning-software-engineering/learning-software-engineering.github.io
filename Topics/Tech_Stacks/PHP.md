# Learning PHP

## Table of contents
### [Introduction](#introduction-1)
### [Why use PHP](#why-use-php-1)
### [Setup](#setup-1)
### [PHP Basics](#php-basics-1)
### [PHP Example Use Cases](#php-example-use-cases-1)
### [Additional Resources](#additional-resources-1)


## Introduction
PHP stands for Hypertext Preprocessor, and it is a server-side scripting language designed for web development written in C. This makes it different from client-side languages such as JavaScript, which is executed on the client's browser rather than the web server. PHP is embedded within HTML code and is widely used to create dynamic and interactive web pages. It can be used to perform various tasks such as collecting form data, generating dynamic page content, managing databases, handling cookies and sessions, and more.

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

However the above example is the exact same as this static HTML page:
```html
<!DOCTYPE html>
<html>
<body>

<h1>My first PHP page</h1>

Hello World!

</body>
</html>
```
Let's take a look at a few more complex examples of PHP in action.

## PHP Example Use Cases
### Variables
Variables are used to store information. PHP has no command for declaring a variable. A variable is created the moment you first assign a value to it. Variables in PHP start with the $ sign, followed by the name of the variable. Variable names are case-sensitive. 

```php
<?php
    $txt = "Hello World!";
    $x = 5;
    $y = 10.5;
?>
```
In the above example, we have created three variables: $txt, $x, and $y. $txt stores the string "Hello World!", $x stores the integer 5, and $y stores the float 10.5. We can output the values of these variables in our HTML document using echo:
```php
<!DOCTYPE html>
<html>
<body>

<?php
    // Display variables in a HTML list
    $txt = "Hello World!";
    $x = 5;
    $y = 10.5;
    echo "<ul>";
    echo "<li>$txt</li>";
    echo "<li>$x</li>";
    echo "<li>$y</li>";
    echo "</ul>";
?>

</body>
</html>
```
You can see that in the above echo calls we don't just use the variables, but we also include HTML tags. By employing more powerful logic, we can make more complex reactive web pages, as PHP can be used to dynamically generate HTML content.   

In addition to variables PHP has much of the functionality you would expect from a programming language, such as loops, conditionals, functions, and more. You can learn more about the specific PHP syntax for those operations [here](https://www.w3schools.com/php/php_if_else.asp).

### JavaScript
We can also run JavaScript code directly in PHP. This allows us to use PHP together with JavaScript to create dynamic web pages.
```php
<!DOCTYPE html>
<html>
<body>

<?php
    // Generate a random number between 1 and 10
    $randomNumber = rand(1, 10);
    echo "<p>Random number: $randomNumber</p>";
?>

<script>
    // Use the random number in a JavaScript function
    function multiplyByRandomNumber(num) {
        return num * <?php echo $randomNumber; ?>;
    }
    document.write('<p>5 * random number = ' + multiplyByRandomNumber(5) + '</p>');
</script>

</body>
</html>
```
In the example above we use the PHP rand() function to generate a random number between 1 and 10 and store it in the $randomNumber variable. We then use the PHP echo function to output the value of $randomNumber in the JavaScript function. This allows us to use the PHP variable in the JavaScript function.

### Forms
PHP can also be used to handle form data. In the following example, we have a simple HTML form that asks the user to enter their name. When the user submits the form, the PHP script will display the name they entered.
```php
<!DOCTYPE html>
<html>
<body>

<form method="post" action="<?php echo $_SERVER['PHP_SELF'];?>">
    Name: <input type="text" name="name">
    <input type="submit">
</form>

<?php
    if ($_SERVER["REQUEST_METHOD"] == "POST") {
        // collect value of input field
        $name = $_POST['name'];
        if (empty($name)) {
            echo "Name is empty";
        } else {
            echo "Hello $name!";
        }
    }
?>

</body>
</html>
```
### Databases
PHP can also be used to connect to databases. In the following example, we connect to a MySQL database and display the contents of a table.
```php
<!DOCTYPE html>
<html>
<body>

<?php
// Replace these values with your actual database credentials
$servername = "your_servername";
$username = "your_username";
$password = "your_password";
$dbname = "your_dbname";

// Create connection
$conn = new mysqli($servername, $username, $password, $dbname);

// Check connection
if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}

// SQL query to retrieve data from the table
$sql = "SELECT * FROM example_table";
$result = $conn->query($sql);

// Display table if there are results
if ($result->num_rows > 0) {
    echo "<table>";
    echo "<tr><th>ID</th><th>Name</th><th>Description</th></tr>";

    // Output data of each row
    while($row = $result->fetch_assoc()) {
        echo "<tr><td>" . $row["id"] . "</td><td>" . $row["name"] . "</td><td>" . $row["description"] . "</td></tr>";
    }

    echo "</table>";
} else {
    echo "0 results";
}

// Close connection
$conn->close();
?>

</body>
</html>
```

The above examples are just a few of the many ways PHP can be used. You can learn more about PHP and its extensive uses through the following resources.

## Additional Resources
- Much of the information in this guide was taken from [this tutorial](https://www.w3schools.com/php/default.asp) by W3Schools. You can find more information about PHP including a step-by-step tutorial on how to get started, as well as more advanced topics such as PHP forms, PHP cookies, PHP sessions, PHP filters, PHP MySQL, and PHP OOP on their website.
- For a great and indepth way of getting started with PHP, check out [this YouTube course by FreeCodeCamp](https://www.youtube.com/watch?v=OK_JCtrrv-c&ab_channel=freeCodeCamp.org).
- For a tutorial specific to web development with PHP, check out [this video by Simplilearn](https://www.youtube.com/watch?v=PGvrnas2_Pk).