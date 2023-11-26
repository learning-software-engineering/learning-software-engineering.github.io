# Firebase for Serverless Backends and Cloud Functions

## Serverless Backends

Serverless backends in Firebase encompass the entire infrastructure required to power an application, offering a range of services such as databases (Firestore, Realtime Database), authentication, hosting, and more. These backends abstract away server management, allowing developers to focus solely on writing code without worrying about underlying infrastructure concerns.

## Cloud Functions

Cloud Functions in Firebase are integral to implementing serverless backends within the Firebase ecosystem. They are small, event-driven functions that respond to various triggers like database events, HTTP requests, authentication events, and more. These functions execute specific tasks or logic in response to these events, providing a scalable and managed way to handle functionalities within the serverless architecture.

### Integration within Firebase

Firebase's Cloud Functions are a key component used to build serverless backends. While Cloud Functions handle specific tasks triggered by events, a complete serverless backend in Firebase involves utilizing these functions in conjunction with other Firebase services like Firestore, Realtime Database, Authentication, and Hosting. Together, these services enable developers to create a holistic, scalable, and fully managed backend infrastructure for their applications.

### Key Relationship

Cloud Functions can be seen as Firebase's implementation of serverless functions within the broader context of building serverless backends. They are instrumental in enabling developers to add custom logic, respond to events, and create specific functionalities without managing servers. However, they are just one piece of the larger puzzle that constitutes a serverless backend in Firebase.

In essence, Cloud Functions within Firebase serve as a crucial part of building serverless backends, working alongside other Firebase services to create scalable, event-driven, and fully managed backend infrastructures for modern applications.

### Sample Code

Here's an example of Firebase Cloud Functions using Python:

```python
# The Cloud Functions for Firebase SDK to create Cloud Functions and set up triggers.
from firebase_functions import firestore_fn, https_fn

# The Firebase Admin SDK to access Cloud Firestore.
from firebase_admin import initialize_app, firestore
import google.cloud.firestore

app = initialize_app()

@https_fn.on_request()
def addmessage(req: https_fn.Request) -> https_fn.Response:
    """Take the text parameter passed to this HTTP endpoint and insert it into
    a new document in the messages collection."""
    # Grab the text parameter.
    original = req.args.get("text")
    if original is None:
        return https_fn.Response("No text parameter provided", status=400)

    firestore_client: google.cloud.firestore.Client = firestore.client()

    # Push the new message into Cloud Firestore using the Firebase Admin SDK.
    _, doc_ref = firestore_client.collection("messages").add({"original": original})

    # Send back a message that we've successfully written the message
    return https_fn.Response(f"Message with ID {doc_ref.id} added.")

@firestore_fn.on_document_created(document="messages/{pushId}")
def makeuppercase(event: firestore_fn.Event[firestore_fn.DocumentSnapshot | None]) -> None:
    """Listens for new documents to be added to /messages. If the document has
    an "original" field, creates an "uppercase" field containing the contents of
    "original" in uppercase."""

    # Get the value of "original" if it exists.
    if event.data is None:
        return
    try:
        original = event.data.get("original")
    except KeyError:
        # No "original" field, so do nothing.
        return

    # Set the "uppercase" field.
    print(f"Uppercasing {event.params['pushId']}: {original}")
    upper = original.upper()
    event.data.reference.update({"uppercase": upper})
