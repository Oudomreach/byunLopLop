<template>
  <div
    v-if="isOpen"
    class="absolute inset-0 z-[100] flex items-center justify-center bg-rose-950/40 backdrop-blur-sm px-4 animate-fade-in"
    @click.self="closeModal"
  >
    <div
      class="bg-white/95 p-4 rounded-3xl shadow-2xl border-2 border-pink-300 max-w-lg text-center animate-bounce-slight font-sans text-stone-800 text-sm sm:text-base leading-relaxed space-y-1 max-h-[64vh] overflow-y-auto pr-1 select-text"
    >
      <h2
        class="text-3xl font-serif font-bold italic text-rose-500 mb-3 drop-shadow-sm"
      >
        You found the secret message!
      </h2>
      <p class="text-xl font-serif font-bold text-rose-500 mb-3 drop-shadow-sm">
        did i make it too obvious? o.O
      </p>

      <!-- <p class="text-lg font-serif font-bold text-rose-500 mb-3 drop-shadow-sm">
        Updated
      </p> -->
      <p class="text-rose-800 text-lg leading-relaxed text-start">
        I wasn't sure if I should write this, but I wanted to be honest. There
        were days when I felt so overwhelmed that I almost convinced myself to
        walk away. Not because I hated you, but because I cared more than I knew
        how to handle. I got lost in my own thoughts, questioned a lot of
        things, and wondered if letting go would be easier for both of us. I
        kept asking myself questions I never seemed to have answers to.
        Somewhere along the way, I started feeling like what we had was more
        than friendship. Maybe I misunderstood our closeness. Maybe I let my
        feelings grow faster than reality. I don't know. Sometimes I wondered if
        I should have stepped back before I became this attached. I wondered if
        staying so close was making it harder for me to accept what you had
        already told me. I kept trying to understand where I stood, and in doing
        so, I think I spent too much time searching for answers that only
        existed in my own head. This isn't me blaming you. You were honest with
        me about how you felt, and I respect that. I just wanted you to know
        that behind every smile, every game, every conversation, there was
        someone trying to balance loving you while also trying to learn how to
        let go. If there's one thing I hope you never carry from this message,
        it's guilt.
      </p>
      <p class="text-rose-800 text-lg leading-relaxed text-start">
        I don't regret meeting you.
      </p>
      <p class="text-rose-800 text-lg leading-relaxed text-start">
        I don't regret caring about you.
      </p>
      <p class="text-rose-800 text-lg leading-relaxed text-start">
        I just wanted to be honest bout how much this journey meant to me even
        this will never be me!
      </p>
      <p class="mb-4"></p>
      <p class="text-rose-800 text-lg leading-relaxed text-start">
        Thank you for every conversation, every game, every laugh, and even
        every misunderstanding that taught me something. Whether our paths stay
        close or slowly drift apart, I'm genuinely grateful that our lives
        crossed.
      </p>
      <p class="text-rose-800 text-lg leading-relaxed text-start">
        No matter what tomorrow looks like, No matter what the outcome take
        turn, even im no longer part of your daily routine, I will always be
        grateful for all the moment we shared and I hope today and everyday and
        many more day, reminds you how loved and appreciated u are. You truly
        one of the kind for me and
      </p>
      <p class="text-rose-800 text-lg leading-relaxed text-start">
        I hope you never doubt how lovable you are!
      </p>
      <p class="text-rose-800 text-lg leading-relaxed text-start">
        You are part of my daily routine!
      </p>
      <p class="text-rose-800 text-lg leading-relaxed text-start">
        You have become a habit I never want to break.
      </p>
      <p class="text-rose-800 text-lg leading-relaxed text-start">
        Your the best part of my day! well most of it 🤣 cuz me mostly upset
        with you and you have no fking clue xD
      </p>
      <p
        class="text-rose-800 font-bold text-lg leading-relaxed text-start italic"
      >
        Love you ❤️ and Happy Birthday Chheng 💚
      </p>
      <button
        @click="closeModal"
        class="mt-6 px-6 py-2.5 bg-gradient-to-r from-rose-400 to-pink-500 hover:from-rose-500 hover:to-pink-600 text-white rounded-full font-bold tracking-wide transition-all duration-300 shadow-md active:scale-95"
      >
        Close
      </button>
    </div>
  </div>
</template>

<script setup>
defineProps({
  isOpen: Boolean,
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
