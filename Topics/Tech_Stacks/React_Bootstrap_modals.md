# Learning Modals from React-Bootstrap

## Table of Contents

### [Introduction](#introduction-1)

### [Set Up](#set-up-1)

### [Non Static Modal](#non-static-modal-1)

### [Extracting Data](#extracting-data-1)

### [Official Documentation](#official-documentation-1)

## Introduction
This is a short introduction into using the Modal Component from React-Bootstrap. Modals are popups that can be used to notify the user or to obtain user information.
This article covers the setup, how to create a modal that pops up and how to get user-entered information from the modal. There is official documentation linked at the bottom for further reading.

## Set Up
In order to use Modals from React-Bootstrap we first need to install it. Assuming you have React already installed, the most basic way this can be done is through bash with npm:

Using npm:
```sh
> npm install react-bootstrap bootstrap
```

Next, in order to use a React-Bootstrap component, it is important to only import the needed individual component instead of the entire library. This will significantly reduce the amount of code sent to the client.
```javascript
import Button from 'react-bootstrap/Button';

// the frowned upon method
import { Button } from 'react-bootstrap';
```
Finally, users can optionally install vanilla Bootstrap if they wish to stylize their components with it. Note that this is not required, see the Bootstrap article for more details.

## Non-Static Modal
To create a standard modal that can be displayed and dismissed, use </ Modal> and useState. The Modal component includes <Modal.Header/>, <Modal.Title/>, <Modal.Body/>, and <Modal.Footer/> which each allows you to customize the component of the Modal they are named after.
```js
import { useState } from 'react';
import Button from 'react-bootstrap/Button';
import Modal from 'react-bootstrap/Modal';

function Example() {
  const [show, setShow] = useState(false);

  const handleClose = () => setShow(false);
  const handleShow = () => setShow(true);

  return (
    <>
      //variant is a styling method using vanilla Bootstrap
      //it is not needed for Modals and vanilla CSS can also be used to stylize it
      <Button variant="primary" onClick={handleShow}>
        Launch demo modal
      </Button>

      <Modal show={show} onHide={handleClose}>
        <Modal.Header closeButton>
          <Modal.Title>Modal heading</Modal.Title>
        </Modal.Header>
        <Modal.Body>Woohoo, you are reading this text in a modal!</Modal.Body>
        <Modal.Footer>
          <Button variant="secondary" onClick={handleClose}>
            Close
          </Button>
          <Button variant="primary" onClick={handleClose}>
            Save Changes
          </Button>
        </Modal.Footer>
      </Modal>
    </>
  );
}

export default Example;
```
-This code is taken as an example from the React-Bootstrap Official Website: https://react-bootstrap.netlify.app/docs/components/modal

The "show" attribute of a Modal determines if it is displayed, this is controlled by the show state which is controlled by the button.
```js
import { useState } from 'react';
import Button from 'react-bootstrap/Button';
import Modal from 'react-bootstrap/Modal';

function Example() {
  //this is passed as the "show" attribute of the Modal
  const [show, setShow] = useState(false);

  //these are functions that alter the show state
  const handleClose = () => setShow(false);
  const handleShow = () => setShow(true);

  return (
    <>
      //when the button is clicked, set the "show" attribute to true with the above function
      <Button variant="primary" onClick={handleShow}>
        Launch demo modal
      </Button>
      //pass through the show state into the Modal's "show" attribute and connects the closing function to the
      //Modal's closing action
      <Modal show={show} onHide={handleClose}>
      //... the rest of the Modal Code
```
The full Modal can be displayed statically if state isn't involved and the "show" attribute is set to a constant true. The user adds what they want to any of the Modal Components by placing what they want to add within it.
```js
      <Modal show={show} onHide={handleClose}>
        //closeButton creates an x in the top right corner that the user can click to trigger the onHide event
        //and close the Modal
        <Modal.Header closeButton>
          //The user would add anything they want to the Header here
          <Modal.Title>Modal heading</Modal.Title>
        </Modal.Header>
        <Modal.Body>Woohoo, you are reading this text in a modal!</Modal.Body>
        <Modal.Footer>
          //onClick={handleClose} is connected to the useState functions earlier and will close the Modal
          <Button variant="secondary" onClick={handleClose}>
            Close
          </Button>
          <Button variant="primary" onClick={handleClose}>
            Save Changes
          </Button>
        </Modal.Footer>
      </Modal>
```

## Extracting Data
One of the primary applications of Modals is the ability to extract information from the user. We can do this through React-Bootstrap's Form component. The example below illustrates a function that takes in an item and when the form is opened, ask the user for the first name and last name, upon completion it updates the items first and last name accordingly.
```js
import { useState } from 'react';
import Button from 'react-bootstrap/Button';
import Modal from 'react-bootstrap/Modal';
//we import React-Bootstrap's Form
import Form from 'react-bootstrap/Form';

function Example(item) {
  const [show, setShow] = useState(false);

  const handleClose = () => setShow(false);
  const handleShow = () => setShow(true);

  //here we initialize the first name and last name values with useState
  //we also set up a onChange function so that everytime the field is changed, the value is updated accordingly
  const [firstValue, setFirstValue] = useState(item.firstname);
  const firstValueChange = (event) => {
      setFirstValue(event.target.value);
  }
  const [lastValue, setLastValue] = useState(item.lastname);
  const lastValueChange = (event) => {
      setLastValue(event.target.value);
  }
  //set values as necessary and close the function
  const handleSubmit = () => {
        item.firstname = firstValue
        item.lastname = lastValue
        handleClose()
    }

  return (
    <>
      <Button variant="primary" onClick={handleShow}>
        Get First and Last Name
      </Button>

      <Modal show={show} onHide={handleClose}>
        <Modal.Header closeButton>
          //modal title prompts first and last name
          <Modal.Title>Please Enter First and Last Name</Modal.Title>
        </Modal.Header>
            <Modal.Body>
                <Form>
                    <Form.Group
                    className="mb-3"
                    controlId="itemForm.ControlFirstName"
                    >
                    <Form.Label>First Name</Form.Label>
                    //set up the first name value
                    //determine what happens when the field is changed through onChange
                    //in this case we want the correct variable to stay updated
                    <Form.Control
                        type="text"
                        value={firstValue} 
                        onChange={firstValueChange} 
                        autoFocus
                    />
                    </Form.Group>   
                    <Form.Group
                    className="mb-3"
                    controlId="itemForm.ControlLastName"
                    >
                    <Form.Label>Last Name</Form.Label>
                    <Form.Control
                        type="text"
                        value={lastValue} 
                        onChange={lastValueChange} 
                    />
                    </Form.Group>
                </Form>
            </Modal.Body>
        <Modal.Footer>
          <Button variant="secondary" onClick={handleClose}>
            Close
          </Button>
          <Button variant="primary" onClick={onSubmit}>
            Save Changes
          </Button>
        </Modal.Footer>
      </Modal>
    </>
  );
}

export default Example;
```

## Official Documentation
- [React-Bootstrap Introduction and Installation](https://react-bootstrap.netlify.app/docs/getting-started/introduction)
- [React-Bootstrap's Modal Page](https://react-bootstrap.netlify.app/docs/components/modal)
