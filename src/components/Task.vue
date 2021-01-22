<template>
  <div id="task">
    <button type="button" @click="logout" id="logout">ログアウト</button>
    <form>
      <input type="text" v-model="message" id="message" />
      <div @click="send">送信</div>
    </form>
  </div>
</template>

<script>
import firebase from "firebase"; // firebaseのインポート

// const db = firebase.firestore();
// db.settings({
//   timestampsInSnapshots: true,
// });
// const collection = db.collection("messages");
// const submitBtn = document.getElementById("submit-button");

// collection.orderBy("created").onSnapshot((snapshot) => {
//   /* messageCollectionに変化があった場合 */
//   snapshot.docChanges().forEach((change) => {
//     /* snapshot.docChanges()の返り値は、コレクション自体 */
//     if (change.type === "added") {
//       /* コレクションのデータ変化が追加出会った場合？ */
//       chatMessages.push(change.doc.data());
//     }
//   });
// });

// submitBtn.addEventListener("click", (e) => {
//   e.preventDefault();

// const val = message.value.trim();
// if (val === "") return;

// message.value = "";
// message.focus();

// collection
//   .add({
//     message: val,
// userName: loginUser.displayName,
// created: firebase.firestore.FieldValue.serverTimestamp(),
//     })
//     .catch((error) => {
//       console.log(error);
//     });
// });

// message.focus();

export default {
  name: "logout",
  data: function () {
    return {
      message: "",
    };
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
      console.log(this.message);
    },
  },
};
</script>
