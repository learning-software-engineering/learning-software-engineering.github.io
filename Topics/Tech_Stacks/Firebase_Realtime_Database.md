# Introduction to Firebase Realtime Database


## 1. What is Firebase?
Firebase is a leading backend-as-a-service platform which was developed by Google. It is known to be very easy to learn and use as it has extensive documentation and is popular for many mobile and web applications. Some of the key features include the Realtime Database, authenication features, Cloud Firestore, Google Analytics, and Cross-Platform SDKs.


## 2. The Realtime Database

### Overview 

Firebase Realtime Database is a cloud-hosted NoSQL database. It allows you to store and sync data between your users in real-time. Therefore, when you build cross-platform apps all clients/users share one Realtime Database instance and automatically receive updates with the newest data. The setup is very minimal, security rules are highly customizable and intuitive 

### Key Features 

The Realtime Database has supports many use cases and has hundreds of features, here are the three most used ones. 

#### Real-Time Synchronization
It synchronizes data across all clients/users in real time. When data changes, every connected user is updated within a few miliseconds as it also has conflict management. 

#### Offline Capabilities 
Data is accessibile even if the user's device goes offline. When the connection is restored, the user will recieve any changes to get back to the current server state.

#### NoSQL Data Model
There are no fixed schemas so you can structure your data as seen fit. There are a many best practices you can follow, but this allows you to pass all sorts of data between the app and database.


## 3. Setup 

This set up will be for Flask and Python, equivalent setups can be done for other languages and frameworks as the core functionality is the same.

#### Create a Firebase Project
First go to the [Firebase Console](https://console.firebase.google.com/u/0/)
Click on "Add Project" and set it up as per your needs

#### Add Firebase to your Python/Flask application

First install Firebase from the terminal:
```
pip install firebase-admin
```

Next initialize it within your app:
```
import firebase_admin
from firebase_admin import credentials, db

cred = credentials.Certificate('path/to/serviceAccountKey.json')
firebase_admin.initialize_app(cred, {
    'databaseURL': 'https://your-database-name.firebaseio.com'
})

# You can put your credentials elsewhere as a JSON file for security
```

## 4. Structuring Data
Firebase stores data in JSON format. As a developer, it is important to follow good practices as JSON can get messy very quickly. 

The Firebase team themselves have made an easy guide for this: [Structure Guide](https://firebase.google.com/docs/database/admin/structure-data)

## 5. Saving and Recieving Data

Here is a brief overview on common use cases of using and manipulating data.

### Create Data
#### Use the ```.push()``` method

```python
# Creating a new user

users_ref = db.reference('users')
new_user_ref = users_ref.push({
    'name': 'First Last',
    'email': 'user@example.com'
})
```

### Read Data
#### Use the ```.get()``` method

```python
# Reading data from users

all_users = db.reference('users').get()
for user_id, user_info in all_users.items():
    print(user_id, user_info['name'])
```

### Update Data
#### Use the ```.update()``` method

```python
# Updating a user's name

user_update_ref = db.reference('users/{user_id}'.format(user_id='user1'))
user_update_ref.update({
    'name': 'NewFirst NewLast'
})
```

### Delete Data
#### Use the ```.delete()``` method

```python
# Deleting a user

delete_ref = db.reference('users/{user_id}'.format(user_id='user2'))
delete_ref.delete()
```

### Basic Queries
#### Queries can be specified by the child key, value, or key name

```python
# Querying users by name

query = db.reference('users').order_by_child('name').equal_to('Test User').get()

for user_id, user_info in query.items():
    print(user_id, user_info)
``` 

## 6. Additional Resources
[Official Documentation](https://firebase.google.com/docs/database) 

[Python Pyerbase Tutorial Series](https://www.youtube.com/playlist?list=PLs3IFJPw3G9Jwaimh5yTKot1kV5zmzupt)

[Realtime Database for Web Applications Summary Video](https://www.youtube.com/watch?v=pP7quzFmWBY) 
