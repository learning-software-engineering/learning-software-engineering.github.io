# Protobufs and gRPC

## Introduction
Protobufs are a way to serialize data whereas gRPC is used to send them over RPC calls between microservices. gRPC is usually closely used with Protobufs. Further in depth detail can be found on the official websites of both products. In this overview we will go over a very basic Protobuf implementation and then a basic call for gRPC. gRPC supports a wide variety of languages which is one of the features that makes it so useful since it allows microservices written in different languages to communicate between one another, for this example though we will use Python.

https://protobuf.dev/

https://grpc.io/

A more in depth tutorial that this document was derived from can be found here: https://grpc.io/docs/languages/python/basics/

## Setting up the Protobuf
Below is a very simple Protobuf, with a "message" and a "service". A "message" in Protobuf looks very similar to a C++ struct. It actually has the same functionality as a C++ struct, is essentially the data structure we are creating. The "service" is basically the definition for the rpc call itself. Usually there is some additional properties that must be specified in the file such as the Protobuf version etc. but for the purpose of this overview only the main part of our Protobuf file is include, which is the data structure we are serializing. One important key point to mention is that Protobufs all have the `.proto` file extension.

```
message RequestObject{
    string text = 1;
}

message ResponseObject{
    string text = 1;
}

service Example{
    rpc RunExample (RequestObject) returns (ResponseObject) {}
}
```

Here in our example we have a very simple message with just a text field that is a string. There are additional options such as making certain fields optional, refer to the official documentation for further details.

## Populating the Protobuf
Now how does one use the Protobuf? A Python program cannot read the `.proto` file directly. Actually Protobufs allows you to generate files for the language you are using, so for example it will generate a Python file with methods to use such as set and get on fields of our Proto. There will also be a file generated for the grpc.

For example, lets say our file name is `example.proto`, by compiling our proto we will then get `example_pb2.py` and `example_pb2_grpc.py` (assuming we are using Protobuf 2).

After we get our generated methods, we can simply make our Proto objects within python directly.

### Client End

Below is a very simple client that sends in the `RequestObject` from our proto definition with the text field set to `'CSC301'`.
```Python
def example() -> None:
    ip = 'localhost:50051'
    channel = grpc.insecure_channel(ip)
    stub = example_pb2_grpc.RouteGuideStub(channel)
    request_object = example_pb2.RequestObject(text='CSC301')
    response = stub.Example(request_object)
```

### Server End
Below is a very simplified version of a server for handling requests. The server initialization is left out, but more details can be found on the official website. It simply takes our request's text field which would be the `RequestObject`'s text and appends on `' is fun'`. This new result `'CSC301 is fun'` will then be set to our `ResponseObject` text field and returned. 

```Python
# ExampleServicer is Auto generated
class ExampleServicer(example_pb2_grpc.ExampleServicer):
    def example(self, request, context):

        # Get the text from request object (passed in by client)
        new_text = request.text + ' is fun'

        # Create a ResponseObject (from proto definition)
        return example_pb2.ResponseObject(text=new_text)
```

Running this server with our client we should get the return `'CSC301 is fun'` back on the client end.

## Conclusion
Protobufs are an efficient way to serialize data, and is very convenient as it supports a variety of languages. It is also very simple to set data fields as seen from our example above due to the auto generated functions that we get from compiling our proto file. Protobufs work very well with gRPC, which we can use to establish communication between microservices.

