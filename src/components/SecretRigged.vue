Here is the complete, updated Vue component with the new breathing animation
fully integrated. You can copy and paste this directly into your file: ```vue
<template>
  <div
    v-if="!showModal"
    :style="spawnStyle"
    class="fixed flex flex-col items-center group z-20"
  >
    <span
      class="text-[10px] font-bold text-amber-600 bg-white/90 backdrop-blur-sm px-2 py-0.5 rounded-md shadow-md mb-1 animate-wobble pointer-events-none select-none border border-amber-200"
    >
      🎮
    </span>

    <button
      @click="openModal"
      class="w-14 h-14 rounded-full hover:scale-110 active:scale-95 transition-all duration-300 cursor-pointer border-2 border-amber-400 p-1.5 bg-white shadow-lg shadow-amber-400/40 animate-pulse-slow relative flex items-center justify-center"
    >
      <img
        src="https://img.icons8.com/fluent/96/controller.png"
        alt="Game Secret"
        class="w-full h-full object-contain animate-icon-breathe"
      />
    </button>
  </div>

  <div
    v-if="showModal"
    class="fixed inset-0 z-50 bg-rose-950/20 backdrop-blur-md flex items-center justify-center p-4"
  >
    <div
      class="bg-white/95 border border-white max-w-sm w-full rounded-3xl p-6 text-center shadow-2xl space-y-6 scale-up-animation"
    >
      <div
        class="flex justify-between items-center border-b border-rose-100 pb-3"
      >
        <h2 class="text-xl font-serif font-bold text-rose-800">
          Quick Mini-Game
        </h2>
        <button
          @click="closeModal"
          class="text-rose-400 hover:text-rose-700 font-bold text-lg cursor-pointer transition-colors"
        >
          ✕
        </button>
      </div>

      <p class="text-xs text-rose-600/80 font-medium">
        Beat Chicken to win your ultimate prize!
      </p>

      <div
        class="bg-gradient-to-br from-rose-50/50 to-amber-50/50 rounded-2xl p-4 border border-rose-100/60 flex justify-around items-center min-h-[100px]"
      >
        <div class="flex flex-col items-center">
          <span
            class="text-xs uppercase font-bold tracking-wider text-rose-400 mb-1"
            >Chheng</span
          >
          <span class="text-4xl">{{ playerChoiceDisplay || "❓" }}</span>
        </div>

        <div class="text-xl font-serif font-black text-rose-300 italic">VS</div>

        <div class="flex flex-col items-center">
          <span
            class="text-xs uppercase font-bold tracking-wider text-rose-400 mb-1"
            >Chicken</span
          >
          <span class="text-4xl" :class="{ 'animate-bounce': isThinking }">
            {{ aiChoiceDisplay || "❓" }}
          </span>
        </div>
      </div>

      <div
        v-if="resultMessage"
        class="p-3 bg-rose-50 border border-rose-100 rounded-xl transition-all duration-300"
      >
        <p class="text-sm font-extrabold text-rose-700">
          {{ resultMessage }}
        </p>
      </div>

      <div class="space-y-2">
        <p
          class="text-[10px] uppercase font-extrabold tracking-widest text-rose-400"
        >
          Make your selection:
        </p>
        <div class="grid grid-cols-3 gap-3">
          <button
            @click="playGame('rock')"
            :disabled="isThinking"
            class="p-3 bg-white border-2 border-pink-100 rounded-xl hover:border-pink-400 active:scale-95 disabled:opacity-50 disabled:pointer-events-none transition-all text-2xl shadow-sm cursor-pointer"
          >
            ✊
          </button>
          <button
            @click="playGame('paper')"
            :disabled="isThinking"
            class="p-3 bg-white border-2 border-pink-100 rounded-xl hover:border-pink-400 active:scale-95 disabled:opacity-50 disabled:pointer-events-none transition-all text-2xl shadow-sm cursor-pointer"
          >
            🖐️
          </button>
          <button
            @click="playGame('scissors')"
            :disabled="isThinking"
            class="p-3 bg-white border-2 border-pink-100 rounded-xl hover:border-pink-400 active:scale-95 disabled:opacity-50 disabled:pointer-events-none transition-all text-2xl shadow-sm cursor-pointer"
          >
            ✌️
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

const spawnStyle = ref({ top: "70%", left: "75%" });
const showModal = ref(false);
const isThinking = ref(false);
const playerChoiceDisplay = ref("");
const aiChoiceDisplay = ref("");
const resultMessage = ref("");

// Isolated logic to randomize placement anywhere on the viewport safely
const randomizeSpawn = () => {
  const left = Math.floor(Math.random() * 66) + 15;
  let top = Math.floor(Math.random() * 15) + 5;
  if (Math.random() > 0.5) top += 60;
  spawnStyle.value = { top: `${top}%`, left: `${left}%` };
};

onMounted(() => {
  randomizeSpawn();
});

const openModal = () => {
  showModal.value = true;
  playerChoiceDisplay.value = "";
  aiChoiceDisplay.value = "";
  resultMessage.value = "";
};

const closeModal = () => {
  showModal.value = false;
  randomizeSpawn(); // Moves the button to a fresh location on close
};

const playGame = (userChoice) => {
  isThinking.value = true;
  resultMessage.value = "";

  const emojiMap = { rock: "✊", paper: "🖐️", scissors: "✌️" };
  playerChoiceDisplay.value = emojiMap[userChoice];
  aiChoiceDisplay.value = "🔄";

  setTimeout(() => {
    isThinking.value = false;

    // Rigged Logic: AI always counterpicks perfectly to ensure defeat
    if (userChoice === "rock") {
      aiChoiceDisplay.value = emojiMap["paper"];
      resultMessage.value = "Smart move but u lose chheng! 😂 Try again!";
    } else if (userChoice === "paper") {
      aiChoiceDisplay.value = emojiMap["scissors"];
      resultMessage.value = "Chheng still here? Try again! I WIN ☺️";
    } else if (userChoice === "scissors") {
      aiChoiceDisplay.value = emojiMap["rock"];
      resultMessage.value = "Ouch! ចង់ចាក់គេមែន 😭😭😭, I still beat u 😝";
    }
  }, 500);
};
</script>

<style scoped>
/* Snappier scale animation for full container cards */
.scale-up-animation {
  animation: scaleUp 0.3s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
}

@keyframes scaleUp {
  0% {
    transform: scale(0.9);
    opacity: 0;
  }
  100% {
    transform: scale(1);
    opacity: 1;
  }
}

/* Breathing Animation for the Icon */
.animate-icon-breathe {
  animation: iconBreathing 3s ease-in-out infinite;
}

@keyframes iconBreathing {
  0%,
  100% {
    transform: scale(0.85);
    filter: drop-shadow(0px 0px 2px rgba(245, 158, 11, 0.3));
  }
  50% {
    transform: scale(1.15);
    filter: drop-shadow(0px 4px 8px rgba(245, 158, 11, 0.7));
  }
}

/* Outer button pulsing */
.animate-pulse-slow {
  animation: smoothBreathing 2.5s ease-in-out infinite;
}

@keyframes smoothBreathing {
  0%,
  100% {
    transform: scale(1);
    box-shadow: 0 10px 15px -3px rgba(245, 158, 11, 0.3);
  }
  50% {
    transform: scale(1.08);
    box-shadow: 0 20px 25px -5px rgba(245, 158, 11, 0.6);
    border-color: rgba(245, 158, 11, 0.8);
  }
}

/* "Play me!" tooltip wobble */
.animate-wobble {
  animation: sideWobble 2s ease-in-out infinite;
}

@keyframes sideWobble {
  0%,
  100% {
    transform: translateX(0) rotate(0deg);
  }
  25% {
    transform: translateX(-2px) rotate(-3deg);
  }
  75% {
    transform: translateX(2px) rotate(3deg);
  }
}
</style>

```
