<template>
  <!-- Fullscreen container using direct v-if without transition engine blockages -->
  <div
    v-if="isOpen"
    class="fixed inset-0 z-50 min-h-screen w-full bg-gradient-to-br from-rose-100 via-pink-200 to-amber-100 text-rose-950 flex flex-col items-center justify-center font-sans p-6 overflow-hidden animate-fade-in"
  >
    <!-- FIXED BACK BUTTON -->
    <button
      @click="$emit('close')"
      class="absolute top-6 left-6 text-rose-600/80 hover:text-rose-900 transition-all duration-300 flex items-center space-x-2 text-xs font-extrabold tracking-widest uppercase z-50 bg-white/70 backdrop-blur-md px-4 py-2.5 rounded-full border border-white/60 shadow-sm active:scale-95 group"
    >
      <span
        class="transform group-hover:-translate-x-0.5 transition-transform duration-200"
        >←</span
      >
      <span>Back Menu</span>
    </button>

    <!-- Decorative Ambient Particles -->
    <div
      class="absolute inset-0 pointer-events-none overflow-hidden z-0 opacity-40"
    >
      <span class="animate-pulse absolute top-[15%] right-[20%] text-3xl"
        >📸</span
      >
      <span
        class="animate-pulse absolute bottom-[25%] left-[10%] text-2xl"
        style="animation-delay: 1.5s"
        >✨</span
      >
    </div>

    <!-- MAIN TIMELINE WINDOW BOARD -->
    <div
      class="w-full max-w-md bg-white/85 backdrop-blur-md rounded-3xl border border-white/50 shadow-xl p-6 sm:p-8 space-y-6 z-10 flex flex-col max-h-[85vh] animate-slide-up"
    >
      <div class="text-center pb-2 border-b border-rose-100/60">
        <h1
          class="text-2xl sm:text-3xl font-serif font-extrabold italic bg-clip-text text-transparent bg-gradient-to-br from-rose-500 to-pink-500 drop-shadow-sm"
        >
          Our Journey Timeline
        </h1>
        <p class="text-rose-600/90 font-medium text-xs mt-1">
          How we built up our core routines
        </p>
      </div>

      <!-- Scrollable Timeline Track -->
      <div
        class="overflow-y-auto pr-1 space-y-6 flex-1 relative scrollbar-thin py-2"
      >
        <!-- Main Vertical Timeline Line -->
        <div
          class="absolute left-4 top-2 bottom-2 w-0.5 bg-gradient-to-b from-rose-300 via-pink-400 to-amber-200"
        ></div>

        <!-- Event Item 1 -->
        <div class="relative pl-10 group">
          <div
            class="absolute left-2.5 top-1.5 w-3 h-3 bg-rose-500 rounded-full ring-4 ring-rose-100 group-hover:scale-125 transition-transform duration-300"
          ></div>
          <span
            class="text-[10px] font-extrabold tracking-wider text-rose-500 uppercase"
            >Phase 01 — The Hello</span
          >
          <h4 class="text-base font-bold text-rose-950 mt-0.5">
            Where It Began
          </h4>
          <p class="text-sm text-rose-800/80 mt-1 leading-relaxed">
            A simple greeting that rolled down into late-night Discord
            discussions and shared playlist link swaps. Who knew a standard
            encounter would break into a full daily layout routine?
          </p>
        </div>

        <!-- Event Item 2 -->
        <div class="relative pl-10 group">
          <div
            class="absolute left-2.5 top-1.5 w-3 h-3 bg-pink-500 rounded-full ring-4 ring-pink-100 group-hover:scale-125 transition-transform duration-300"
          ></div>
          <span
            class="text-[10px] font-extrabold tracking-wider text-pink-500 uppercase"
            >Phase 02 — The Queue</span
          >
          <h4 class="text-base font-bold text-rose-950 mt-0.5">
            Duo Performance Unlocked
          </h4>
          <p class="text-sm text-rose-800/80 mt-1 leading-relaxed">
            Carrying, flashing, or getting completely lost on the map. Clocking
            countless gaming hours filled with running gags, tactical banter,
            and heavy mutual carries that secured our alignment.
          </p>
        </div>

        <!-- Event Item 3 -->
        <div class="relative pl-10 group">
          <div
            class="absolute left-2.5 top-1.5 w-3 h-3 bg-amber-400 rounded-full ring-4 ring-amber-100 group-hover:scale-125 transition-transform duration-300"
          ></div>
          <span
            class="text-[10px] font-extrabold tracking-wider text-amber-600 uppercase"
            >Phase 03 — Present Day</span
          >
          <h4 class="text-base font-bold text-rose-950 mt-0.5">
            The Blindbox Standard
          </h4>
          <p class="text-sm text-rose-800/80 mt-1 leading-relaxed">
            Now we are right here, turning memories into interactive application
            blocks. Always cheering for you through your layout routines and
            daily grinds, Chheng! 💚
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
defineProps({
  isOpen: Boolean,
});
defineEmits(["close"]);
</script>

<style scoped>
.scrollbar-thin::-webkit-scrollbar {
  width: 4px;
}
.scrollbar-thin::-webkit-scrollbar-track {
  background: transparent;
}
.scrollbar-thin::-webkit-scrollbar-thumb {
  background: rgba(244, 63, 94, 0.2);
  border-radius: 99px;
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

@keyframes slide-up {
  0% {
    transform: translateY(20px);
    opacity: 0;
  }
  100% {
    transform: translateY(0);
  }
}
.animate-slide-up {
  animation: slide-up 0.5s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}
</style>
