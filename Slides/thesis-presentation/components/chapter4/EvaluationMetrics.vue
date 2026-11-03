<script setup>
import { ref, computed, watch, onMounted, onBeforeUnmount } from 'vue'
import { useNav } from '@slidev/client'

const { currentPage } = useNav()
const isExporting =
  typeof window !== 'undefined' &&
  (
    window.location.pathname.startsWith('/export') ||
    new URLSearchParams(window.location.search).has('print') ||
    new URLSearchParams(window.location.search).has('range')
  )

watch(currentPage, () => {
  if (isExporting) {
    visibleCount.value = totalItems
  } else {
    visibleCount.value = 0
  }
})

const visibleCount = ref(0)

const metrics = [
  {
    number: '01',
    name: 'Precision',
    description: 'How accurately predicted regulatory interactions correspond to true interactions.',
    symbol: 'P',
    corner: 'corner-br'
  },
  {
    number: '02',
    name: 'Recall',
    description: 'How completely the inferred network recovers true regulatory interactions.',
    symbol: 'R',
    corner: 'corner-bl'
  },
  {
    number: '03',
    name: 'Structural Accuracy',
    description: 'How well the inferred network reproduces the true regulatory structure.',
    symbol: 'SA',
    corner: 'corner-tr'
  },
  {
    number: '04',
    name: 'Dynamics Accuracy',
    description: 'How well the inferred network captures the observed gene-expression dynamics.',
    symbol: 'DA',
    corner: 'corner-tl'
  }
]

const totalItems = metrics.length

const progressDeg = computed(() => (visibleCount.value / totalItems) * 360)

function handleKeydown(event) {
  if (event.code !== 'Space') return

  event.preventDefault()
  event.stopPropagation()

  if (visibleCount.value < totalItems) {
    visibleCount.value += 1
  }
}

onMounted(() => {
  if (isExporting) {
    visibleCount.value = totalItems
  }
  window.addEventListener('keydown', handleKeydown, true)
})

onBeforeUnmount(() => {
  window.removeEventListener('keydown', handleKeydown, true)
})
</script>

<template>
  <div class="metrics-slide">

    <div class="metrics-grid">

      <Transition
        v-for="(metric, index) in metrics"
        :key="metric.name"
        name="reveal"
      >
        <section
          v-if="visibleCount >= index + 1"
          class="metric-card"
          :class="metric.corner"
        >
          <div class="card-header">
            <span class="number">{{ metric.number }}</span>
            <span class="metric-symbol">{{ metric.symbol }}</span>
          </div>

          <h2>{{ metric.name }}</h2>

          <p>{{ metric.description }}</p>
        </section>
      </Transition>

      <!-- =========================
           CENTER — doubles as a
           pie-chart progress indicator:
           each quarter fills in, using the
           same teal as the other progress
           dots throughout the deck, as one
           item is revealed via SPACE.
      ========================== -->

      <div
        class="center-gear"
        :style="{ background: `conic-gradient(#2a9d8f ${progressDeg}deg, #ffffff ${progressDeg}deg 360deg)` }"
        role="img"
        :aria-label="`${visibleCount} of ${totalItems} metrics revealed`"
      >
        <div class="center-gear-inner">
          <svg viewBox="0 0 24 24" class="gear-icon" aria-hidden="true">
            <circle cx="12" cy="12" r="8.5" />
            <path d="M12 7.5v5l3.2 1.9" />
          </svg>
        </div>
      </div>

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
}

/* =========================
   GRID
========================= */

.metrics-grid {
  flex: 1;
  min-height: 0;

  position: relative;

  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  grid-template-rows: repeat(2, minmax(0, 1fr));

  gap: 5px;
}

/* =========================
   CARD
========================= */

.metric-card {
  min-width: 0;
  min-height: 0;

  position: relative;

  padding: 18px 18px 20px;
  box-sizing: border-box;

  display: flex;
  flex-direction: column;

  background: #ffffff;
  border: 1px solid #dce4e9;
  border-top: 4px solid #173f5f;
  border-radius: 10px;

  box-shadow: 0 4px 12px rgba(23, 63, 95, 0.05);
}

.metrics-grid > :nth-child(1) .metric-card,
.metric-card:nth-of-type(1) {
  border-top-color: #20639b;
}

/* =========================
   INNER CORNERS — rounded away
   from the center so the four
   quarter-circle cuts together
   form one full circle at the
   middle of the 2x2 grid.
========================= */

:root {
  --notch-r: 100px;
}

/* Card 01 — góc trong là bottom-right */
.corner-br {
  border-top-color: #20639b;

  border-bottom-right-radius: 0;
}
.corner-br::after {
  content: '';
  position: absolute;
  right: 0;
  bottom: 0;
  width: var(--notch-r);
  height: var(--notch-r);
  background: radial-gradient(
    circle at bottom right,
    transparent var(--notch-r),
    #f8fafb calc(var(--notch-r) + 1px)
  );
  pointer-events: none;
  
}

/* Card 02 — góc trong là bottom-left */
.corner-bl {
  border-top-color: #2a9d8f;

  border-bottom-left-radius: 0;
}
.corner-bl::after {
  content: '';
  position: absolute;
  left: 0;
  bottom: 0;
  width: var(--notch-r);
  height: var(--notch-r);
  background: radial-gradient(
    circle at bottom left,
    transparent var(--notch-r),
    #f8fafb calc(var(--notch-r) + 1px)
  );
  pointer-events: none;
}

/* Card 03 — góc trong là top-right */
.corner-tr {
  border-top-color: #e9c46a;

  border-top-right-radius: 0;
}
.corner-tr::after {
  content: '';
  position: absolute;
  right: 0;
  top: 0;
  width: var(--notch-r);
  height: var(--notch-r);
  background: radial-gradient(
    circle at top right,
    transparent var(--notch-r),
    #f8fafb calc(var(--notch-r) + 1px)
  );
  pointer-events: none;
}

/* Card 04 — góc trong là top-left */
.corner-tl {
  border-top-color: #7a5af8;

  border-top-left-radius: 0;
  padding-left: 30px;
}
.corner-tl::after {
  content: '';
  position: absolute;
  left: 0;
  top: 0;
  width: var(--notch-r);
  height: var(--notch-r);
  background: radial-gradient(
    circle at top left,
    transparent var(--notch-r),
    #f8fafb calc(var(--notch-r) + 1px)
  );
  pointer-events: none;
}

/* =========================
   CENTER + PIE PROGRESS

   The outer ring's background is a
   conic-gradient driven by visibleCount,
   filled with the same teal used for the
   progress dots elsewhere in the deck
   (#2a9d8f). The inner white disk + icon
   sit on top, unaffected by the fill.
========================= */

.center-gear {
  position: absolute;

  top: 50%;
  left: 50%;

  width: 100px;
  height: 100px;

  transform: translate(-50%, -50%);

  display: flex;
  align-items: center;
  justify-content: center;

  border-radius: 50%;
  border: 1.5px solid #dce4e9;

  box-shadow:
    0 6px 18px rgba(23, 63, 95, 0.12),
    0 2px 6px rgba(23, 63, 95, 0.06);

  z-index: 5;

  transition: background 0.4s ease;
}

.center-gear-inner {
  width: 68px;
  height: 68px;

  display: flex;
  align-items: center;
  justify-content: center;

  border-radius: 50%;

  background: #ffffff;
  box-shadow: inset 0 0 0 1px rgba(23, 63, 95, 0.06);
}

.gear-icon {
  width: 34px;
  height: 34px;

  fill: none;
  stroke: #173f5f;
  stroke-width: 1.6;
  stroke-linecap: round;
  stroke-linejoin: round;
}

@media (prefers-reduced-motion: reduce) {
  .center-gear {
    transition: none;
  }
}

/* =========================
   HEADER
========================= */

.card-header {
  display: flex;
  align-items: center;
  justify-content: space-between;

  margin-bottom: 16px;
}

.number {
  flex: 0 0 auto;

  color: #2a9d8f;
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 14px;
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

.metric-card h2 {
  margin: 0;

  color: #173f5f;
  font-size: 18px;
  line-height: 1.2;
  font-weight: 700;
}

.metric-card p {
  margin: 10px 0 0;

  color: #64748b;
  font-size: 12px;
  line-height: 1.45;
}

/* =========================
   REVEAL
========================= */

.reveal-enter-active {
  transition:
    opacity 0.35s ease,
    transform 0.35s ease;
}

.reveal-enter-from {
  opacity: 0;
  transform: translateY(10px);
}

/* =========================
   RESPONSIVE
========================= */

@media (max-width: 850px) {
  .metrics-grid {
    grid-template-columns: 1fr;
    grid-template-rows: auto;
    overflow-y: auto;
  }

  .metric-card {
    min-height: 200px;
  }

  .corner-br,
  .corner-bl,
  .corner-tr,
  .corner-tl {
    border-radius: 10px;
  }

  .corner-br::after,
  .corner-bl::after,
  .corner-tr::after,
  .corner-tl::after {
    display: none;
  }

  .center-gear {
    display: none;
  }
}

@media (prefers-reduced-motion: reduce) {
  .reveal-enter-active {
    transition: none;
  }
}
</style>