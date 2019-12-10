<script>
  import { FirebaseApp, User, Doc, Collection } from "sveltefire";

  import firebase from "firebase/app";
  import "firebase/firestore";
  import "firebase/auth";
  import "firebase/performance";
  import "firebase/analytics";

  let firebaseConfig = {
	// Insert Firebase Credentials here
  };

  firebase.initializeApp(firebaseConfig);
</script>

<main>

  {#if !firebaseConfig.projectId}
    <strong>Step 0</strong>
    Create a
    <a href="https://firebase.google.com/">Firebase Project</a>
    and paste your web config into
    <code>App.svelte</code>
    .
  {/if}

  <!-- 1. 🔥 Firebase App -->
  <FirebaseApp {firebase}>

    <h1>SvelteFire Mode Activated</h1>

    <p>
      <strong>PRO Tip:</strong>
      Open the browser console for development logging.
    </p>


    <!-- 2. 😀 Get the current user -->
    <User let:user let:auth>
      Howdy! User
      <em>{user.uid}</em>

      <button on:click={() => auth.signOut()}>Sign Out</button>

      <div slot="signed-out">
        <p>
          <strong>Step 1</strong>
          Sign-in or create a Firebase user
        </p>
        <button on:click={() => auth.signInAnonymously()}>
          Sign In Anonymously
        </button>
      </div>

      <hr />

      <!-- 3. 📜 Get a Firestore document owned by a user -->
      <Doc path={`posts/${user.uid}`} let:data={post} let:ref={postRef} log>

        <h2>{post.title}</h2>

        <p>
          Document
          <em>{postRef.path}</em>
          created at {new Date(post.createdAt)}
        </p>

        <span slot="loading">Loading post...</span>
        <span slot="fallback">
          <p>
            <strong>Step 2</strong>
            Push the button below to create a document in Firestore for this
            user.
          </p>

          <button
            on:click={() => postRef.set({
                title: 'I like Svelte',
                createdAt: Date.now()
              })}>
            Create Document
          </button>
        </span>

        <!-- 4. 💬 Get all the comments in its subcollection -->

        <h3>Comments</h3>
        <Collection
          path={postRef.collection('comments')}
          query={ref => ref.orderBy('createdAt')}
          let:data={comments}
          let:ref={commentsRef}
          log>

          {#if !comments.length}
            <p>
              <strong>Step 3</strong>
              Add comments to the document's subcollection
            </p>
          {/if}

          {#each comments as comment}
            <p>
              <em>{comment.ref.path}</em>
            </p>
            <p>
              {comment.text}
              <button on:click={() => comment.ref.delete()}>Delete</button>
            </p>
          {/each}


          <button
            on:click={() => commentsRef.add({
                text: 'Me too!',
                createdAt: Date.now()
              })}>
            Add Comment
          </button>

          <span slot="loading">Loading comments...</span>

        </Collection>
      </Doc>
    </User>
  </FirebaseApp>

</main>


<!-- Styles -->
<style>
  main {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1,
  em {
    color: #ff3e00;
  }

  hr {
    height: 1px;
    border: none;
    background: rgb(195, 195, 195);
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>