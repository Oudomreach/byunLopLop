<template>
  <div
    class="min-h-screen w-full bg-gradient-to-br from-rose-100 via-pink-200 to-amber-100 text-rose-950 flex items-center justify-center p-4 relative select-none"
  >
    <button
      @click="goBack"
      class="absolute top-6 left-6 text-rose-600/80 hover:text-rose-900 transition-all duration-200 flex items-center space-x-1.5 text-xs font-bold tracking-widest uppercase bg-white/60 backdrop-blur-md px-3.5 py-2 rounded-full border border-white/60 shadow-sm active:scale-95 z-40"
    >
      <span>← Menu</span>
    </button>

    <div
      class="w-full max-w-sm bg-white/85 backdrop-blur-md rounded-3xl p-8 border border-white/50 shadow-xl shadow-rose-200/20 text-center space-y-6 relative mx-4"
    >
      <!-- <h2 class="text-2xl font-serif font-bold text-rose-700">🧸</h2> -->
      <h2
        class="text-2xl font-serif font-bold text-rose-700 flex justify-center"
      >
        <img :src="pigAngry" alt="Pig" class="w-20 h-auto" />
      </h2>

      <div class="py-4 flex justify-center">
        <button
          @click="isOpen = !isOpen"
          class="text-8xl focus:outline-none transition-transform duration-300 active:scale-90 select-none cursor-pointer filter drop-shadow-sm"
          :class="{ 'animate-bounce': !isOpen, 'scale-110 rotate-6': isOpen }"
        >
          {{ isOpen ? "🎂" : "🎁" }}
        </button>
      </div>

      <transition name="pop-reveal">
        <div v-if="isOpen" class="space-y-3">
          <p class="font-serif italic text-xl font-extrabold text-pink-600">
            Surprise!! Happy Birthday!
          </p>
          <p class="text-sm text-rose-800 leading-relaxed font-medium">
            Here is a little virtual birthday cake baked with ♾️ lovesss and
            100% emoji 🙄 just for you! and thats why it is virtual cake! OMG me
            so stupiddd!
          </p>
          <p class="text-sm text-rose-800 leading-relaxed font-medium">
            Now blow the candle and make a wish! 🕯️✨
          </p>
        </div>
      </transition>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";
import pigAngryImg from "../assets/pigLove.gif";

const pigAngry = ref(pigAngryImg);
let interval;

onMounted(() => {
  // Change 3000 to the exact length of your GIF in milliseconds
  interval = setInterval(() => {
    // Adding a timestamp forces the browser to re-render the GIF from the start
    pigAngry.value = `${pigAngryImg}?t=${Date.now()}`;
  }, 3000);
});

onUnmounted(() => {
  clearInterval(interval);
});

const emit = defineEmits(["back"]);
const isOpen = ref(false);

const goBack = () => {
  emit("back");
};
</script>

<style scoped>
.pop-reveal-enter-active {
  transition: all 0.5s cubic-bezier(0.34, 1.56, 0.64, 1);
}
.pop-reveal-enter-from {
  opacity: 0;
  transform: translateY(15px) scale(0.9);
}
</style>
