<template>
  <div class="thesis-slide">
    <div class="top-line"></div>
    <header class="slide-header">
      <div v-if="eyebrow" class="eyebrow">{{ eyebrow }}</div>
      <h1 v-if="title">{{ title }}</h1>
    </header>
    <main class="slide-content">
      <slot />
    </main>
    <LabFooter />
  </div>
</template>

<script setup>
import { computed } from 'vue'
import { useNav } from '@slidev/client'
import LabFooter from '../components/LabFooter.vue'

const { currentFrontmatter } = useNav()

const title = computed(() => currentFrontmatter.value?.title || '')
const eyebrow = computed(() => currentFrontmatter.value?.eyebrow || '')
</script>

<style scoped>
.thesis-slide {
  position: relative;
  width: 100%;
  height: 100%;
  background: #f8fafb;
  color: #24313a;
  overflow: hidden;
  font-family: 'Inter', 'Segoe UI', sans-serif;
}
.top-line {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 4px;
  background: #173f5f;
}
.slide-header {
  position: absolute;
  top: 25px;
  left: 50px;
  right: 30px;
  z-index: 20;
}
.eyebrow {
  margin-bottom: 7px;
  color: #2a9d8f;
  font-size: 10px;
  font-weight: 700;
  letter-spacing: 0.16em;
}
.slide-header h1 {
  margin: 0;
  color: #173f5f;
  font-size: 30px;
  font-weight: 700;
  line-height: 1.15;
  letter-spacing: -0.02em;
}
 .slide-content {
  position: absolute;
  top: 100px;
  left: 30px;
  right: 30px;
  bottom: 45px;
  z-index: 1;
  overflow: hidden;
  width: auto;
  height: auto;

  min-width: 0;
  min-height: 0;

  overflow: hidden;
  box-sizing: border-box;
  /* border: 2px solid red; */
}
.slide-content,
.slide-content > :first-child {
  margin: 0;
  padding: 0;
}
.slide-content > :first-child {
  width: 100%;
  height: 100%;

  min-width: 0;
  min-height: 0;

  margin: 0;
  padding: 0;
}
</style>