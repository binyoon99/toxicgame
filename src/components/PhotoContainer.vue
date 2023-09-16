<template>
  <!-- <button @click="play"> Play</button> -->
  <div class="container">
    <!-- <div  :style="`background-image:url${championInfo[0]?.url}`"  alt="League of Legends Champion"    class="champion-image"/> -->
    <div class="test">
      <img
        :src="`${championInfo[currentChampIndex]?.url}`"
        alt="League of Legends Champion"
        class="champion-image"
      />
      <div class="black-background"></div>
    </div>
    <button @click="changeImage"> Testing </button>
    <!-- <img :src="`${championNames[0]}`" alt="League of Legends Champion" class="champion-image"> -->
    <p>Enter the name of the champion:</p>
    <p>You have {{ chances }} to guess it correctly</p>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "PhotoContainer",
  data() {
    return {
      chances: 4,
      championInfo: [],
      currentChampName: "",
      currentChampIndex : 0,

    };
  },
  props:{
 
  },
  mounted() {
     axios
        .get(
          "http://ddragon.leagueoflegends.com/cdn/11.11.1/data/en_US/champion.json"
        )
        .then((res) => {
          console.log("first" + res.data.data.Aatrox.name);
          const datas = res.data;
          let i = 0;
          let name = "";
          let id = 0;
          let splashArtUrl = "";
          // Champion Name parsing
          for (const data in datas.data) {
            name = data; //sneaky
            id = i;
            splashArtUrl = `http://ddragon.leagueoflegends.com/cdn/img/champion/loading/${name}_0.jpg`;
            i++;
            var championList = {
              id: id,
              champName: name,
              url: splashArtUrl,
            };
            this.championInfo.push(championList);
          }
          console.log("Sibal "+this.championInfo[0].id);
        })
        .catch((err) => {
          console.log("u r stupid u have error" + err);
        });
  },
  methods:{
    changeImage(){
      this.currentChampIndex = Math.floor(Math.random() * this.championInfo.length);
      this.currentChampName = this.championInfo[this.currentChampIndex].name;
    }
  }
};
</script>

<style>
</style>