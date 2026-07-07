<template>
  <div>
    <!-- Hidden HTML5 Audio Element -->
    <audio ref="audioPlayer" loop>
      <source src="../assets/flashlight.mp3" type="audio/mpeg" />
    </audio>

    <!-- Floating Audio Control Button -->
    <button
      @click="toggleMusic"
      class="absolute bottom-6 right-6 z-30 flex items-center justify-center w-14 h-14 rounded-full border border-white/60 shadow-lg backdrop-blur-md transition-all duration-300 active:scale-95 group bg-white/80 cursor-pointer"
      :class="
        isPlaying ? 'border-pink-300 shadow-pink-200/50' : 'border-rose-200'
      "
      :title="isPlaying ? 'Pause Music' : 'Play Music'"
    >
      <span
        class="text-2xl select-none transition-transform duration-500 inline-block"
        :class="{ 'animate-spin-slow': isPlaying }"
      >
        {{ isPlaying ? "🎵" : "🔇" }}
      </span>
    </button>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

const audioPlayer = ref(null);
const isPlaying = ref(false);
const targetVolume = 0.3;

onMounted(() => {
  if (audioPlayer.value) {
    audioPlayer.value.volume = targetVolume;
  }
});

const toggleMusic = () => {
  if (!audioPlayer.value) return;
  if (isPlaying.value) {
    audioPlayer.value.pause();
    isPlaying.value = false;
  } else {
    audioPlayer.value.volume = targetVolume;
    audioPlayer.value
      .play()
      .then(() => {
        isPlaying.value = true;
      })
      .catch((err) => {
        console.log("Interaction required:", err);
      });
  }
};

const stopMusicInstance = () => {
  if (audioPlayer.value) {
    audioPlayer.value.pause();
    audioPlayer.value.currentTime = 0;
  }
  isPlaying.value = false;
};

// Expose the stop function so the parent menu can call it when hitting "Back"
defineExpose({
  stopMusicInstance,
});
</script>

<style scoped>
@keyframes spin-slow {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}
.animate-spin-slow {
  animation: spin-slow 4s linear infinite;
}
</style>
