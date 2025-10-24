<template>
  <div class="vinyl-container">
    <img
        src="/images/vinyl.png"
        class="vinyl"
        :class="{ spin: isPlaying }"
        @click="playAlbum"
    />
    <img
        src="/images/HOB.jpg"
        class="sleeve"
        :class="{ open: isOpen }"
    />
    <button @click="playAlbum">Play Album</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isOpen: false,
      isPlaying: false,
    };
  },
  methods: {
    playAlbum() {
      if (!this.isOpen) {
        this.isOpen = true;
        setTimeout(() => {
          this.isPlaying = true;
          const audio = new Audio('/audio/HouseOfBallons/tildawn.mp3');
          audio.play();
        }, 1000);
      }
    },
  },
};
</script>

<style>
.vinyl-container {
  position: relative;
  width: 300px;
  height: 300px;
  overflow: hidden;
  margin: 50px auto;
  background-color: #111;
  border-radius: 10px;
  padding: 10px;
}

button {
  position: absolute;
  bottom: 10px;
  left: 50%;
  transform: translateX(-50%);
  z-index: 3;
  background-color: #ff0000;
  border: none;
  padding: 8px 16px;
  cursor: pointer;
}

.vinyl-container {
  position: relative;
  width: 300px;
  height: 300px;
  overflow: hidden;
  margin: 50px auto;
  background-color: #111;
  border-radius: 10px;
  padding: 10px;
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

@keyframes spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}
</style>