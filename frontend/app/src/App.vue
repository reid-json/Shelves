<script>
export default {
  data() {
    return {
      albums: [
        {
          id: 0,
          title: 'Skate',
          sleeveSrc: '/images/BrunoCover.jpeg',
          vinylSrc: '/images/vinyl.png',
          audioSrc: '/audio/BrunoMars/Skate.mp3',
          isOpen: false,
          isPlaying: false,
          audio: null,
        },
        {
          id: 1,
          title: 'forever??????????',
          sleeveSrc: '/images/GlassCover.jpg',
          vinylSrc: '/images/vinyl.png',
          audioSrc: '/audio/GlassBeach/forever.mp3',
          isOpen: false,
          isPlaying: false,
          audio: null,
        },
        {
          id: 2,
          title: 'Earthquake',
          sleeveSrc: '/images/FKJCover.jpg',
          vinylSrc: '/images/vinyl.png',
          audioSrc: '/audio/FKJ/Earthquake.mp3',
          isOpen: false,
          isPlaying: false,
          audio: null,
        },
        {
          id: 3,
          title: 'Change',
          sleeveSrc: '/images/DeftonesCover.jpg',
          vinylSrc: '/images/vinyl.png',
          audioSrc: '/audio/Deftones/Change.mp3',
          isOpen: false,
          isPlaying: false,
          audio: null,
        },
        {
          id: 4,
          title: 'Touch',
          sleeveSrc: '/images/KatseyeCover.jpg',
          vinylSrc: '/images/vinyl.png',
          audioSrc: '/audio/Katseye/Touch.mp3',
          isOpen: false,
          isPlaying: false,
          audio: null,
        },
        {
          id: 5,
          title: 'River',
          sleeveSrc: '/images/LeonBridgesCover.jpg',
          vinylSrc: '/images/vinyl.png',
          audioSrc: '/audio/LeonBridges/River.mp3',
          isOpen: false,
          isPlaying: false,
          audio: null,
        },
        {
          id: 6,
          title: 'Big Sleep',
          sleeveSrc: '/images/TheWeekndCover.jpg',
          vinylSrc: '/images/vinyl.png',
          audioSrc: '/audio/TheWeeknd/BigSleep.mp3',
          isOpen: false,
          isPlaying: false,
          audio: null,
        },
        {
          id: 7,
          title: 'Beyond The Sun',
          sleeveSrc: '/images/ShinedownCover.jpg',
          vinylSrc: '/images/vinyl.png',
          audioSrc: '/audio/Shinedown/Beyond the Sun.mp3',
          isOpen: false,
          isPlaying: false,
          audio: null,
        },
        {
          id: 8,
          title: 'Californication',
          sleeveSrc: '/images/RHCPCover.jpg',
          vinylSrc: '/images/vinyl.png',
          audioSrc: '/audio/RHCP/Californication.mp3',
          isOpen: false,
          isPlaying: false,
          audio: null,
        },
        {
          id: 9,
          title: 'From Eden',
          sleeveSrc: '/images/HozierCover.jpg',
          vinylSrc: '/images/vinyl.png',
          audioSrc: '/audio/Hozier/FromEden.mp3',
          isOpen: false,
          isPlaying: false,
          audio: null,
        },

      ],
    };
  },
  methods: {
    stopAllExcept(indexToKeep) {
      this.albums.forEach((album, i) => {
        if (i !== indexToKeep) {
          if (album.audio) {
            album.audio.pause();
            album.audio.currentTime = 0;
          }
          album.isOpen = false;
          album.isPlaying = false;
        }
      });
    },
    playSong(index) {
      this.stopAllExcept(index);
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
      this.stopAllExcept(index);
      const album = this.albums[index];
      if (!album.audio) {
        album.audio = new Audio(album.audioSrc);
      } else {
        album.audio.pause();
        album.audio.currentTime = 0;
      }
      album.audio.play();
      album.isOpen = true;
      album.isPlaying = true;
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
    <h1 class="shop-title">Song Collection</h1>
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
        <h2 class="album-title">{{ album.title }}</h2>
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

.album-title {
  margin: 10px 0;
  font-size: 1.2rem;
  color: #ff7777;
  font-weight: bold;
}
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