<template>
  <div id="task">
    <button type="button" @click="logout" id="logout">ログアウト</button>
  </div>
</template>

<script>
import firebase from "firebase"; // firebaseのインポート

export default {
  name: "logout",
  created() {
    var user = firebase.auth().currentUser;
    console.log(user);
  },
  methods: {
    logout: function () {
      firebase
        .auth()
        .signOut()
        .then(() => {
          console.log("ログアウトしました");
          location.href = "/";
        });
    },
  },
};
</script>
