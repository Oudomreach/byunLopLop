<template>
  <div
    class="min-h-screen w-full bg-gradient-to-br from-rose-100 via-pink-200 to-amber-100 text-rose-950 flex flex-col items-center justify-center font-sans p-6 overflow-hidden relative"
  >
    <!-- Hidden HTML5 Audio Element -->
    <audio ref="audioPlayer" loop>
      <source src="../assets/flashlight.mp3" type="audio/mpeg" />
    </audio>

    <button
      @click="goBack"
      class="absolute top-6 left-6 text-rose-600/80 hover:text-rose-900 transition-all duration-300 flex items-center space-x-2 text-xs font-extrabold tracking-widest uppercase z-30 bg-white/70 backdrop-blur-md px-4 py-2.5 rounded-full border border-white/60 shadow-sm active:scale-95 group"
    >
      <span
        class="transform group-hover:-translate-x-0.5 transition-transform duration-200"
        >←</span
      >
      <span>Back</span>
    </button>

    <button
      @click="showSecretMessage = true"
      class="absolute top-6 right-6 z-30 p-2 opacity-100 hover:opacity-100 transition-all duration-300 cursor-pointer group hover:scale-125"
      title="?"
    >
      <span class="text-2xl drop-shadow-md animate-spin-slow inline-block">
        <img :src="reachEmoji" alt="reach" class="w-12 h-auto" />
      </span>
    </button>

    <button
      @click="showMonkeySecret = true"
      class="absolute bottom-44 left-6 z-30 p-2 opacity-50 hover:opacity-100 transition-all duration-300 cursor-pointer group hover:scale-125"
      title="🙈"
    >
      <span class="text-4xl drop-shadow-md animate-bounce inline-block"
        >🐔</span
      >
    </button>

    <!-- NEW MUSIC PLAYER FLOATING CONTROL BUTTON (Bottom Right) -->
    <button
      @click="toggleMusic"
      class="absolute bottom-6 right-6 z-30 flex items-center justify-center w-14 h-14 rounded-full border border-white/60 shadow-lg backdrop-blur-md transition-all duration-300 active:scale-95 group bg-white/80"
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

    <div
      class="absolute inset-0 pointer-events-none overflow-hidden z-0 opacity-60"
    >
      <span class="animate-pulse absolute top-[10%] left-[20%] text-3xl"
        >✨</span
      >
      <span
        class="animate-pulse absolute bottom-[15%] right-[25%] text-2xl"
        style="animation-delay: 1s"
        >💖</span
      >
      <span
        class="animate-pulse absolute top-[40%] right-[10%] text-4xl"
        style="animation-delay: 0.5s"
        >🌸</span
      >
    </div>

    <div
      class="w-full max-w-[320px] sm:max-w-md bg-white/85 backdrop-blur-md rounded-3xl border border-white/50 shadow-xl shadow-rose-200/20 p-8 space-y-8 z-10 text-center animate-slide-up"
    >
      <div class="space-y-2">
        <h1
          class="text-3xl sm:text-4xl font-serif font-extrabold italic tracking-tight bg-clip-text text-transparent bg-gradient-to-br from-rose-500 to-pink-500 drop-shadow-sm"
        >
          Let's the fun BEGIN!
        </h1>
        <p class="text-rose-600/90 font-medium text-sm px-4">
          act like this is a blindbox
        </p>
        <p class="text-rose-600/90 font-medium text-sm px-4">
          becareful of what u pick! KEKEKEKE 😈😈😈
        </p>
      </div>

      <div class="flex flex-col gap-4 w-full">
        <button
          @click="selectOption('gift')"
          class="group relative w-full px-6 py-5 bg-white/60 hover:bg-white/90 border-2 border-pink-200/60 hover:border-pink-400/80 rounded-2xl shadow-sm hover:shadow-md hover:shadow-pink-200 transition-all duration-300 flex items-center justify-between overflow-hidden active:scale-[0.98]"
        >
          <div class="flex items-center space-x-4">
            <span
              class="text-3xl group-hover:scale-110 transition-transform duration-300 origin-bottom"
              >❓</span
            >
            <span
              class="text-lg font-bold text-rose-700 tracking-wide font-sans"
            ></span>
          </div>
          <svg
            class="w-6 h-6 text-pink-400 opacity-0 group-hover:opacity-100 transform translate-x-[-10px] group-hover:translate-x-0 transition-all duration-300"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M14 5l7 7m0 0l-7 7m7-7H3"
            ></path>
          </svg>
        </button>

        <button
          @click="selectOption('letter')"
          class="group relative w-full px-6 py-5 bg-white/60 hover:bg-white/90 border-2 border-pink-200/60 hover:border-pink-400/80 rounded-2xl shadow-sm hover:shadow-md hover:shadow-pink-200 transition-all duration-300 flex items-center justify-between overflow-hidden active:scale-[0.98]"
        >
          <div class="flex items-center space-x-4">
            <span
              class="text-3xl group-hover:scale-110 transition-transform duration-300 origin-bottom"
              >❓</span
            >
            <span
              class="text-lg font-bold text-rose-700 tracking-wide font-sans"
            ></span>
          </div>
          <svg
            class="w-6 h-6 text-pink-400 opacity-0 group-hover:opacity-100 transform translate-x-[-10px] group-hover:translate-x-0 transition-all duration-300"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M14 5l7 7m0 0l-7 7m7-7H3"
            ></path>
          </svg>
        </button>

        <!-- FLOWERS POPUP INITIATOR -->
        <button
          @click="openFlowerPopup"
          class="group relative w-full px-6 py-5 bg-white/60 hover:bg-white/90 border-2 border-pink-200/60 hover:border-pink-400/80 rounded-2xl shadow-sm hover:shadow-md hover:shadow-pink-200 transition-all duration-300 flex items-center justify-between overflow-hidden active:scale-[0.98]"
        >
          <div class="flex items-center space-x-4">
            <span
              class="text-3xl group-hover:scale-110 transition-transform duration-300 origin-bottom"
              >❓</span
            >
            <span
              class="text-lg font-bold text-rose-700 tracking-wide font-sans"
            ></span>
          </div>
          <svg
            class="w-6 h-6 text-pink-400 opacity-0 group-hover:opacity-100 transform translate-x-[-10px] group-hover:translate-x-0 transition-all duration-300"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M14 5l7 7m0 0l-7 7m7-7H3"
            ></path>
          </svg>
        </button>
      </div>
    </div>

    <!-- CLEAN DECOUPLED MODAL CALLS -->
    <SecretMessage
      :is-open="showSecretMessage"
      @close="showSecretMessage = false"
    />
    <FlowerPopup :is-open="showFlowerPopup" @close="showFlowerPopup = false" />

    <!-- MONKEY SECRET MODAL -->
    <div
      v-if="showMonkeySecret"
      class="absolute inset-0 z-[101] flex items-center justify-center bg-black/60 backdrop-blur-sm px-4 animate-fade-in"
      @click.self="showMonkeySecret = false"
    >
      <div
        class="bg-white p-6 rounded-3xl shadow-2xl border-2 border-amber-300 max-w-sm w-full text-center animate-bounce-slight flex flex-col items-center"
      >
        <span class="text-5xl text-rose-600/80 mb-4 block animate-bounce-slight"
          >u thought u escaped this? lol</span
        >
        <div
          class="w-full aspect-square rounded-2xl overflow-hidden bg-amber-50 border border-rose-800 mb-4 flex items-center justify-center relative shadow-inner"
        >
          <img
            :src="monkeyImg"
            alt="Secret Monkey"
            class="w-full h-full object-cover"
          />
        </div>
        <span class="text-3xl font-mono block mb-4">🙈 🙉 🙊</span>
        <button
          @click="showMonkeySecret = false"
          class="w-full py-2.5 bg-gradient-to-r from-amber-400 to-orange-500 hover:from-amber-500 hover:to-orange-600 text-white rounded-full font-bold tracking-wide transition-all duration-300 shadow-md active:scale-95"
        >
          Close
        </button>
      </div>
    </div>

    <GhostJumpscare />
    <RealHorroJumpscare />
    <SecretGame />
    <SecretRigged />
  </div>
</template>

<script setup>
import GhostJumpscare from "./GhostJumpscare.vue";
import RealHorroJumpscare from "./RealHorroJumpscare.vue";
import SecretGame2 from "./SecretGame2.vue";
import SecretGame from "./SecretGame.vue";
import SecretRigged from "./SecretRigged.vue";
import FlowerPopup from "./FlowerPopup.vue";
import SecretMessage from "./SecretMessage.vue"; // Newly imported component!
import monkeyImg from "../assets/monkey2.png";
import reachEmoji from "../assets/reachEmoji.png";
import { ref, onMounted } from "vue";

const showSecretMessage = ref(false);
const showMonkeySecret = ref(false);
const showFlowerPopup = ref(false);

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

const emit = defineEmits(["option-selected", "back-to-lock"]);

const selectOption = (choice) => {
  emit("option-selected", choice);
};

const openFlowerPopup = () => {
  showFlowerPopup.value = true;
  emit("option-selected", "flowers");
};

const goBack = () => {
  stopMusicInstance();
  emit("back-to-lock");
};
</script>

<style scoped>
@keyframes slide-up {
  0% {
    transform: translateY(20px);
    opacity: 0;
  }
  100% {
    transform: translateY(0);
  }
}
.animate-slide-up {
  animation: slide-up 0.5s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}
@keyframes fade-in {
  from {
    opacity: 0;
    backdrop-filter: blur(0px);
  }
  to {
    opacity: 1;
    backdrop-filter: blur(4px);
  }
}
.animate-fade-in {
  animation: fade-in 0.4s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}
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
