# JSON-RPC

## Introduction
JSON-RPC is an approach to building APIs for communication between different software systems. Let's compare it to REST, which is the most common way of developing APIs. JSON-RPC is not as popular, but it offers its own advantages. Like REST, JSON-RPC uses JSON for its data format and uses HTTP as a transport protocol. JSON-RPC is mainly focused on calling functions or procedures on a remote server and asking this server to perform a certain action. On the other hand, REST is focused on working with and changing data.

This makes it so that JSON-RPC is a better option in scenarios where remote functions have to be called on a server that require an action result. For example, a good time to use JSON-RPC is transferring money between bank accounts on a remote system. 

REST is generally more useful in situations where actions such as adding data to databases or updating information are needed due to its ability to easily perform CRUD operations. [Read more about the differences between remote procedure calls and REST here](https://nordicapis.com/whats-the-difference-between-rpc-and-rest/). Below is a representation of how REST works.


![Rest Visualization](https://www.altexsoft.com/static/blog-post/2023/11/72f74918-0345-4be1-bed3-08d1cfe138cc.webp)




#### Request and Repsonse of JSON-RPC Calls

JSON-RPC calls require two things, which are called request objects and response objects. Request objects are what are sent to the server during a JSON-RPC method call, and the response objects are what the server responds with at the end of the method call.

JSON-RPC calls are represented by sending request objects to a server. These request objects contain the method to be called, parameters values that are passed into the method, an id that established by the client, and JSON-RPC string that specifies the version of the JSON-RPC protocol. 

The response object contains a result, which contains the correct value when the method results in a success, an error in cases where the method throws an error, and a JSON-RPC string and id that are identical to the one in the request object. Below is a representation of JSON-RPC in action.

![JSON-RPC Visualization](https://assets-global.website-files.com/5ff66329429d880392f6cba2/61b76e7fdf48bbef0026f39a_JSON%20works.png)

JSON-RPC is very useful for a variety of reasons. It is simple and very straight forward due to its standard of remote procedure calls, making it easy to implement and understand. This also makes it so products built with JSON-RPC end up being more scalable. In addition, it serializes data in JSON format and is able to be implemented in a variety of languages, making it flexible. Furthermore, JSON-RPC has standardized error handling, making debugging and troubleshooting a smoother process.

Overall, JSON-RPC is a great tool due to its lightweight design and ease of implementation, making it a versatile and efficient choice for remote procedure calls in various applications.

Below are some more resources related to JSON-RPC

[Here is some basic documentation on JSON-RPC](https://www.jsonrpc.org/specification)

[Here is more on the benefits of JSON-RPC and more comparisons of JSON-RPC with REST](https://rpcfast.com/blog/remote-procedure-calls-what-is-json-rpc)

[Here is an example of how to set up JSON-RPC using TypeScript and guide on how to install it using npm](https://www.npmjs.com/package/json-rpc-2.0)