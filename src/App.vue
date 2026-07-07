<script setup>
import { ref } from "vue";
import LandingPage from "./components/LandingPage.vue";
import MenuPage from "./components/MenuPage.vue";
import GiftPage from "./components/GiftPage.vue";
import LetterPage from "./components/LetterPage.vue";
import FlowerPage from "./components/FlowerPage.vue";
import MenuPage2 from "./components/MenuPage2.vue";
import FlowerPopup from "./components/FlowerPopup.vue";

// Tracks which view to display on screen ('lock-flow' or 'menu-flow')
const currentPage = ref("lock-flow");

// Tracks which sub-option the user clicked inside the menu page ('gift', 'letter', 'flowers')
const activeSubPage = ref("");

const handleMenuNavigation = () => {
  currentPage.value = "menu-flow";
};

const handleOptionSelected = (choice) => {
  activeSubPage.value = choice;
};

// Clear sub-page state to return back to core deck safely
const handleBackToMenu = () => {
  activeSubPage.value = "";
};

const handleBackToLock = () => {
  activeSubPage.value = "";
  currentPage.value = "lock-flow";
};
</script>

<template>
  <div class="app-wrapper">
    <transition name="page-fade" mode="out-in">
      <KeepAlive>
        <LandingPage
          v-if="currentPage === 'lock-flow'"
          key="landing-screen"
          @go-to-menu="handleMenuNavigation"
        />

        <GiftPage
          v-else-if="currentPage === 'menu-flow' && activeSubPage === 'gift'"
          key="gift-subpage"
          @back="handleBackToMenu"
        />

        <LetterPage
          v-else-if="currentPage === 'menu-flow' && activeSubPage === 'letter'"
          key="letter-subpage"
          @back="handleBackToMenu"
        />

        <FlowerPage
          v-else-if="currentPage === 'menu-flow' && activeSubPage === 'flowers'"
          key="flowers-subpage"
          @back="handleBackToMenu"
        />

        <MenuPage2
          v-else-if="currentPage === 'menu-flow' && !activeSubPage"
          key="menu-deck"
          @option-selected="handleOptionSelected"
          @back-to-lock="handleBackToLock"
        />
      </KeepAlive>
    </transition>
  </div>
</template>

<style>
body {
  margin: 0;
  padding: 0;
  background-color: #fce7f3;
}

.page-fade-enter-active,
.page-fade-leave-active {
  transition: opacity 0.4s ease-in-out, transform 0.4s ease-in-out;
}
.page-fade-enter-from {
  opacity: 0;
  transform: translateY(8px);
}
.page-fade-leave-to {
  opacity: 0;
  transform: translateY(-8px);
}
</style>
