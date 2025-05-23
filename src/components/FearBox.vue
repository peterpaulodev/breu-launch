<template>
  <div
    class="flex flex-col items-center justify-center h-screen relative z-10 overflow-hidden text-white"
  >
    <!-- Elementos visuais de fundo sombrios -->
    <div class="absolute inset-0 z-0 pointer-events-none">
      <div
        class="w-[800px] h-[800px] bg-purple-900/10 blur-3xl rounded-full absolute top-[-200px] left-[-200px] animate-pulse-slow"
      ></div>
      <div
        class="w-[600px] h-[600px] bg-indigo-800/10 blur-2xl rounded-full absolute bottom-[-150px] right-[-150px] animate-pulse-slower"
      ></div>
    </div>

    <!-- Card de input -->
    <transition name="fade">
      <div
        v-if="!submitted"
        class="bg-black/60 backdrop-blur-md p-8 rounded-2xl shadow-[0_0_40px_rgba(125,106,255,0.2)] border border-[#2d2d3a] w-11/12 sm:w-96 text-center space-y-6 z-10"
      >
        <p
          class="text-2xl sm:text-3xl font-unbounded tracking-wider text-gray-300 drop-shadow-md"
        >
          O que te consome?
        </p>
        <input
          v-model="fear"
          placeholder="Eu conheço seus medos..."
          class="w-full p-3 bg-[#15151a] border border-gray-700 rounded text-white placeholder-gray-500 focus:outline-none focus:ring-2 focus:ring-violet-700 shadow-inner shadow-black"
        />
        <button
          @click="submit"
          class="cursor-pointer w-full bg-white hover:bg-gray-100 text-gray-800 font-semibold py-2 px-4 border border-gray-400 rounded shadow"
        >
          Confessar
        </button>
      </div>
    </transition>

    <!-- Exibição do medo confessado -->
    <transition name="zoom">
      <div
        v-if="submitted"
        class="absolute top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 text-5xl sm:text-8xl text-zinc-100 animate-glow text-center w-full px-6 font-[HelpMe] tracking-widest drop-shadow-[0_0_20px_rgba(255,255,255,0.15)] z-10"
      >
        {{ fear }}
      </div>
    </transition>
  </div>
</template>

<script setup>
import { ref } from "vue";

const fear = ref("");
const submitted = ref(false);

function submit() {
  if (fear.value.trim()) submitted.value = true;
}
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.8s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.zoom-enter-active {
  transition: transform 1.5s ease, opacity 1.5s ease;
}
.zoom-enter-from {
  transform: scale(0.6);
  opacity: 0;
}

@keyframes glow {
  0%,
  100% {
    text-shadow: 0 0 10px rgba(206, 198, 202, 0.4),
      0 0 20px rgba(206, 198, 202, 0.3), 0 0 30px rgba(206, 198, 202, 0.2);
  }
  50% {
    text-shadow: 0 0 20px rgba(206, 198, 202, 0.6),
      0 0 30px rgba(206, 198, 202, 0.5), 0 0 40px rgba(206, 198, 202, 0.4);
  }
}

.animate-glow {
  animation: glow 3s infinite ease-in-out;
}

@keyframes pulse-slow {
  0%,
  100% {
    transform: scale(1);
    opacity: 0.4;
  }
  50% {
    transform: scale(1.1);
    opacity: 0.7;
  }
}

@keyframes pulse-slower {
  0%,
  100% {
    transform: scale(1);
    opacity: 0.3;
  }
  50% {
    transform: scale(1.2);
    opacity: 0.5;
  }
}

.animate-pulse-slow {
  animation: pulse-slow 6s infinite;
}
.animate-pulse-slower {
  animation: pulse-slower 10s infinite;
}
</style>

<style>
@import url("https://fonts.googleapis.com/css2?family=Saira+Condensed:wght@400;600&family=Unbounded:wght@500&display=swap");

.font-unbounded {
  font-family: "Unbounded", sans-serif;
}

.font-saira {
  font-family: "Saira Condensed", sans-serif;
}
</style>