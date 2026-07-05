<template>
  <div
    class="min-h-screen w-full bg-gradient-to-br from-rose-100 via-pink-200 to-amber-100 text-rose-950 flex items-center justify-center font-sans overflow-hidden select-none relative"
  >
    <button
      v-if="currentScreen !== 'lock'"
      @click="handleBack"
      class="absolute top-6 left-6 text-rose-600/80 hover:text-rose-900 transition-all duration-200 flex items-center space-x-1.5 text-xs font-bold tracking-widest uppercase font-sans z-40 bg-white/60 backdrop-blur-md px-3.5 py-2 rounded-full border border-white/60 shadow-sm active:scale-95"
    >
      <span>←</span>
      <span>{{ backLabel }}</span>
    </button>

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

    <transition name="fullscreen-popup">
      <div
        v-if="showSuccessPopup"
        class="fixed inset-0 z-50 w-screen h-screen bg-rose-950/40 backdrop-blur-lg flex flex-col items-center justify-center p-6 text-center select-none"
      >
        <div
          class="w-[calc(100%-2rem)] max-w-sm bg-white/90 backdrop-blur-2xl rounded-3xl p-8 shadow-2xl shadow-rose-900/30 border border-white/60 flex flex-col items-center space-y-6 animate-scale-up"
        >
          <div
            class="w-56 h-56 sm:w-64 sm:h-64 bg-rose-50 rounded-2xl overflow-hidden flex items-center justify-center border-2 border-rose-200/60 shadow-md relative"
          >
            <img
              :src="surpriseFace"
              alt="Success Monkey"
              class="w-full h-full object-cover"
            />
          </div>
          <div class="space-y-1.5 w-full">
            <h4
              class="font-serif italic font-extrabold text-transparent bg-clip-text bg-gradient-to-r from-rose-600 via-pink-600 to-amber-500 text-2xl sm:text-3xl tracking-wide drop-shadow-sm"
            >
              Unlocked! ✨
            </h4>
            <p
              class="text-rose-700/90 font-sans text-sm sm:text-base font-bold tracking-wide"
            >
              Danggg! You cracked it! 🫪🫪🫪
            </p>
          </div>
          <div class="flex space-x-2 text-xl tracking-wider animate-bounce">
            <span>🎉</span><span>🥳</span><span>🎈</span>
          </div>
        </div>
      </div>
    </transition>

    <transition name="popup">
      <div
        v-if="showErrorPopup"
        class="absolute top-24 z-50 bg-gradient-to-r from-rose-500 to-pink-500 backdrop-blur-md text-white px-6 py-3 rounded-full shadow-lg shadow-rose-300/50 border border-white/20 flex items-center space-x-2 animate-bounce"
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
          <div
            class="text-rose-600/90 text-sm leading-relaxed px-4 font-sans space-y-2"
          >
            <p>
              Think of it as someone's birthday... something like
              <span
                class="bg-rose-100 px-2 py-0.5 rounded font-mono text-xs font-bold text-rose-600"
                >cancer</span
              >
              as a sign but with a
              <span
                class="bg-rose-100 px-2 py-0.5 rounded font-mono text-xs font-bold text-rose-600"
                >date</span
              >
            </p>
            <p class="mt-2 text-xs text-rose-500/90 italic">
              but i still mad at u for not getting it right the first time 🖕🏻 💖
            </p>
          </div>
          <button
            @click="showHintAfterAttempts = false"
            class="w-full py-3 rounded-xl bg-gradient-to-r from-rose-400 to-pink-400 hover:from-rose-500 hover:to-pink-500 text-white text-sm font-semibold tracking-wide shadow-md shadow-rose-200 transition-all active:scale-98"
          >
            OKIE, now try again! 😤
          </button>
        </div>
      </div>
    </transition>

    <transition name="fade-slide" mode="out-in">
      <div
        v-if="currentScreen === 'lock'"
        key="lockscreen"
        class="w-[calc(100%-2rem)] max-w-[340px] flex flex-col items-center h-auto justify-center p-6 pt-8 z-10 bg-white/85 backdrop-blur-md rounded-3xl border border-white/50 shadow-xl shadow-rose-200/20 space-y-5 mx-4"
      >
        <div class="text-center space-y-1">
          <div class="flex justify-center mb-0.5">
            <span
              class="text-2xl sm:text-3xl animate-none origin-bottom-right inline-block"
            >
              <img
                :src="pigFire"
                alt=""
                class="w-22 h-22 object-cover rounded-2xl"
              />
            </span>
          </div>
          <h2
            class="text-3xl sm:text-4xl font-serif italic tracking-wide text-transparent bg-clip-text bg-gradient-to-r from-rose-600 via-pink-600 to-rose-500 font-medium drop-shadow-sm"
          >
            Security Check
            <span>Who's this?</span>
          </h2>
          <p
            class="text-[10px] sm:text-[11px] text-pink-500/80 tracking-widest uppercase font-bold font-sans"
          >
            Enter the Lock!
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
              'bg-gradient-to-tr from-rose-400 to-pink-400 scale-[1.15] shadow-[0_0_12px_rgba(244,63,94,0.6)] border-rose-300':
                passcode.length >= index,
              'bg-transparent': passcode.length < index,
            }"
          ></div>
        </div>

        <div class="grid grid-cols-3 gap-2.5 w-full">
          <button
            v-for="num in [1, 2, 3, 4, 5, 6, 7, 8, 9]"
            :key="num"
            @click="pressKey(num.toString())"
            class="w-full aspect-[4/3] max-h-14 rounded-2xl bg-white/70 backdrop-blur-sm border border-white/80 text-xl sm:text-2xl font-serif font-semibold text-rose-700 shadow-[0_4px_10px_rgba(244,63,94,0.03),inset_0_1px_2px_rgba(255,255,255,0.9)] hover:bg-white/90 active:scale-95 transition-all duration-150 flex items-center justify-center"
          >
            {{ num }}
          </button>
          <button
            @click="clearPasscode"
            class="w-full aspect-[4/3] max-h-14 rounded-2xl flex items-center justify-center text-[11px] font-bold tracking-wider uppercase text-rose-400 hover:text-rose-600 active:scale-95 transition-all font-sans"
          >
            Clear
          </button>
          <button
            @click="pressKey('0')"
            class="w-full aspect-[4/3] max-h-14 rounded-2xl bg-white/70 backdrop-blur-sm border border-white/80 text-xl sm:text-2xl font-serif font-semibold text-rose-700 shadow-[0_4px_10px_rgba(244,63,94,0.03),inset_0_1px_2px_rgba(255,255,255,0.9)] hover:bg-white/90 active:scale-95 transition-all duration-150 flex items-center justify-center"
          >
            0
          </button>
          <button
            @click="deleteLast"
            class="w-full aspect-[4/3] max-h-14 rounded-2xl flex items-center justify-center text-[11px] font-bold tracking-wider uppercase text-rose-400 hover:text-rose-600 active:scale-95 transition-all font-sans"
          >
            Del
          </button>
        </div>
      </div>

      <div
        v-else-if="currentScreen === 'date'"
        key="datescreen"
        class="w-[calc(100%-2rem)] max-w-sm text-center p-6 sm:p-8 pt-8 z-10 bg-white/85 backdrop-blur-md rounded-3xl border border-white/50 shadow-xl shadow-rose-200/20 flex flex-col items-center justify-center space-y-6 mx-4"
      >
        <div
          class="relative w-32 h-32 sm:w-36 sm:h-36 flex items-center justify-center bg-white/95 rounded-3xl shadow-md shadow-pink-100/60 border border-rose-200/60 overflow-hidden animate-bounce custom-bounce-delay"
        >
          <img
            :src="bunnyDance"
            alt="Special Date"
            class="w-full h-full object-cover"
          />
          <span class="absolute -top-1 -right-1 text-2xl animate-pulse z-10"
            >✨</span
          >
        </div>
        <div class="space-y-3 w-full">
          <h1
            class="text-3xl sm:text-4xl md:text-5xl font-serif font-extrabold italic tracking-tight bg-clip-text text-transparent bg-gradient-to-br from-pink-500 via-rose-500 to-amber-400 drop-shadow-[0_2px_12px_rgba(244,63,94,0.35)] py-1"
          >
            22/July/2026
          </h1>
          <p
            class="text-sm sm:text-base text-rose-800/90 font-sans font-medium max-w-sm mx-auto leading-relaxed px-2 tracking-wide"
          >
            Happy another lap around the sun :P
          </p>
        </div>
        <div class="flex items-center space-x-3 py-1 text-pink-300">
          <span
            class="h-px w-12 bg-gradient-to-r from-transparent to-pink-300"
          ></span>
          <span class="text-lg animate-spin duration-[3000ms]">🌸</span>
          <span
            class="h-px w-12 bg-gradient-to-l from-transparent to-pink-300"
          ></span>
        </div>
      </div>

      <div
        v-else-if="currentScreen === 'birthday'"
        key="birthday"
        class="w-[calc(100%-2rem)] max-w-sm text-center p-6 sm:p-8 pt-8 z-10 bg-white/85 backdrop-blur-md rounded-3xl border border-white/50 shadow-xl shadow-rose-200/20 flex flex-col items-center justify-center space-y-5 sm:space-y-6 mx-4"
      >
        <div class="relative">
          <span
            class="absolute -top-4 -left-4 text-3xl z-20 animate-flower-sway drop-shadow-sm inline-block"
            >🌷</span
          >
          <span
            class="absolute -top-4 -right-4 text-3xl z-20 animate-flower-float drop-shadow-sm inline-block"
            >🌼</span
          >
          <span
            class="absolute -bottom-3 -left-3 text-2xl z-20 animate-flower-sway-delayed drop-shadow-sm inline-block"
            >🌼</span
          >
          <span
            class="absolute -bottom-3 -right-3 text-3xl z-20 animate-flower-float-delayed drop-shadow-sm inline-block"
            >🌷</span
          >

          <div
            class="relative w-32 h-32 sm:w-36 sm:h-36 flex items-center justify-center bg-white/95 rounded-3xl shadow-md shadow-pink-100/60 border border-rose-200/70 overflow-hidden animate-img-float z-10"
          >
            <img
              :src="uuuImg"
              alt="Birthday Special"
              class="w-full h-full object-cover"
            />
            <span class="absolute -top-1 -right-1 text-2xl animate-pulse z-10"
              >✨</span
            >
          </div>
        </div>

        <div class="space-y-3 w-full">
          <h1
            class="text-3xl sm:text-4xl font-serif font-extrabold italic tracking-tight bg-clip-text text-transparent bg-gradient-to-br from-rose-500 via-pink-500 to-amber-500 drop-shadow-[0_2px_12px_rgba(244,63,94,0.35)] py-1 leading-tight"
          >
            Happy Birthday, Chheng!
          </h1>
          <p
            class="text-xs sm:text-sm text-rose-800/90 font-sans font-semibold max-w-xs sm:max-w-sm mx-auto leading-relaxed px-2"
          >
            To the absolute most wonderful person who brings so much light and
            joy into my life. May your special day be overflowing with pure
            love, magic, endless happy smiles, and all the love you completely
            deserve! 💖✨
          </p>
        </div>

        <div class="flex items-center space-x-3 py-1 text-pink-300">
          <span
            class="h-px w-12 bg-gradient-to-r from-transparent to-pink-300"
          ></span>
          <img :src="pigIcon" alt="Pig Icon" class="h-5 w-5 object-contain" />
          <span
            class="h-px w-12 bg-gradient-to-l from-transparent to-pink-300"
          ></span>
        </div>

        <button
          @click="handleNextScreen"
          class="w-full py-3 rounded-xl bg-gradient-to-r from-rose-400 to-pink-500 hover:from-rose-500 hover:to-pink-600 text-white text-xs sm:text-sm font-bold tracking-widest uppercase shadow-lg shadow-pink-300/70 transform hover:-translate-y-0.5 active:translate-y-0 transition-all duration-200 font-sans flex items-center justify-center space-x-2"
        >
          <span>Next</span>
          <span class="text-lg">✨</span>
        </button>
      </div>

      <div
        v-else-if="currentScreen === 'birthday-message'"
        key="birthdaymessage"
        class="w-[calc(100%-2rem)] max-w-sm text-center p-6 sm:p-8 pt-8 z-10 bg-white/85 backdrop-blur-md rounded-3xl border border-white/50 shadow-xl shadow-rose-200/20 flex flex-col items-center justify-center space-y-6 mx-4"
      >
        <div class="space-y-4 w-full">
          <h2
            class="flex justify-around items-center text-2xl sm:text-3xl font-serif font-extrabold italic tracking-tight bg-clip-text text-transparent bg-gradient-to-br from-rose-500 via-pink-500 to-amber-500 py-1 leading-tight"
          >
            One more thing
            <img :src="pigBIU" alt="Pig" class="w-20 h-auto" />
          </h2>

          <div
            class="bg-white/60 p-5 rounded-2xl border border-pink-100 shadow-inner space-y-4 relative"
          >
            <span class="absolute -top-3 -right-3 text-2xl animate-bounce"
              >💌</span
            >
            <p
              class="text-xs sm:text-sm text-rose-800/90 font-sans font-medium leading-relaxed"
            >
              Thanks you for being you! I hope this year brings you closer to
              your dreams and fills your heart with endless happiness. You're
              truly one of a kind and I am so grateful for you! 💖
            </p>
            <p
              class="text-xs sm:text-sm text-rose-800/90 font-sans font-medium leading-relaxed"
            >
              Thanks you for putting up with this person
            </p>
            <p
              class="text-xs sm:text-sm text-rose-800/90 font-sans font-medium leading-relaxed"
            >
              Enjoy every single second of your day! Eat lots of cake! 🎂 and
            </p>
            <p
              class="text-xs sm:text-sm text-rose-800/90 font-sans font-medium leading-relaxed"
            >
              HAPPY BIRTHDAY!
            </p>
          </div>
        </div>

        <div class="flex items-center space-x-3 py-1 text-pink-300">
          <span
            class="h-px w-12 bg-gradient-to-r from-transparent to-pink-300"
          ></span>
          <span class="text-lg animate-pulse">kimmy</span>
          <span
            class="h-px w-12 bg-gradient-to-l from-transparent to-pink-300"
          ></span>
        </div>

        <button
          @click="emitMenuEvent"
          class="w-full py-3 rounded-xl bg-gradient-to-r from-rose-400 to-pink-500 hover:from-rose-500 hover:to-pink-600 text-white text-xs sm:text-sm font-bold tracking-widest uppercase shadow-lg shadow-pink-300/70 transform hover:-translate-y-0.5 active:translate-y-0 transition-all duration-200 font-sans flex items-center justify-center space-x-2"
        >
          <span>To Menu</span>
          <span class="text-lg">🐷</span>
        </button>
      </div>
    </transition>
  </div>
</template>

<script setup>
import { ref, computed, onUnmounted, onMounted } from "vue";
import monkeyImg from "../assets/monkey2.png";
import uuuImg from "../assets/uuu.jpg";
import pigIcon from "../assets/pig.png";
import bunnyDance from "../assets/bunnyDance2.gif";
import surpriseFace from "../assets/surprise.png";
import angryPig from "../assets/angryPig.gif";
import pigBIU from "../assets/pigBIU.gif";
import pigFire from "../assets/pigFire.gif";

const emit = defineEmits(["go-to-menu"]);

const CORRECT_PIN = "0000";
const passcode = ref("");
const currentScreen = ref("lock");
const isShaking = ref(false);
const showErrorPopup = ref(false);
const showSuccessPopup = ref(false);
const errorMessage = ref("");
const incorrectAttempts = ref(0);
const showHintAfterAttempts = ref(false);

// 1. INITIALIZE THE HISTORY STACK HERE
const history = ref([]);

let screenTimeout = null;

// Dynamic label context based on what is currently the last item in our history stack
const backLabel = computed(() => {
  if (history.value.length === 0) return "";
  const previousScreen = history.value[history.value.length - 1];
  if (previousScreen === "lock") return "Lock";
  if (previousScreen === "date") return "Date";
  if (previousScreen === "birthday") return "Birthday";
  return "Back";
});

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
    showSuccessPopup.value = true;

    setTimeout(() => {
      showSuccessPopup.value = false;

      // 2. UPDATE HERE: Save 'lock' to history before moving to 'date'
      history.value.push(currentScreen.value);
      currentScreen.value = "date";

      incorrectAttempts.value = 0;
      showHintAfterAttempts.value = false;

      screenTimeout = setTimeout(() => {
        // 3. UPDATE HERE: Save 'date' to history before auto-moving to 'birthday'
        history.value.push(currentScreen.value);
        currentScreen.value = "birthday";
      }, 1000);
    }, 1000);
  } else {
    isShaking.value = true;
    incorrectAttempts.value++;
    if (incorrectAttempts.value === 1)
      errorMessage.value = "Huh? Try again! Another code!";
    else if (incorrectAttempts.value === 2)
      errorMessage.value =
        "Wow, like WOW! we been talking this long and u didnt get it?";
    else errorMessage.value = "Alright!";

    showErrorPopup.value = true;
    if (incorrectAttempts.value >= 3) {
      setTimeout(() => {
        showHintAfterAttempts.value = true;
      }, 1000);
    }
    setTimeout(() => {
      isShaking.value = false;
      passcode.value = "";
    }, 2000);
    setTimeout(() => {
      showErrorPopup.value = false;
    }, 1000);
  }
};

// 4. UPDATE HERE: Clean rewrite of handleBack using the history stack
const handleBack = () => {
  if (screenTimeout) clearTimeout(screenTimeout);

  if (history.value.length > 0) {
    // Extract the last screen we visited and go back to it
    currentScreen.value = history.value.pop();

    // Context cleanup fixes:
    if (currentScreen.value === "lock") {
      passcode.value = "";
    } else if (currentScreen.value === "date") {
      // Re-trigger the automatic 5-second redirect if they went back to the date screen
      screenTimeout = setTimeout(() => {
        history.value.push(currentScreen.value);
        currentScreen.value = "birthday";
      }, 1000);
    }
  }
};

const handleNextScreen = () => {
  // 5. UPDATE HERE: Save 'birthday' to history before moving to message card
  history.value.push(currentScreen.value);
  currentScreen.value = "birthday-message";
};

const emitMenuEvent = () => {
  emit("go-to-menu");
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

.fullscreen-popup-enter-active,
.fullscreen-popup-leave-active {
  transition: all 0.4s cubic-bezier(0.34, 1.56, 0.64, 1);
}
.fullscreen-popup-enter-from {
  opacity: 0;
  transform: scale(0.92);
}
.fullscreen-popup-leave-to {
  opacity: 0;
  transform: scale(1.04);
}

@keyframes scale-up {
  0% {
    transform: scale(0.9);
    opacity: 0;
  }
  100% {
    transform: scale(1);
    opacity: 1;
  }
}
.animate-scale-up {
  animation: scale-up 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards;
}

/* FLOWER CORNER ANIMATIONS */
@keyframes flower-sway {
  0%,
  100% {
    transform: rotate(-10deg) scale(1);
  }
  50% {
    transform: rotate(12deg) scale(1.08);
  }
}
@keyframes flower-float {
  0%,
  100% {
    transform: translateY(0px) scale(1);
  }
  50% {
    transform: translateY(-6px) scale(1.05);
  }
}

.animate-flower-sway {
  animation: flower-sway 2.4s ease-in-out infinite;
}
.animate-flower-float {
  animation: flower-float 2.8s ease-in-out infinite;
}
.animate-flower-sway-delayed {
  animation: flower-sway 2.6s ease-in-out infinite;
  animation-delay: 0.4s;
}
.animate-flower-float-delayed {
  animation: flower-float 3s ease-in-out infinite;
  animation-delay: 0.6s;
}

/* MAIN IMAGE SOFT BREATHING FLOAT ANIMATION */
@keyframes img-float {
  0%,
  100% {
    transform: translateY(0px) scale(1);
  }
  50% {
    transform: translateY(-7px) scale(1.03);
  }
}
.animate-img-float {
  animation: img-float 3.5s ease-in-out infinite;
}
</style>
