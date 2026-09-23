<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

const visibleCount = ref(0)

const totalItems = 3

function handleKeydown(event) {
  if (event.code !== 'Space') return

  // Prevent Slidev from advancing to the next slide
  event.preventDefault()
  event.stopPropagation()

  if (visibleCount.value < totalItems) {
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
  <div class="research-gap-03">


    <!-- Main content -->
    <div class="gap-flow">

      <!-- 01 -->
      <Transition name="reveal">
        <div
          v-if="visibleCount >= 1"
          class="gap-item"
        >
          <div class="number">01</div>

          <div class="content">
            <div class="label">
              BIOLOGICAL COMPLEXITY
            </div>

            <h3>
              GRNs require coordinated temporal observations
            </h3>

            <p>
              Reconstructing GRNs requires observing
              <strong>coordinated gene expression trajectories</strong>
              over temporal steps.
            </p>
          </div>
        </div>
      </Transition>

      <!-- 02 -->
      <Transition name="reveal">
        <div
          v-if="visibleCount >= 2"
          class="gap-item"
        >
          <div class="number">02</div>

          <div class="content">
            <div class="label">
              DATA COLLECTION CONSTRAINTS
            </div>

            <h3>
              Biological experiments limit temporal sampling
            </h3>

            <p>
              Biological experiments face
              <strong>high costs, measurement noise,</strong>
              and strict environmental constraints,
              resulting in severely restricted time-step observations.
            </p>
          </div>
        </div>
      </Transition>

      <!-- 03 -->
      <Transition name="reveal">
        <div
          v-if="visibleCount >= 3"
          class="gap-item impact"
        >
          <div class="number">03</div>

          <div class="content">
            <div class="label">
              IMPACT ON INFERENCE
            </div>

            <h3>
              Short time-series data weakens GRN inference
            </h3>

            <p>
              Short time-series data significantly reduces the
              <strong>accuracy and stability</strong>
              of computational inference algorithms.
            </p>
          </div>
        </div>
      </Transition>

    </div>

  </div>
</template>

<style scoped>
.research-gap-03 {
  width: 100%;
  height: 100%;
  box-sizing: border-box;

  display: flex;
  flex-direction: column;

  color: #24313a;
}

/* ============================================================
   Intro
   ============================================================ */

.intro {
  display: flex;
  align-items: flex-start;
  gap: 12px;

  margin-bottom: 22px;
}

.intro-line {
  width: 4px;
  min-width: 4px;
  height: 42px;

  background: #2a9d8f;
  border-radius: 2px;
}

.intro-text {
  margin: 0;

  max-width: 820px;

  font-size: 17px;
  line-height: 1.4;
  font-weight: 500;

  color: #173f5f;
}

/* ============================================================
   Main flow
   ============================================================ */

.gap-flow {
  flex: 1;

  display: flex;
  flex-direction: column;
  justify-content: center;

  gap: 15px;

  min-height: 0;
}

/* ============================================================
   Gap item
   ============================================================ */

.gap-item {
  display: grid;
  grid-template-columns: 54px minmax(0, 1fr);

  column-gap: 16px;

  padding: 15px 20px 15px 14px;

  background: #ffffff;

  border: 1px solid #dce4e9;
  border-radius: 9px;

  box-sizing: border-box;
}

/* Number */

.number {
  width: 38px;
  height: 38px;

  display: flex;
  align-items: center;
  justify-content: center;

  border-radius: 50%;

  background: #f0f5f7;
  border: 1px solid #cbd8df;

  color: #173f5f;

  font-family:
    'IBM Plex Mono',
    'JetBrains Mono',
    monospace;

  font-size: 12px;
  font-weight: 700;
}

/* Content */

.content {
  min-width: 0;
}

.label {
  margin-bottom: 4px;

  font-family:
    'IBM Plex Mono',
    'JetBrains Mono',
    monospace;

  font-size: 9px;
  font-weight: 700;

  letter-spacing: 0.12em;

  color: #20639b;
}

.gap-item h3 {
  margin: 0 0 5px;

  font-size: 16px;
  line-height: 1.25;
  font-weight: 700;

  color: #173f5f;
}

.gap-item p {
  margin: 0;

  max-width: 900px;

  font-size: 12px;
  line-height: 1.45;

  color: #64748b;
}

.gap-item strong {
  color: #24313a;
  font-weight: 700;
}

/* ============================================================
   Impact item
   ============================================================ */

.gap-item.impact {
  border-color: #b8dcd7;
  background: #f8fbfb;
}

.gap-item.impact .number {
  background: #e7f4f2;
  border-color: #a9d4ce;
  color: #247f76;
}

.gap-item.impact .label {
  color: #2a9d8f;
}

.gap-item.impact h3 {
  color: #173f5f;
}

/* ============================================================
   Progress
   ============================================================ */

.progress {
  display: flex;
  align-items: center;
  justify-content: flex-end;

  gap: 7px;

  margin-top: 12px;

  height: 18px;
}

.progress-dot {
  width: 6px;
  height: 6px;

  border-radius: 50%;

  background: #dce4e9;

  transition:
    background 0.2s ease,
    transform 0.2s ease;
}

.progress-dot.active {
  background: #2a9d8f;
  transform: scale(1.15);
}

.progress-text {
  margin-left: 4px;

  font-family:
    'IBM Plex Mono',
    'JetBrains Mono',
    monospace;

  font-size: 9px;

  color: #94a3b8;
}

/* ============================================================
   Reveal animation
   ============================================================ */

.reveal-enter-active {
  transition:
    opacity 0.3s ease,
    transform 0.3s ease;
}

.reveal-enter-from {
  opacity: 0;
  transform: translateY(10px);
}

.reveal-enter-to {
  opacity: 1;
  transform: translateY(0);
}

/* ============================================================
   Reduced motion
   ============================================================ */

@media (prefers-reduced-motion: reduce) {
  .reveal-enter-active {
    transition: none;
  }

  .progress-dot {
    transition: none;
  }
}
</style>