A starter template for [SvelteFire](https://github.com/codediodeio/sveltefire). 

## 1. Degit the Template

```bash
npx degit codediodeio/sveltefire-template fireapp
cd fireapp
npm install
```

## 2. Get a Firebase Project

Create a Firebase project at https://firebase.google.com/ and grab your web config:

![](https://firebasestorage.googleapis.com/v0/b/firestarter-96e46.appspot.com/o/project-config.PNG?alt=media&token=5eabb205-7ba2-4fc3-905f-e9547055e754)

Opt-in to the following services from the Firebase console to run the demo. 

1. **Anonymous** Login under *authentication -> sign-in method*
1. **Cloud Firestore** under *database*. Make sure it's in test mode (or provide write access to the `posts/` collection using Security Rules).  


## 3. Update the Firebase Config

Open `App.svelte` and replace the `firebaseConfig` prop with your Firebase project credentials.

```js
let firebaseConfig = {
  // Insert Firebase Credentials here
};
```

Run it:

```bash
npm run dev
```

You should see something like this:

![sveltefire demo app](https://firebasestorage.googleapis.com/v0/b/sveltefire-testing.appspot.com/o/sveltefire-demo.gif?alt=media&token=d5ea2807-7c50-4f94-bc73-8698b9528902)

*Forked from the official --> [sveltejs/template](https://github.com/sveltejs/component-template)*
