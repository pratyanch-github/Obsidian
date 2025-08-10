
1. install firebase library using npm 
2. create a js file, in that file initialize a firebase app - for this a initializeapp func is provideb by library like 
3. you can import any firebase service like `/firebase/<service>` 
   ![[image_212.png]]
   

> [!NOTE]
> > you have to first initialize firebase app before you can use any service


# Firebase Firestore CRUD Operations Cheat Sheet

### **Setup Firestore**

1. Install Firebase SDK:
    
    ```bash
    npm install firebase
    ```
    
2. Import and initialize Firebase in your project:
    
    ```javascript
    import { initializeApp } from "firebase/app";
    import { getFirestore } from "firebase/firestore";
    
    const firebaseConfig = {
      apiKey: "YOUR_API_KEY",
      authDomain: "YOUR_AUTH_DOMAIN",
      projectId: "YOUR_PROJECT_ID",
      storageBucket: "YOUR_STORAGE_BUCKET",
      messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
      appId: "YOUR_APP_ID",
    };
    
    // Initialize Firebase and Firestore
    const app = initializeApp(firebaseConfig);
    const db = getFirestore(app);
    ```
    

---

## **1. Create/Insert Data**

Add data to Firestore with **`addDoc`** or **`setDoc`**.

### Add a Document with Auto-ID:

```javascript
import { collection, addDoc } from "firebase/firestore";

// Reference to a collection
const usersRef = collection(db, "users");

// Add a document
addDoc(usersRef, {
  name: "John Doe",
  email: "johndoe@example.com",
  age: 30,
})
  .then((docRef) => console.log("Document written with ID: ", docRef.id))
  .catch((error) => console.error("Error adding document: ", error));
```

### Set a Document with Custom ID:

```javascript
import { doc, setDoc } from "firebase/firestore";

// Reference to a document
const userDoc = doc(db, "users", "user_123");

// Set the document
setDoc(userDoc, {
  name: "Jane Doe",
  email: "janedoe@example.com",
  age: 25,
})
  .then(() => console.log("Document written successfully!"))
  .catch((error) => console.error("Error setting document: ", error));
```

---

## **2. Read/Fetch Data**

### Get a Single Document:

```javascript
import { doc, getDoc } from "firebase/firestore";

// Reference to a document
const userDoc = doc(db, "users", "user_123");

// Fetch the document
getDoc(userDoc)
  .then((docSnap) => {
    if (docSnap.exists()) {
      console.log("Document data:", docSnap.data());
    } else {
      console.log("No such document!");
    }
  })
  .catch((error) => console.error("Error fetching document: ", error));
```

### Get All Documents in a Collection:

```javascript
import { collection, getDocs } from "firebase/firestore";

// Reference to a collection
const usersRef = collection(db, "users");

// Fetch all documents
getDocs(usersRef)
  .then((querySnapshot) => {
    querySnapshot.forEach((doc) => {
      console.log(doc.id, " => ", doc.data());
    });
  })
  .catch((error) => console.error("Error fetching documents: ", error));
```

---

## **3. Update Data**

### Update Specific Fields:

```javascript
import { doc, updateDoc } from "firebase/firestore";

// Reference to a document
const userDoc = doc(db, "users", "user_123");

// Update fields
updateDoc(userDoc, {
  age: 31, // Update the age
  email: "updatedemail@example.com", // Update the email
})
  .then(() => console.log("Document updated successfully!"))
  .catch((error) => console.error("Error updating document: ", error));
```

---

## **4. Delete Data**

### Delete a Document:

```javascript
import { doc, deleteDoc } from "firebase/firestore";

// Reference to a document
const userDoc = doc(db, "users", "user_123");

// Delete the document
deleteDoc(userDoc)
  .then(() => console.log("Document deleted successfully!"))
  .catch((error) => console.error("Error deleting document: ", error));
```

### Delete Specific Fields:

```javascript
import { doc, updateDoc, deleteField } from "firebase/firestore";

// Reference to a document
const userDoc = doc(db, "users", "user_123");

// Delete a field
updateDoc(userDoc, {
  email: deleteField(),
})
  .then(() => console.log("Field deleted successfully!"))
  .catch((error) => console.error("Error deleting field: ", error));
```

---

## **5. Querying Data**

Fetch data based on conditions using **`where`**.

### Query with Filters:

```javascript
import { collection, query, where, getDocs } from "firebase/firestore";

// Reference to a collection
const usersRef = collection(db, "users");

// Query documents where age > 25
const q = query(usersRef, where("age", ">", 25));

// Fetch query results
getDocs(q)
  .then((querySnapshot) => {
    querySnapshot.forEach((doc) => {
      console.log(doc.id, " => ", doc.data());
    });
  })
  .catch((error) => console.error("Error fetching query: ", error));
```

---

## **6. Real-Time Updates**

Listen to real-time changes with **`onSnapshot`**.

### Listen to a Collection:

```javascript
import { collection, onSnapshot } from "firebase/firestore";

// Reference to a collection
const usersRef = collection(db, "users");

// Real-time listener
onSnapshot(usersRef, (snapshot) => {
  snapshot.forEach((doc) => {
    console.log(doc.id, " => ", doc.data());
  });
});
```

### Listen to a Document:

```javascript
import { doc, onSnapshot } from "firebase/firestore";

// Reference to a document
const userDoc = doc(db, "users", "user_123");

// Real-time listener
onSnapshot(userDoc, (docSnap) => {
  if (docSnap.exists()) {
    console.log("Current data:", docSnap.data());
  } else {
    console.log("No such document!");
  }
});
```

---

## **Basic Functions Overview**

|**Operation**|**Function**|**Purpose**|
|---|---|---|
|**Create**|`addDoc`, `setDoc`|Add new documents to Firestore.|
|**Read**|`getDoc`, `getDocs`|Fetch single or multiple documents.|
|**Update**|`updateDoc`|Update specific fields in a document.|
|**Delete**|`deleteDoc`, `deleteField`|Delete documents or fields in Firestore.|
|**Real-Time Updates**|`onSnapshot`|Listen to real-time changes.|
|**Query**|`query`, `where`|Fetch documents based on conditions.|

---

### **Tips for Beginners:**

1. Always initialize Firestore before using it.
2. Use **`addDoc`** for generating unique document IDs.
3. Use **`onSnapshot`** for real-time updates.
4. Structure your database properly for scalability.
5. Test queries in the Firebase Console to better understand the data structure.

This cheat sheet should help you get started with Firestore CRUD operations. Let me know if you have any questions!
   