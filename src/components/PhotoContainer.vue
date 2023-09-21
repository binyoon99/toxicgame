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
      <div
        class="black-background"
        :style="`height: ${blackBoxPercentage}%`"
      ></div>
    </div>
    <button v-if="hasPlayedLast24hours == false" @click="changeImage"  class="submit-button" >Skip</button>
     <button v-else  class="submit-button" style="opacity: 0.7"> You already played</button>
    <!-- <img :src="`${championNames[0]}`" alt="League of Legends Champion" class="champion-image"> -->
    <div style="color: white;
    background-color: #808080; width: 50%; margin: 0 auto; border-radius: 10px; position: center;">
    <p>Enter the name of the champion:</p>
    <p>
      You have <span style="color: red">{{ chances }}</span> to guess it
      correctly
    </p>
    </div>
  </div>
  <InputContainer
    :blackBoxPercentage="blackBoxPercentage"
    @changeblackBoxPercentage="blackBoxPercentage = $event"
    @chancesDumbe="chances = $event"
    :chances="chances"
    :currentChampName="currentChampName"
    :hasPlayedLast24hours="hasPlayedLast24hours"
  />
</template>

<script>
import axios from "axios";
import InputContainer from "./InputContainer.vue";

export default {
  name: "PhotoContainer",
  data() {
    return {
      chances: 4,
      championInfo: [],
      currentChampName: "Aatrox",
      currentChampIndex: 0,
      blackBoxPercentage: 90,

    };
  },
  props: {
    hasPlayedLast24hours: Boolean
  },
  components: {
    InputContainer: InputContainer,
  },
  mounted() {},
  created() {
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
        console.log("Sibal " + this.championInfo[0].id);
        this.currentChampIndex = Math.floor(
          Math.random() * this.championInfo.length
        );
        this.currentChampName =
          this.championInfo[this.currentChampIndex].champName;
      })
      .catch((err) => {
        console.log("u r stupid u have error" + err);
      });
  },
  methods: {
    changeImage() {
      this.currentChampIndex = Math.floor(
        Math.random() * this.championInfo.length
      );
      this.currentChampName =
        this.championInfo[this.currentChampIndex].champName;
         location. reload(); 
    },
  },
};
</script>
