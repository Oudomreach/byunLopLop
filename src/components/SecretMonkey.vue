<template>
  <div
    v-if="isOpen"
    class="absolute inset-0 z-[101] flex items-center justify-center bg-black/60 backdrop-blur-sm px-4 animate-fade-in"
    @click.self="closeModal"
  >
    <div
      class="bg-white p-6 rounded-3xl shadow-2xl border-2 border-amber-300 max-w-sm w-full text-center animate-bounce-slight flex flex-col items-center"
    >
      <span class="text-5xl text-rose-600/80 mb-4 block animate-bounce-slight"
        >u thought u escaped this? lol</span
      >
      <div
        class="w-full aspect-square rounded-2xl overflow-hidden bg-amber-50 border border-rose-800 mb-4 flex items-center justify-center relative shadow-inner"
      >
        <img
          :src="monkeyImg"
          alt="Secret Monkey"
          class="w-full h-full object-cover"
        />
      </div>
      <span class="text-3xl font-mono block mb-4">🙈 🙉 🙊</span>
      <button
        @click="closeModal"
        class="w-full py-2.5 bg-gradient-to-r from-amber-400 to-orange-500 hover:from-amber-500 hover:to-orange-600 text-white rounded-full font-bold tracking-wide transition-all duration-300 shadow-md active:scale-95 cursor-pointer"
      >
        Close
      </button>
    </div>
  </div>
</template>

<script setup>
defineProps({
  isOpen: Boolean,
  monkeyImg: String,
});

const emit = defineEmits(["close"]);

const closeModal = () => {
  emit("close");
};
</script>

<style scoped>
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
