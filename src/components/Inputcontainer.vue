<template>
  <div class="inputContainer">
    <input
      type="text"
      v-model="inputTest"
      class="champion-input shattered"
      placeholder="Enter champion name..."
    />
    <br />
    <button @click="submit" class="submit-button">Submit</button>
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
  },
  methods: {
    submit() {
      console.log(
        this.inputTest.toLowerCase() == this.currentChampName.toLowerCase()
      );
      console.log(
        " InputTest : " +
          this.inputTest +
          " CurrentChampName : " +
          this.currentChampName.toLowerCase()
      );

      if (this.inputTest.toLowerCase().replace(/\s/g, '') == this.currentChampName.toLowerCase().replace(/\s/g, '')) {
        alert("Guessed it correct, the champion is " + this.currentChampName);
      } else {
        if (this.chances == 0) {
          document.getElementById("mainContainer").classList.add("evilMerc");
          document.getElementById("mainContainer").style.transform =
            "translate(-50%, -50%) rotate(360deg)";
          setTimeout(() => {
            alert(
              "You used up all 4 chances and broke my website. Thank you for playing!"
            );
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