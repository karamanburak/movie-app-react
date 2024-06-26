# movie-app-react

 [Movie App Live](https://cinemaparadiso.vercel.app/)


<a href="https://cinemaparadiso.vercel.app/" target="_blank"></a>

## Description
A react movie project where you can access many details and trailers about the desired movie using tmdb api. Firebase, toastify, tailwind.css were used in this project.

## Project Skeleton

```
- Movie App (folder)
|
SOLUTION
├── public
│     └── index.html
├── src
│    ├── assets
│    │     └── [icons]
│    ├── auth
│    │     └── firebase.js
│    ├── components
│    │     ├── ErrorPage.jsx
│    │     ├── MovieCard.jsx
│    │     ├── Navbar.jsx
│    │     ├── SearchInput.jsx
│    │     ├── Switch.jsx
│    │     └── VideoSection.js
│    ├── context
│    │     ├── AuthContext.js
│    │     └── MovieContext.jsx
│    ├── helpers
│    │     └── toastNotify.js
│    ├── pages
│    │     ├── Login.jsx
│    │     ├── Main.jsx
│    │     ├── MovieDetail.jsx
│    │     ├── NotFound.jsx
│    │     └── Register.jsx
│    ├── router
│    │     ├── AppRouter.jsx
│    │     └── PrivateRouter.jsx
│    ├── App.js
│    ├── index.css
│    └── index.js
├── .env.local
├── .gitignore
├── example.env.local
├── LICENSE
├── package.json
├── README.md
├── tailwind.config.js
└── yarn.lock
```

![Project Snapshot](movie-app_structure.png)

## Outcome

![Project Snapshot](https://github.com/karamanburak/movie-app-react/assets/150926922/d1f623ba-4882-40b1-9555-26faefdac5b4)


## Steps to Solution

- Before start you can watch these tutorials:
  - https://www.youtube.com/watch?v=9bXhf_TELP4
  - https://www.youtube.com/watch?v=vDT7EnUpEoo
- Step 1 : Create React App using `npx create-react-app movie-app` and install firebase `npm i firebase` / `yarn add firebase`

- Step 2 : Signup `https://firebase.google.com/` and create new app in firebase.
  Firebase is a backed application development software that enables developers to develop iOS, Android and Web apps. It provides developers with a variety of tools and services to help them develop quality apps, grow their user base, and earn profit. It is built on Google’s infrastructure. Firebase offers a number of services, including: analytics,authentication, cloud messaging, realtime database, performance and test lab. Firebase is categorized as a NoSQL database program, which stores data in JSON-like documents.

![Project  Snapshot](firebase-create-app.gif)

- Step 3 : Use `https://firebase.google.com/docs/auth/web/start` and create `Authentication` operations.
  - Add the Firebase Authentication JS codes in your `firebase.js` file and initialize Firebase Authentication:

```jsx
import { initializeApp } from "firebase/app";
import { getAuth } from "firebase/auth";

// TODO: Replace the following with your app's Firebase project configuration at project settings part
// See: https://firebase.google.com/docs/web/learn-more#config-object
const firebaseConfig = {
  // ...
};

// Initialize Firebase
const app = initializeApp(firebaseConfig);

// Initialize Firebase Authentication and get a reference to the service
const auth = getAuth(app);
```

- Use this method to `Sign up new users` :

```jsx
import { getAuth, createUserWithEmailAndPassword } from "firebase/auth";

createUserWithEmailAndPassword(auth, email, password)
  .then((userCredential) => {
    // Signed in
    const user = userCredential.user;
  })
  .catch((error) => {
    console.log(error);
  });
```

- Go to https://console.firebase.google.com => Authentication => sign-in-method => `enable Email/password`
- Use this method to `Sign in existing users` :

```jsx
import { getAuth, signInWithEmailAndPassword } from "firebase/auth";

signInWithEmailAndPassword(auth, email, password)
  .then((userCredential) => {
    // Signed in
    const user = userCredential.user;
  })
  .catch((error) => {
    console.log(error);
  });
```

- Use this method to `Set an authentication state observer and get user data` :

```jsx
import { getAuth, onAuthStateChanged } from "firebase/auth";

onAuthStateChanged(auth, (user) => {
  if (user) {
    // User is signed in, see docs for a list of available properties
    // https://firebase.google.com/docs/reference/js/firebase.User
  } else {
    // User is signed out
  }
});
```

- Go to https://console.firebase.google.com => Authentication => sign-in-method => `enable Google`
- Use this method to `Authenticate Using Google with Popup` :

```jsx
import { GoogleAuthProvider } from "firebase/auth";

const provider = new GoogleAuthProvider();

signInWithPopup(auth, provider)
  .then((result) => {
    // The signed-in user info.
    const user = result.user;
  })
  .catch((error) => {
    // Handle Errors here.
    console.log(error);
  });
```

- Use this method to `Sign Out` :

```jsx
import { getAuth, signOut } from "firebase/auth";

signOut(auth)
  .then(() => {
    // Sign-out successful.
  })
  .catch((error) => {
    // An error happened.
  });
```

- Use this method to `Send a password reset email` :

```jsx
import { getAuth, sendPasswordResetEmail } from "firebase/auth";

sendPasswordResetEmail(auth, email)
  .then(() => {
    // Password reset email sent!
  })
  .catch((error) => {
    const errorMessage = error.message;
    // ..
  });
```

- Step 4 : Signup `https://www.themoviedb.org/documentation/api` and get API key. In order to get data use `https://api.themoviedb.org/3/discover/movie?api_key=${API_KEY}`
 or 
 `https://api.themoviedb.org/3/movie/now_playing?language=en-US&page=1&api_key=${API_KEY}` 
 to search movies use `https://api.themoviedb.org/3/search/movie?api_key=${API_KEY}&query=`, to get movie details use `https://api.themoviedb.org/3/movie/${id}?api_key=${API_KEY}` and to get video key use `https://api.themoviedb.org/3/movie/${id}/videos?api_key=${API_KEY}`. Use `https://image.tmdb.org/t/p/w1280${poster_path}` for image `src`.




