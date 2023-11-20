### JSON-RPC

## Introduction
JSON-RPC is a an approach to building APIs for communication between different software systems. The most common approach is REST, but JSON-RPC offers its own advantages. Like REST, JSON-RPC uses JSON for its data format and uses HTTP as a transport protocol. JSON-RPC focuses on remote procedure calls whereas the more popular REST is more focused on resource manipulation. REST is generally easier to implement through being able to control information like HTTP headers and representation. Client implementations do not have to rely on endpoint names but message formats instead. JSON RPC is generally more complicated and more useful for large application that go past simple CRUD applicatons, where REST would be the simpler choice. 

JSONRPC calls are represented by sending request objects to a server. These request objects contain the method to be called, parameters values that are passed into the method, an id that established by the client, and jsonrpc string that specifies the version of the JSON-RPC protocol.

The response object contains a result, which contains the correct value when the method results in a success, an error in cases where the method throws an error, and a jsonrpc string and id that are identical to the one in the request object.

Here is some basic documentation on JSON-RPC https://www.jsonrpc.org/specification

