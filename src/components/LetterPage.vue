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
      class="w-full max-w-md bg-stone-50/95 backdrop-blur-sm rounded-2xl p-6 sm:p-8 border-r-4 border-b-4 border-stone-300/60 shadow-2xl space-y-6 mx-4 relative overflow-hidden"
    >
      <div
        class="absolute top-4 right-4 text-3xl opacity-30 select-none pointer-events-none rotate-12"
      >
        R 🩷
      </div>

      <div class="border-b border-rose-200/60 pb-3">
        <h3
          class="text-2xl font-serif italic font-bold text-rose-700 tracking-wide"
        >
          To Chheng,
        </h3>
      </div>

      <div
        class="lowercase font-sans text-stone-800 text-sm sm:text-base leading-relaxed space-y-4 max-h-[48vh] overflow-y-auto pr-1 select-text"
      >
        <p>
          i wanted to write you something a little more personal for your
          birthday.
        </p>
        <p>
          it is been about a year since we talked to know each other, and im
          really glad we did, i just wish i could have talk to u sooner. Thank
          you for being yourself, for the kindness you show, the laughs we have
          shared, the argument i never win and the little moments that always
          make my day a whole lot better.
        </p>
        <p>
          i hope this new chapter of your life brings you happiness, good
          health, and opportunities that make you excited for whats ahead. You
          deserve to be proud of everything you're working toward for.
        </p>
        <p>
          Thank you for every conversation, every game, every laugh, and even
          every misunderstanding that taught me something. Whether our paths
          stay close or slowly drift apart, I'm genuinely grateful that our
          lives crossed.
        </p>
        <p>
          no matter how fast time flies by, no matter where life takes you, i
          will always be cheering you on, even i cannot be there in person, a
          part of me will always be wishing the best for you. Happy Birthday,
          and I hope today treats you as well as you deserve
        </p>
        <p>
          No matter what tomorrow looks like, even there is no more me in ur
          daily routine, I hope today reminds you how loved and appreciated u
          are. Happy Birthday Chheng 💚
        </p>
      </div>

      <div
        class="text-right border-t border-rose-200/60 pt-4 font-serif italic text-rose-700 font-bold"
      >
        <p
          class="text-xs text-stone-400 not-italic font-sans tracking-wider mb-1"
        >
          From,
        </p>
        <p class="text-lg">Chicken 🐔</p>
      </div>
    </div>
  </div>
</template>

<script setup>
const emit = defineEmits(["back"]);

const goBack = () => {
  emit("back");
};
</script>
