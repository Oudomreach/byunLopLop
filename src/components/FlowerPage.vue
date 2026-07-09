<template>
  <div
    class="min-h-screen w-full bg-gradient-to-br from-rose-100 via-pink-200 to-amber-100 text-rose-950 flex flex-col items-center justify-center p-4 relative select-none"
  >
    <button
      @click="goBack"
      class="absolute top-6 left-6 text-rose-600/80 hover:text-rose-900 transition-all duration-200 flex items-center space-x-1.5 text-xs font-bold tracking-widest uppercase bg-white/60 backdrop-blur-md px-3.5 py-2 rounded-full border border-white/60 shadow-sm active:scale-95 z-40"
    >
      <span>← Menu</span>
    </button>

    <div
      class="w-full max-w-sm text-center flex flex-col items-center justify-center space-y-6 z-10 mx-4"
    >
      <div class="space-y-1">
        <h2
          class="text-2xl sm:text-3xl font-serif italic font-bold text-rose-700"
        >
          Your Fresh Bouquet 💐
        </h2>
        <p class="text-xs text-rose-800/70 font-medium">💖</p>
      </div>

      <div
        class="w-72 h-72 sm:w-80 sm:h-80 bg-white/60 backdrop-blur-md rounded-full shadow-xl border border-white flex items-center justify-center relative overflow-hidden group"
      >
        <svg
          viewBox="0 0 200 200"
          class="w-56 h-56 transform transition-transform duration-700 group-hover:scale-105"
        >
          <path
            d="M100,180 Q85,120 70,80"
            fill="none"
            stroke="#65a30d"
            stroke-width="3"
            stroke-linecap="round"
          />
          <path
            d="M100,180 Q100,110 100,65"
            fill="none"
            stroke="#4d7c0f"
            stroke-width="3.5"
            stroke-linecap="round"
          />
          <path
            d="M100,180 Q115,130 130,85"
            fill="none"
            stroke="#65a30d"
            stroke-width="3"
            stroke-linecap="round"
          />

          <path d="M85,145 Q100,150 115,145 Q100,135 85,145" fill="#f43f5e" />
          <circle cx="100" cy="143" r="5" fill="#f43f5e" />
          <path
            d="M96,143 Q80,130 75,145 Q85,150 96,143"
            fill="#fda4af"
            opacity="0.85"
          />
          <path
            d="M104,143 Q120,130 125,145 Q115,150 104,143"
            fill="#fda4af"
            opacity="0.85"
          />

          <g class="animate-flower-sway origin-[70px_80px]">
            <circle cx="70" cy="62" r="7" fill="#ffffff" />
            <circle cx="70" cy="98" r="7" fill="#ffffff" />
            <circle cx="52" cy="80" r="7" fill="#ffffff" />
            <circle cx="88" cy="80" r="7" fill="#ffffff" />
            <circle cx="57" cy="67" r="7" fill="#ffffff" />
            <circle cx="83" cy="93" r="7" fill="#ffffff" />
            <circle cx="57" cy="93" r="7" fill="#ffffff" />
            <circle cx="83" cy="67" r="7" fill="#ffffff" />
            <circle cx="70" cy="80" r="10" fill="#facc15" />
          </g>

          <g class="animate-flower-float origin-[130px_85px]">
            <path
              d="M112,85 C112,60 122,50 130,50 C138,50 148,60 148,85 C148,100 112,100 112,85 Z"
              fill="#fb7185"
            />
            <path
              d="M120,85 C120,65 126,55 130,55 C134,55 140,65 140,85 C140,98 120,98 120,85 Z"
              fill="#f43f5e"
            />
            <path
              d="M125,85 C125,70 128,62 130,62 C132,62 135,70 135,85 C135,95 125,95 125,85 Z"
              fill="#ffe4e6"
              opacity="0.7"
            />
          </g>

          <g class="animate-flower-sway-delayed origin-[100px_65px]">
            <path
              d="M84,65 C84,38 94,28 100,28 C106,28 116,38 116,65 C116,82 84,82 84,65 Z"
              fill="#fbbf24"
            />
            <path
              d="M91,65 C91,42 96,33 100,33 C104,33 109,42 109,65 C109,79 91,79 91,65 Z"
              fill="#ea580c"
            />
          </g>
        </svg>
      </div>
      <div
        class="space-y-2 text-xs text-rose-700 max-w-[240px] text-start leading-relaxed italic font-serif"
      >
        <p>🌹 For your happiness.</p>
        <p>🌼 For your strength.</p>
        <p>🌷 For new beginnings.</p>
      </div>

      <p
        class="text-xs text-rose-700 max-w-[240px] leading-relaxed italic font-serif"
      >
        "Flowers grow back, even after the harshest winters. May your joy do the
        exact same."
      </p>
      <p
        class="text-xs text-rose-700 max-w-[240px] leading-relaxed italic font-serif"
      >
        "If I could, I would hand these flowers to you in person. Since I cant,
        I hope this little bouquet carries my wishes instead. They might not
        have a scent but they will never wilt."
      </p>
      <p
        class="text-xs text-rose-700 max-w-[240px] leading-relaxed italic font-serif"
      >
        "NOPEEE! cuz i have no money :((("
      </p>
      <p
        class="text-xs text-rose-700 max-w-[240px] leading-relaxed italic font-serif"
      >
        "i want to get a real flower too :((("
      </p>
    </div>
  </div>
</template>

<script setup>
const emit = defineEmits(["back"]);

const goBack = () => {
  emit("back");
};
</script>

<style scoped>
@keyframes flower-sway {
  0%,
  100% {
    transform: rotate(-5deg);
  }
  50% {
    transform: rotate(6deg);
  }
}
@keyframes flower-float {
  0%,
  100% {
    transform: translateY(0px);
  }
  50% {
    transform: translateY(-4px);
  }
}
.animate-flower-sway {
  animation: flower-sway 3s ease-in-out infinite;
}
.animate-flower-float {
  animation: flower-float 2.6s ease-in-out infinite;
}
.animate-flower-sway-delayed {
  animation: flower-sway 3.4s ease-in-out infinite;
  animation-delay: 0.5s;
}
</style>
