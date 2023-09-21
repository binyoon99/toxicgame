<template>
  <div class="inputContainer">
    <input
      type="text"
      v-model="inputTest"
      class="champion-input shattered"
      placeholder="Enter champion name..."
    />
    <br />
    <button v-if="hasPlayedLast24hours == false" @click="submit" class="submit-button">Submit</button>
     <button v-else  class="submit-button" style="opacity: 0.7"> You already played</button>

  </div>
</template>

<script>
export default {
  name: "InputContainer",
  data() {
    return {
      inputTest: "",
    };
  },
  props: {
    chances: Number,
    currentChampName: String,
    blackBoxPercentage: Number,
    hasPlayedLast24hours : Boolean,
  },
  methods: {
    submit() {
      let cate = new Date()
      console.log(cate);
      // console.log(
      //   this.inputTest.toLowerCase() == this.currentChampName.toLowerCase() 
      // );
      // console.log(
      //   " InputTest : " +
      //     this.inputTest +
      //     " CurrentChampName : " +
      //     this.currentChampName.toLowerCase()
      // );

      if (this.inputTest.toLowerCase().replace(/\s/g, '') == this.currentChampName.toLowerCase().replace(/\s/g, '')) {
        alert("Guessed it correct, the champion is " + this.currentChampName);
         localStorage.setItem("myTime",cate)
      } else {
        if (this.chances == 1) {
          document.getElementById("app").classList.add("evilMerc");
          document.getElementById("app").style.transform =
            "translate(-50%, -50%) rotate(360deg)";
          setTimeout(() => {
            alert(
              "You used up all 4 chances and broke my website. Thank you for playing!"
            );
               localStorage.setItem("myTime",cate)
          }, 1000);
          return;
        } else {
          this.$emit("chancesDumbe", this.chances - 1);
          console.log("blackBoxPercentage: " + this.blackBoxPercentage);
          this.$emit("changeblackBoxPercentage", this.blackBoxPercentage - 10);
        }
      }
    },
  },
};
</script>

<style>
</style>