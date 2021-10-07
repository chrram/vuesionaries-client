<template>
  <view class="container">
    <text class="text-color-primary"
      >You have ordered {{ cups }} cups of coffee</text
    >
    <image
      :style="{width: 100, height: 100}"
      :source="{
        uri: 'https://64.media.tumblr.com/389eab7635fa3a13d04cb945e1974a73/tumblr_ml5xhbUWC21qg6rkio1_500.gifv',
      }"
    />
  </view>
</template>

<script>
import firebase from 'firebase';

const firebaseConfig = {
  apiKey: 'AIzaSyD1peEn0FDGojiMbhTl-Y-uIuSSQL_XH2s',
  authDomain: 'mwsd-project-3b871.firebaseapp.com',
  projectId: 'mwsd-project-3b871',
  storageBucket: 'mwsd-project-3b871.appspot.com',
  messagingSenderId: '888827003326',
  appId: '1:888827003326:web:4d218192bd4ca25e2fb9ef',
};

export default {
  data() {
    return {
      cups: 0,
    };
  },

  methods: {},
  async mounted() {
    if (!firebase.default.apps.length) {
      firebase.initializeApp(firebaseConfig);
    }
    dbRef = firebase.default.firestore().collection('coffees');
    dbRef.doc('9IpwtC8Qh1jrlJ3STbrP');
    try {
      const documents = await dbRef.onSnapshot((querySnapshot) => {
        querySnapshot.docChanges().forEach((change) => {
          this.cups = change.doc.data().numberOrdered;
        });
      });
    } catch (error) {
      console.log(error, 'error');
    }
  },
};
</script>

<style>
.container {
  background-color: white;
  align-items: center;
  margin-top: 150;
  flex: 1;
}
.text-color-primary {
  color: brown;
  padding: 45;
}
</style>
