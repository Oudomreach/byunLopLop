<template>
  <div class="flex flex-col items-center justify-center p-4">
    <button
      @click="triggerJumpscare"
      class="px-8 py-4 bg-gradient-to-r from-amber-400 to-orange-500 hover:from-amber-500 hover:to-orange-600 text-white font-extrabold text-lg rounded-2xl shadow-lg transform hover:scale-105 active:scale-95 transition-all duration-200 cursor-pointer border border-amber-300 tracking-wide"
    >
      Click here to see more!
    </button>

    <div
      v-if="isScared"
      class="fixed inset-0 z-[999] bg-black flex flex-col items-center justify-center overflow-hidden select-none pointer-events-none animate-screamer-flash"
    >
      <div
        class="w-full h-full flex flex-col items-center justify-center animate-screamer-shake"
      >
        <div
          class="w-4/5 max-w-lg h-auto text-white filter drop-shadow-[0_0_50px_rgba(255,255,255,0.8)] animate-ghost-lunges"
        >
          <svg viewBox="0 0 24 24" fill="currentColor" class="w-full h-full">
            <path
              d="M12 2A10 10 0 0 0 2 12v9a1 1 0 0 0 1.7.7l2.3-2.3 2.3 2.3a1 1 0 0 0 1.4 0l2.3-2.3 2.3 2.3a1 1 0 0 0 1.4 0l2.3-2.3 2.3 2.3a1 1 0 0 0 1.7-.7v-9A10 10 0 0 0 12 2zm-3 9a1.5 1.5 0 1 1 1.5-1.5A1.5 1.5 0 0 1 9 11zm6 0a1.5 1.5 0 1 1 1.5-1.5A1.5 1.5 0 0 1 15 11zm-5.2 4a3.5 3.5 0 0 1 4.4 0 1 1 0 1 1-1.2 1.6 1.5 1.5 0 0 0-2 0 1 1 0 1 1-1.2-1.6z"
            />
          </svg>
        </div>

        <h1
          class="text-6xl md:text-8xl font-black text-red-600 tracking-tighter mt-4 uppercase font-mono animate-text-grow"
        >
          BOO!
        </h1>
      </div>
    </div>

    <audio ref="scareAudio" preload="auto">
      <source
        src="https://assets.mixkit.co/active_storage/sfx/947/947-84.wav"
        type="audio/wav"
      />
    </audio>
  </div>
</template>

<script setup>
import { ref } from "vue";

const isScared = ref(false);
const scareAudio = ref(null);

const triggerJumpscare = () => {
  // 1. Immediately activate full screen overlay graphics
  isScared.value = true;

  // 2. Max out sound volume and blast it instantly
  if (scareAudio.value) {
    scareAudio.value.volume = 1.0;
    scareAudio.value.currentTime = 0; // Rewind to start if clicked repeatedly
    scareAudio.value.play().catch((err) => {
      console.warn("Audio play blocked or failed:", err);
    });
  }

  // 3. Automatically shut down overlay canvas after 1.5 seconds
  setTimeout(() => {
    isScared.value = false;
  }, 1500);
};
</script>

<style scoped>
/* 1. Strobe Flashing Backdrop (Alternates pitch black and dark blood red) */
.animate-screamer-flash {
  animation: strobeEffect 0.1s infinite alternate;
}

@keyframes strobeEffect {
  0% {
    background-color: #000000;
  }
  100% {
    background-color: #200000;
  }
}

/* 2. Violent Screen Shake Layout */
.animate-screamer-shake {
  animation: violentQuake 0.15s infinite linear;
}

@keyframes violentQuake {
  0% {
    transform: translate(0, 0) rotate(0deg);
  }
  20% {
    transform: translate(-8px, 5px) rotate(-1deg);
  }
  40% {
    transform: translate(-3px, -7px) rotate(1deg);
  }
  60% {
    transform: translate(6px, 3px) rotate(0deg);
  }
  80% {
    transform: translate(4px, -5px) rotate(-1deg);
  }
  100% {
    transform: translate(-5px, 4px) rotate(1deg);
  }
}

/* 3. Violent Ghost Lunge (Flies straight from zero right into your face) */
.animate-ghost-lunges {
  animation: lungeIn 0.25s cubic-bezier(0.25, 1, 0.5, 1) forwards;
}

@keyframes lungeIn {
  0% {
    transform: scale(0.1) rotate(-15deg);
    opacity: 0;
  }
  50% {
    opacity: 1;
  }
  100% {
    transform: scale(1.4) rotate(0deg);
    opacity: 1;
  }
}

/* 4. Text expansion slam */
.animate-text-grow {
  animation: slamText 0.2s ease-out forwards;
}

@keyframes slamText {
  0% {
    transform: scale(0.3);
    opacity: 0;
  }
  100% {
    transform: scale(1);
    opacity: 1;
  }
}
</style>
