<template>
  <div class="overview">
    <div class="journey">
      <div class="journey-axis"></div>
      <div class="journey-nodes">
        <button
          v-for="(item, index) in items"
          :key="item.id"
          class="journey-node"
          :class="{ active: selected === index }"
          :aria-label="item.title"
          @click="selectItem(index)"
        >
          <span>{{ item.id }}</span>
        </button>
      </div>
      <div class="journey-info">
        <div
          v-for="(item, index) in items"
          :key="`${item.id}-info`"
          class="journey-info-item"
          :class="{ active: selected === index }"
          @click="selectItem(index)"
        >
          <div class="journey-title">{{ item.title }}</div>
          <div class="journey-description">{{ item.paper }}</div>
        </div>
      </div>
    </div>
    <div class="detail-panel">
      <div class="detail-number">{{ currentItem.id }}</div>
      <div class="detail-content">
        <div class="detail-label">{{ currentItem.label }}</div>
        <div class="detail-paper">{{ currentItem.paper }}</div>
        <h2>{{ currentItem.question }}</h2>
        <p>{{ currentItem.contribution }}</p>
      </div>
    </div>
  </div>
</template>
<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'
const selected = ref(0)
const items = [
  {
    id: '01',
    label: 'BACKGROUND',
    title: 'Research Problem',
    paper: 'Why time-series data?',
    question: 'How can regulatory relationships be uncovered from limited and complex time-series gene expression data?',
    contribution: 'Define the research challenges, gaps, and objectives of the thesis.'
  },
  {
    id: '02',
    label: 'INFERENCE',
    title: 'Mutual Information-based GRN Inference',
    paper: 'Issue 1',
    question: 'Can a more informative representation improve the identification of regulatory relationships?',
    contribution: 'Develop a multiple-level discretization and mutual information-based inference method.'
  },
  {
    id: '03',
    label: 'REPRESENTATION LEARNING',
    title: 'Learning Representations for GRN Inference',
    paper: 'Issue 2',
    question: 'Can informative representations be learned automatically from time-series expression data?',
    contribution: 'Develop a representation learning framework for GRN inference.'
  },
  {
    id: '04',
    label: 'DATA SYNTHESIS',
    title: 'Synthetic Time-Series Data',
    paper: 'Issue 3',
    question: 'Can synthetic time-series expression data improve GRN inference performance?',
    contribution: 'Generate synthetic expression profiles using an autoencoder and validate them through GRN inference.'
  }
]
const currentItem = computed(() => items[selected.value])
const selectItem = (index) => {
  selected.value = index
}
const nextItem = () => {
  selected.value = (selected.value + 1) % items.length
}
const handleKeydown = (event) => {
  if (event.code === 'Space') {
    event.preventDefault()
    nextItem()
  }
}
onMounted(() => {
  window.addEventListener('keydown', handleKeydown)
})
onUnmounted(() => {
  window.removeEventListener('keydown', handleKeydown)
})
</script>
<style scoped>
.overview {
  position: relative;
  width: 100%;
  height: auto;
  display: flex;
  flex-direction: column;
  gap: 28px;
  box-sizing: border-box;
  padding: 8px 4px 0;
}
.journey {
  position: relative;
  width: 100%;
  flex: 0 0 auto;
  padding: 8px 8px 0;
  box-sizing: border-box;
  overflow: hidden;
}
.journey-axis {
  position: absolute;
  left: 25px;
  right: 25px;
  top: 25px;
  height: 2px;
  background: #dce4e9;
  z-index: 0;
}
.journey-nodes {
  position: relative;
  z-index: 2;
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.journey-node {
  width: 36px;
  height: 36px;
  flex: 0 0 36px;
  padding: 0;
  border: 2px solid #dce4e9;
  border-radius: 50%;
  background: #ffffff;
  color: #64748b;
  font-size: 10px;
  font-weight: 700;
  cursor: pointer;
  transition: all 0.2s ease;
  box-sizing: border-box;
}
.journey-node:hover {
  border-color: #2a9d8f;
  color: #2a9d8f;
  transform: scale(1.08);
}
.journey-node.active {
  border-color: #173f5f;
  background: #173f5f;
  color: #ffffff;
  box-shadow: 0 0 0 5px rgba(42, 157, 143, 0.12);
}
.journey-info {
  display: grid;
  grid-template-columns: repeat(4, minmax(0, 1fr));
  margin-top: 16px;
  width: 100%;
}
.journey-info-item {
  min-width: 0;
  padding: 0 14px;
  text-align: center;
  cursor: pointer;
}
.journey-info-item:first-child {
  padding-left: 0;
}
.journey-info-item:last-child {
  padding-right: 0;
}
.journey-title {
  color: #173f5f;
  font-size: 15px;
  font-weight: 700;
  line-height: 1.3;
}
.journey-description {
  margin-top: 5px;
  color: #64748b;
  font-size: 11px;
  line-height: 1.35;
}
.journey-info-item.active .journey-title {
  color: #2a9d8f;
}
.detail-panel {
  display: flex;
  align-items: flex-start;
  gap: 22px;
  width: 100%;
  box-sizing: border-box;
  padding: 24px 28px;
  border: 1px solid #dce4e9;
  border-left: 5px solid #2a9d8f;
  border-radius: 12px;
  background: #ffffff;
  margin-top: 0;
  flex: 0 0 auto;
}
.detail-number {
  flex: 0 0 auto;
  color: #173f5f;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 28px;
  font-weight: 700;
  line-height: 1.2;
}
.detail-content {
  min-width: 0;
  flex: 1;
}
.detail-label {
  color: #2a9d8f;
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 0.12em;
  line-height: 1.3;
}
.detail-paper {
  margin-top: 5px;
  color: #64748b;
  font-size: 12px;
  font-weight: 600;
  line-height: 1.35;
}
.detail-content h2 {
  margin: 9px 0 9px;
  color: #173f5f;
  font-size: 24px;
  font-weight: 700;
  line-height: 1.3;
}
.detail-content p {
  margin: 0;
  max-width: 900px;
  color: #64748b;
  font-size: 14px;
  line-height: 1.55;
}
</style>