<template>
  <div
    v-if="!showModal"
    :style="spawnStyle"
    class="fixed flex flex-col items-center group z-20"
  >
    <span
      class="text-[10px] font-bold text-rose-500 bg-white/90 backdrop-blur-sm px-2 py-0.5 rounded-md shadow-md mb-1 animate-wobble pointer-events-none select-none border border-rose-200"
    >
      ?
    </span>

    <button
      @click="openModal"
      class="w-14 h-14 rounded-full hover:scale-110 active:scale-95 transition-all duration-300 cursor-pointer border-2 border-rose-400 p-1.5 bg-white shadow-lg animate-heart-container relative flex items-center justify-center"
    >
      <img
        src="https://img.icons8.com/fluent/96/hearts.png"
        alt="Love Secret"
        class="w-full h-full object-contain animate-heart-icon"
      />
    </button>
  </div>

  <div
    v-if="showModal"
    class="fixed inset-0 z-50 bg-rose-950/40 backdrop-blur-md flex items-center justify-center p-4"
  >
    <div
      class="bg-white/95 border border-white max-w-xs w-full rounded-3xl p-6 text-center shadow-2xl space-y-6 relative overflow-hidden min-h-[300px] flex flex-col justify-center items-center scale-up-animation"
    >
      <button
        @click="closeModal"
        class="absolute top-4 right-4 text-gray-400 hover:text-rose-500 transition-colors text-lg font-bold cursor-pointer select-none z-50"
      >
        ✕
      </button>

      <div v-if="!prankSuccess" class="space-y-4 w-full">
        <div v-if="currentStep === 1" class="space-y-4 w-full">
          <span class="text-3xl animate-bounce inline-block">GOT YA! 😈</span>
          <h2 class="text-2xl font-serif font-bold text-rose-800">
            Do you like me?
          </h2>
          <p class="text-xs text-rose-600/70">Be completely honest now...</p>

          <div
            class="flex justify-center items-center gap-6 pt-4 min-h-[50px] w-full"
          >
            <button
              @click="prankSuccess = true"
              class="px-6 py-2.5 bg-gradient-to-r from-rose-500 to-pink-500 text-white font-bold rounded-xl shadow-md shadow-pink-300 active:scale-95 transition-transform z-10"
            >
              Yes
            </button>

            <button
              @click="advanceToStepTwo"
              class="px-6 py-2.5 bg-gray-100 border border-gray-200 text-gray-500 font-bold rounded-xl active:scale-95 transition-all shadow-sm"
            >
              No
            </button>
          </div>
        </div>

        <div v-else-if="currentStep === 2" class="space-y-4 w-full">
          <span class="text-3xl animate-bounce inline-block">Really? 🥺</span>
          <h2 class="text-2xl font-serif font-bold text-rose-800 px-2">
            Not even a little bit?
          </h2>
          <p class="text-sm text-rose-600/70">
            Think carefully about this one... 🤭
          </p>

          <div
            class="flex justify-center items-center gap-6 pt-4 min-h-[60px] w-full"
          >
            <button
              @click="prankSuccess = true"
              class="px-6 py-2.5 bg-gradient-to-r from-rose-500 to-pink-500 text-white font-bold rounded-xl shadow-md shadow-pink-300 active:scale-95 transition-transform z-10"
            >
              Yes!
            </button>

            <button
              v-if="!hasMovedYet"
              @mouseenter="teleportNoButton"
              @touchstart.prevent="teleportNoButton"
              class="px-6 py-2.5 bg-gray-100 border border-gray-200 text-gray-500 font-bold rounded-xl shadow-sm select-none"
            >
              No
            </button>
          </div>
        </div>
      </div>

      <div v-else class="space-y-4 py-4 w-full">
        <span class="text-6xl animate-pulse inline-block">🥰🎉</span>
        <h2
          class="text-2xl font-serif font-extrabold text-transparent bg-clip-text bg-gradient-to-r from-rose-600 to-pink-500"
        >
          I Knew It!
        </h2>
        <p class="text-rose-800 text-sm font-medium px-2">
          You love me forever! No returns, no exchanges! ❤️✨
        </p>
        <button
          @click="closeModal"
          class="mt-2 px-5 py-2 bg-rose-100 text-rose-700 text-xs font-bold rounded-full hover:bg-rose-200 transition-colors"
        >
          Close Panel
        </button>
      </div>
    </div>

    <button
      v-if="currentStep === 2 && hasMovedYet && !prankSuccess"
      @mouseenter="teleportNoButton"
      @touchstart.prevent="teleportNoButton"
      @click.prevent="teleportNoButton"
      :style="noButtonStyles"
      class="fixed px-6 py-2.5 bg-gray-100 border border-gray-200 text-gray-500 font-bold rounded-xl transition-all duration-200 ease-out z-50 whitespace-nowrap select-none shadow-xl pointer-events-auto"
    >
      No 🚫
    </button>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from "vue";

const spawnStyle = ref({ top: "20%", left: "15%" });
const showModal = ref(false);
const currentStep = ref(1);
const prankSuccess = ref(false);
const hasMovedYet = ref(false);

const noBtnLeft = ref(0);
const noBtnTop = ref(0);

// Computed positions tied to the root screen viewport frame
const noButtonStyles = computed(() => {
  return {
    left: `${noBtnLeft.value}%`,
    top: `${noBtnTop.value}%`,
    transform: "translate(-50%, -50%)",
  };
});

onMounted(() => {
  randomizeSpawn();
});

const randomizeSpawn = () => {
  let left = Math.floor(Math.random() * 32) + 5;
  let top = Math.floor(Math.random() * 65) + 12;
  if (Math.random() > 0.5) left += 58;
  spawnStyle.value = { top: `${top}%`, left: `${left}%` };
};

const openModal = () => {
  showModal.value = true;
  currentStep.value = 1;
  prankSuccess.value = false;
  hasMovedYet.value = false;
};

const closeModal = () => {
  showModal.value = false;
  randomizeSpawn();
};

const advanceToStepTwo = () => {
  currentStep.value = 2;
  hasMovedYet.value = false;
};

const teleportNoButton = (e) => {
  if (e) {
    e.preventDefault();
    e.stopPropagation();
  }
  hasMovedYet.value = true;

  // Generates randomized target nodes spanning across 5% to 95% of the total screen window width/height
  noBtnLeft.value = Math.floor(Math.random() * 80) + 10;
  noBtnTop.value = Math.floor(Math.random() * 80) + 10;

  // Safety buffer: If it lands directly over the center modal box, push it toward the edges
  if (
    noBtnLeft.value > 35 &&
    noBtnLeft.value < 65 &&
    noBtnTop.value > 30 &&
    noBtnTop.value < 70
  ) {
    noBtnLeft.value = noBtnLeft.value < 50 ? 15 : 85;
    noBtnTop.value = noBtnTop.value < 50 ? 15 : 85;
  }
};
</script>

<style scoped>
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

/* ==========================================================================
       BREATHING & HEARTBEAT ANIMATION ENGINE
       ========================================================================== */
.animate-heart-container {
  animation: containerBreath 3s ease-in-out infinite;
}

@keyframes containerBreath {
  0%,
  100% {
    transform: scale(1);
    box-shadow: 0 4px 14px 0 rgba(244, 63, 94, 0.2),
      0 0 1px 1px rgba(244, 63, 94, 0.1);
    border-color: rgba(244, 63, 94, 0.4);
  }
  50% {
    transform: scale(1.05);
    box-shadow: 0 12px 28px 4px rgba(244, 63, 94, 0.45),
      0 0 10px 4px rgba(251, 113, 133, 0.25);
    border-color: rgba(244, 63, 94, 0.8);
  }
}

.animate-heart-icon {
  animation: heartRate 3s ease-in-out infinite;
}

@keyframes heartRate {
  0%,
  100% {
    transform: scale(1);
  }
  14% {
    transform: scale(1.15);
  }
  28% {
    transform: scale(1.05);
  }
  42% {
    transform: scale(1.22);
  }
  70% {
    transform: scale(1);
  }
}
</style>
