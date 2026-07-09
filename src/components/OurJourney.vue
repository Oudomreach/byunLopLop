<template>
  <div
    v-if="isOpen"
    class="fixed inset-0 z-50 min-h-screen w-full bg-gradient-to-br from-rose-100 via-pink-100 to-amber-50 text-rose-950 overflow-y-auto scroll-smooth snap-y snap-mandatory font-sans select-none animate-fade-in"
    @scroll="handleScroll"
    ref="scrollContainer"
  >
    <!-- OPTION 2: PARALLAX BLURRED BOKEH ORBS LAYER -->
    <div class="absolute inset-0 overflow-hidden pointer-events-none z-0">
      <!-- Orb 1: Top Left Soft Pink -->
      <div
        class="absolute w-72 h-72 rounded-full bg-pink-300/25 blur-[90px] transition-transform duration-300 ease-out"
        :style="{
          transform: `translate(-10%, calc(15% + ${scrollY * -0.15}px))`,
        }"
      ></div>

      <!-- Orb 2: Middle Right Warm Amber -->
      <div
        class="absolute w-80 h-80 rounded-full bg-amber-200/30 blur-[100px] transition-transform duration-300 ease-out right-0"
        :style="{
          transform: `translate(20%, calc(45% + ${scrollY * -0.22}px))`,
        }"
      ></div>

      <!-- Orb 3: Deep Left Sweet Rose -->
      <div
        class="absolute w-96 h-96 rounded-full bg-rose-300/20 blur-[110px] transition-transform duration-300 ease-out left-0"
        :style="{
          transform: `translate(-30%, calc(70% + ${scrollY * -0.12}px))`,
        }"
      ></div>

      <!-- Orb 4: Bottom Right Dreamy Coral -->
      <div
        class="absolute w-80 h-80 rounded-full bg-pink-400/15 blur-[90px] transition-transform duration-300 ease-out right-[10%]"
        :style="{
          transform: `translate(0, calc(100% + ${scrollY * -0.28}px))`,
        }"
      ></div>
    </div>

    <!-- ANIMATED FIXED BACK MENU BUTTON -->
    <button
      @click="$emit('close')"
      class="fixed top-6 left-6 text-rose-600/80 hover:text-rose-900 flex items-center space-x-2 text-xs font-extrabold tracking-widest uppercase z-50 bg-white/80 backdrop-blur-md px-4 py-2.5 rounded-full border border-white/60 shadow-sm active:scale-90 transition-all duration-300 hover:shadow-md hover:bg-white hover:border-rose-200 group animate-btn-entry"
    >
      <span
        class="transform group-hover:-translate-x-1 transition-transform duration-300 ease-out"
        >←</span
      >
      <span class="tracking-widest">Back Menu</span>
    </button>

    <!-- Header Frame -->
    <div
      class="w-full max-w-xl mx-auto text-center pt-20 pb-12 snap-start relative z-10"
    >
      <h1
        class="text-4xl font-serif font-black tracking-tight bg-clip-text text-transparent bg-gradient-to-r from-rose-600 to-pink-600 drop-shadow-sm"
      >
        Our Journey Timeline
      </h1>
      <p
        class="text-rose-600/80 font-bold text-xs uppercase tracking-widest mt-2 animate-pulse"
      >
        Scroll Down ⬇️
      </p>
    </div>

    <!-- MAIN IMMERSIVE PICTURE TIMELINE LOOP -->
    <div
      class="w-full max-w-xl mx-auto flex flex-col items-center space-y-32 pb-40 relative z-10"
    >
      <div
        v-for="(moment, index) in memories"
        :key="moment.id"
        :ref="
          (el) => {
            if (el) cardRefs[index] = el;
          }
        "
        class="w-full max-w-sm snap-center flex flex-col items-center text-center space-y-4 animate-slide-up"
      >
        <!-- Polaroid Framework Block Component -->
        <div
          class="w-full aspect-[4/5] sm:aspect-square bg-white p-3 pb-12 shadow-xl rounded-sm border border-rose-100/40 transform transition-transform duration-500 hover:scale-[1.02] relative"
          :style="{ transform: `rotate(${index % 2 === 0 ? -2 : 2}deg)` }"
        >
          <img
            v-if="moment.imgSrc"
            :src="moment.imgSrc"
            :alt="moment.title"
            class="w-full h-full object-cover"
          />
          <div
            v-else
            class="w-full h-full bg-rose-50/60 flex flex-col items-center justify-center space-y-2 text-rose-300"
          >
            <span class="text-5xl">📸</span>
            <span class="text-[10px] font-mono uppercase tracking-widest"
              >[ Photo {{ index + 1 }} ]</span
            >
          </div>

          <span
            class="absolute bottom-3 right-4 font-mono text-[10px] text-rose-300 font-bold"
          >
            {{ String(index + 1).padStart(2, "0") }} / 10
          </span>
        </div>

        <!-- DYNAMIC DESCRIPTIONS TRANSITION PANEL -->
        <div
          class="space-y-1 max-w-xs px-4 transition-all duration-500 transform"
          :class="[
            activeIndex === index
              ? 'opacity-100 translate-y-0 scale-100 pointer-events-auto'
              : 'opacity-0 translate-y-2 scale-95 pointer-events-none',
          ]"
        >
          <div
            class="text-[10px] font-black tracking-widest text-rose-500 uppercase font-mono"
          >
            {{ moment.date }}
          </div>
          <h3 class="text-lg font-black text-rose-950 tracking-wide">
            {{ moment.title }}
          </h3>
          <p class="text-xs text-rose-800/80 font-medium leading-relaxed">
            {{ moment.description }}
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

defineProps({
  isOpen: Boolean,
});
defineEmits(["close"]);

const scrollContainer = ref(null);
const cardRefs = ref([]);
const activeIndex = ref(0);
const scrollY = ref(0); // Tracking precise pixels for math operations

const memories = ref([
  {
    id: 1,
    date: "Jan 12, 2025",
    title: "Memory Title One",
    description: "Add details or descriptions regarding this milestone photo.",
    imgSrc: "",
  },
  {
    id: 2,
    date: "Feb 14, 2025",
    title: "Memory Title Two",
    description: "Add details or descriptions regarding this milestone photo.",
    imgSrc: "",
  },
  {
    id: 3,
    date: "Mar 03, 2025",
    title: "Memory Title Three",
    description: "Add details or descriptions regarding this milestone photo.",
    imgSrc: "",
  },
  {
    id: 4,
    date: "Apr 19, 2025",
    title: "Memory Title Four",
    description: "Add details or descriptions regarding this milestone photo.",
    imgSrc: "",
  },
  {
    id: 5,
    date: "May 22, 2025",
    title: "Memory Title Five",
    description: "Add details or descriptions regarding this milestone photo.",
    imgSrc: "",
  },
  {
    id: 6,
    date: "Jun 30, 2025",
    title: "Memory Title Six",
    description: "Add details or descriptions regarding this milestone photo.",
    imgSrc: "",
  },
  {
    id: 7,
    date: "Jul 09, 2025",
    title: "Memory Title Seven",
    description: "Add details or descriptions regarding this milestone photo.",
    imgSrc: "",
  },
  {
    id: 8,
    date: "Aug 15, 2025",
    title: "Memory Title Eight",
    description: "Add details or descriptions regarding this milestone photo.",
    imgSrc: "",
  },
  {
    id: 9,
    date: "Sep 27, 2025",
    title: "Memory Title Nine",
    description: "Add details or descriptions regarding this milestone photo.",
    imgSrc: "",
  },
  {
    id: 10,
    date: "Oct 31, 2025",
    title: "Memory Title Ten",
    description: "Add details or descriptions regarding this milestone photo.",
    imgSrc: "",
  },
]);

const handleScroll = (event) => {
  // Update state logic for background parallax styling calculation variables
  scrollY.value = event.target.scrollTop;

  // Active item viewport checker evaluation routine loop
  const midPoint = window.innerHeight / 2;
  cardRefs.value.forEach((card, index) => {
    if (!card) return;
    const rect = card.getBoundingClientRect();
    const cardMid = rect.top + rect.height / 2;
    if (Math.abs(cardMid - midPoint) < rect.height / 2) {
      activeIndex.value = index;
    }
  });
};

onMounted(() => {
  setTimeout(() => {
    if (scrollContainer.value) {
      scrollY.value = scrollContainer.value.scrollTop;
    }
  }, 100);
});
</script>

<style scoped>
/* Clean display hide tags */
::-webkit-scrollbar {
  display: none;
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
    transform: translateY(30px);
    opacity: 0;
  }
  100% {
    transform: translateY(0);
    opacity: 1;
  }
}
.animate-slide-up {
  animation: slide-up 0.6s cubic-bezier(0.16, 1, 0.3, 1) forwards;
}

@keyframes btn-entry {
  0% {
    opacity: 0;
    transform: translateX(-15px);
  }
  100% {
    opacity: 1;
    transform: translateX(0);
  }
}
.animate-btn-entry {
  animation: btn-entry 0.5s cubic-bezier(0.16, 1, 0.3, 1) 0.2s both;
}
</style>
