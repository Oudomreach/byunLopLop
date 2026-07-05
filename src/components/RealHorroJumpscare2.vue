<template>
  <div
    class="relative w-full min-h-[300px] flex items-center justify-center p-4"
  >
    <button
      @click="triggerJumpscare"
      :style="buttonStyle"
      class="absolute z-10 px-8 py-4 bg-gradient-to-r from-pink-400 to-pink-500 hover:from-pink-500 hover:to-pink-600 text-white font-extrabold text-lg rounded-2xl shadow-lg transform -translate-x-1/2 -translate-y-1/2 hover:scale-105 active:scale-95 transition-all duration-200 cursor-pointer border border-pink-300 tracking-wide select-none"
    >
      ?
    </button>

    <div
      v-if="isScared"
      class="fixed inset-0 z-[9999] bg-black flex flex-col items-center justify-center overflow-hidden select-none pointer-events-none animate-nightmare-flash"
    >
      <div
        class="w-full h-full flex flex-col items-center justify-center animate-nightmare-shake"
      >
        <div
          class="w-11/12 max-w-xl h-auto text-red-600 filter drop-shadow-[0_0_60px_rgba(220,38,38,0.9)] scale-up-lunge"
        >
          <svg
            viewBox="0 0 100 100"
            fill="currentColor"
            class="w-full h-full transform scale-y-110"
          >
            <path
              d="M50,5 C25,5 15,25 15,55 C15,75 25,95 30,95 C35,95 38,80 50,80 C62,80 65,95 70,95 C75,95 85,75 85,55 C85,25 75,5 50,5 Z"
              fill="#111"
              stroke="#dc2626"
              stroke-width="2"
            />
            <path
              d="M28,40 C22,40 20,52 28,55 C36,58 38,43 28,40 Z"
              fill="#000"
              stroke="#ff0000"
              stroke-width="1.5"
            />
            <path
              d="M72,40 C78,40 80,52 72,55 C64,58 62,43 72,40 Z"
              fill="#000"
              stroke="#ff0000"
              stroke-width="1.5"
            />
            <circle cx="29" cy="46" r="2.5" fill="#fff" class="animate-pulse" />
            <circle cx="71" cy="46" r="2.5" fill="#fff" class="animate-pulse" />
            <path d="M26,53 L24,70 L28,65 L29,75 L31,60 Z" fill="#990000" />
            <path d="M74,53 L76,70 L72,65 L71,75 L69,60 Z" fill="#990000" />
            <path
              d="M30,68 Q50,60 70,68 Q50,95 30,68 Z"
              fill="#050505"
              stroke="#dc2626"
              stroke-width="2"
            />
            <polygon
              points="33,67 36,75 39,66 42,76 45,66 48,77 52,77 55,66 58,76 61,66 64,75 67,67"
              fill="#eeeeee"
            />
            <polygon
              points="34,72 38,83 42,73 46,85 50,74 54,85 58,73 62,83 66,72"
              fill="#eeeeee"
            />
          </svg>
        </div>

        <h1
          class="text-7xl md:text-9xl font-black text-white tracking-widest mt-6 uppercase font-serif italic filter invert animate-glitch-text"
        >
          NIGHTMARE
        </h1>
      </div>
    </div>

    <div
      v-if="showPostMessage"
      class="fixed inset-0 z-[9998] bg-black/80 backdrop-blur-md flex items-center justify-center p-4 transition-all duration-300"
    >
      <div
        class="bg-zinc-900 border border-red-900 max-w-md w-full rounded-2xl p-6 text-center shadow-2xl transform scale-in-bounce"
      >
        <p
          class="text-zinc-200 text-lg font-medium leading-relaxed mb-6 font-mono tracking-wide"
        >
          Why would you click this? T.T
        </p>

        <button
          @click="showPostMessage = false"
          class="w-full py-3 bg-red-700 hover:bg-red-600 active:bg-red-800 text-white font-bold rounded-xl transition-colors duration-200 tracking-wide cursor-pointer uppercase text-sm"
        >
          Close Log File
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

const isScared = ref(false);
const showPostMessage = ref(false);

const buttonStyle = ref({
  top: "50%",
  left: "50%",
});

onMounted(() => {
  // Safe zone random placement inside container boundaries
  const randomTop = Math.floor(Math.random() * 60) + 20;
  const randomLeft = Math.floor(Math.random() * 60) + 20;

  buttonStyle.value = {
    top: `${randomTop}%`,
    left: `${randomLeft}%`,
  };
});

const playHorrorScreech = () => {
  try {
    const AudioContext = window.AudioContext || window.webkitAudioContext;
    if (!AudioContext) return;

    const ctx = new AudioContext();

    const primaryOsc = ctx.createOscillator();
    primaryOsc.type = "sawtooth";
    primaryOsc.frequency.setValueAtTime(900, ctx.currentTime);
    primaryOsc.frequency.exponentialRampToValueAtTime(
      3500,
      ctx.currentTime + 0.1
    );
    primaryOsc.frequency.exponentialRampToValueAtTime(
      200,
      ctx.currentTime + 0.7
    );

    const growlOsc = ctx.createOscillator();
    growlOsc.type = "square";
    growlOsc.frequency.setValueAtTime(75, ctx.currentTime);
    growlOsc.frequency.linearRampToValueAtTime(45, ctx.currentTime + 0.8);

    const stutterMod = ctx.createOscillator();
    stutterMod.type = "sawtooth";
    stutterMod.frequency.setValueAtTime(65, ctx.currentTime);

    const modGain = ctx.createGain();
    modGain.gain.setValueAtTime(300, ctx.currentTime);

    stutterMod.connect(modGain);
    modGain.connect(primaryOsc.frequency);

    const volumeControl = ctx.createGain();
    volumeControl.gain.setValueAtTime(0, ctx.currentTime);
    volumeControl.gain.linearRampToValueAtTime(1.0, ctx.currentTime + 0.01);
    volumeControl.gain.exponentialRampToValueAtTime(
      0.001,
      ctx.currentTime + 1.2
    );

    const audioFilter = ctx.createBiquadFilter();
    audioFilter.type = "peaking";
    audioFilter.frequency.setValueAtTime(2500, ctx.currentTime);
    audioFilter.Q.setValueAtTime(12, ctx.currentTime);

    primaryOsc.connect(audioFilter);
    growlOsc.connect(audioFilter);
    audioFilter.connect(volumeControl);
    volumeControl.connect(ctx.destination);

    primaryOsc.start();
    growlOsc.start();
    stutterMod.start();

    primaryOsc.stop(ctx.currentTime + 1.3);
    growlOsc.stop(ctx.currentTime + 1.3);
    stutterMod.stop(ctx.currentTime + 1.3);
  } catch (error) {
    console.error("Web Audio API execution failed:", error);
  }
};

const triggerJumpscare = () => {
  showPostMessage.value = false;
  isScared.value = true;

  playHorrorScreech();

  setTimeout(() => {
    isScared.value = false;
    showPostMessage.value = true;
  }, 1400);
};
</script>

<style scoped>
/* SEVERE GLITCH FLASH BACKGROUND */
.animate-nightmare-flash {
  animation: chaosStrobe 0.08s infinite steps(1);
}

@keyframes chaosStrobe {
  0% {
    background-color: #000000;
    filter: invert(0);
  }
  33% {
    background-color: #1a0000;
    filter: invert(0);
  }
  66% {
    background-color: #ffffff;
    filter: invert(1);
  }
  100% {
    background-color: #000000;
    filter: invert(0);
  }
}

/* VIOLENT DISPLACEMENT QUAKE */
.animate-nightmare-shake {
  animation: extremeQuake 0.1s infinite linear;
}

@keyframes extremeQuake {
  0% {
    transform: translate(0, 0) scale(1);
  }
  20% {
    transform: translate(-25px, 15px) rotate(-2deg) scale(1.05);
  }
  40% {
    transform: translate(20px, -20px) rotate(3deg) scale(0.95);
  }
  60% {
    transform: translate(-15px, -10px) rotate(-3deg) scale(1.08);
  }
  80% {
    transform: translate(25px, 20px) rotate(2deg) scale(1);
  }
  100% {
    transform: translate(-20px, -15px) rotate(0deg) scale(1.03);
  }
}

/* VIOLENT FACE LUNGE */
.scale-up-lunge {
  animation: demonLunge 0.18s cubic-bezier(0.6, -0.28, 0.735, 0.045) forwards;
}

@keyframes demonLunge {
  0% {
    transform: scale(0.05) rotate(45deg);
    opacity: 0;
    filter: saturate(0) brightness(0);
  }
  30% {
    opacity: 1;
    filter: saturate(2) brightness(2);
  }
  100% {
    transform: scale(1.6) rotate(0deg);
    opacity: 1;
  }
}

/* TEXT GLITCH EFFECT */
.animate-glitch-text {
  animation: textGlitch 0.2s infinite ease-in-out alternate;
}

@keyframes textGlitch {
  0% {
    transform: skewX(-15deg) scale(0.9);
    text-shadow: 4px 0 #ff0000;
  }
  100% {
    transform: skewX(15deg) scale(1.1);
    text-shadow: -4px 0 #00ffff;
  }
}

/* POP-UP ENTRY ANIMATION */
.scale-in-bounce {
  animation: modalScale 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards;
}

@keyframes modalScale {
  0% {
    transform: scale(0.8);
    opacity: 0;
  }
  100% {
    transform: scale(1);
    opacity: 1;
  }
}
</style>
