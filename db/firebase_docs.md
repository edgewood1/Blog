# Firebase Database Notes

This document contains notes on common operations in the Firebase Realtime Database.

### Get a Unique ID for Pushed Data

When you use the `push()` method to add data to a Firebase reference, it generates a unique key (or ID) for that data. You can access this key via the `.key` property on the snapshot that is returned in the promise.

```javascript
import { ref, push } from "firebase/database";

// Get a reference to the database service and a specific location
const db = getDatabase();
const itemsRef = ref(db, 'items');

// Push new data
push(itemsRef, {
  name: "New Item",
  value: "Some Value"
}).then((snap) => {
  // The unique key for the new data
  const uniqueKey = snap.key;
  console.log("Pushed data with key:", uniqueKey);
});
```

### Listen for New Children

You can listen for new children being added to a specific location in your database using the `onChildAdded` event listener. The callback function receives a `snapshot` of the new child data. The `snapshot.key` property contains the unique ID of that child.

```javascript
import { ref, onChildAdded } from "firebase/database";

const db = getDatabase();
const commentsRef = ref(db, 'comments');

onChildAdded(commentsRef, (snapshot) => {
  const newComment = snapshot.val();
  const commentId = snapshot.key;

  console.log("New comment added:", commentId, newComment);
  // Example: displayChatMessage(newComment.author, newComment.text);
});
```
