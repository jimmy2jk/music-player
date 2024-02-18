<script>
export default {
  props: ["song"],
};
</script>

<template>
  <div class="song-container">
    <div class="song-album">
      <img :src="song.img" alt="album" class="album-img" />
    </div>
    <div class="song-info">
      <span class="song-title">{{ song.title }}</span>
      <span class="song-artist">{{ song.artist }}</span>
    </div>
  </div>
</template>

<style scoped>
.song-container {
  display: flex;
  box-sizing: border-box;
  height: 100px;
  text-align: left;
  padding: 10px 20px;
  margin: 15px 30px;
  gap: 20px;
  background-color: rgb(40, 39, 39);
  color: white;
  border-radius: 10px;
  transition: all 350ms ease;
}

.song-container:hover {
  cursor: pointer;
  transform: scale(1.05) ;
}

.song-album {
  display: flex;
  box-sizing: border-box;
  width: 100px;
}

.album-img {
  display: flex;
  width: 100%;
}

.song-info {
  display: flex;
  flex-direction: column;
}

.song-title {
  font-size: 24px;
  font-weight: 700;
}

.song-artist {
  font-size: 18px;
  font-weight: normal;
}
</style>
