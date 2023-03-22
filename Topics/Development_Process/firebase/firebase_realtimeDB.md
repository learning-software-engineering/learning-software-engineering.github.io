# Using Firebase Realtime Database
## Table of Contents:
### [Introduction](#introduction-1)
### [Step By Step Tips](#Step_By_Step_Tips-1)
### [External Resources](#External_Resources-1)

## Introduction

Do you want to use a NoSQL database (DB)? Then you can use firebase Realtime DB. However, using the Firebase Firestore Database is better to use for long term data storage. But for starters, learning Firebase Realtime DB is essential.
The data in firebase realtime database is stored in JSON-like objects. 

What is NoSQL Database? It is a database that does not have the stringency and rules of a SQL database. NoSQL database is more commonly used when you are handling a lot of data that might not have a perfect structure (unstructured or semi-structured).

To set up firebase, first, you will need to login to [Firebase](https://firebase.google.com/), click the console button on the top right corner, create a new project as instructed, under build, click on Realtime Database.

## Step By Step Tips

I will demosntrate tips to get started on the firebase realtime database using the example below:

To store values in the firebase realtimeDB, you must first have your project front end in place. Then, you will create a JS file, and start writing code in that file to create a connection to the database, similar to the structure of the code below: 

Let us say that my HTML page contains two buttons with ids #startbtn and #stopbtn. When the user hits the start button, I want to record the current time in the database, and when the user clicks on the stop button, I want the new current time to be placed in the database under the same user. I will also ask the user for an ID in the field with ID #enterID to save their start and stop times under their ID of choice. 

Hence, I will have the code below:
First, initialize the database: 
```
// Import the functions you need from the SDKs you need
        import { initializeApp } from 
        "https://www.gstatic.com/firebasejs/9.17.1/firebase-app.js";
      
        // Your web app's Firebase configuration
        const firebaseConfig = {
            // this section, you will get from your firebase console
        };
      
        // Initialize Firebase
        const app = initializeApp(firebaseConfig);

        import {getDatabase, set, get, update, remove, ref, child}
         from 'https://www.gstatic.com/firebasejs/9.17.1 
         firebase-database.js'

        const db = getDatabase();
```
Then, put variables for the start button, stop button, and enterID values. 
```
        var startbtn = document.querySelector('#startbtn');
        var stopbtn = document.querySelector("#stopbtn");
        
        var enterID = document.querySelector("#enterID");
```

Add event listeners for when the buttons are pressed, which call the functions saveStartTime and saveEndTime.

saveStartTime will save the current start time under the Tasks/ID container.

```
        startbtn.addEventListener('click', saveStartTime);
        stopbtn.addEventListener('click', saveEndTime);

        
        function saveStartTime() {
            set(ref(db, "Tasks/" + enterID.value), {
                //I will trivially define the end time here as well
                StartTime: Date.now(),
                EndTime: Date.now(),
                                
            })
            .then(()=> {
                alert("Data added successfuly!");
            })
            .catch((error)=>{
                alert(error);
            });

        }

        function saveEndTime() {
            update(ref(db, "Tasks/" + enterID.value), {
                EndTime: Date.now(),
                
            })
            .then(()=> {
                alert("Data updated successfuly!");
            })
            .catch((error)=>{
                alert(error);
            });

        }


```

Now, When the user clicks the start button, the current time is saved, and lateron when they click the stop button, the next current time is saved. 

Make sure to add the JS file to the file containing the frontend (in my case, an HTML page)
```
<script type="module" src="./mail.js"></script>

```

## External Resources
Below is a tutorial in learning the firebase realtime database. It goes through step by step, how to set up your realtime database.

[Tutorial](https://firebase.google.com/docs/database)