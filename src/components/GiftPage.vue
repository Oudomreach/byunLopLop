<template>
  <div
    class="min-h-screen w-full bg-gradient-to-br from-rose-100 via-pink-200 to-amber-100 text-rose-950 flex flex-col items-center justify-center font-sans p-6 relative select-none"
  >
    <!-- MATCHED BACK BUTTON: Emits your exact parent routing hook -->
    <button
      @click="$emit('back')"
      class="absolute top-6 left-6 text-rose-600/80 hover:text-rose-900 transition-all duration-300 flex items-center space-x-2 text-xs font-extrabold tracking-widest uppercase z-30 bg-white/70 backdrop-blur-md px-4 py-2.5 rounded-full border border-white/60 shadow-sm active:scale-95"
    >
      <span>←</span>
      <span>Back</span>
    </button>

    <!-- MAIN COMPACT CARD CONTAINER -->
    <div
      class="w-full max-w-[340px] bg-white/85 backdrop-blur-md rounded-3xl border border-white/50 shadow-xl p-6 space-y-6 text-center animate-slide-up"
    >
      <!-- Dynamic Title Block -->
      <div class="space-y-1">
        <h1 class="text-2xl font-serif font-black text-rose-900">?</h1>
        <p class="text-xs text-rose-600/90 font-medium">
          {{
            isRevealed
              ? "System Override Activated!"
              : "Spin the wheel to win your birthday present!"
          }}
        </p>
      </div>

      <!-- GAME PLAYING LAYOUT (THE ROULETTE WINDOW) -->
      <div v-if="!isRevealed" class="space-y-5 w-full">
        <!-- Digital Display Box -->
        <div
          class="w-full py-6 px-4 bg-gradient-to-tr from-rose-50 to-pink-50 border border-rose-200/60 rounded-2xl flex flex-col items-center justify-center min-h-[90px]"
        >
          <span class="text-3xl mb-1 select-none animate-bounce-slight">{{
            currentDisplayIcon
          }}</span>
          <p
            class="text-sm font-black tracking-wide text-rose-900 font-mono uppercase"
          >
            {{ currentDisplayText }}
          </p>
        </div>

        <!-- Spin Dynamic Trigger Action Button -->
        <button
          @click="startRiggedSpin"
          :disabled="isSpinning"
          :class="[
            'w-full py-4 rounded-xl font-sans text-xs font-black tracking-widest uppercase transition-all duration-200 shadow-md border',
            isSpinning
              ? 'bg-rose-100 border-rose-200 text-rose-400 cursor-not-allowed'
              : 'bg-rose-600 hover:bg-rose-700 text-white active:scale-98',
          ]"
        >
          {{ isSpinning ? "🎰 Spinning Matrix..." : "🎯 Spin For Present" }}
        </button>
      </div>

      <!-- FINAL REVEAL LAYOUT: AUTOMATIC PIVOT REWARD -->
      <div v-else class="space-y-5 animate-fade-in">
        <div class="text-5xl animate-bounce">🛵🍔✈️</div>

        <div class="space-y-2 px-1">
          <h2 class="text-xl font-black font-serif text-rose-900">
            The Synchronized Midnight Feast!
          </h2>
          <p class="text-xs text-rose-800/90 font-medium leading-relaxed">
            The wheel was rigged! I would never give you a bad gift. You choose
            exactly what you want to eat right now. I will order it directly to
            your door via a delivery app, order something for myself, and we
            have a synced video-call birthday dinner date!
          </p>
        </div>

        <button
          @click="isClaimed = true"
          :disabled="isClaimed"
          :class="[
            'w-full py-3.5 rounded-xl font-sans text-xs font-black tracking-widest uppercase transition-all duration-300 shadow-md border',
            isClaimed
              ? 'bg-emerald-500 border-emerald-600 text-white cursor-not-allowed animate-pulse'
              : 'bg-gradient-to-r from-rose-500 to-pink-500 text-white hover:opacity-90 active:scale-98',
          ]"
        >
          {{ isClaimed ? "📡 Invitation Sent to Him!" : "💖 Lock in the Date" }}
        </button>

        <p
          v-if="isClaimed"
          class="text-[10px] font-bold text-emerald-600 font-mono animate-fade-in"
        >
          Next Step: Tell me on chat what you want to eat! 😉
        </p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

// Explicitly match the event name defined in your project architecture setup
defineEmits(["back-to-lock"]);

const isSpinning = ref(false);
const isRevealed = ref(false);
const isClaimed = ref(false);

const currentDisplayText = ref("Ready to Roll...");
const currentDisplayIcon = ref("🎰");

// Mock list of completely terrible joke items it bounces through rapidly
const jokePool = [
  { text: "A Dirty Old Sock", icon: "🧦" },
  { text: "One Single Potato", icon: "🥔" },
  { text: "Nothing (Better luck next year)", icon: "💨" },
  { text: "A Wet Napkin", icon: "🧻" },
  { text: "A Broken Rubber Band", icon: "🪡" },
];

const startRiggedSpin = () => {
  if (isSpinning.value) return;
  isSpinning.value = true;

  let ticks = 0;
  const totalTicks = 12; // Controls duration of rapid shuffling

  const interval = setInterval(() => {
    // Pick a random joke from the pool to flash across the display box window frame
    const randomJoke = jokePool[Math.floor(Math.random() * jokePool.length)];
    currentDisplayText.value = randomJoke.text;
    currentDisplayIcon.value = randomJoke.icon;

    ticks++;

    if (ticks >= totalTicks) {
      clearInterval(interval);

      // Forces a 1-second pause on the "terrible" landing item so she can digest it
      setTimeout(() => {
        // Swap states immediately into the premium real gift panel reveal
        isRevealed.value = true;
        isSpinning.value = false;
      }, 3000);
    }
  }, 120); // Shuffle speed
};
</script>

<style scoped>
@keyframes slide-up {
  0% {
    transform: translateY(15px);
    opacity: 0;
  }
  100% {
    transform: translateY(0);
    opacity: 1;
  }
}
.animate-slide-up {
  animation: slide-up 0.4s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}

@keyframes fade-in {
  from {
    opacity: 0;
    transform: scale(0.97);
  }
  to {
    opacity: 1;
    transform: scale(1);
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
    transform: translateY(-4px);
  }
}
.animate-bounce-slight {
  animation: bounce-slight 2s ease-in-out infinite;
}
</style>
