# FastAPI

## Table of Contents
### [Introduction](#introduction-1)
### [Writing APIs](#writing-apis-1)
### [Testing](#testing-1)


## Introduction

FastAPI is a popular web framework in Python for writing REST APIs. It is fast and easy to use, with type hints and automatic data validation. 

It also auto generates documentation for your APIs with the [OpenAPI](https://www.openapis.org/) specifications and with an UI such as [Swagger UI](https://swagger.io/)

You can check out FastAPI's tutorials [here](https://fastapi.tiangolo.com/tutorial/) at their own website with instructions on how to install FastAPI and how to get started with your first REST API using FastAPI

Or if you wish to browse their documentation at your leisure, click [here](https://fastapi.tiangolo.com/)


## Writing APIs

The FastAPI tutorial on writing your first API from [here](https://fastapi.tiangolo.com/tutorial/first-steps/) is a very good starting point. It shows that all your API files will look something like this:

``` {python}
from fastapi import FastAPI

app = FastAPI()

# your APIs here
@app.get("/test")
def test():
  return {"test message": "hello world"}

```

However, it is highly likely that not all your APIs are going to be in the same file. For example, take the above as your main.py. You are likely not going to put all your APIs there, so you may create a file called
more_apis.py.

To connect more_apis.py with your main.py, you will need to use routers like this:

main.py
``` {python}
from fastapi import FastAPI
import more_apis  # change this import to whatever file you create and to whatever location you created it at

app = FastAPI()
app.include_router(more_apis.router) # your router connecting more_apis.py APIs

@app.get("/test")
def test():
  return {"test message": "hello world"}

```

more_apis.py
``` {python}
from fastapi import APIRouter

router = APIRouter()

# your other APIs
@router.get("/otherAPI")
def other_API():
  return {"different message": "hello world again"}

```

You can see more details about FastAPi and routers [here](https://fastapi.tiangolo.com/tutorial/bigger-applications/)

As always, you can check the official FastAPI tutorial [here](https://fastapi.tiangolo.com/tutorial/) for anything about writing APIs.


## Testing

Testing with FastAPI can be automated with GitHub actions and uses FastAPI's TestClient and [pytest](https://docs.pytest.org/en/7.4.x/) to test. 

Your test file should look something like this, using the main.py above (wherever it is located in your file system) or any other API file:

test_main.py

``` {python}
import pytest
from fastapi.testclient import TestClient

import main

client = TestClient(main.app)

# your tests here
def test_other_API():
  ...

```

The pytest.ficture is one way to do setup and teardown for a test file. Check out more details about pytest fictures [here](https://docs.pytest.org/en/6.2.x/fixture.html#fixture). It may not be needed, as there are other ways to do the same thing. You can include it into the test file above if you would like.

``` {python}
# setup and teardown for doing things before and after tests
@pytest.fixture(scope="module", autouse=True)
def setup_and_teardown():
  ... # do something
  yield
  ... # do something
```

You can check out the testing tutorial [here](https://fastapi.tiangolo.com/tutorial/testing/) from FastAPI website.
