# Firebase and Firestore


## This post will be about setting up Firebase and utilizing Firestore:


## Introduction:
Firebase is an all in one platform that hosts a myriad of services that cover the development cycle of an application. It includes services such as analytics, authentication, and for what we will be covering, database management.

Firestore is a NoSql document database, this means that data is structured hierarchically within collections.


## Setting up Firebase for a Web Application :
1. First, create a firebase project and register that app w/ the project.
2. Once registering is done you'll get a firebase config object to connect your app with firebase reasources
3. In the firebase console follow the installation steps to create a new project
4. For App registration:
- In the Firebase console's project overview page, click the </> icon to set up, then enter the App's name and follow the instructions to add and initialize Firebase SDK int eh app
5. SDK initialization
- First do: npm i -g firebase-tools or npm i -D firebase-tools (as a dev tool) in your project’s terminal
- Next type npx firebase login, this will open up a browser to login with your firebase account
- Next, type npx firebase init hosting to begin the project setup process
- Next, follow the installation steps displayed in the terminal and choose the options you desire


## Setting Up Firestore 
1. Before using in your app, go to the firebase console go to build > Firestore database > Create database >start in test mode >next 
2. Add the following scripts in your app:
```
<script src="https://www.gstatic.com/firebasejs/10.6.0/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.6.0/firebase-firestore-compat.js"></script>
```
3. Install firebase if not already with this command in your terminal:
```
npm install firebase@10.6.0 --save
```
4. Manually import firebase and firestore at the top of the file in your code
```
import firebase from "firebase/compat/app";
import "firebase/firestore";
```

## Writing to a Database
Firebase stores data in documents that are stored in collections.
Here's an example of adding data to the “users” collection in a hypothetical database
```
db.collection("users").add({
    first: "Ada",
    last: "Lovelace",
    born: 1815
})
.then((docRef) => {
    console.log("Document written with ID: ", docRef.id);
})
.catch((error) => {
    console.error("Error adding document: ", error);
});
```
FROM: https://firebase.google.com/docs/firestore/quickstart


Lets use another example and break it down

After you’ve initialized your app, first get a reference to firestore with the getFirestore() function.

Then pass that reference into the doc() function along with the path to the document, in this example we are looking at the 2021-09-14 document in the  dailySpecial collection.

```
const firestore = getFirestore()

const specialOfTheDay= doc(firestore, 'dailySpecial')
```

When we write to a document, we pass in the reference as well as data, this is represented as key-value pairs.
```
function write(){
    const data={
        val_1:a,
        val_2:b
    }
}

write()
```
Note that writing to a path will create the document if it doesn't exist and replace it with the new data if it does.

To resolve this, you may choose to do updateDoc() (with the same parameters above), but this requires the document existing, thus you may choose to add an additional parameter to the setDoc command to merge any updates, you pass in {merge:true} along with the parameters you’ve specified.

Since the setDoc() call is asynchronous, you must handle it as such.


## Getting/Fetching a document 
Lets Break down the following example:
```

const document_we_want= <document path here>
async function readOneDocument(){
const docSnapshot = await getDoc(document_we_want)
    if (docSnapshot.exists()){
        const docData = docSnapshot.data()
        // do something with this data
    }
}
```
We use the getDoc() call and pass in a document reference, which is the path to the document we want.

This resolves to a snapshot which is essentially just the document itself at that point in time.

Next, we check to see if it exists and if it does, we extract the data.

Here you may choose to do something different, like parsing it and displaying it somewhere.


##Making Queries

```

const artistQuery = query(
    collection(firestore, 'music artists'),
    where('musician', '==', 'Ado'),
    limit(20)
);

const artistQuerySnapshot = await getDocs(artistQuery);
const allAdoSongs = artistQuerySnapshot.forEach((song) => {
//do something with the data
}
)

```

In databases, oftentimes you want to find multiple objects that fit some criteria, in firestore this is referred to as querying for multiple documents.

In the query() call, you first pass in a collection instead of a document, then from there you may choose to add additional filters. 

From there when you getDocs instead of getDoc on the result of the query, what is returned is a snapshot of a query instead of a snapshot of a document. 

The query snapshot itself, is an array of documents.

You may choose to use docs() on the returned data to directly return the array, however you may also choose to do a .forEach() on it, in order to iteratively parse it. 



## Extra Resources:
* Getting started with firebase on the web: https://www.youtube.com/watch?v=ILTo8IvFXJw
* Getting started with Firebase Authentication on the web https://www.youtube.com/watch?si=VSKhNhRBs6ZqYv7g&v=rbuSx1yEgV8&feature=youtu.be
* Getting started with Cloud Firestore for the web: https://www.youtube.com/watch?v=BjtxPj6jRM8&t=1s
* firestore documentation: https://firebase.google.com/docs/firestore


