<template>
  <header class="flex flex-row w-full items-center max-sm:justify-between bg-green-400 border-b-2 border-grey-400 relative text-xl text-black">
    <!-- Logo Section -->
    <div class="basis-1/4 flex items-center justify-start px-4">
      <img src="./assets/images/circle.png" alt="Logo" class="w-20 h-16 bg-transparent">
    </div>
    
    <div class="basis-1/4 max-sm:basis-auto"></div>

    <!-- Navigation Menu -->
    <nav :class="{
      'basis-1/2 flex flex-row items-center justify-end gap-4': !burger || burger,
      'max-sm:basis-auto max-sm:absolute max-sm:top-full max-sm:w-full max-sm:justify-center max-sm:flex-col max-sm:gap-0 max-sm:bg-white max-sm:px-0': burger,
      'max-sm:hidden': !burger
    }">
      <NuxtLink to="/" class="my-auto p-2 hover:bg-gray-500 hover:text-white max-sm:w-full max-sm:text-center max-sm:px-0 max-sm:pb-0">Home</NuxtLink>
      
      <!-- Labs Menu -->
      <div class="relative">
        <button @click="toggleLabs" class="my-auto p-2 hover:bg-gray-500 hover:text-white max-sm:w-full max-sm:text-center max-sm:px-0 max-sm:pb-0">
          Labs
        </button>
        <div v-if="labsOpen" class="flex flex-col absolute top-full bg-white text-black w-56 text-center max-sm:relative max-sm:w-full max-sm:bg-red-100">
          <NuxtLink to="/Lab3" class="my-auto p-2 border-b-2 border-black hover:bg-gray-500 hover:text-white max-sm:w-full max-sm:border-t-2 max-sm:text-center">Lab3</NuxtLink>
          <NuxtLink to="/Lab4" class="my-auto p-2 border-b-2 border-black hover:bg-gray-500 hover:text-white max-sm:w-full max-sm:text-center">Lab4</NuxtLink>
          <NuxtLink to="/Lab5" class="my-auto p-2 border-b-2 border-black hover:bg-gray-500 hover:text-white max-sm:w-full max-sm:text-center">Lab5</NuxtLink>
          <NuxtLink to="/Lab6" class="my-auto p-2 border-b-2 border-black hover:bg-gray-500 hover:text-white max-sm:w-full max-sm:border-black max-sm:text-center">Lab6</NuxtLink>
        </div>
      </div>
      
      <NuxtLink to="/login" class="my-auto p-2 hover:bg-gray-500 hover:text-white max-sm:w-full max-sm:border-b-2 max-sm:border-black max-sm:text-center">LogIn</NuxtLink>
      <NuxtLink to="/logout" class="my-auto p-2 hover:bg-gray-500 hover:text-white max-sm:w-full max-sm:border-b-2 max-sm:border-black max-sm:text-center">LogOut</NuxtLink>
    </nav>

    <!-- Burger Menu Icon -->
    <div v-if="!burger" @click="switch_burger" class="max-sm:flex max-sm:flex-col max-sm:mr-8 max-sm:justify-between max-sm:items-center max-sm:w-8 max-sm:h-6">
      <span class="h-[3px] w-full bg-blue-950"></span>
      <span class="h-[3px] w-full bg-blue-950"></span>
      <span class="h-[3px] w-full bg-blue-950"></span>
    </div>
    <div v-else @click="switch_burger" class="max-sm:flex max-sm:flex-col max-sm:mr-8 max-sm:justify-between max-sm:items-center max-sm:w-8 max-sm:h-6">
      <span class="h-[3px] w-full bg-blue-950 rotate-45 relative top-[9px]"></span>
      <span class="h-[3px] w-full bg-blue-950 opacity-0"></span>
      <span class="h-[3px] w-full bg-blue-950 relative bottom-3 rotate-[-45deg]"></span>
    </div>
  </header>

  <!-- Main Content -->
  <main class="p-5 flex bg-green-100 h-screen">
    <slot />
  </main>

  <!-- Footer Section -->
  <footer class="flex flex-row w-full bg-green-400 border-t-2 border-gray-400 items-center justify-center px-4 py-2 gap-4">
    <a href=""><img src="./assets/images/youtube.png" class="w-16 h-16"></a>
    <a href="https://github.com/"><img src="./assets/images/github.png" class="w-16 h-16"></a>
    <a href="https://www.facebook.com"><img src="./assets/images/Facebook.png" class="w-16 h-16 bg-transparent"></a>
  </footer>
</template>

<script setup lang="ts">
  // Google Tag Manager
  useHead({
    script: [
      {
        src: "https://www.googletagmanager.com/gtag/js?id=G-YM1HZ1JLP4",
        async: true
      },
      {
        innerHTML: `
          window.dataLayer = window.dataLayer || [];
          function gtag(){dataLayer.push(arguments);}
          gtag('js', new Date());
          gtag('config', 'G-YM1HZ1JLP4');
        `,
        type: "text/javascript"
      }
    ]
  });

  const burger = ref<boolean>(false);
  const labsOpen = ref<boolean>(false); // Состояние для подменю Labs

  const switch_burger = () => {
    burger.value = !burger.value;
  };

  // Функция для переключения состояния подменю Labs
  const toggleLabs = () => {
    labsOpen.value = !labsOpen.value;
  };
</script>

<style scoped>
</style>