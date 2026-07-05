<template>
  <div
    class="min-h-screen w-full bg-gradient-to-br from-rose-100 via-pink-200 to-amber-100 text-rose-950 flex flex-col items-center justify-center font-sans p-6 overflow-hidden relative"
  >
    <!-- BACK BUTTON -->
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

    <!-- HIGHLY VISIBLE INTERACTIVE EMOJI ICON (Moved out of container, top right of screen, 50% opacity, pulse animation) -->
    <button
      @click="showSecretMessage = true"
      class="absolute top-6 right-6 z-30 p-2 opacity-100 hover:opacity-100 transition-all duration-300 cursor-pointer group hover:scale-125"
      title="?"
    >
      <span class="text-2xl drop-shadow-md animate-pulse inline-block">🩷</span>
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

        <button
          @click="selectOption('flowers')"
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

    <div
      v-if="showSecretMessage"
      class="absolute inset-0 z-[100] flex items-center justify-center bg-rose-950/40 backdrop-blur-sm px-4 animate-fade-in"
      @click.self="showSecretMessage = false"
    >
      <div
        class="bg-white/95 p-8 rounded-3xl shadow-2xl border-2 border-pink-300 max-w-sm text-center animate-bounce-slight"
      >
        <span class="text-4xl mb-2 block">shttt!</span>
        <h2
          class="text-3xl font-serif font-bold italic text-rose-500 mb-3 drop-shadow-sm"
        >
          You found the secret message!
        </h2>
        <p class="text-rose-800 font-medium text-lg leading-relaxed text-start">
          I hope you never doubt how lovable you are
        </p>
        <p class="text-rose-800 font-medium text-lg leading-relaxed text-start">
          You are part of my daily routine
        </p>
        <p class="text-rose-800 font-medium text-lg leading-relaxed text-start">
          You have become a habit I never want to break.
        </p>
        <p class="text-rose-800 font-medium text-lg leading-relaxed text-start">
          Your the best part of my day! well most of it 🤣 cuz me mostly upset
          with u and u have no fking clue xD
        </p>
        <p class="text-red-800 font-medium text-2xl leading-relaxed text-start">
          LOVE YOU ✨
        </p>
        <p></p>
        <button
          @click="showSecretMessage = false"
          class="mt-6 px-6 py-2.5 bg-gradient-to-r from-rose-400 to-pink-500 hover:from-rose-500 hover:to-pink-600 text-white rounded-full font-bold tracking-wide transition-all duration-300 shadow-md active:scale-95"
        >
          Close
        </button>
      </div>
    </div>

    <GhostJumpscare />
    <RealHorroJumpscare />
    <SecretGame2 />
    <SecretRigged />
  </div>
</template>

<script setup>
import GhostJumpscare from "./GhostJumpscare.vue";
import RealHorroJumpscare from "./RealHorroJumpscare.vue";
import SecretGame2 from "./SecretGame2.vue";
import SecretRigged from "./SecretRigged.vue";
import { ref } from "vue";

// Secret feature state
const showSecretMessage = ref(false);

const emit = defineEmits(["option-selected", "back-to-lock"]);

const selectOption = (choice) => {
  emit("option-selected", choice);
};
const goBack = () => {
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
    opacity: 1;
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

@keyframes bounce-slight {
  0%,
  100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-8px);
  }
}
.animate-bounce-slight {
  animation: bounce-slight 3s ease-in-out infinite;
}
</style>
