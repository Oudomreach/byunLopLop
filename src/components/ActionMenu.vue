<template>
  <div
    class="min-h-screen w-full bg-gradient-to-br from-rose-100 via-pink-200 to-amber-100 text-rose-950 flex items-center justify-center font-sans p-6 overflow-hidden relative"
  >
    <!-- Background Details -->
    <div
      class="absolute inset-0 pointer-events-none overflow-hidden z-0 opacity-60"
    >
      <span class="animate-pulse absolute top-[10%] left-[20%] text-3xl"
        >✨</span
      >
      <span
        class="animate-pulse absolute bottom-[15%] right-[25%] text-2xl"
        style="animation-delay: 1s"
        >💖</span
      >
      <span
        class="animate-pulse absolute top-[40%] right-[10%] text-4xl"
        style="animation-delay: 0.5s"
        >🌸</span
      >
    </div>

    <!-- Main Container -->
    <div
      class="w-full max-w-[320px] sm:max-w-md bg-white/85 backdrop-blur-md rounded-3xl border border-white/50 shadow-xl shadow-rose-200/20 p-8 space-y-8 z-10 text-center animate-slide-up"
    >
      <!-- Header -->
      <div class="space-y-2">
        <h1
          class="text-3xl sm:text-4xl font-serif font-extrabold italic tracking-tight bg-clip-text text-transparent bg-gradient-to-br from-rose-500 to-pink-500 drop-shadow-sm"
        >
          What's Next?
        </h1>
        <p class="text-rose-600/90 font-medium text-sm px-4">
          Choose a surprise below to continue the celebration!
        </p>
      </div>

      <!-- Navigation Buttons -->
      <div class="flex flex-col gap-4 w-full">
        <!-- Button 1: Gift -->
        <button
          @click="navigateTo('/gift')"
          class="group relative w-full px-6 py-5 bg-white/60 hover:bg-white/90 border-2 border-pink-200/60 hover:border-pink-400/80 rounded-2xl shadow-sm hover:shadow-md hover:shadow-pink-200 transition-all duration-300 flex items-center justify-between overflow-hidden active:scale-[0.98]"
        >
          <div class="flex items-center space-x-4">
            <span
              class="text-3xl group-hover:scale-110 transition-transform duration-300 origin-bottom"
              >🎁</span
            >
            <span
              class="text-lg font-bold text-rose-700 tracking-wide font-sans"
              >Open Gift</span
            >
          </div>
          <svg
            class="w-6 h-6 text-pink-400 opacity-0 group-hover:opacity-100 transform translate-x-[-10px] group-hover:translate-x-0 transition-all duration-300"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M14 5l7 7m0 0l-7 7m7-7H3"
            ></path>
          </svg>
        </button>

        <!-- Button 2: Letter -->
        <button
          @click="navigateTo('/letter')"
          class="group relative w-full px-6 py-5 bg-white/60 hover:bg-white/90 border-2 border-pink-200/60 hover:border-pink-400/80 rounded-2xl shadow-sm hover:shadow-md hover:shadow-pink-200 transition-all duration-300 flex items-center justify-between overflow-hidden active:scale-[0.98]"
        >
          <div class="flex items-center space-x-4">
            <span
              class="text-3xl group-hover:scale-110 transition-transform duration-300 origin-bottom"
              >💌</span
            >
            <span
              class="text-lg font-bold text-rose-700 tracking-wide font-sans"
              >Read Letter</span
            >
          </div>
          <svg
            class="w-6 h-6 text-pink-400 opacity-0 group-hover:opacity-100 transform translate-x-[-10px] group-hover:translate-x-0 transition-all duration-300"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M14 5l7 7m0 0l-7 7m7-7H3"
            ></path>
          </svg>
        </button>

        <!-- Button 3: Flowers -->
        <button
          @click="navigateTo('/flowers')"
          class="group relative w-full px-6 py-5 bg-white/60 hover:bg-white/90 border-2 border-pink-200/60 hover:border-pink-400/80 rounded-2xl shadow-sm hover:shadow-md hover:shadow-pink-200 transition-all duration-300 flex items-center justify-between overflow-hidden active:scale-[0.98]"
        >
          <div class="flex items-center space-x-4">
            <span
              class="text-3xl group-hover:scale-110 transition-transform duration-300 origin-bottom"
              >🌷</span
            >
            <span
              class="text-lg font-bold text-rose-700 tracking-wide font-sans"
              >See Flowers</span
            >
          </div>
          <svg
            class="w-6 h-6 text-pink-400 opacity-0 group-hover:opacity-100 transform translate-x-[-10px] group-hover:translate-x-0 transition-all duration-300"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M14 5l7 7m0 0l-7 7m7-7H3"
            ></path>
          </svg>
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { useRouter } from "vue-router";

const router = useRouter();

const navigateTo = (path) => {
  // Update these paths in your router/index.js configuration
  router.push(path);
};
</script>

<style scoped>
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
</style>
