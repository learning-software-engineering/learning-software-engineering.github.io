### JSON-RPC

## Introduction
JSON-RPC is a an approach to building APIs for communication between different software systems. Let's compare it to REST, which is the most common way of developing APIs. JSON-RPC is not as popular, but it offers its own advantages. Like REST, JSON-RPC uses JSON for its data format and uses HTTP as a transport protocol. JSON-RPC focuses on remote procedure calls whereas the more popular REST is more focused on resource manipulation. 

This makes it so JSON-RPC is a better option in scenarios where remote functions have to be called on a server that require an action result. It's most useful for when complex calculations or calling remote procedures on the server are needed. For example, a good time to JSON-RPC is transfering money between bank account on a remote system. 

REST is generally more useful in situations where actions such as adding data to databases or updating information are needed due to its ability to easily perform CRUD operations.


#### Request and Repsonse of JSON-RPC Calls

JSON-RPC calls require two things, which are called request objects and response objects. Request objects are what are sent to the server during a JSON-RPC method call, and the response objects are what the server responds with at the end of the method call.

JSONRPC calls are represented by sending request objects to a server. These request objects contain the method to be called, parameters values that are passed into the method, an id that established by the client, and jsonrpc string that specifies the version of the JSON-RPC protocol.

The response object contains a result, which contains the correct value when the method results in a success, an error in cases where the method throws an error, and a jsonrpc string and id that are identical to the one in the request object.

JSONRPC is very useful for a variety of reasons. It is simple and very straight forward due to its standard of remote procedure calls, making it easy to implement and understand. In addition, it serializes data in JSON format and is able to be implemented in a variety of languages, making it flexible.

Here is some basic documentation on JSON-RPC https://www.jsonrpc.org/specification

Read more about the differences between remote procedure calls and rest here https://nordicapis.com/whats-the-difference-between-rpc-and-rest/

Here is an example of how to set up JSON-RPC using TypeScript and guide on how to install it using npm. https://www.npmjs.com/package/json-rpc-2.0