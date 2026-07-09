<template>
  <Transition name="fade">
    <div
      v-if="isOpen"
      class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-rose-950/40 backdrop-blur-md animate-fade-in"
      @click.self="$emit('close')"
    >
      <div
        class="w-full max-w-sm bg-white/90 backdrop-blur-xl rounded-3xl border border-white/60 shadow-2xl p-6 text-center relative overflow-hidden transform transition-all duration-500 scale-100 flex flex-col items-center justify-center"
      >
        <!-- Close Button -->
        <button
          @click="$emit('close')"
          class="absolute top-4 right-4 text-rose-400 hover:text-rose-700 font-extrabold text-lg p-1 transition-colors"
        >
          ✕
        </button>

        <h3 class="text-2xl font-serif font-black text-rose-800 mb-1">
          Freshly Picked for U! 💐
        </h3>
        <p class="text-xs text-rose-600/80 mb-6 font-medium">
          A custom local bouquet that will never fade.
        </p>

        <!-- BOUQUET CONTAINER (Perfectly Centered Grid) -->
        <div
          class="bg-rose-50/50 border border-rose-100/60 rounded-2xl p-6 w-full flex justify-center items-center gap-8 min-h-[160px] shadow-inner mb-6"
        >
          <!-- DAISY ACCENT -->
          <div class="flex flex-col items-center justify-center relative group">
            <div
              class="w-14 h-14 relative flex items-center justify-center animate-spin-slow"
            >
              <!-- White Petals -->
              <div
                class="absolute w-3 h-12 bg-white rounded-full rotate-0"
              ></div>
              <div
                class="absolute w-3 h-12 bg-white rounded-full rotate-45"
              ></div>
              <div
                class="absolute w-3 h-12 bg-white rounded-full rotate-90"
              ></div>
              <div
                class="absolute w-3 h-12 bg-white rounded-full rotate-[135deg]"
              ></div>
              <!-- Yellow Pistil Center -->
              <div
                class="absolute w-5 h-5 bg-amber-400 rounded-full border border-amber-300 shadow-sm z-10"
              ></div>
            </div>
            <!-- Stem and Leaf -->
            <div
              class="w-1.5 h-16 bg-emerald-500 rounded-full mt-[-4px] relative flex justify-center"
            >
              <div
                class="absolute w-4 h-2 bg-emerald-400 rounded-full right-1 top-3 rotate-[30deg]"
              ></div>
            </div>
            <span
              class="text-xs font-bold text-rose-700/80 mt-2 bg-white px-2 py-0.5 rounded-full shadow-sm border border-rose-100"
              >Daisy</span
            >
          </div>

          <!-- TULIP ACCENT -->
          <div class="flex flex-col items-center justify-center relative group">
            <div
              class="w-12 h-14 relative flex items-end justify-center mb-1 overflow-visible"
            >
              <!-- Tulip Bud Layers -->
              <div
                class="absolute w-10 h-12 bg-pink-500 rounded-b-full rounded-t-2xl shadow-sm z-10"
              ></div>
              <div
                class="absolute w-6 h-11 bg-rose-400 rounded-b-full rounded-t-xl left-1 bottom-0 rotate-[-12deg]"
              ></div>
              <div
                class="absolute w-6 h-11 bg-rose-400 rounded-b-full rounded-t-xl right-1 bottom-0 rotate-[12deg]"
              ></div>
              <div
                class="absolute w-4 h-9 bg-pink-300 rounded-b-full rounded-t-lg z-20 bottom-0"
              ></div>
            </div>
            <!-- Stem and Leaf -->
            <div
              class="w-1.5 h-16 bg-emerald-500 rounded-full relative flex justify-center"
            >
              <div
                class="absolute w-5 h-2.5 bg-emerald-400 rounded-full left-1 top-4 rotate-[-35deg]"
              ></div>
            </div>
            <span
              class="text-xs font-bold text-rose-700/80 mt-2 bg-white px-2 py-0.5 rounded-full shadow-sm border border-rose-100"
              >Tulip</span
            >
          </div>
        </div>

        <p class="text-sm font-semibold italic text-rose-900 px-4">
          "Like these flowers, some configurations are hard-coded to stay
          bright."
        </p>
      </div>
    </div>
  </Transition>
</template>

<script setup>
defineProps({
  isOpen: Boolean,
});
defineEmits(["close"]);
</script>

<style scoped>
.animate-spin-slow {
  animation: spin 12s linear infinite;
}
@keyframes spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}
</style>
