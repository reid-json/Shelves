<script>
export default {
  data() {
    return {
      albums: Array.from({ length: 20 }, (_, i) => ({
        id: i,
        title: `Album ${i + 1}`,
        sleeveSrc: `/images/HOB.jpg`,
        vinylSrc: `/images/vinyl.png`,
        audioSrc: `/audio/HouseOfBallons/tildawn.mp3`,
        isOpen: false,
        isPlaying: false,
        audio: null,
      })),
    };
  },
  methods: {
    playSong(index) {
      this.albums.forEach((album, i) => {
        if (i !== index) {
          if (album.audio) {
            album.audio.pause();
            album.audio.currentTime = 0;
          }
          album.isOpen = false;
          album.isPlaying = false;
        }
      });

      const album = this.albums[index];
      if (!album.isOpen) {
        album.isOpen = true;
        setTimeout(() => {
          album.audio = new Audio(album.audioSrc);
          album.audio.play();
          album.isPlaying = true;
        }, 1000);
      } else if (album.audio && album.audio.paused) {
        album.audio.play();
        album.isPlaying = true;
      }
    },
    pauseSong(index) {
      const album = this.albums[index];
      if (album.audio) {
        album.audio.pause();
        album.isPlaying = false;
      }
    },
    restartSong(index) {
      const album = this.albums[index];
      if (album.audio) {
        album.audio.pause();
        album.audio.currentTime = 0;
        album.audio.play();
        album.isPlaying = true;
      }
    },
    closeAlbum(index) {
      const album = this.albums[index];
      if (album.audio) {
        album.audio.pause();
        album.audio.currentTime = 0;
      }
      album.isOpen = false;
      album.isPlaying = false;
    },
  },
};
</script>
<template>
  <div class="vinyl-shop">
    <h1 class="shop-title">🎵 Vinyl Shop Collection 🎵</h1>
    <div class="vinyl-grid">
      <div
          v-for="(album, index) in albums"
          :key="album.id"
          class="vinyl-container"
      >
        <div class="vinyl-wrapper">
          <img
              :src="album.vinylSrc"
              class="vinyl"
              :class="{ spin: album.isPlaying }"
              @click="playSong(index)"
          />
          <img
              :src="album.sleeveSrc"
              class="sleeve"
              :class="{ open: album.isOpen }"
          />
        </div>
        <div class="controls">
          <button @click="playSong(index)">Play Song</button>
          <button @click="pauseSong(index)">Pause</button>
          <button @click="restartSong(index)">Restart</button>
          <button @click="closeAlbum(index)">Close</button>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped>
.vinyl-shop {
  background-color: #0a0a0a;
  color: #f5f5f5;
  min-height: 100vh;
  padding: 2rem;
  font-family: 'Courier New', monospace;
  text-align: center;
}

.shop-title {
  font-size: 3rem;
  margin-bottom: 2rem;
  letter-spacing: 2px;
  color: #ff5555;
}

.vinyl-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 2rem;
  justify-items: center;
}

.vinyl-container {
  background-color: #111;
  border-radius: 10px;
  box-shadow: 0 0 15px #000;
  padding: 10px;
  width: 300px;
}

.vinyl-wrapper {
  position: relative;
  width: 100%;
  height: 300px;
  overflow: hidden;
}

.vinyl {
  position: absolute;
  width: 100%;
  height: auto;
  top: 0;
  left: 0;
  z-index: 1;
  cursor: pointer;
}

.vinyl.spin {
  animation: spin 3s linear infinite;
}

.sleeve {
  position: absolute;
  width: 100%;
  height: auto;
  top: 0;
  left: 0;
  z-index: 2;
  transition: transform 1s ease;
}

.sleeve.open {
  transform: translateX(-120%);
  pointer-events: none;
}

.controls {
  margin-top: 10px;
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  justify-content: center;
  background-color: #222;
  padding: 10px;
  border-radius: 0 0 10px 10px;
}

.controls button {
  background-color: #ff5555;
  border: none;
  padding: 6px 10px;
  color: #fff;
  font-size: 0.85rem;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.controls button:hover {
  background-color: #ff7777;
}

@keyframes spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}
</style>