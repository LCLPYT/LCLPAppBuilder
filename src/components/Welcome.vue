<script setup lang="ts">
import WelcomeNavItem from './WelcomeNavItem.vue';
import {onMounted, ref} from "vue";

defineProps<{}>()

const filePicker = ref(null as null | HTMLCanvasElement);
const errorDisplay = ref(null as null | HTMLDivElement);

function openFilePicker() {
  filePicker.value?.click();
}

function displayError(error: string) {
  if (errorDisplay.value) {
    errorDisplay.value.innerHTML = error;
  }
}

onMounted(() => {
  filePicker.value?.addEventListener('change', event => {
    const fileList = (<HTMLInputElement> event.target).files;
    if (!fileList || fileList.length <= 0) return;

    const file = fileList[0];
    if (!file.name.endsWith('.jsonc')) {
      displayError('Invalid installer. Please upload a .jsonc file.');
    } else {
      displayError('');
      console.log('success');
    }
  })
})
</script>

<template>
  <div class="flex flex-col justify-center h-full">
    <div class="container mx-auto md:px-16 xl:px-36">
      <div class="dark:bg-slate-800 rounded-lg px-6 py-8 ring-1 ring-slate-900/5 shadow-xl">
        <h1 class="text-slate-500 text-3xl font-bold mb-2">Application Builder</h1>
        <WelcomeNavItem label="Import installer" @click="openFilePicker">
          <div ref="errorDisplay" class="text-red-600 ml-5 mt-px inline-flex items-center" />
        </WelcomeNavItem>
        <WelcomeNavItem label="Create Installer" />

        <input type="file" ref="filePicker" accept=".jsonc" hidden />
      </div>
    </div>
  </div>
</template>
