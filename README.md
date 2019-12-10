## 1. Degit the Template

```bash
npx degit codediodeio/sveltefire-template fireapp
cd fireapp
npm install

npm run dev
```

## 2. Add Firebase Project Config

Create a project at https://firebase.google.com/ and grab your web config:

![](https://firebasestorage.googleapis.com/v0/b/firestarter-96e46.appspot.com/o/project-config.PNG?alt=media&token=5eabb205-7ba2-4fc3-905f-e9547055e754)


## 3. Active Firebase Services

Opt-in to the following services from the Firebase console to run the demo. 

1. **Anonymous** Login under *authentication -> sign-in method*
1. **Cloud Firestore** under *database*. Make sure it's in test mode (or provide write access to the `posts/` collection using Security Rules).  

*Forked from the official --> [sveltejs/template](https://github.com/sveltejs/component-template)*
