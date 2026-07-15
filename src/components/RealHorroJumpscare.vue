<template>
  <div class="flex flex-col items-center justify-center p-4 min-h-[20vh]">
    <button
      @click="goToMenu"
      class="px-8 py-4 bg-gradient-to-r from-pink-400 to-pink-500 hover:from-pink-500 hover:to-pink-600 text-white font-extrabold text-lg rounded-2xl shadow-lg transform hover:scale-105 active:scale-95 transition-all duration-200 cursor-pointer border border-pink-300 tracking-wide select-none"
    >
      ✨ Open Birthday Surprise Hub
    </button>
  </div>
</template>

<script setup>
const goToMenu = () => {
  // Directly redirects the user to the birthday menu router hash cleanly
  window.location.href = "https://byunloplop.netlify.app/#/menu";
};
</script>

<style scoped>
/* All jumpscare flashes, sound configurations, and horror stylesheets have been entirely cleared */
</style>
