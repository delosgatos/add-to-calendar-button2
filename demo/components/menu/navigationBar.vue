<script setup lang="ts">
import Menu from "@/components/menu/menu.vue";
import LightModeSwitch from "@/components/lightModeSwitch.vue";
import LightModeSwitchPlaceholder from "@/components/placeholders/lightModeSwitchPlaceholder.vue";
import { Bars3Icon, XMarkIcon } from '@heroicons/vue/24/outline';
import LogoGithub from "@/components/logos/logoGithub.vue";

const showMM = ref(false);

// blocking page scrolling, if the mobile menu is open
watch(showMM, val => {
  if (val) {
    document.documentElement.style.overflow = "hidden";
  } else {
    document.documentElement.style.overflow = "auto";
  }
});
</script>

<template>
  <!-- regular menu -->
  <nav class="ml-10 flex space-x-6 self-center text-white lg:ml-0 lg:space-x-3">
    <div class="hidden space-x-3 self-center lg:inline">
      <Menu />
    </div>
    <div class="hidden self-center py-2 px-3 leading-none lg:block">
      <ClientOnly>
        <LightModeSwitch />
        <template #fallback>
          <LightModeSwitchPlaceholder />
        </template>
      </ClientOnly>
    </div>
    <a class="hidden w-8 self-center py-2 leading-none text-white hover:text-black lg:block lg:w-6" target="_blank" rel="noopener" href="https://github.com/add2cal/add-to-calendar-button"><LogoGithub /></a>
    <Bars3Icon :class="{ hidden: showMM }" class="block h-10 w-10 cursor-pointer self-center rounded-md border border-transparent p-0 leading-none opacity-100 hover:border-white hover:p-1 hover:opacity-80 lg:hidden" @click="(showMM = !showMM)" />
  </nav>
  <!-- mobile menu -->
  <nav :class="{ hidden: !showMM }" class="fixed top-0 left-0 z-50 h-full w-full overflow-y-auto bg-gradient-to-tr from-primary via-primary to-primary-dark dark:via-primary-dark dark:to-primary-dark">
    <XMarkIcon class="fixed top-8 right-8 block h-10 w-10 cursor-pointer text-white hover:text-secondary" @click="(showMM = !showMM)" />
    <div class="grid grid-cols-1 gap-10 px-6 pt-24 pb-12 text-white">
      <Menu @close-mobile-menu="(showMM = false)" />
      <a class="mx-auto w-8 self-center py-2 leading-none opacity-80 hover:text-black hover:opacity-100" target="_blank" rel="noopener" href="https://github.com/add2cal/add-to-calendar-button"><LogoGithub /></a>
      <div class="self-center py-2 px-3 leading-none">
        <ClientOnly>
          <LightModeSwitch />
          <template #fallback>
            <LightModeSwitchPlaceholder />
          </template>
        </ClientOnly>
      </div>
    </div>
  </nav>
</template>
