<template>
  <div
    v-if="isOpen"
    class="fixed inset-0 z-[150] flex items-center justify-center bg-rose-950/40 backdrop-blur-md px-4 animate-fade-in"
    @click.self="closePopup"
  >
    <!-- Modal Card Container - Center aligned with strict max width -->
    <div
      class="bg-white/95 p-6 sm:p-8 rounded-3xl shadow-2xl border-2 border-pink-200 w-full max-w-[340px] text-center relative flex flex-col items-center overflow-hidden animate-scale-up"
    >
      <!-- Sparkle Background Effects -->
      <div class="absolute inset-0 pointer-events-none opacity-40">
        <span class="absolute top-6 left-6 text-xl animate-pulse">✨</span>
        <span
          class="absolute bottom-6 right-6 text-xl animate-pulse"
          style="animation-delay: 1s"
          >✨</span
        >
      </div>

      <!-- Header Content -->
      <h3
        class="text-2xl font-serif font-extrabold italic text-rose-700 mb-1 tracking-tight"
      >
        A Bouquet for You! 🌸
      </h3>
      <p class="text-xs text-rose-500/90 font-semibold mb-5">
        Watch them grow right on your screen
      </p>

      <!-- THE FLOWER CONTAINER CANVAS (Guaranteed Center Alignment) -->
      <div
        class="w-48 h-56 bg-gradient-to-b from-rose-50/40 to-rose-100/60 rounded-2xl border border-pink-100 relative overflow-hidden shadow-inner flex items-center justify-center mx-auto"
      >
        <svg
          viewBox="0 0 100 120"
          class="w-full h-full drop-shadow-md overflow-visible"
        >
          <!-- Wrapping Ribbon Base Layer -->
          <path
            d="M43 95 C47 90, 53 90, 57 95 C53 99, 47 99, 43 95"
            fill="#f472b6"
            class="animate-ribbon"
          />

          <!-- Left Daisy Block -->
          <g class="flower-group">
            <path
              d="M50 95 Q35 75, 30 52"
              fill="none"
              stroke="#4ade80"
              stroke-width="2.5"
              stroke-linecap="round"
              class="animate-stem"
            />
            <path
              d="M42 78 Q32 75, 38 70 Q43 73, 42 78"
              fill="#22c55e"
              class="animate-leaf"
            />
            <g
              transform="translate(30, 52)"
              class="animate-bloom"
              style="animation-delay: 0.6s"
            >
              <circle cx="0" cy="0" r="8" fill="#facc15" />
              <!-- Daisy Petals Layout -->
              <circle cx="0" cy="-10" r="4.5" fill="#ffffff" />
              <circle cx="0" cy="10" r="4.5" fill="#ffffff" />
              <circle cx="-10" cy="0" r="4.5" fill="#ffffff" />
              <circle cx="10" cy="0" r="4.5" fill="#ffffff" />
              <circle cx="-7" cy="-7" r="4.5" fill="#ffffff" />
              <circle cx="7" cy="-7" r="4.5" fill="#ffffff" />
              <circle cx="-7" cy="7" r="4.5" fill="#ffffff" />
              <circle cx="7" cy="7" r="4.5" fill="#ffffff" />
            </g>
          </g>

          <!-- Right Tulip Block -->
          <g class="flower-group">
            <path
              d="M50 95 Q65 73, 70 48"
              fill="none"
              stroke="#4ade80"
              stroke-width="2.5"
              stroke-linecap="round"
              class="animate-stem"
              style="animation-delay: 0.2s"
            />
            <path
              d="M58 80 Q68 75, 62 68 Q57 73, 58 80"
              fill="#22c55e"
              class="animate-leaf"
              style="animation-delay: 0.7s"
            />
            <g
              transform="translate(70, 48)"
              class="animate-bloom"
              style="animation-delay: 0.8s"
            >
              <!-- Beautiful Custom Tulip Shapes -->
              <path
                d="M-9 -5 C-9 11, 9 11, 9 -5 C4 -1, 0 -8, 0 -8 C0 -8, -4 -1, -9 -5"
                fill="#f43f5e"
              />
              <path
                d="M-6 -5 C-6 7, 6 7, 6 -5 C3 -2, 0 -7, 0 -7 C0 -7, -3 -2, -6 -5"
                fill="#fda4af"
              />
            </g>
          </g>

          <!-- Centered Rose Block -->
          <g class="flower-group">
            <path
              d="M50 95 L50 38"
              fill="none"
              stroke="#22c55e"
              stroke-width="3"
              stroke-linecap="round"
              class="animate-stem"
              style="animation-delay: 0.4s"
            />
            <path
              d="M50 65 Q40 60, 44 55 Z"
              fill="#15803d"
              class="animate-leaf"
              style="animation-delay: 0.9s"
            />
            <path
              d="M50 55 Q60 50, 56 45 Z"
              fill="#15803d"
              class="animate-leaf"
              style="animation-delay: 1.1s"
            />
            <g
              transform="translate(50, 38)"
              class="animate-bloom"
              style="animation-delay: 1.2s"
            >
              <circle cx="0" cy="0" r="13" fill="#ec4899" />
              <circle cx="0" cy="0" r="9" fill="#f43f5e" />
              <circle cx="0" cy="0" r="5" fill="#e11d48" />
            </g>
          </g>
        </svg>
      </div>

      <!-- Action Button -->
      <button
        @click="closePopup"
        class="mt-6 w-full py-2.5 bg-gradient-to-r from-rose-400 to-pink-500 hover:from-rose-500 hover:to-pink-600 text-white rounded-full font-bold tracking-wide transition-all duration-300 shadow-md shadow-pink-100 active:scale-95 cursor-pointer"
      >
        Sweet! 💖
      </button>
    </div>
  </div>
</template>

<script setup>
defineProps({
  isOpen: Boolean,
});
const emit = defineEmits(["close"]);

const closePopup = () => {
  emit("close");
};
</script>

<style scoped>
/* Modal Fade-In */
@keyframes fade-in {
  from {
    opacity: 0;
    backdrop-filter: blur(0px);
  }
  to {
    opacity: 1;
    backdrop-filter: blur(6px);
  }
}
.animate-fade-in {
  animation: fade-in 0.35s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}

/* Modal Bounce Scale-Up */
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
  animation: scale-up 0.4s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
}

/* 1. Stem Drawing Animation */
.animate-stem {
  stroke-dasharray: 120;
  stroke-dashoffset: 120;
  animation: growStem 1.2s cubic-bezier(0.4, 0, 0.2, 1) forwards;
}
@keyframes growStem {
  to {
    stroke-dashoffset: 0;
  }
}

/* 2. Leaves Popping Animation */
.animate-leaf {
  transform: scale(0);
  transform-origin: 50px 85px;
  animation: popLeaf 0.4s cubic-bezier(0.34, 1.56, 0.64, 1) forwards;
}
@keyframes popLeaf {
  to {
    transform: scale(1);
  }
}

/* 3. Blooms Popping & Springing Open */
.animate-bloom {
  transform: scale(0);
  transform-origin: center;
  animation: bloomEffect 0.7s cubic-bezier(0.175, 0.885, 0.32, 1.275) forwards;
}
@keyframes bloomEffect {
  0% {
    transform: scale(0) rotate(-10deg);
  }
  70% {
    transform: scale(1.1) rotate(3deg);
  }
  100% {
    transform: scale(1) rotate(0deg);
  }
}

/* Decorative Ribbon Base Animation */
.animate-ribbon {
  transform: scale(0);
  transform-origin: 50px 95px;
  animation: popLeaf 0.35s ease-out 0.25s forwards;
}
</style>
