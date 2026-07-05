<template>
  <div
    class="min-h-screen w-full bg-gradient-to-br from-rose-100 via-pink-200 to-amber-100 text-rose-950 flex items-center justify-center font-sans overflow-hidden select-none relative"
  >
    <div
      class="absolute inset-0 pointer-events-none overflow-hidden z-0 opacity-[0.65]"
    >
      <span
        class="animate-background-drift-1 text-2xl absolute top-[8%] left-[12%]"
        >💖</span
      >
      <span
        class="animate-background-drift-2 text-3xl absolute top-[15%] right-[14%]"
        >⭐</span
      >
      <span
        class="animate-background-drift-3 text-xl absolute top-[22%] left-[6%]"
        >✨</span
      >
      <span
        class="animate-background-drift-4 text-2xl absolute top-[28%] right-[8%]"
        >🍬</span
      >
      <span
        class="animate-background-drift-1 text-3xl absolute top-[4%] right-[32%]"
        >🌷</span
      >
      <span
        class="animate-background-drift-3 text-2xl absolute top-[5%] left-[30%]"
        >☁️</span
      >

      <span
        class="animate-background-drift-4 text-4xl absolute top-[45%] left-[4%]"
        >🎀</span
      >
      <span
        class="animate-background-drift-1 text-3xl absolute top-[40%] right-[5%]"
        >🧸</span
      >
      <span
        class="animate-background-drift-2 text-2xl absolute top-[58%] left-[9%]"
        >🌸</span
      >
      <span
        class="animate-background-drift-3 text-4xl absolute top-[62%] right-[7%]"
        >🩰</span
      >
      <span
        class="animate-background-drift-2 text-3xl absolute top-[34%] left-[11%]"
        >🧁</span
      >
      <span
        class="animate-background-drift-4 text-3xl absolute top-[48%] right-[12%]"
        >🦄</span
      >

      <span
        class="animate-background-drift-3 text-2xl absolute bottom-[14%] left-[15%]"
        >💖</span
      >
      <span
        class="animate-background-drift-1 text-xl absolute bottom-[22%] right-[12%]"
        >✨</span
      >
      <span
        class="animate-background-drift-4 text-3xl absolute bottom-[8%] right-[18%]"
        >🌸</span
      >
      <span
        class="animate-background-drift-2 text-2xl absolute bottom-[10%] left-[6%]"
        >⭐</span
      >
      <span
        class="animate-background-drift-3 text-3xl absolute bottom-[4%] left-[35%]"
        >🌼</span
      >
    </div>

    <transition name="popup">
      <div
        v-if="showErrorPopup"
        class="absolute top-10 z-50 bg-gradient-to-r from-rose-500 to-pink-500 backdrop-blur-md text-white px-6 py-3 rounded-full shadow-lg shadow-rose-300/50 border border-white/20 flex items-center space-x-2 animate-bounce"
      >
        <span class="text-lg">💕</span>
        <span class="font-medium tracking-wide text-sm font-sans">{{
          errorMessage
        }}</span>
      </div>
    </transition>

    <transition name="hint-popup">
      <div
        v-if="showHintAfterAttempts"
        class="absolute inset-0 z-50 flex items-center justify-center p-6 bg-rose-950/20 backdrop-blur-md"
      >
        <div
          class="w-full max-w-sm bg-white/90 backdrop-blur-2xl rounded-3xl p-8 text-center shadow-xl shadow-pink-200/50 border border-white/60 space-y-5 animate-slide-up"
        >
          <span class="text-4xl animate-pulse inline-block">💡</span>
          <h3 class="text-2xl font-serif italic text-rose-700 font-medium">
            Here a little hint!
          </h3>
          <p class="text-rose-600/90 text-sm leading-relaxed px-4 font-sans">
            Think of it as someone birthday... something like
            <span
              class="bg-rose-100 px-2 py-0.5 rounded font-mono text-xs font-bold text-rose-600"
              >cancer</span
            >
            as a
            <span
              class="bg-rose-100 px-2 py-0.5 rounded font-mono text-xs font-bold text-rose-600"
              >sign</span
            >
            <div>
                here the hint, but imma be mad at u for not getting it right 🖕🏻
            </div> 💖
          </p>
          <button
            @click="showHintAfterAttempts = false"
            class="w-full py-3 rounded-xl bg-gradient-to-r from-rose-400 to-pink-400 hover:from-rose-500 hover:to-pink-500 text-white text-sm font-semibold tracking-wide shadow-md shadow-rose-200 transition-all active:scale-98"
          >
            OKIE, now try again! 😤✨
          </button>
        </div>
      </div>
    </transition>

    <transition name="fade-slide" mode="out-in">
      <div
        v-if="!isUnlocked"
        key="lockscreen"
        class="w-full max-w-[320px] sm:max-w-sm flex flex-col items-center h-auto justify-center p-5 sm:p-7 z-10 bg-white/85 backdrop-blur-md rounded-3xl border border-white/50 shadow-xl shadow-rose-200/20 space-y-5 mx-4"
      >
        <div class="text-center space-y-1">
          <div class="flex justify-center mb-0.5">
            <span
              class="text-2xl sm:text-3xl animate-wave origin-bottom-right inline-block"
              >👋</span
            >
          </div>
          <h2
            class="text-3xl sm:text-4xl font-serif italic tracking-wide text-transparent bg-clip-text bg-gradient-to-r from-rose-600 via-pink-600 to-rose-500 font-medium drop-shadow-sm"
          >
            Hey Pretty ✨
          </h2>
          <p
            class="text-[10px] sm:text-[11px] text-pink-500/80 tracking-widest uppercase font-bold font-sans"
          >
            Enter Passcode to Unlock
          </p>
        </div>

        <div
          class="flex space-x-5 my-1"
          :class="{ 'animate-shake': isShaking }"
        >
          <div
            v-for="index in 4"
            :key="index"
            class="w-3 h-3 sm:w-3.5 sm:h-3.5 rounded-full border-2 border-pink-300/80 transition-all duration-200"
            :class="{
              'bg-gradient-to-tr from-rose-400 to-pink-400 scale-115 shadow-[0_0_12px_rgba(244,63,94,0.6)] border-rose-300':
                passcode.length >= index,
              'bg-transparent': passcode.length < index,
            }"
          ></div>
        </div>

        <div
          class="grid grid-cols-3 gap-3 w-full max-w-[280px] sm:max-w-[290px]"
        >
          <button
            v-for="num in [1, 2, 3, 4, 5, 6, 7, 8, 9]"
            :key="num"
            @click="pressKey(num.toString())"
            class="w-[76px] sm:w-20 h-14 sm:h-16 rounded-2xl bg-white/70 backdrop-blur-sm border border-white/80 text-xl sm:text-2xl font-serif font-semibold text-rose-700 shadow-[0_4px_10px_rgba(244,63,94,0.03),inset_0_1px_2px_rgba(255,255,255,0.9)] hover:bg-white/90 active:scale-95 transition-all duration-150 flex items-center justify-center mx-auto"
          >
            {{ num }}
          </button>

          <button
            @click="clearPasscode"
            class="w-[76px] sm:w-20 h-14 sm:h-16 rounded-2xl flex items-center justify-center text-[11px] sm:text-xs font-bold tracking-wider uppercase text-rose-400 hover:text-rose-600 active:scale-95 transition-all mx-auto font-sans"
          >
            Clear
          </button>

          <button
            @click="pressKey('0')"
            class="w-[76px] sm:w-20 h-14 sm:h-16 rounded-2xl bg-white/70 backdrop-blur-sm border border-white/80 text-xl sm:text-2xl font-serif font-semibold text-rose-700 shadow-[0_4px_10px_rgba(244,63,94,0.03),inset_0_1px_2px_rgba(255,255,255,0.9)] hover:bg-white/90 active:scale-95 transition-all duration-150 flex items-center justify-center mx-auto"
          >
            0
          </button>

          <button
            @click="deleteLast"
            class="w-[76px] sm:w-20 h-14 sm:h-16 rounded-2xl flex items-center justify-center text-[11px] sm:text-xs font-bold tracking-wider uppercase text-rose-400 hover:text-rose-600 active:scale-95 transition-all mx-auto font-sans"
          >
            Delete
          </button>
        </div>
      </div>

      <div
        v-else
        key="birthday"
        class="w-full max-w-md text-center px-6 py-10 flex flex-col items-center justify-center space-y-6 z-10"
      >
        <div
          class="relative w-24 h-24 flex items-center justify-center bg-white/85 rounded-3xl shadow-md shadow-pink-100 border border-white animate-bounce custom-bounce-delay"
        >
          <span class="text-5xl">🎂</span>
          <span class="absolute -top-2 -right-2 text-2xl animate-pulse"
            >✨</span
          >
        </div>

        <div class="space-y-3">
          <h1
            class="text-5xl font-serif font-extrabold italic tracking-tight bg-clip-text text-transparent bg-gradient-to-br from-rose-500 via-pink-500 to-amber-400 drop-shadow-[0_2px_12px_rgba(244,63,94,0.35)] py-1"
          >
            Happy Birthday! 🎉
          </h1>
          <p
            class="text-base text-rose-800/90 font-sans font-normal max-w-sm mx-auto leading-relaxed px-2"
          >
            You successfully cracked the secret lock! Wishing you a gorgeous day
            filled with sweet moments, magical surprises, and tons of love.
          </p>
        </div>

        <div class="flex items-center space-x-3 py-2 text-pink-300">
          <span
            class="h-px w-16 bg-gradient-to-r from-transparent to-pink-300"
          ></span>
          <span class="text-lg">🌸</span>
          <span
            class="h-px w-16 bg-gradient-to-l from-transparent to-pink-300"
          ></span>
        </div>

        <button
          @click="lockScreenAgain"
          class="px-8 py-3 rounded-xl bg-gradient-to-r from-rose-400 to-pink-500 hover:from-rose-500 hover:to-pink-600 text-white text-sm font-semibold tracking-wide shadow-lg shadow-pink-300/70 transform hover:-translate-y-0.5 active:translate-y-0 transition-all duration-200 font-sans"
        >
          Lock Screen Again 🔒
        </button>
      </div>
    </transition>
  </div>
</template>

<script setup>
import { ref } from "vue";

const CORRECT_PIN = "0101";
const passcode = ref("");
const isUnlocked = ref(false);
const isShaking = ref(false);
const showErrorPopup = ref(false);
const errorMessage = ref(""); // New placeholder for the text
const incorrectAttempts = ref(0);
const showHintAfterAttempts = ref(false);

const pressKey = (num) => {
  if (passcode.value.length < 4) {
    passcode.value += num;
    if (passcode.value.length === 4) {
      verifyPasscode();
    }
  }
};

const deleteLast = () => {
  passcode.value = passcode.value.slice(0, -1);
};

const clearPasscode = () => {
  passcode.value = "";
};

const verifyPasscode = () => {
  if (passcode.value === CORRECT_PIN) {
    setTimeout(() => {
      isUnlocked.value = true;
      incorrectAttempts.value = 0;
      showHintAfterAttempts.value = false;
    }, 200);
  } else {
    isShaking.value = true;
    incorrectAttempts.value++;

    // Update message based on how many times they missed it
    if (incorrectAttempts.value === 1) {
      errorMessage.value = "Huh? Try again! Another code!";
    } else if (incorrectAttempts.value === 2) {
      errorMessage.value =
        "Wow, like WOW! we been talking this long and u didnt get it?";
    } else {
      errorMessage.value = "Alright!";
    }

    showErrorPopup.value = true;

    if (incorrectAttempts.value >= 3) {
      setTimeout(() => {
        showHintAfterAttempts.value = true;
      }, 800);
    }

    setTimeout(() => {
      isShaking.value = false;
      passcode.value = "";
    }, 500);

    setTimeout(() => {
      showErrorPopup.value = false;
    }, 3500);
  }
};

const lockScreenAgain = () => {
  isUnlocked.value = false;
  passcode.value = "";
};
</script>

<style scoped>
@keyframes wave {
  0%,
  100% {
    transform: rotate(0deg);
  }
  25% {
    transform: rotate(-15deg);
  }
  75% {
    transform: rotate(15deg);
  }
}
.animate-wave {
  animation: wave 1.5s ease-in-out infinite;
}

@keyframes shake {
  0%,
  100% {
    transform: translateX(0);
  }
  20%,
  60% {
    transform: translateX(-8px);
  }
  40%,
  80% {
    transform: translateX(8px);
  }
}
.animate-shake {
  animation: shake 0.4s ease-in-out;
}

.custom-bounce-delay {
  animation-duration: 2.2s;
}

@keyframes background-drift-1 {
  0%,
  100% {
    transform: translateY(0px) rotate(0deg);
  }
  50% {
    transform: translateY(-15px) rotate(8deg) scale(1.05);
  }
}
.animate-background-drift-1 {
  animation: background-drift-1 9s ease-in-out infinite;
}

@keyframes background-drift-2 {
  0%,
  100% {
    transform: translateY(0px) rotate(0deg);
  }
  50% {
    transform: translateY(15px) rotate(-8deg) scale(0.95);
  }
}
.animate-background-drift-2 {
  animation: background-drift-2 11s ease-in-out infinite;
}

@keyframes background-drift-3 {
  0%,
  100% {
    transform: translateX(0px);
  }
  50% {
    transform: translateX(10px) rotate(5deg);
  }
}
.animate-background-drift-3 {
  animation: background-drift-3 8s ease-in-out infinite;
}

@keyframes background-drift-4 {
  0%,
  100% {
    transform: translateX(0px) translateY(0px);
  }
  50% {
    transform: translateX(-10px) translateY(-12px) rotate(-6deg);
  }
}
.animate-background-drift-4 {
  animation: background-drift-4 13s ease-in-out infinite;
}

@keyframes slide-up {
  0% {
    transform: translateY(25px);
    opacity: 0;
  }
  100% {
    transform: translateY(0px);
    opacity: 1;
  }
}
.animate-slide-up {
  animation: slide-up 0.4s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
}

.fade-slide-enter-active,
.fade-slide-leave-active {
  transition: all 0.5s cubic-bezier(0.34, 1.56, 0.64, 1);
}
.fade-slide-enter-from {
  opacity: 0;
  transform: scale(0.96) translateY(12px);
}
.fade-slide-leave-to {
  opacity: 0;
  transform: scale(1.04) translateY(-12px);
}

.popup-enter-active {
  transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}
.popup-leave-active {
  transition: all 0.25s ease-in;
}
.popup-enter-from {
  transform: translateY(-40px) scale(0.9);
  opacity: 0;
}
.popup-leave-to {
  transform: translateY(-15px);
  opacity: 0;
}

.hint-popup-enter-active {
  transition: all 0.3s ease-out;
}
.hint-popup-leave-active {
  transition: all 0.2s ease-in;
}
.hint-popup-enter-from {
  opacity: 0;
}
.hint-popup-leave-to {
  opacity: 0;
}
</style>

```
