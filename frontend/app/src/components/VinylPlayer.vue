<script>
export default {
  data() {
    return {
      isOpen: false,
    };
  },
  methods: {
    playAlbum() {
      this.isOpen = true;
      const audio = new Audio('/audio/HOB.mp3');
      audio.play();
    },
  },
};

</script>

<template>
  <div class="vinyl-container">
    <img src="/images/vinyl.png" class="vinyl" />
    <img
        src="/images/HOB.jpg"
        class="sleeve"
        :class="{ open: isOpen }"
    />
    <button @click="playAlbum">Play Album</button>
  </div>

</template>

<style>
.vinyl-container {
  position: relative;
  width: 300px;
  height: 300px;
  overflow: hidden;
}

.vinyl {
  width: 100%;
  height: auto;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 1;
  pointer-events: auto;
}

.sleeve {
  width: 100%;
  height: auto;
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
  transition: transform 1s ease;
}

.sleeve.open {
  transform: translateX(-120%);
  pointer-events: none;
}

</style>

