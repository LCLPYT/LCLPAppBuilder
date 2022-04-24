<script setup lang="ts">
import {ChevronRightIcon} from '@heroicons/vue/solid';

defineProps<{
  label: string
}>()
</script>

<template>
  <div class="flex align-center py-1 text-slate-500 hover:text-slate-400 cursor-pointer transition">
    <ChevronRightIcon class="h-8 aspect-square" />
    <div class="bold text-2xl">{{label}}</div>
    <slot />
  </div>
</template>