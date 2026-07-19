<template>
  <div
    class="min-h-screen w-full bg-gradient-to-br from-rose-100 via-pink-200 to-amber-100 text-rose-950 flex flex-col items-center justify-center font-sans p-6 overflow-hidden relative"
  >
    <!-- Back Menu Navigation Button -->
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

    <!-- Secret Message Trigger -->
    <!-- <button
      @click="showSecretMessage = true"
      class="absolute top-2 right-2 z-30 p-2 animate-spin opacity-20 hover:opacity-100 transition-all duration-300 cursor-pointer group hover:scale-125"
      title="?"
    >
      <span class="text-4xl drop-shadow-md inline-block">
        <img :src="reachEmoji" alt="reach" class="w-10 h-auto" />
        🌼
      </span>
    </button> -->

    <!-- Secret Monkey Trigger -->
    <button
      @click="showMonkeySecret = true"
      class="absolute bottom-44 left-6 z-30 p-2 opacity-50 hover:opacity-100 transition-all duration-300 cursor-pointer group hover:scale-125"
      title="🙈"
    >
      <span class="text-4xl drop-shadow-md animate-bounce inline-block"
        >🐔</span
      >
    </button>

    <!-- <SecretAudio ref="audioRef" /> -->

    <!-- BACKGROUND INTERACTIVE ATMOSPHERE LAYERS -->
    <div
      class="absolute inset-0 pointer-events-none overflow-hidden z-0 opacity-80"
    >
      <span class="animate-pulse absolute top-[10%] left-[20%] text-3xl"
        >✨</span
      >
      <span
        class="animate-pulse absolute top-[40%] right-[10%] text-4xl"
        style="animation-delay: 0.5s"
        >🌸</span
      >
    </div>

    <!-- NEW: Dedicated Floating Hearts Module Container -->
    <div class="absolute bottom-[25%] right-[25%] z-20">
      <button
        @click="showLoveMessage = true"
        class="pointer-events-autohover:bg-white/80 backdrop-blur-xs p-3 rounded-full shadow-sm hover:shadow-md hover:scale-125 active:scale-90 transition-all duration-300 group flex items-center justify-center cursor-pointer animate-float-heart"
        title="I Love You"
      >
        <span class="text-3xl filter drop-shadow-sm group-hover:animate-pulse"
          >💖</span
        >
      </button>
    </div>

    <!-- MAIN BOX WRAPPER -->
    <div
      class="w-full max-w-[320px] sm:max-w-md bg-white/85 backdrop-blur-md rounded-3xl border border-white/50 shadow-xl shadow-rose-200/20 p-8 space-y-8 z-10 text-center animate-slide-up"
    >
      <div class="space-y-2">
        <h1
          class="text-3xl sm:text-4xl font-serif font-extrabold italic tracking-tight bg-clip-text text-transparent bg-gradient-to-br from-rose-500 to-pink-500 drop-shadow-sm"
        >
          Let's the fun BEGIN!
        </h1>
        <!-- <p class="text-rose-600/90 font-medium text-sm px-4">
          act like this is a blindbox
        </p> -->
        <p class="text-rose-600/90 font-medium text-sm px-4">
          becareful of what u pick! 😈😈😈
        </p>
      </div>

      <div
        class="flex flex-col gap-4 w-full max-h-[380px] overflow-y-auto pr-1"
      >
        <!-- Button 1: Gift -->
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
            >
              <img :src="pigImg" alt="" class="w-12 h-auto" />
            </span>
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

        <!-- Button 2: Letter -->
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
              ><img :src="pigImg" alt="" class="w-12 h-auto"
            /></span>
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

        <!-- Button 3: Flowers -->
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
              ><img :src="pigImg" alt="" class="w-12 h-auto"
            /></span>
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

        <!-- Button 4: Journey Timeline -->
        <button
          @click="openJourneyModal"
          class="group relative w-full px-6 py-5 bg-white/60 hover:bg-white/90 border-2 border-pink-200/60 hover:border-pink-400/80 rounded-2xl shadow-sm hover:shadow-md hover:shadow-pink-200 transition-all duration-300 flex items-center justify-between overflow-hidden active:scale-[0.98]"
        >
          <div class="flex items-center space-x-4">
            <span
              class="text-3xl group-hover:scale-110 transition-transform duration-300 origin-bottom"
              >❓</span
            >
            <span
              class="text-lg font-bold text-rose-700 tracking-wide font-sans"
              ><img :src="pigImg" alt="" class="w-12 h-auto"
            /></span>
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
    <NewButton />
    <RealHorroJumpscare />

    <!-- UPDATE: DETAILED SURPRISE LOVE NOTE MODAL LAYER -->
    <div
      v-if="showLoveMessage"
      class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/40 backdrop-blur-xs animate-fade-in"
      @click.self="showLoveMessage = false"
    >
      <div
        class="w-full max-w-sm bg-white p-6 pt-10 rounded-3xl border border-rose-100 text-center shadow-2xl transform scale-up-pop space-y-5 relative"
      >
        <!-- 1. TOP RIGHT CLOSE BUTTON (X MARKER) -->
        <button
          @click="showLoveMessage = false"
          class="absolute top-4 right-4 text-rose-300 hover:text-rose-600 font-bold transition-all duration-200 p-1 bg-rose-50 hover:bg-rose-100 rounded-full w-7 h-7 flex items-center justify-center text-sm cursor-pointer shadow-xs active:scale-90"
          title="Close"
        >
          ✕
        </button>

        <div class="text-4xl animate-bounce-slight">💖</div>
        <h2
          class="text-2xl sm:text-base text-rose-950/80 font-medium leading-relaxed px-2"
        >
          Love You chheng! 🥰
        </h2>

        <h2 class="text-2xl font-serif font-black text-rose-600">
          <!-- I Love you 🥰 -->
        </h2>

        <!-- 2. BOTTOM COMPACT ACTION LAYOUT (CONTAINING COMPACT BACK CONTROLS) -->
        <!-- <div class="pt-2 flex items-center justify-center w-full">
          <button
            @click="showLoveMessage = false"
            class="w-full max-w-[140px] px-5 py-2.5 bg-gradient-to-r from-rose-400 to-pink-500 hover:from-rose-500 hover:to-pink-600 text-white font-extrabold text-xs uppercase tracking-widest rounded-xl transition-all shadow-sm hover:shadow active:scale-95 flex items-center justify-center space-x-1 cursor-pointer"
          >
            <span>←</span>
            <span>Back</span>
          </button>
        </div> -->
      </div>
    </div>

    <!-- MODAL POPUP LAYER RENDERS -->
    <SecretMessage
      :is-open="showSecretMessage"
      @close="showSecretMessage = false"
    />
    <OurJourney :is-open="showJourneyModal" @close="showJourneyModal = false" />
    <SecretMonkey
      :is-open="showMonkeySecret"
      :monkey-img="monkeyImg"
      @close="showMonkeySecret = false"
    />

    <!-- Gameplay Modules -->

    <!-- <SecretGame /> -->
    <!-- <SecretRigged /> -->
  </div>
</template>

<script setup>
import { ref } from "vue";
import GhostJumpscare from "./GhostJumpscare.vue";
import RealHorroJumpscare from "./RealHorroJumpscare.vue";
import SecretGame from "./SecretGame.vue";
import SecretRigged from "./SecretRigged.vue";
import OurJourney from "./OurJourney.vue";
import SecretMessage from "./SecretMessage.vue";
import SecretMonkey from "./SecretMonkey.vue";
import SecretAudio from "./SecretAudio.vue";
import monkeyImg from "../assets/monkey2.png";
import reachEmoji from "../assets/reachEmoji.png";
import pigImg from "../assets/pig.png";
import NewButton from "./NewButton.vue";

const showSecretMessage = ref(false);
const showMonkeySecret = ref(false);
const showJourneyModal = ref(false);
const showLoveMessage = ref(false);
const audioRef = ref(null);

const emit = defineEmits(["option-selected", "back-to-lock"]);

const selectOption = (choice) => {
  emit("option-selected", choice);
};

const openJourneyModal = () => {
  showJourneyModal.value = true;
};

const goBack = () => {
  if (audioRef.value) {
    audioRef.value.stopMusicInstance();
  }
  emit("back-to-lock");
};
</script>

<style scoped>
/* Scrollbar cleanup layer for menu boxes stack */
div::-webkit-scrollbar {
  width: 4px;
}
div::-webkit-scrollbar-thumb {
  background: rgba(244, 63, 94, 0.2);
  border-radius: 10px;
}

/* HEART FLOAT FLOATING MOTION ANIMATION KEYFRAMES */
@keyframes floatHeart {
  0%,
  100% {
    transform: translateY(0) scale(1);
  }
  50% {
    transform: translateY(-12px) scale(1.05);
  }
}
.animate-float-heart {
  animation: floatHeart 2.5s ease-in-out infinite;
}

@keyframes scaleUpPop {
  0% {
    transform: scale(0.9) translateY(10px);
    opacity: 0;
  }
  100% {
    transform: scale(1) translateY(0);
    opacity: 1;
  }
}
.scale-up-pop {
  animation: scaleUpPop 0.4s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}

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

```
