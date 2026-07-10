<template>
  <div
    v-if="isOpen"
    class="fixed inset-0 z-50 min-h-screen w-full bg-gradient-to-br from-rose-100 via-pink-100 to-amber-50 text-rose-950 overflow-y-auto scroll-smooth snap-y snap-mandatory font-sans p-6 select-none animate-fade-in"
    @scroll="handleScroll"
    ref="scrollContainer"
  >
    <div class="absolute inset-0 overflow-hidden pointer-events-none z-0">
      <div
        class="absolute w-72 h-72 rounded-full bg-pink-300/25 blur-[90px] transition-transform duration-300 ease-out"
        :style="{
          transform: `translate(-10%, calc(15% + ${scrollY * -0.15}px))`,
        }"
      ></div>
      <div
        class="absolute w-80 h-80 rounded-full bg-amber-200/30 blur-[100px] transition-transform duration-300 ease-out right-0"
        :style="{
          transform: `translate(20%, calc(45% + ${scrollY * -0.22}px))`,
        }"
      ></div>
      <div
        class="absolute w-96 h-96 rounded-full bg-rose-300/20 blur-[110px] transition-transform duration-300 ease-out left-0"
        :style="{
          transform: `translate(-30%, calc(70% + ${scrollY * -0.12}px))`,
        }"
      ></div>
      <div
        class="absolute w-80 h-80 rounded-full bg-pink-400/15 blur-[90px] transition-transform duration-300 ease-out right-[10%]"
        :style="{
          transform: `translate(0, calc(100% + ${scrollY * -0.28}px))`,
        }"
      ></div>
    </div>

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

    <div
      class="w-full max-w-xl mx-auto text-center pt-20 pb-12 snap-start relative z-10"
    >
      <h1
        class="text-4xl font-serif font-black tracking-tight bg-clip-text text-transparent bg-gradient-to-r from-rose-600 to-pink-600 drop-shadow-sm"
      >
        Timeline
      </h1>
      <p
        class="text-rose-600/80 font-bold text-xs uppercase tracking-widest mt-2 animate-pulse"
      >
        Scroll Down ⬇️
      </p>
    </div>

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
        <div
          class="w-full aspect-video bg-white p-3 pb-12 shadow-xl rounded-sm border border-rose-100/40 transform transition-transform duration-500 hover:scale-[1.02] relative"
          :style="{ transform: `rotate(${index % 2 === 0 ? -2 : 2}deg)` }"
        >
          <template v-if="moment.src">
            <div
              v-if="moment.type === 'video'"
              class="w-full h-full relative group/video bg-neutral-900 rounded-xs overflow-hidden flex items-center justify-center"
            >
              <video
                :src="moment.src"
                autoplay
                loop
                :muted="isMuted"
                playsinline
                class="max-w-full max-h-full object-contain rounded-xs"
              ></video>

              <button
                @click.stop="isMuted = !isMuted"
                class="absolute bottom-2 left-2 z-30 bg-black/60 backdrop-blur-md text-white p-1.5 rounded-full border border-white/10 transition-all shadow"
              >
                <span class="text-[10px] flex items-center space-x-1">
                  <span>{{ isMuted ? "🔇" : "🔊" }}</span>
                </span>
              </button>
            </div>

            <div
              v-else
              class="w-full h-full bg-neutral-900 rounded-xs overflow-hidden flex items-center justify-center"
            >
              <img
                :src="moment.src"
                :alt="moment.title"
                class="max-w-full max-h-full object-contain block rounded-xs"
              />
            </div>
          </template>

          <div
            v-else
            class="w-full h-full bg-rose-50/60 flex flex-col items-center justify-center space-y-2 text-rose-300 rounded-xs"
          >
            <span class="text-5xl">📸</span>
            <span class="text-[10px] font-mono uppercase tracking-widest"
              >[ Item {{ index + 1 }} ]</span
            >
          </div>

          <span
            class="absolute bottom-3 right-4 font-mono text-[10px] text-rose-300 font-bold"
          >
            {{ String(index + 1).padStart(2, "0") }}
            <!-- {{ String(index + 1).padStart(2, "0") }} / {{ memories.length }} -->
          </span>
        </div>

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
          <p class="text-sm text-rose-800/80 font-medium leading-relaxed">
            {{ moment.description }}
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import photo1 from "../assets/photo/photo1.jpg";
import photo2 from "../assets/photo/photo2.png";
import photo3 from "../assets/photo/photo3.jpg";
import photo4 from "../assets/photo/photo4.jpg";
import photo5 from "../assets/photo/photo5.jpg";
import photo6 from "../assets/photo/photo6.jpg";
import vid1 from "../assets/photo/vid1.MOV";
import vid2 from "../assets/photo/vid2MOV.MOV";

defineProps({
  isOpen: Boolean,
});
defineEmits(["close"]);

const scrollContainer = ref(null);
const cardRefs = ref([]);
const activeIndex = ref(0);
const scrollY = ref(0);

// FIXED: Defined missing state engine variable for tracking video volumes
const isMuted = ref(true);

const memories = ref([
  {
    id: 1,
    type: "image",
    date: "July 01, 2026",
    title: "Deranked Partner <3",
    description: "😝😝😝",
    src: photo1,
  },
  {
    id: 2,
    type: "image",
    date: "Oct 24, 2025",
    title: "Genshin Moment",
    description: "I guess this is where everything started?",
    src: photo2,
  },
  {
    id: 3,
    type: "image",
    date: "Apr 16, 2025",
    title: "It Takes Two",
    description: "We play it take two after the heat argument! 🤣🤣🤣",
    src: photo3,
  },
  {
    id: 4,
    type: "image",
    date: "July 09, 2026",
    title: "Sleep Call?",
    description: "idk what to say!!!",
    src: photo4,
  },
  {
    id: 5,
    type: "image",
    date: "Dec 23, 2025",
    title: "BlindBox Unboxing",
    description: "First time you let me see ur round face and small eyes! 🤣",
    src: photo5,
  },
  {
    id: 6,
    type: "video",
    date: "Dec 31, 2025",
    title: "Bro got game!",
    description: "Countdown day btw XDDDD",
    src: vid1,
  },
  {
    id: 7,
    type: "video",
    date: "Jul 09, 2026",
    title: "LMAOOOOO 🤣🤣🤣",
    description: "Zorrrrry ><' 👉🏻👈🏻",
    src: vid2,
  },
  {
    id: 8,
    type: "image",
    date: "Jan 29, 2026",
    title: "Birth Sa Day",
    description: "Believe it or not this is My First ever Cake from a Girl!",
    src: photo6,
  },
]);

const handleScroll = (event) => {
  scrollY.value = event.target.scrollTop;

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
/* Completely hides scroll bars for total storytelling interface focus */
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
