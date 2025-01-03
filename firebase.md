# FireBase

## FireBase Notification

> bun i firebase

src/firebase.js

```js
// Import the functions you need from the SDKs you need
import { initializeApp } from "firebase/app";
import { getAnalytics } from "firebase/analytics";
// TODO: Add SDKs for Firebase products that you want to use
// https://firebase.google.com/docs/web/setup#available-libraries

// for cloud messageing
import { getMessaging } from "firebase/messaging";

// Your web app's Firebase configuration
// For Firebase JS SDK v7.20.0 and later, measurementId is optional
const firebaseConfig = {
  apiKey: "AIzaSyBfq8Id1vtRM1Z4rKtWnekh78A6dExJmz0",
  authDomain: "omnileadz-35755.firebaseapp.com",
  projectId: "omnileadz-35755",
  storageBucket: "omnileadz-35755.firebasestorage.app",
  messagingSenderId: "323171451785",
  appId: "1:323171451785:web:500322cf4896097db51758",
  measurementId: "G-V8N3EZQ411",
};

// Initialize Firebase
export const app = initializeApp(firebaseConfig);
const analytics = getAnalytics(app);

export const messaging = getMessaging(app);
```

get notification permission from user

.jsx

```jsx
import { messaging } from "./firebase";
import {getToken } from "firebase/messaging";
async function requestPermission() {
  const permission = Notification.requestPermission();
  if (permission == "granted") {
   const token=await getToken(messaging,{vapidKey:"BESv_aedO0wgZ5bhcWIwuagJYDrs8FFqfvqHdAra0lXzkp7h_y5Zk85wDv0AGkhOE6SUQWDxLekOaimjtT4JMtY"});
   console.log(token);
  } else if (permission == "denied") {
  }
}

useEffect(() => {
  requestPermission();
}, []);
```

firebase-messaging-sw.js in public folder
```js
importScripts('https://www.gstatic.com/firebasejs/9.23.0/firebase-app-compat.js');
importScripts('https://www.gstatic.com/firebasejs/9.23.0/firebase-messaging-compat.js');

firebase.initializeApp({
    apiKey: "AIzaSyBfq8Id1vtRM1Z4rKtWnekh78A6dExJmz0",
    authDomain: "omnileadz-35755.firebaseapp.com",
    projectId: "omnileadz-35755",
    storageBucket: "omnileadz-35755.firebasestorage.app",
    messagingSenderId: "323171451785",
    appId: "1:323171451785:web:500322cf4896097db51758",
    measurementId: "G-V8N3EZQ411",
});

const messaging = firebase.messaging();

messaging.onBackgroundMessage((payload) => {
    console.log('[firebase-messaging-sw.js] Received background message ', payload);
    const notificationTitle = payload.notification.title;
    const notificationOptions = {
        body: payload.notification.body,
        icon: payload.notification.icon,
    };

    self.registration.showNotification(notificationTitle, notificationOptions);
});
 
```
