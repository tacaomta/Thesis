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
import LabFooter from '../components/LabFooter.vue'
const props = defineProps({
  title: {
    type: String,
    default: ''
  },
  eyebrow: {
    type: String,
    default: ''
  }
})
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
  top: 10px;
  left: 64px;
  right: 64px;
  z-index: 2;
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
  top: 116px;
  left: 64px;
  right: 64px;
  bottom: 42px;
  z-index: 2;
  overflow: hidden;
}
</style>