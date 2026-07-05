<template>
  <div
    class="min-h-screen bg-gradient-to-b from-[#FAF4F5] via-[#FFFDFB] to-[#F3EFF1] flex items-center justify-center font-sans select-none overflow-hidden relative"
  >
    <div class="absolute inset-0 opacity-30 pointer-events-none">
      <div class="absolute top-12 left-12 text-3xl animate-float-slow">✨</div>
      <div class="absolute top-24 right-16 text-4xl opacity-50">🌸</div>
      <div class="absolute bottom-20 left-16 text-3xl">🌸</div>
      <div
        class="absolute bottom-12 right-12 text-4xl animate-float-slow"
        style="animation-delay: -2s"
      >
        ✨
      </div>
    </div>

    <div
      class="w-full max-w-md px-6 py-8 flex flex-col justify-between min-h-[80vh] relative z-10"
    >
      <transition name="fade-scale" mode="out-in">
        <div
          v-if="!isUnlocked"
          key="lockscreen"
          class="flex-1 flex flex-col items-center justify-center relative"
        >
          <div
            class="flex flex-col items-center text-center mb-8 animate-float"
          >
            <div
              class="relative w-24 h-24 flex items-center justify-center bg-rose-50/60 rounded-3xl border border-rose-100/50 shadow-sm"
            >
              <svg
                viewBox="0 0 24 24"
                class="w-14 h-14"
                fill="none"
                xmlns="http://www.w3.org/2000/svg"
              >
                <path
                  d="M12 2C12.5 3 12 4 11.5 4C11 4 11 3 11.5 2C11.8 1.5 12 1.8 12 2Z"
                  fill="#F59E0B"
                />
                <rect
                  x="11"
                  y="4.5"
                  width="1"
                  height="3.5"
                  rx="0.5"
                  fill="#FBBF24"
                />
                <rect
                  x="6"
                  y="9"
                  width="11"
                  height="4"
                  rx="1.5"
                  fill="#FDA4AF"
                />
                <rect
                  x="4"
                  y="14"
                  width="15"
                  height="6"
                  rx="2"
                  fill="#F43F5E"
                />
                <line
                  x1="3"
                  y1="21"
                  x2="20"
                  y2="21"
                  stroke="#E11D48"
                  stroke-width="1"
                  stroke-linecap="round"
                />
              </svg>
            </div>

            <div class="mt-4 space-y-1">
              <h2 class="text-xl font-medium text-stone-700 tracking-wide">
                A Special Delivery ✨
              </h2>
              <p class="text-sm text-rose-400/90 font-medium">
                For a wonderful friend
              </p>
              <p class="text-xs text-stone-400/80 italic pt-1">
                Enter the 4-digit code to open...
              </p>
            </div>
          </div>

          <div
            class="flex flex-col items-center mb-8"
            :class="{ 'animate-shake': isError }"
          >
            <div class="flex gap-3 mb-2">
              <div
                v-for="(slot, index) in 4"
                :key="index"
                class="w-11 h-11 border border-stone-300 rounded-xl flex items-center justify-center bg-white/80 transition-all duration-200"
                :class="{
                  'border-rose-300 bg-white shadow-[0_0_12px_rgba(244,63,94,0.08)]':
                    passcode[index],
                }"
              >
                <span
                  v-if="passcode[index]"
                  class="text-xl font-semibold text-rose-500 pt-0.5 animate-pop"
                  >*</span
                >
              </div>
            </div>
            <p
              v-if="isError"
              class="text-xs text-rose-500 font-medium animate-pulse"
            >
              Incorrect code, try again
            </p>
            <div v-else class="h-4"></div>
          </div>

          <div
            class="w-full max-w-[260px] grid grid-cols-3 gap-3 justify-items-center"
          >
            <button
              v-for="num in ['1', '2', '3', '4', '5', '6', '7', '8', '9']"
              :key="num"
              @click="handleKeyPress(num)"
              class="w-16 h-14 flex items-center justify-center rounded-xl bg-white/60 border border-stone-200 shadow-sm hover:bg-rose-50/50 active:scale-95 text-lg font-medium text-stone-700 transition-all duration-100 focus:outline-none"
            >
              {{ num }}
            </button>

            <div class="w-16 h-14"></div>

            <button
              @click="handleKeyPress('0')"
              class="w-16 h-14 flex items-center justify-center rounded-xl bg-white/60 border border-stone-200 shadow-sm hover:bg-rose-50/50 active:scale-95 text-lg font-medium text-stone-700 transition-all duration-100 focus:outline-none"
            >
              0
            </button>

            <button
              @click="handleDelete"
              class="w-16 h-14 flex items-center justify-center rounded-xl bg-transparent text-stone-400 hover:text-stone-600 active:scale-90 transition-all duration-100 focus:outline-none"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                fill="none"
                viewBox="0 0 24 24"
                stroke-width="2"
                stroke="currentColor"
                class="w-5 h-5"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  d="M12 9.75L14.25 12m0 0l2.25 2.25M14.25 12l2.25-2.25M14.25 12L12 14.25m-2.58 4.92l-6.375-6.375a1.125 1.125 0 010-1.59L9.42 4.83c.211-.211.498-.33.796-.33H19.5a2.25 2.25 0 012.25 2.25v10.5a2.25 2.25 0 01-2.25 2.25h-9.284c-.298 0-.585-.119-.796-.33z"
                />
              </svg>
            </button>
          </div>

          <transition name="pop-up">
            <div
              v-if="showSuccess"
              class="absolute inset-0 bg-white/95 backdrop-blur-sm rounded-3xl flex flex-col items-center justify-center text-center p-6 z-20 shadow-xl border border-rose-100"
            >
              <div class="text-4xl mb-3 animate-bounce">🎉</div>
              <h3 class="text-xl font-medium text-stone-800 mb-1">
                Correct Code!
              </h3>
              <p class="text-sm text-stone-500 max-w-[200px]">
                Unwrapping your birthday surprise now...
              </p>
              <div
                class="w-24 h-1 bg-stone-100 rounded-full mt-4 overflow-hidden"
              >
                <div
                  class="h-full bg-rose-400 rounded-full animate-progress-bar"
                ></div>
              </div>
            </div>
          </transition>
        </div>

        <div
          v-else
          key="birthday"
          class="flex-1 flex flex-col items-center justify-center text-center px-4 py-12 animate-fade-in"
        >
          <h1
            class="text-2xl md:text-5xl font-serif text-[#A94A53] mb-4 tracking-wide font-medium"
          >
            Happy Birthday! 🎉
          </h1>
          <p
            class="text-stone-600 text-sm md:text-base leading-relaxed max-w-xs mx-auto mb-8 font-light"
          >
            Wishing you a fantastic day ahead filled with laughter, great
            treats, and all your favorite things! Have an amazing celebration!
          </p>

          <div
            class="inline-flex justify-center items-center gap-3 text-3xl animate-bounce"
          >
            🍰 🥳 🎈 🎂
          </div>
        </div>
      </transition>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const CORRECT_CODE = "2207";
const passcode = ref([]);
const isUnlocked = ref(false);
const isError = ref(false);
const showSuccess = ref(false); // State to manage the 2s pop-up message

const handleKeyPress = (num) => {
  if (isError.value || showSuccess.value || passcode.value.length >= 4) return;

  passcode.value.push(num);

  if (passcode.value.length === 4) {
    if (passcode.value.join("") === CORRECT_CODE) {
      // Trigger the intermediate success message
      showSuccess.value = true;

      // Keep message visible for exactly 2000ms (2 seconds) before loading the next page
      setTimeout(() => {
        isUnlocked.value = true;
      }, 1200);
    } else {
      setTimeout(() => {
        isError.value = true;
        setTimeout(() => {
          isError.value = false;
          passcode.value = [];
        }, 600);
      }, 200);
    }
  }
};

const handleDelete = () => {
  if (isError.value || showSuccess.value) return;
  passcode.value.pop();
};
</script>

<style scoped>
/* Shake UI Response on Errors */
@keyframes shake {
  0%,
  100% {
    transform: translateX(0);
  }
  20%,
  60% {
    transform: translateX(-5px);
  }
  40%,
  80% {
    transform: translateX(5px);
  }
}
.animate-shake {
  animation: shake 0.4s ease-in-out;
}

/* Float Animation for Header Layout */
@keyframes float {
  0%,
  100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-6px);
  }
}
.animate-float {
  animation: float 4s ease-in-out infinite;
}
.animate-float-slow {
  animation: float 6s ease-in-out infinite;
}

/* Character Entry Pop Animation */
@keyframes pop {
  0% {
    transform: scale(0.6);
    opacity: 0;
  }
  100% {
    transform: scale(1);
    opacity: 1;
  }
}
.animate-pop {
  animation: pop 0.15s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
}

/* 2-Second Pop-up Message Transitions */
.pop-up-enter-active {
  transition: all 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
}
.pop-up-leave-active {
  transition: all 0.25s ease-in;
}
.pop-up-enter-from {
  opacity: 0;
  transform: scale(0.9);
}
.pop-up-leave-to {
  opacity: 0;
  transform: scale(1.05);
}

/* Progress loader line animation (lasts exactly 2s) */
@keyframes progress {
  from {
    width: 0%;
  }
  to {
    width: 100%;
  }
}
.animate-progress-bar {
  animation: progress 2s linear forwards;
}

/* Screen Cross-fade transitions */
.fade-scale-enter-active,
.fade-scale-leave-active {
  transition: all 0.45s cubic-bezier(0.4, 0, 0.2, 1);
}
.fade-scale-enter-from {
  opacity: 0;
  transform: scale(0.98);
}
.fade-scale-leave-to {
  opacity: 0;
  transform: scale(1.02);
}

/* Content Scene Entrance fade */
@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(8px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
.animate-fade-in {
  animation: fadeIn 0.5s ease-out forwards;
}
</style>
