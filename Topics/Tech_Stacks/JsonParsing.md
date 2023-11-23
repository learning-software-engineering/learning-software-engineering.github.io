# Introduction to JSON Parsing



## Introduction to JSON

JSON (JavaScript Object Notation), is a lightweight and human-readable data interchange format. It serves as a standard data format for transmitting and exchanging data between a server and a web application, as well as between different parts of an application. JSON is language-agnostic, meaning it can be easily understood and used by various programming languages.


## JSON Data Types

### Primitive Data Types

JSON supports several primitive data types. These primitive data types are the basic building blocks used to represent values within a JSON structure. The primary primitive data types in JSON are: 

 * String: Represents a sequence of characters enclosed in double quotation marks (")
  
    Example: "Hello, World!" 


 * Number: Represents numeric values, including integers and floating-point numbers.
    
    Examples: 42, 3.14, -17 

 * Boolean: Represents a logical value, either true or false. 
    
    Examples: true, false 

 * Null: Represents an empty value or the absence of a value. 
    
    Example: null

These primitive data types can be used alone or combined to create more complex JSON structures such as objects and arrays. For example, an object may contain key-value pairs where the values can be strings, numbers, booleans, null, or even nested objects and arrays.

### Complex Data Types

JSON allows for the construction of more complex data structures beyond primitive data types by using objects and arrays. 

 * Objects: An object in JSON is an unordered collection of key-value pairs. Key-value pairs are separated by commas and enclosed in curly braces {}. Keys must be strings, and values can be strings, numbers, booleans, null, objects, or arrays. 
 Example:


{
  "name": "John Doe",
  "age": 30,
  "isStudent": false,
  "address": {
    "city": "Exampleville",
    "zipcode": "12345"
  }
}

 * Array: An array in JSON is an ordered list of values. Values are separated by commas and enclosed in square brackets []. Values can be strings, numbers, booleans, null, objects, or other arrays. 
 Example:

 [
  "apple",
  "banana",
  "orange",
  {
    "color": "red",
    "quantity": 5
  }
]

## JSON Parsing in Different Programming Languages

### Python Parse JSON

#### Parse JSON String in Python

Python has a built in module that allows you to work with JSON data. At the top of your file, you will need to import the json module.

```{python}
import json
```


If you need to parse a JSON string that returns a dictionary, then you can use the json.loads() method.
```{python}
import json

# assigns a JSON string to a variable called jess 
jess = '{"name": "Jessica Wilkins", "hobbies": ["music", "watching TV", "hanging out with friends"]}'

# parses the data and assigns it to a variable called jess_dict
jess_dict = json.loads(jess)

# Printed output: {"name": "Jessica Wilkins", "hobbies": ["music", "watching TV", "hanging out with friends"]}
print(jess_dict)

```

#### Parse and Read JSON File in Python

Suppose we have a JSON file called fcc.json. If we want to read that file, we first need to use Python's built-in `open()` function with the mode of read. We are using the `with` keyword to make sure that the file is properly closed.

```{python}
with open('fcc.json', 'r') as fcc_file:
```
We can then parse the file using the json.load() method and assign it to a variable called fcc_data.

```{python}
fcc_data = json.load(fcc_file)
```
The final step would be to print the results.

```{python}
print(fcc_data)
```

### JavaScript Parse JSON

#### Parse JSON String in JavaScript

The `JSON.parse()` static method parses a JSON string, constructing the JavaScript value or object described by the string. 

```{python}
const json = '{"result":true, "count":42}';
const obj = JSON.parse(json);

console.log(obj.count);
# Expected output: 42

console.log(obj.result);
# Expected output: true

```
#### Parse JSON File in JavaScript

Suppose we have a json file called sample.json under your the current directory. 

We can use the `fetch()` method: Open the JavaScript file, In the `fetch()` method pass the address of the file, use the `.json` method to parse the document and display the content on the console

```{python}
function Func() {
    fetch("./sample.json")
        .then((res) => {
        return res.json();
    })
    .then((data) => console.log(data));
}
```

We can also use the `require` method using require module: Create a script.js and use the require method of the node to import the JSON file.

```{python}
const sample = require('./sample.json'); 
console.log(sample);
```

To run the application, we can open the current folder in the terminal and type the following command

```{python}
node script.js
```

### Parse JSON in Java

#### Read JSON File in Java

To read the JSON file in Java, `FileReader()` method is used to read given JSON file.

Example: 

```{python}
{

    "name" : "Kotte",
    "college" : "BVRIT"

}
```

The above code is the file that is used to read. we use the `json.simple` library.

```{python}
// program for reading a JSON file

import org.json.simple.JSONArray;
import org.json.simple.JSONObject;
import org.json.simple.parser.*;

public class JSON
{
  public static void main(Strings args[])
  {

    // file name is File.json
    Object o = new JSONParser().parse(new FileReader(File.json));

    JSONObject j = (JSONObject) o;

    String Name = (String) j.get("Name");
    String College = (String) j.get("College");

    System.out.println("Name :" + Name);
    System.out.println("College :" +College);

  }

}

```

Output:

```{python}
Name: Kotte

College: BVRIT
```

## Parsing Optimization

JSON parse optimization is crucial for achieving optimal performance, resource efficiency, and a seamless user experience in applications that handle JSON data. It becomes particularly relevant in scenarios involving large datasets, real-time updates, and applications with high concurrency and scalability requirements. Performance optimization in the context of JSON involves strategic measures to enhance the efficiency of handling and transmitting JSON data. This includes focusing on two key aspects:

Streaming and Incremental Processing: Implementing streaming and incremental processing techniques can be beneficial for large JSON datasets. This approach allows for parsing or serializing data incrementally, reducing memory overhead and improving overall processing speed. For example, `msgspec` could be a useful library to schema-based decoding and encoding for JSON. `msgspec` allows you to define schemas for the records you’re parsing. msgspec has significantly lower memory usage, and it is by far the fastest solution.


Minimizing JSON Payload Size: Implementing data compression techniques, such as gzip or deflate, before transmitting JSON data over the network can significantly reduce payload size. This not only conserves bandwidth but also expedites data transfer. Using GZIP for JSON involves compressing JSON data before transmitting it over the network and decompressing it on the receiving end. This compression technique helps minimize the payload size, reducing the amount of data that needs to be transferred and improving overall network efficiency. [Here is an eternal website which demonstrates how to use GZip for JSON](https://www.baeldung.com/json-reduce-data-size#:~:text=Compressing%20with%20gzip&text=That's%20why%20gzip%20is%20our,and%20compress%20it%20with%20gzip).










