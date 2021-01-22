<template>
  <div id="task">
    <p>uid: {{ user_uid }}</p>
    <p>
      <button type="button" @click="logout" id="logout">ログアウト</button>
    </p>

    <div v-for="chatMessage in chatMessages" :key="chatMessage.message">
      <p>
        {{ chatMessage.message }}<span>&emsp;by&emsp;</span
        >{{ chatMessage.userName }}
      </p>
    </div>
    <form>
      <input type="text" v-model="message" id="message" />
      <div @click="send">送信</div>
    </form>
  </div>
</template>

<script>
import firebase from "firebase"; // firebaseのインポート
require("firebase/firestore");

let db;
let user;
let collection;
let chatMessages = [];

export default {
  name: "logout",
  data() {
    return {
      message: "",
      chatMessages: chatMessages,
      user_uid: firebase.auth().currentUser.uid,
    };
  },
  created() {
    db = firebase.firestore();
    db.settings({
      timestampsInSnapshots: false,
    });
    collection = db.collection("messages");
    user = firebase.auth().currentUser;
    collection.orderBy("created").onSnapshot((snapshot) => {
      /* messageCollectionに変化があった場合 */
      snapshot.docChanges().forEach((change) => {
        /* snapshot.docChanges()の返り値は、コレクション自体 */
        if (change.type === "added") {
          /* コレクションのデータ変化が追加出会った場合？ */
          chatMessages.push(change.doc.data());
        }
      });
    });
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
    send: function () {
      let val = this.message.trim();
      if (val === "") return;

      this.message = "";

      collection
        .add({
          message: val,
          userName: user.displayName,
          created: firebase.firestore.FieldValue.serverTimestamp(),
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>
