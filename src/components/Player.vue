<script>
import Song from "./Song.vue";

export default {
  props: ["songs"],

  components: {
    Song,
  },

  data() {
    return {
      current: {},
      index: 0,
      isPlaying: false,
      player: new Audio(),
    };
  },

  methods: {
    play(song) {
      if (typeof song !== "undefined") {
        this.current = song;
        this.player.src = this.current.src;
      }
      this.player.play();
      this.player.addEventListener("ended", () => this.next());
      this.isPlaying = true;
    },
    pause() {
      this.player.pause();
      this.isPlaying = false;
    },
    next() {
      this.index = this.index === this.songs.length - 1 ? 0 : this.index + 1;
      this.play(this.songs[this.index]);
    },
    prev() {
      this.index = this.index === 0 ? this.songs.length - 1 : this.index - 1;
      this.play(this.songs[this.index]);
    },
    incVolume() {
      if (this.player.volume < 1.0) {
        this.player.volume += 0.1;
      }
    },
    decVolume() {
      if (this.player.volume > 0) {
        this.player.volume -= 0.1;
      }
    },
  },

  created() {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
    this.player.volume = 0.5;
  },
};
</script>

<template>
  <main>
    <div class="player">
      <div class="current">
        <h2 class="song-title">{{ current.title }}</h2>
        <h2 class="song-artist">{{ current.artist }}</h2>
        <div class="current-img">
          <img :src="current.img" />
        </div>
      </div>

      <div class="controls">
        <button class="volume-" @click="decVolume">🔉</button>
        <button class="prev" @click="prev">◀◀</button>
        <button class="play" v-if="!isPlaying" @click="play()">▷</button>
        <button class="pause" v-else @click="pause">◻</button>
        <button class="next" @click="next">▶▶</button>
        <button class="volume+" @click="incVolume">🔊</button>
      </div>
    </div>

    <div class="playlist">
      <div class="playlist--title">
        <h3>The Playlist</h3>
      </div>
      <Song
        v-for="song in songs"
        :song="song"
        :key="song.src"
        @click="play(song)"
        :class="song.src === current.src ? 'song playing' : 'song'"
      />
    </div>
  </main>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

main {
  display: flex;
  height: 100%;
}

.player {
  display: flex;
  flex-direction: column;
  width: 100%;
  background-color: white;
  justify-content: center;
  align-items: center;
  background: linear-gradient(to right, black, rgb(29, 143, 109));
}

.current {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
}

.song-title {
  font-size: 40px;
  font-weight: 700;
  font-family: cursive;
  font-style: italic;
}

.song-artist {
  font-weight: normal;
  font-family: cursive;
}

.current-img {
  display: flex;
  justify-content: center;
  margin-bottom: 50px;
  width: max-content;
  border-radius: 50%;
  box-sizing: border-box;
  box-shadow: 0px 0px 7px 7px rgba(0, 0, 0, 0.3);
}

.current-img > img {
  border-radius: 50%;
  height: 300px;
}

button {
  width: 50px;
  height: 50px;
  border: 2px solid black;
  border-radius: 50%;
  font-weight: 700;
  text-align: center;
  color: black;
  font-size: 16px;
  background: transparent;
  box-shadow: 0px 0px 3px 3px rgba(0, 0, 0, 0.2);
  transition: all 100ms ease;
}
button:hover {
  transform: scale(1.2);
}

.controls {
  display: flex;
  align-items: center;
  gap: 20px;
}

.play, .pause {
  height: 80px;
  width: 80px;
  font-size: 32px;
  background: radial-gradient(circle, rgb(22, 129, 97) 20%,black);
  border: none;
}


.playlist {
  width: 80%;
  background-color: rgb(21, 21, 21);
}

.playlist--title {
  height: 100px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-family:Verdana, Geneva, Tahoma, sans-serif;
  font-size: 36px;
}
</style>
