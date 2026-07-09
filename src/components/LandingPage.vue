Here is the complete, fully corrected code for **`LandingPage.vue`** with
`v-slot:default` stripped out so it compiles smoothly: ```vue
<template>
  <div
    class="min-h-screen w-full bg-gradient-to-br from-rose-100 via-pink-200 to-amber-100 text-rose-950 flex items-center justify-center font-sans overflow-hidden select-none relative"
    @mousemove="handleMouseMove"
  >
    <div
      v-for="sparkle in mouseSparkles"
      :key="sparkle.id"
      class="pointer-events-none fixed z-50 text-xs animate-ping opacity-70"
      :style="{ left: sparkle.x + 'px', top: sparkle.y + 'px' }"
    >
      ✨
    </div>

    <div
      class="absolute inset-0 pointer-events-none overflow-hidden z-0 opacity-60"
    >
      <div
        v-for="petal in backgroundPetals"
        :key="petal.id"
        class="absolute text-pink-400/50 animate-fall select-none"
        :style="{
          left: petal.left + '%',
          animationDelay: petal.delay + 's',
          animationDuration: petal.duration + 's',
          fontSize: petal.size + 'px',
        }"
      >
        🌸
      </div>
    </div>

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
    </div>

    <transition name="fullscreen-popup">
      <div
        v-if="showSuccessPopup"
        class="fixed inset-0 z-50 w-screen h-screen bg-rose-950/40 backdrop-blur-lg flex flex-col items-center justify-center p-6 text-center select-none"
      >
        <div
          class="w-[calc(100%-2rem)] max-w-sm bg-white/90 backdrop-blur-2xl rounded-3xl p-8 shadow-2xl border border-white/60 flex flex-col items-center space-y-6 animate-scale-up"
        >
          <div
            class="w-56 h-56 sm:w-64 sm:h-64 bg-rose-50 rounded-2xl overflow-hidden flex items-center justify-center border-2 border-rose-200/60 shadow-md"
          >
            <img
              :src="surpriseFace"
              alt="Success"
              class="w-full h-full object-cover"
            />
          </div>
          <div class="space-y-1.5 w-full">
            <h4
              class="font-serif italic font-extrabold text-transparent bg-clip-text bg-gradient-to-r from-rose-600 via-pink-600 to-amber-500 text-2xl tracking-wide"
            >
              Unlocked! ✨
            </h4>
            <p class="text-rose-700/90 font-sans text-sm font-bold">
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
        class="absolute top-24 z-50 bg-gradient-to-r from-rose-500 to-pink-500 text-white px-6 py-3 rounded-full shadow-lg border border-white/20 flex items-center space-x-2 animate-bounce"
      >
        <span>💕</span
        ><span class="font-medium text-sm font-sans">{{ errorMessage }}</span>
      </div>
    </transition>

    <transition name="hint-popup">
      <div
        v-if="showHintAfterAttempts"
        class="absolute inset-0 z-50 flex items-center justify-center p-6 bg-rose-950/20 backdrop-blur-md"
      >
        <div
          class="w-full max-w-sm bg-white/90 backdrop-blur-2xl rounded-3xl p-8 text-center shadow-xl border border-white/60 space-y-5 animate-slide-up"
        >
          <span class="text-4xl animate-pulse inline-block">💡</span>
          <h3 class="text-2xl font-serif italic text-rose-700">
            Here a little hint!
          </h3>
          <div
            class="text-rose-600/90 text-sm leading-relaxed px-4 font-sans space-y-2"
          >
            <p>
              Think of it as someone's birthday... like
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
            class="w-full py-3 rounded-xl bg-gradient-to-r from-rose-400 to-pink-400 text-white text-sm font-semibold transition-all active:scale-98"
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
        class="w-[calc(100%-2rem)] max-w-[340px] flex flex-col items-center p-6 pt-8 z-10 bg-white/85 backdrop-blur-md rounded-3xl border border-white/50 shadow-xl space-y-5 mx-4"
      >
        <div class="text-center space-y-1">
          <div class="flex justify-center mb-0.5">
            <img
              :src="pigFire"
              alt=""
              class="w-22 h-22 object-cover rounded-2xl"
            />
          </div>
          <h2
            class="text-3xl font-serif italic tracking-wide text-transparent bg-clip-text bg-gradient-to-r from-rose-600 via-pink-600 to-rose-500 font-medium"
          >
            Security Check <span class="block text-xl">Who's this?</span>
          </h2>
          <p
            class="text-[10px] text-pink-500/80 tracking-widest uppercase font-bold font-sans"
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
            class="w-3 h-3 rounded-full border-2 border-pink-300/80 transition-all duration-200"
            :class="{
              'bg-gradient-to-tr from-rose-400 to-pink-400 scale-[1.15] shadow-md border-rose-300':
                passcode.length >= index,
            }"
          ></div>
        </div>

        <div class="grid grid-cols-3 gap-2.5 w-full">
          <button
            v-for="num in [1, 2, 3, 4, 5, 6, 7, 8, 9]"
            :key="num"
            @click="pressKey(num.toString())"
            class="w-full aspect-[4/3] max-h-14 rounded-2xl bg-white/70 backdrop-blur-sm border border-white/80 text-xl font-serif font-semibold text-rose-700 shadow-sm hover:bg-white/90 active:scale-95 transition-all flex items-center justify-center"
          >
            {{ num }}
          </button>
          <button
            @click="clearPasscode"
            class="w-full aspect-[4/3] max-h-14 rounded-2xl flex items-center justify-center text-[11px] font-bold uppercase text-rose-400 hover:text-rose-600 font-sans"
          >
            Clear
          </button>
          <button
            @click="pressKey('0')"
            class="w-full aspect-[4/3] max-h-14 rounded-2xl bg-white/70 border border-white/80 text-xl font-serif font-semibold text-rose-700 hover:bg-white/90 active:scale-95 transition-all flex items-center justify-center"
          >
            0
          </button>
          <button
            @click="deleteLast"
            class="w-full aspect-[4/3] max-h-14 rounded-2xl flex items-center justify-center text-[11px] font-bold uppercase text-rose-400 hover:text-rose-600 font-sans"
          >
            Del
          </button>
        </div>
      </div>

      <div
        v-else-if="currentScreen === 'date'"
        key="datescreen"
        class="w-[calc(100%-2rem)] max-w-sm text-center p-6 sm:p-8 pt-8 z-10 bg-white/85 backdrop-blur-md rounded-3xl border border-white/50 shadow-xl flex flex-col items-center justify-center space-y-6 mx-4"
      >
        <div
          class="relative w-32 h-32 flex items-center justify-center bg-white/95 rounded-3xl shadow-md border border-rose-200/60 overflow-hidden animate-bounce custom-bounce-delay"
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
            class="text-3xl sm:text-4xl font-serif font-extrabold italic bg-clip-text text-transparent bg-gradient-to-br from-pink-500 via-rose-500 to-amber-400 drop-shadow-sm py-1"
          >
            22/July/2026
          </h1>
          <p
            class="text-sm text-rose-800/90 font-medium max-w-sm mx-auto tracking-wide"
          >
            Happy another lap around the sun :P
          </p>
        </div>
        <div class="flex items-center space-x-3 py-1 text-pink-300">
          <span
            class="h-px w-12 bg-gradient-to-r from-transparent to-pink-300"
          ></span>
          <span class="text-lg animate-spin" style="animation-duration: 3s"
            >🌸</span
          >
          <span
            class="h-px w-12 bg-gradient-to-l from-transparent to-pink-300"
          ></span>
        </div>
      </div>

      <div
        v-else-if="currentScreen === 'birthday'"
        key="birthday"
        class="w-[calc(100%-2rem)] max-w-md text-center p-8 z-10 bg-white/75 backdrop-blur-xl rounded-3xl border border-white/60 shadow-2xl shadow-rose-200/40 flex flex-col items-center relative mx-4 space-y-6 overflow-hidden"
      >
        <div
          class="absolute -top-4 -left-6 text-4xl animate-balloon-float pointer-events-none select-none"
        >
          🎈
        </div>
        <div
          class="absolute -top-2 -right-8 text-4xl animate-balloon-float pointer-events-none select-none"
          style="animation-delay: 1.5s"
        >
          🎈
        </div>

        <div class="relative mt-8 z-10 animate-img-float">
          <span
            class="absolute -top-16 left-1/2 -translate-x-1/2 text-4xl z-30 select-none drop-shadow-md filter saturate-120 animate-none"
          >
            <img :src="birthdayHat" alt="Birthday Hat" />
          </span>

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
            class="relative w-40 h-40 flex items-center justify-center bg-white/95 rounded-2xl shadow-md border border-rose-200/80 overflow-hidden"
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
            class="text-3xl sm:text-4xl font-serif font-black tracking-tight bg-clip-text text-transparent bg-gradient-to-r from-rose-600 via-pink-500 to-pink-600 drop-shadow-sm"
          >
            Happy Birthday, Chheng! 💚
          </h1>

          <div class="h-6 flex items-center justify-center">
            <p
              class="text-rose-500 font-mono text-xs font-bold tracking-wide border-r-2 border-rose-400 pr-1 animate-caret"
            >
              {{ typewriterText }}
            </p>
          </div>

          <!-- <p
            class="text-xs sm:text-sm text-rose-900/80 font-sans font-medium leading-relaxed px-2 text-center max-w-sm mx-auto"
          >
            To one of the most wonderful people I know, thank you for bringing
            so much light and joy into my life. I hope your birthday is filled
            with laughter, unforgettable moments, and all the happiness you
            truly deserve.
          </p> -->
        </div>

        <div
          @click="triggerCakeWish"
          class="relative p-4 bg-white/40 border border-white/60 rounded-2xl cursor-pointer hover:bg-white/80 hover:scale-105 active:scale-95 transition-all duration-300 shadow-sm flex flex-col items-center group w-80 select-none"
        >
          <div
            class="absolute inset-0 pointer-events-none overflow-visible z-30"
          >
            <span
              v-for="petal in cakePetals"
              :key="petal.id"
              class="absolute text-xl animate-cake-petal"
              :style="{
                '--target-x': petal.x + 'px',
                '--target-y': petal.y + 'px',
                '--spin': petal.spin + 'deg',
                left: '30%',
                top: '80%',
              }"
            >
              🌸
            </span>
            <span
              v-for="petal in cakePetals"
              :key="petal.id"
              class="absolute text-xl animate-cake-petal"
              :style="{
                '--target-x': petal.x + 'px',
                '--target-y': petal.y + 'px',
                '--spin': petal.spin + 'deg',
                left: '50%',
                top: '40%',
              }"
            >
              🌷
            </span>
            <span
              v-for="petal in cakePetals"
              :key="petal.id"
              class="absolute text-xl animate-cake-petal"
              :style="{
                '--target-x': petal.x + 'px',
                '--target-y': petal.y + 'px',
                '--spin': petal.spin + 'deg',
                left: '20%',
                top: '70%',
              }"
            >
              🌹
            </span>
          </div>

          <div class="text-8xl group-hover:animate- tracking-wide select-none">
            {{ isCakeBlown ? "🎂" : "🎂" }}
          </div>
          <span
            class="text-[10px] uppercase font-bold tracking-widest text-rose-500 mt-2 block"
          >
            {{ cakeLabel }}
          </span>

          <transition name="popup">
            <div
              v-if="showWishNotice"
              class="absolute -top-12 bg-rose-600 text-white font-bold font-sans px-3 py-1 rounded-full text-xs shadow-md whitespace-nowrap animate-bounce"
            >
              May all yours wishes come true! 🎂
            </div>
          </transition>
        </div>

        <div
          class="flex items-center space-x-3 py-1 text-pink-300 w-full justify-center"
        >
          <span
            class="h-px w-12 bg-gradient-to-r from-transparent to-pink-300"
          ></span>
          <img :src="pigIcon" alt="Pig Icon" class="h-5 w-5 object-contain" />
          <span
            class="h-px w-12 bg-gradient-to-l from-transparent to-pink-300"
          ></span>
        </div>

        <button
          @click="celebrateAndNext"
          class="group relative w-full py-4 rounded-2xl bg-gradient-to-r from-rose-500 via-pink-500 to-amber-500 hover:from-rose-600 hover:to-amber-600 text-white text-xs sm:text-sm font-extrabold tracking-widest uppercase shadow-lg shadow-pink-300/60 overflow-hidden transform hover:-translate-y-1 active:translate-y-0 transition-all duration-300 font-sans flex items-center justify-center space-x-2 border border-white/20"
        >
          <div
            class="absolute inset-0 w-full h-full bg-white/20 transform scale-x-0 group-hover:scale-x-100 transition-transform duration-500 origin-left"
          ></div>

          <span class="relative z-10 flex items-center gap-1">
            <span>✨ Begin Your Birthday Journey</span>
            <span class="inline-block animate-pulse">✨</span>
          </span>
        </button>

        <div
          v-if="confettiActive"
          class="absolute inset-0 pointer-events-none z-40 overflow-hidden"
        >
          <div
            v-for="confetto in confettiParticles"
            :key="confetto.id"
            class="absolute w-2 h-2 rounded-full animate-ping"
            :style="{
              top: confetto.y + '%',
              left: confetto.x + '%',
              backgroundColor: confetto.color,
            }"
          ></div>
        </div>
      </div>

      <div
        v-else-if="currentScreen === 'birthday-message'"
        key="birthdaymessage"
        class="w-[calc(100%-2rem)] max-w-sm text-center p-6 sm:p-8 pt-8 z-10 bg-white/85 backdrop-blur-md rounded-3xl border border-white/50 shadow-xl flex flex-col items-center justify-center space-y-6 mx-4"
      >
        <div class="space-y-4 w-full">
          <h2
            class="flex justify-around items-center text-2xl font-serif font-extrabold italic bg-clip-text text-transparent bg-gradient-to-br from-rose-500 via-pink-500 to-amber-500 py-1"
          >
            One more thing <img :src="pigBIU" alt="Pig" class="w-20 h-auto" />
          </h2>
          <div
            class="bg-white/60 p-5 rounded-2xl border border-pink-100 shadow-inner space-y-4 relative"
          >
            <span class="absolute -top-3 -right-3 text-2xl animate-bounce"
              >💌</span
            >
            <p
              class="text-xs sm:text-sm text-rose-800/90 font-medium leading-relaxed"
            >
              To one of the most wonderful people I know, thank you for bringing
              so much light and joy into my life. I hope your birthday is filled
              with laughter, unforgettable moments, and all the happiness you
              truly deserve.
            </p>
            <p
              class="text-xs sm:text-sm text-rose-800/90 font-medium leading-relaxed"
            >
              Thanks you for being you! I hope this year brings you closer to
              your dreams and fills your heart with endless happiness. You're
              truly one of a kind and I am so grateful for you! 💖
            </p>
            <p
              class="text-xs sm:text-sm text-rose-800/90 font-medium leading-relaxed"
            >
              Thanks you for putting up with this person
            </p>
            <p
              class="text-xs sm:text-sm text-rose-800/90 font-medium leading-relaxed"
            >
              Enjoy every single second of your day! Eat lots of cake! 🎂 and
            </p>
            <p
              class="text-xs sm:text-sm text-rose-800/90 font-medium leading-relaxed uppercase font-bold"
            >
              HAPPY BIRTHDAY!
            </p>
          </div>
        </div>

        <div class="flex items-center space-x-3 py-1 text-pink-300">
          <span
            class="h-px w-12 bg-gradient-to-r from-transparent to-pink-300"
          ></span>
          <span class="text-sm font-bold animate-pulse">kimmy</span>
          <span
            class="h-px w-12 bg-gradient-to-l from-transparent to-pink-300"
          ></span>
        </div>

        <button
          @click="emitMenuEvent"
          class="w-full py-3 rounded-xl bg-gradient-to-r from-rose-400 to-pink-500 text-white text-xs font-bold tracking-widest uppercase shadow-lg shadow-pink-300/70 transition-all flex items-center justify-center space-x-2"
        >
          <span>To Menu</span><span class="text-lg">🐷</span>
        </button>
      </div>
    </transition>

    <button
      @click="toggleAudioState"
      class="fixed bottom-6 right-6 z-50 w-12 h-12 rounded-full flex items-center justify-center bg-white/80 backdrop-blur-md border border-pink-200 shadow-md text-rose-600 hover:text-rose-900 font-serif text-lg transition-all transform active:scale-90 select-none cursor-pointer"
      :class="{ 'animate-spin': isMusicPlaying }"
      style="animation-duration: 6s"
      title="Background Music"
    >
      ♫
    </button>
    <audio
      ref="audioTrackElement"
      loop
      src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3"
    ></audio>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from "vue";
import uuuImg from "../assets/uuu.jpg";
import pigIcon from "../assets/pig.png";
import bunnyDance from "../assets/bunnyDance2.gif";
import birthdayHat from "../assets/birthdayHat.png";
import surpriseFace from "../assets/surprise.png";
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
const history = ref([]);

let screenTimeout = null;

// Background Canvas Particle Generation Arrays
const backgroundPetals = ref([]);
const mouseSparkles = ref([]);

// Typewriter Logic Block Props
const typewriterText = ref("");
const typewriterPhrases = [
  "One little website...",
  "Made especially for you.",
  "Thank you for being part of my story.",
  "Today is all about you.",
];
let phraseIndex = 0;
let charIndex = 0;
let isDeleting = false;
let typewriterTimeout = null;

const isCakeBlown = ref(false);
const showWishNotice = ref(false);
const cakeLabel = ref("Tap to make wish!");

const confettiActive = ref(false);
const confettiParticles = ref([]);

const isMusicPlaying = ref(false);
const audioTrackElement = ref(null);

const backLabel = computed(() => {
  if (history.value.length === 0) return "";
  const prev = history.value[history.value.length - 1];
  if (prev === "lock") return "Lock";
  if (prev === "date") return "Date";
  if (prev === "birthday") return "Birthday";
  return "Back";
});

onMounted(() => {
  // Generate random drifting petal array metrics
  backgroundPetals.value = Array.from({ length: 20 }).map((_, i) => ({
    id: i,
    left: Math.random() * 100,
    delay: Math.random() * -15,
    duration: 8 + Math.random() * 12,
    size: 12 + Math.random() * 14,
  }));

  runTypewriterLoop();
});

onUnmounted(() => {
  if (typewriterTimeout) clearTimeout(typewriterTimeout);
  if (screenTimeout) clearTimeout(screenTimeout);
});

// Cursor Sparks Mouse Movement Follower
let sparkleId = 0;
const handleMouseMove = (e) => {
  if (Math.random() > 0.85) {
    const id = sparkleId++;
    mouseSparkles.value.push({ id, x: e.clientX, y: e.clientY });
    setTimeout(() => {
      mouseSparkles.value = mouseSparkles.value.filter((p) => p.id !== id);
    }, 800);
  }
};

// Cycle Typing Script Engine
const runTypewriterLoop = () => {
  const currentPhrase = typewriterPhrases[phraseIndex];

  if (isDeleting) {
    typewriterText.value = currentPhrase.substring(0, charIndex - 1);
    charIndex--;
  } else {
    typewriterText.value = currentPhrase.substring(0, charIndex + 1);
    charIndex++;
  }

  let typingSpeed = isDeleting ? 40 : 100;

  if (!isDeleting && charIndex === currentPhrase.length) {
    typingSpeed = 2000;
    isDeleting = true;
  } else if (isDeleting && charIndex === 0) {
    isDeleting = false;
    phraseIndex = (phraseIndex + 1) % typewriterPhrases.length;
    typingSpeed = 400;
  }

  typewriterTimeout = setTimeout(runTypewriterLoop, typingSpeed);
};

// Cake Tap Interaction Action
const cakePetals = ref([]);
let cakePetalId = 0;

const triggerCakeWish = () => {
  // 1. Fire the original status values
  if (!isCakeBlown.value) {
    isCakeBlown.value = true;
    showWishNotice.value = true;
    cakeLabel.value = "Wish Made! ✨";
    generateCardConfettiBurst();

    setTimeout(() => {
      showWishNotice.value = false;
    }, 5000);
  }

  // 2. Spawn 6-8 bursting flower petals EVERY click
  const petalCount = 8;
  for (let i = 0; i < petalCount; i++) {
    const id = cakePetalId++;

    // Generate an explosion path profile radius vector mapping coordinates outwards
    const angle = Math.random() * Math.PI * 2;
    const distance = 60 + Math.random() * 70;
    const x = Math.cos(angle) * distance;
    const y = Math.sin(angle) * distance - 40; // Push upwards slightly naturally
    const spin = 180 + Math.random() * 360;

    cakePetals.value.push({ id, x, y, spin });

    // Remove the petal from memory after the animation finishes
    setTimeout(() => {
      cakePetals.value = cakePetals.value.filter((p) => p.id !== id);
    }, 1200);
  }
};

// Internal Confetti Matrix generator
const generateCardConfettiBurst = () => {
  confettiActive.value = true;
  const colors = ["#f43f5e", "#ec4899", "#f59e0b", "#10b981", "#3b82f6"];

  confettiParticles.value = Array.from({ length: 35 }).map((_, i) => ({
    id: i,
    x: 30 + Math.random() * 40,
    y: 40 + Math.random() * 30,
    color: colors[Math.floor(Math.random() * colors.length)],
  }));

  setTimeout(() => {
    confettiActive.value = false;
    confettiParticles.value = [];
  }, 1500);
};

const celebrateAndNext = () => {
  generateCardConfettiBurst();
  setTimeout(() => {
    history.value.push(currentScreen.value);
    currentScreen.value = "birthday-message";
  }, 600);
};

const toggleAudioState = () => {
  if (!audioTrackElement.value) return;
  if (isMusicPlaying.value) {
    audioTrackElement.value.pause();
    isMusicPlaying.value = false;
  } else {
    audioTrackElement.value.play().catch(() => {});
    isMusicPlaying.value = true;
  }
};

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
      history.value.push(currentScreen.value);
      currentScreen.value = "date";
      incorrectAttempts.value = 0;
      showHintAfterAttempts.value = false;

      screenTimeout = setTimeout(() => {
        history.value.push(currentScreen.value);
        currentScreen.value = "birthday";
      }, 3500);
    }, 1000);
  } else {
    isShaking.value = true;
    incorrectAttempts.value++;
    errorMessage.value =
      incorrectAttempts.value === 1
        ? "Huh? Try again! Another code!"
        : incorrectAttempts.value === 2
        ? "Wow, like WOW! we been talking this long and u didnt get it?"
        : "Alright!";

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
    }, 2500);
  }
};

const handleBack = () => {
  if (screenTimeout) clearTimeout(screenTimeout);
  if (history.value.length > 0) {
    currentScreen.value = history.value.pop();
    if (currentScreen.value === "lock") {
      passcode.value = "";
    } else if (currentScreen.value === "date") {
      screenTimeout = setTimeout(() => {
        history.value.push(currentScreen.value);
        currentScreen.value = "birthday";
      }, 3500);
    }
  }
};

const emitMenuEvent = () => {
  emit("go-to-menu");
};
</script>

<style scoped>
@keyframes fall {
  0% {
    transform: translateY(-5vh) rotate(0deg) translateX(0px);
    opacity: 0;
  }
  10% {
    opacity: 1;
  }
  90% {
    opacity: 1;
  }
  100% {
    transform: translateY(105vh) rotate(360deg) translateX(60px);
    opacity: 0;
  }
}
.animate-fall {
  animation: fall linear infinite;
}

@keyframes caret {
  50% {
    border-color: transparent;
  }
}
.animate-caret {
  animation: caret 0.75s step-end infinite;
}

@keyframes balloon-float {
  0%,
  100% {
    transform: translateY(0px) rotate(-4deg);
  }
  50% {
    transform: translateY(-12px) rotate(4deg);
  }
}
.animate-balloon-float {
  animation: balloon-float 4s ease-in-out infinite;
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
    transform: translateY(-15px) rotate(8deg);
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
    transform: translateY(15px) rotate(-8deg);
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
    transform: translateX(-10px) translateY(-12px);
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
  transition: all 0.2s ease-in;
}
.popup-enter-from {
  transform: translateY(-40px) scale(0.9);
  opacity: 0;
}
.popup-leave-to {
  transform: translateY(-15px);
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

@keyframes img-float {
  0%,
  100% {
    transform: translateY(0px);
  }
  50% {
    transform: translateY(-6px) scale(1.02);
  }
}
.animate-img-float {
  animation: img-float 3.5s ease-in-out infinite;
}
@keyframes cake-petal-burst {
  0% {
    transform: translate(-50%, -50%) scale(0.5) rotate(0deg);
    opacity: 1;
  }
  100% {
    transform: translate(
        calc(-50% + var(--target-x)),
        calc(-50% + var(--target-y))
      )
      scale(1.1) rotate(var(--spin));
    opacity: 0;
  }
}

.animate-cake-petal {
  animation: cake-petal-burst 1.2s cubic-bezier(0.1, 0.8, 0.3, 1) forwards;
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
