<script>
import Player from "./components/Player.vue";
// music imports
import riot from "./assets/audio/riot.mp3";
import never_too_late from "./assets/audio/never_too_late.mp3";
import time_of_dying from "./assets/audio/time-of-dying.mp3";
import good_life from "./assets/audio/theGoodLife.mp3";
//images imports
import neverTooLate from "./assets/images/NeverTooLate.jpg";
import lifeStartsNow from "./assets/images/lifeStartsNow.jpg";
import oneX from "./assets/images/oneX.jpg";

export default {
  components: {
    Player,
  },
  data() {
    return {
      songsList: [
        {
          title: "Never Too Late",
          artist: "Three Days Grace",
          src: never_too_late,
          img: neverTooLate,
        },
        {
          title: "Riot",
          artist: "Three Days Grace",
          src: riot,
          img: oneX,
        },
        {
          title: "Time Of Dying",
          artist: "Three Days Grace",
          src: time_of_dying,
          img: oneX,
        },
        {
          title: "Good Life",
          artist: "Three Days Grace",
          src: good_life,
          img: lifeStartsNow,
        },
      ],
    };
  },
};
</script>

<template>
  <main>
    <Player :songs="songsList" />
  </main>
</template>

<style scoped>
main {
  height: 100vh;
}
</style>
