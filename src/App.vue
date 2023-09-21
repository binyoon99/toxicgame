<script setup>
import Header from "./components/Header.vue";
import PhotoContainer from "./components/PhotoContainer.vue";
</script>
<template>
  <main>
    <p
      v-if="hasPlayedLast24hours == true"
      style="padding: 10px; text-align: center"
    >
      You already played.
      <br />
      <span>{{ textMessageCounter }}</span>
    </p>
    <Header></Header>
    <PhotoContainer :hasPlayedLast24hours="hasPlayedLast24hours" />
  </main>
</template>
<script >
export default {
  name: "App",
  data() {
    return {
      hasPlayedLast24hours: false,
      textMessageCounter: "",
      timeDifference: 0,
    };
  },
  created() {
    const playedTime = new Date(localStorage?.getItem("myTime"));

    if (playedTime != null) {
      const currentTime = new Date();
      this.timeDifference = currentTime - playedTime;
      const millisecondsIn24Hours = 24 * 60 * 60 * 1000;
      if (this.timeDifference > millisecondsIn24Hours) {
        console.log("More than 24 hours have passed.");
      } else {
        console.log("Less than 24 hours have passed.");
        this.hasPlayedLast24hours = true;
      }
    }
  },
  mounted() {
    //  setInterval(this.getCountUp(), 1000);
    // setInterval(()=>{
    //   console.log("There is an interval")
    // },1000)
    if (localStorage.getItem("myTime") != null) {
      var that = this;
      var interval = setInterval(() => {
        that.getCountUp();
      }, 1000);
      if (this.timeDifference == 0) {
        clearInterval(interval);
      }
    }
  },
  methods: {
    getCountUp() {
      const playedTime = new Date(localStorage?.getItem("myTime"));
      const currentTime = new Date();
      this.timeDifference = currentTime - playedTime;
      const hours = Math.floor(this.timeDifference / 3600000); // 1 hour = 3600000 milliseconds
      const minutes = Math.floor((this.timeDifference % 3600000) / 60000); // 1 minute = 60000 milliseconds
      const seconds = Math.floor((this.timeDifference % 60000) / 1000); // 1 sec
      console.log(
        "hours: " + hours + ", minutes: " + minutes + " ,seconds: " + seconds
      );
      this.textMessageCounter =
        "hours: " + hours + ", minutes: " + minutes + " ,seconds: " + seconds +" /24hours";
    },
  },
};
</script>

<style src="./assets/main.css"></style>