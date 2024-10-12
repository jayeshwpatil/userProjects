<script setup>
import { RouterLink, RouterView } from 'vue-router'
import homeView from '@/views/HomeView.vue'
import dummyData from '@/dummyData.js'

import { ref } from 'vue'
// const dummyData = ref(dummyData)
</script>

<template>

  <homeView :dummyData="dummyData"></homeView>
</template>

<style>
a {
  text-decoration: none;
}
</style>
