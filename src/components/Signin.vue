<template>
  <div id="signin">
    <h2>サインイン</h2>
    <button @click="signInWithGoogle">Googleアカウントでサインイン</button>
  </div>
</template>

<script>
import firebase from "firebase"; // firebaseのインポート

export default {
  name: "Signin",
  methods: {
    signInWithGoogle: function () {
      var provider = new firebase.auth.GoogleAuthProvider();
      firebase
        .auth()
        .signInWithPopup(provider)
        .then(() => {
          this.$router.push("/task");
        });
    },
  },
};
</script>


<style>
</style>
