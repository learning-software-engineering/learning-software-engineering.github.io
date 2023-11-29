### Goal for the article
In this guide, we'll explore the utilization of metaprogramming
in Python to create a simple server architecture for handling messages between clients and a server.  
The core concept involves using a base class, Message, 
from which all specific message types inherit. Metaprogramming
techniques are employed to dynamically generate JSON serialization/deserialization methods, enabling seamless
communication between the server and clients. Addiontally every Message class is in of itself a pydantic data class. Which means that it has
all of the data validation capabilities that Pydantic has.

### JSON Schema

Every class is serialized into JSON in the following manner. 

```json
{
    class_name: class_field
}
```

for example the class

```python
class SignInMessage(Message):
    def __init__(self, username, password):
        self.username = josh
        self.password = basketball
```

would be serialized to

```json
{
    "SignInMessage": {
        "username": "josh",
        "password": "basketball"
    }
}
```

Note: any other format can be chosen. This is just the one I chose. You only need to modify the 
to_json_message and from_json_message methods in the Message class.

The magic happens in the message class from which all other message types inherit.

```python
# note that message inherits from Basemodel. Which is a pydantic data class
# this gives us many additionally powers in our message class
# such as validation as well as easy JSON serialization.
# Note it does force us to define classes while using types.
class Message(BaseModel):
    #this is the method that generates the json serialization.
    # for example class SignIn(username: str, password: str) would return
    # {"SignIn": {"username": "username", "password": "password"}}
    def to_json_message(self) -> str:
        # we find the name of the class through the __class__ attribute.
        name = self.__class__.__name__
        # we convert the class to a dictionary using the model_dump method.
        # this method is a part of every pydantic DataClass.
        data = self.model_dump_json()
        # then we add the class name as a key to the dictionary. and convert the dictionary to json.
        return json.dumps({name: data})

    # this is the method that generates the json deserialization and returns a 
    # specific Message object that we can use
    # for dynamic dispatch.
    # for example {"SignIn": {"username": "username", "password": "password"}} 
    # would return a SignIn object with the username and password fields set.
    @staticmethod
    def from_json_message(message: str) -> Message:
        # we convert the json to a dictionary.
        dictionary = json.loads(message)
        # extract the class name and the class fields from the dictionary.
        name, data = next(iter(dictionary.items()))
        data = json.loads(data)
        # we look up the class in the global scope and return a new instance of 
        # the class with the data as the arguments.
        cls = globals()[name]
        return cls(**data)

    # this is the method that handles the logic of the message. We need to implement
    # this method in all our Message subclasses.
    # for example class SignIn(username: str, password: str) would return a SignInResponse object.
    # this is how we get dynamic dispatch to work. We can call the respond method on any Message object and it will return the correct response. as defined by the subclass.
    def respond(self) -> Message:
        raise NotImplementedError
```

Then assuming we have a server object that can send and receive JSON. 
the server architecture is as follows.

```python
    while True:
        # make sure to wrap everything in a try block because every single method here can fail with
        # an exception
        try:
            json: str = server.get_json()
            # we convert the json to a Message object using the from_json_message method.
            message_as_cls: Message = Message.from_json_message(json)
            # we use dynamic dispatch to call the respond method of the Message object.
            response_as_cls: Message = message_as_cls.respond()
            # we convert the response to json and send it back to the client.
            response_json = response_cls.to_json_message()
            server.send_json(response_json)
```

remember to import at the top of the file.

```python
# this is to make defining classes that reference each other's type in a recursive manner possible.
from __future__ import annotations
# importing all type annotations
from typing import *
# brings the ability to turn a dictionary into json.
import json
# imports the Basemodel class of which our message class inherits from
# this means that every Message class is in of itself a pydantic data class
from pydantic import BaseModel
```

Now all we need to do to add a new message type is to create a new class that inherits from Message and implement the respond method.

```python

# a simple example of the kind of message we might want to receive from the client.
class SignIn(Message):
    name: str
    password: str

    # this handles the logic of the message. This is where we would do things like check if the user exists in the database.
    # or if the password is correct. and then we return a SignInResponse object.
    def respond(self) -> SignInResponse:
        return SignInResponse(success=True)


# a simple example of the kind of message we might want to send to the client.
# node we don't need to implement any logic here. We just need to define the fields we want to send.
# we could implement validation logic through pydantic if we wanted too. All our messages are valid pydantic models.
class SignInResponse(Message):
    success: bool
    valid_user: bool = True
    valid_password: bool = True
    error_message: Optional[str] = None
```

### Why you should use this architecture.

While there are many frameworks that do things like this for you (see flask and django). I think there are many advantages to doing it yourself.
Additionally meta programming in python is an incredibly powerful and can be used to do many things.
Even if you won't use it for this specific purpose. I think it is a good thing to know about.

### further readings.
- https://docs.pydantic.dev/latest/ for guides to the powerful capabilities of pydantic data classes.
- https://realpython.com/primer-on-python-decorators/ for a guide on how to use decorators for meta programming in python.
- https://www.geeksforgeeks.org/reflection-in-python/ for a guide on how to do runtime reflection in python.

### further things this guide should cover (but isn't due to lack of time).
- how to automatically generate a json schema from a class.
- how to automatically add items to a database.
- how to generate glue code so other languages can use these classes as well (this is mind twisting. Think of generating java code in python)
