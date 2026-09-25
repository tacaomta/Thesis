<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

const visibleCount = ref(0)

const metrics = [
  {
    number: '01',
    name: 'Precision',
    description: 'How accurately predicted regulatory interactions correspond to true interactions.',
    symbol: 'P'
  },
  {
    number: '02',
    name: 'Recall',
    description: 'How completely the inferred network recovers true regulatory interactions.',
    symbol: 'R'
  },
  {
    number: '03',
    name: 'Structural Accuracy',
    description: 'How well the inferred network reproduces the true regulatory structure.',
    symbol: 'SA'
  },
  {
    number: '04',
    name: 'Dynamic Accuracy',
    description: 'How well the inferred network captures the observed gene-expression dynamics.',
    symbol: 'DA'
  }
]

function handleKeydown(event) {
  if (event.code !== 'Space') return

  event.preventDefault()
  event.stopPropagation()

  if (visibleCount.value < metrics.length) {
    visibleCount.value += 1
  }
}

onMounted(() => {
  window.addEventListener('keydown', handleKeydown, true)
})

onBeforeUnmount(() => {
  window.removeEventListener('keydown', handleKeydown, true)
})
</script>

<template>
  <div class="metrics-slide">
    <div class="metrics-grid">
      <div
        v-for="(metric, index) in metrics"
        :key="metric.name"
        class="metric-card"
        :class="{ visible: index < visibleCount }"
      >
        <div class="metric-top">
          <span class="metric-number">{{ metric.number }}</span>
          <span class="metric-symbol">{{ metric.symbol }}</span>
        </div>

        <h2>{{ metric.name }}</h2>

        <p>{{ metric.description }}</p>
      </div>
    </div>

    <div class="reminder">
      <span class="reminder-line"></span>
      <span>
        Four complementary metrics are used to evaluate the inferred GRN.
      </span>
    </div>
  </div>
</template>

<style scoped>
.metrics-slide {
  width: 100%;
  height: 100%;
  box-sizing: border-box;

  display: flex;
  flex-direction: column;
  justify-content: center;

  padding: 8px 20px 0;
}

/* ─────────────────────────────
   4 metric cards
   ───────────────────────────── */

.metrics-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 18px;
  width: 100%;
}

.metric-card {
  min-width: 0;
  box-sizing: border-box;

  padding: 18px 18px 20px;

  border: 1px solid #dce4e9;
  border-radius: 12px;

  background: #ffffff;

  opacity: 0;
  transform: translateY(8px);

  transition:
    opacity 0.35s ease,
    transform 0.35s ease;
}

.metric-card.visible {
  opacity: 1;
  transform: translateY(0);
}

/* Top row */

.metric-top {
  display: flex;
  align-items: center;
  justify-content: space-between;

  margin-bottom: 16px;
}

.metric-number {
  color: #2a9d8f;

  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 12px;
  font-weight: 700;
  letter-spacing: 0.08em;
}

.metric-symbol {
  display: flex;
  align-items: center;
  justify-content: center;

  min-width: 38px;
  height: 28px;
  padding: 0 8px;

  border-radius: 6px;

  background: #f1f5f7;

  color: #20639b;

  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 11px;
  font-weight: 700;
}

/* Metric name */

.metric-card h2 {
  margin: 0;

  color: #173f5f;

  font-size: 18px;
  line-height: 1.2;
  font-weight: 700;
}

/* Description */

.metric-card p {
  margin: 10px 0 0;

  color: #64748b;

  font-size: 12px;
  line-height: 1.45;
}

/* ─────────────────────────────
   Bottom reminder
   ───────────────────────────── */

.reminder {
  display: flex;
  align-items: center;

  gap: 10px;

  margin-top: 22px;

  color: #64748b;

  font-size: 12px;
  line-height: 1.3;
}

.reminder-line {
  width: 28px;
  height: 2px;

  flex: 0 0 auto;

  background: #2a9d8f;
}

/* ─────────────────────────────
   Responsive
   ───────────────────────────── */

@media (max-width: 900px) {
  .metrics-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}
</style>