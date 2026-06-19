<script setup lang="ts">
// load the computed and ref.

import { computed, ref } from 'vue'

// the variance is decleared and a number 0 is in it as a changable value.
const count = ref<number>(0)
// coutMessage changes automatically whenever cout.value is changed
const countMessage = computed(() => '回数: ' + count.value)
</script>

<template>
  <div>
    <!-- {{  }} displays the calues inside on the screen  -->
    <div>{{ countMessage }}</div>
    <!-- @click specifies a process conducted when button is clicked -->
    <button @click="count++">クリック！</button>
    <button @click="count = 0">リセット！</button>
  </div>
</template>

<style></style>