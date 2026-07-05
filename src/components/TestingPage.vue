<template>
  <div
    class="min-h-screen bg-pink-50 flex items-center justify-center font-sans p-4 antialiased selection:bg-pink-200"
  >
    <!-- LANDING PAGE: PASSCODE LOCK -->
    <transition name="fade-scale" mode="out-in">
      <div
        v-if="!isUnlocked"
        key="lockscreen"
        class="bg-white/80 backdrop-blur-md rounded-3xl shadow-xl shadow-pink-100 p-8 max-w-4xl w-full border border-pink-100/50 grid grid-cols-1 md:grid-cols-2 gap-8 items-center"
      >
        <!-- Left Side: Cute Illustration Box (Referencing Layout from Screenshot 2026-06-09 at 10.19.44 at night.jpg) -->
        <div
          class="flex flex-col items-center justify-center p-4 bg-pink-100/30 rounded-2xl border border-dashed border-pink-200 aspect-square md:aspect-auto md:h-full min-h-[300px] relative overflow-hidden group"
        >
          <!-- Soft background decorative blobs -->
          <div
            class="absolute -top-10 -left-10 w-32 h-32 bg-pink-200/40 rounded-full blur-xl"
          ></div>
          <div
            class="absolute -bottom-10 -right-10 w-32 h-32 bg-pink-300/20 rounded-full blur-xl"
          ></div>

          <!-- Cute Minimal Flower SVG (Nodding to the flower theme in Screenshot 2026-06-09 at 10.19.44 at night.jpg) -->
          <svg
            class="w-32 h-32 text-pink-400 animate-pulse dynamic-heart"
            viewBox="0 0 24 24"
            fill="currentColor"
          >
            <path
              d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"
            />
          </svg>

          <p
            class="text-pink-500 font-medium tracking-wide mt-4 text-sm bg-white/60 px-4 py-1.5 rounded-full shadow-sm"
          >
            Unlock your surprise ✨
          </p>
        </div>

        <!-- Right Side: PIN Entry Screen -->
        <div class="flex flex-col items-center justify-center">
          <!-- 4-Digit Display Slots -->
          <div class="flex gap-3 mb-8" :class="{ 'animate-shake': isWrong }">
            <div
              v-for="(slot, index) in 4"
              :key="index"
              class="w-14 h-14 border-2 rounded-xl flex items-center justify-center text-2xl font-bold transition-all duration-200"
              :class="[
                enteredPin.length > index
                  ? 'border-pink-400 bg-pink-50 text-pink-500 scale-105'
                  : 'border-gray-300 bg-white text-gray-400',
                isWrong ? 'border-red-400 bg-red-50 text-red-500' : '',
              ]"
            >
              <span
                v-if="enteredPin.length > index"
                class="animate-ping-once text-pink-500"
                >🌸</span
              >
            </div>
          </div>

          <!-- Heart-Shaped Keypad Grid -->
          <div
            class="grid grid-cols-3 gap-x-4 gap-y-3 justify-items-center w-full max-w-[280px]"
          >
            <button
              v-for="key in keypadKeys"
              :key="key"
              @click="handleKeyPress(key)"
              class="relative w-16 h-16 flex items-center justify-center font-semibold text-xl active:scale-95 transition-transform duration-100 focus:outline-none group"
            >
              <!-- Heart SVG Background Shapes matching Screenshot 2026-06-09 at 10.19.44 at night.jpg -->
              <svg
                class="absolute inset-0 w-full h-full transition-colors duration-200"
                :class="
                  key === '#'
                    ? 'text-gray-200 group-hover:text-gray-300'
                    : 'text-pink-200 group-hover:text-pink-300/80'
                "
                viewBox="0 0 24 24"
                fill="currentColor"
              >
                <path
                  d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"
                />
              </svg>
              <!-- Key Label Layer -->
              <span
                class="relative z-10 select-none pb-1"
                :class="key === '#' ? 'text-gray-600 text-sm' : 'text-pink-600'"
              >
                {{ key }}
              </span>
            </button>
          </div>
        </div>
      </div>

      <!-- CELEBRATION PAGE: HAPPY BIRTHDAY -->
      <div
        v-else
        key="birthdayscreen"
        class="bg-white/90 backdrop-blur-md rounded-3xl shadow-xl shadow-pink-100 p-10 max-w-md w-full border border-pink-100 text-center relative overflow-hidden"
      >
        <!-- Gentle floating background sparkles -->
        <div class="absolute inset-0 pointer-events-none overflow-hidden">
          <span class="absolute text-xl top-10 left-10 animate-bounce delay-100"
            >✨</span
          >
          <span
            class="absolute text-lg bottom-12 right-12 animate-bounce delay-300"
            >🌸</span
          >
          <span class="absolute text-xl top-1/2 left-8 animate-pulse">💖</span>
        </div>

        <!-- Birthday Content Animated in sequence -->
        <div class="animate-fade-in-up">
          <div
            class="inline-flex items-center justify-center w-24 h-24 bg-pink-100 rounded-full text-5xl mb-6 shadow-inner animate-wiggle"
          >
            🎂
          </div>

          <h1 class="text-3xl font-extrabold text-pink-600 tracking-tight mb-3">
            Happy Birthday! 🎉
          </h1>

          <p class="text-pink-500/90 font-medium mb-6">
            May your day be filled with endless smiles, sweet moments, and all
            the magical things you deserve!
          </p>

          <div class="border-t border-dashed border-pink-200 my-4 pt-4">
            <button
              @click="resetPage"
              class="px-5 py-2 bg-pink-400 text-white font-medium rounded-full text-xs shadow-md shadow-pink-200 hover:bg-pink-500 transition-colors duration-200"
            >
              Lock Page Again 🔒
            </button>
          </div>
        </div>
      </div>
    </transition>
  </div>
</template>

<script setup>
import { ref, watch } from "vue";

const CORRECT_PIN = "0101";
const isUnlocked = ref(false);
const enteredPin = ref("");
const isWrong = ref(false);

// Layout representation derived from the keypad matrix in Screenshot 2026-06-09 at 10.19.44 at night.jpg
const keypadKeys = ["1", "2", "3", "4", "5", "6", "7", "8", "9", "*", "0", "#"];

const handleKeyPress = (key) => {
  if (isWrong.value) return;

  if (key === "#") {
    // Treat '#' as a clean 'Clear/Delete' action
    enteredPin.value = "";
    return;
  }

  if (enteredPin.value.length < 4) {
    enteredPin.value += key;
  }
};

// Watch pin length to auto-evaluate password submission
watch(enteredPin, (newPin) => {
  if (newPin.length === 4) {
    if (newPin === CORRECT_PIN) {
      setTimeout(() => {
        isUnlocked.value = true;
      }, 350);
    } else {
      // Trigger error vibration state
      isWrong.value = true;
      setTimeout(() => {
        enteredPin.value = "";
        isWrong.value = false;
      }, 800);
    }
  }
});

const resetPage = () => {
  enteredPin.value = "";
  isUnlocked.value = false;
};
</script>

<style>
/* Tailored animations keeping the vibe simple and dainty */
@keyframes shake {
  0%,
  100% {
    transform: translateX(0);
  }
  20%,
  60% {
    transform: translateX(-6px);
  }
  40%,
  80% {
    transform: translateX(6px);
  }
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes wiggle {
  0%,
  100% {
    transform: rotate(0deg) scale(1);
  }
  50% {
    transform: rotate(8deg) scale(1.05);
  }
}

.animate-shake {
  animation: shake 0.4s ease-in-out;
}

.animate-fade-in-up {
  animation: fadeInUp 0.6s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}

.animate-wiggle {
  animation: wiggle 2s ease-in-out infinite;
}

.animate-ping-once {
  animation: ping 0.3s cubic-bezier(0, 0, 0.2, 1) 1;
}

/* Page Transition Effects */
.fade-scale-enter-active,
.fade-scale-leave-active {
  transition: all 0.4s cubic-bezier(0.34, 1.56, 0.64, 1);
}

.fade-scale-enter-from {
  opacity: 0;
  transform: scale(0.95);
}

.fade-scale-leave-to {
  opacity: 0;
  transform: scale(1.05);
}
</style>
