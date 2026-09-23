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
  <div class="framework-slide">

    <!-- Main framework -->
    <div class="framework-flow">

      <!-- 01 -->
      <Transition name="reveal">
        <div
          v-if="visibleCount >= 1"
          class="framework-item"
        >
          <div class="number">01</div>

          <div class="content">
            <div class="label">
              CORE OBJECTIVE
            </div>

            <h3>
              Synthesize time-series data from sparse observations
            </h3>

            <p>
              Develop an
              <strong>Autoencoder-based time-series data synthesis framework</strong>
              tailored for sparse gene expression trajectories.
            </p>
          </div>
        </div>
      </Transition>

      <!-- 02 -->
      <Transition name="reveal">
        <div
          v-if="visibleCount >= 2"
          class="framework-item"
        >
          <div class="number">02</div>

          <div class="content">
            <div class="label">
              WORKING HYPOTHESIS
            </div>

            <h3>
              Learn temporal transitions and generate future steps
            </h3>

            <p>
              Training an Autoencoder on
              <strong>consecutive time-step pairs</strong>
              enables auto-regressive generation of future time steps
              while preserving structural network dynamics.
            </p>
          </div>
        </div>
      </Transition>

      <!-- 03 -->
      <Transition name="reveal">
        <div
          v-if="visibleCount >= 3"
          class="framework-item validation"
        >
          <div class="number">03</div>

          <div class="content">
            <div class="label">
              DOWNSTREAM VALIDATION
            </div>

            <h3>
              Validate synthetic data through GRN inference
            </h3>

            <p>
              Evaluate the quality of the generated data using
              <strong>
                Mutual Information Based on Multiple Level
                Discretization Network Inference (MIDNI)
              </strong>
              as the downstream GRN inference algorithm.
            </p>
          </div>
        </div>
      </Transition>

    </div>

    <!-- Framework connection -->
    <Transition name="reveal">
      <div
        v-if="visibleCount >= 3"
        class="framework-message"
      >
        <div class="message-node">
          Sparse observations
        </div>

        <div class="message-arrow">→</div>

        <div class="message-node highlight">
          Autoencoder
        </div>

        <div class="message-arrow">→</div>

        <div class="message-node">
          Synthetic trajectories
        </div>

        <div class="message-arrow">→</div>

        <div class="message-node">
          MIDNI validation
        </div>
      </div>
    </Transition>

  </div>
</template>

<style scoped>
.framework-slide {
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

  max-width: 850px;

  font-size: 17px;
  line-height: 1.4;

  font-weight: 500;

  color: #173f5f;
}

/* ============================================================
   Framework items
   ============================================================ */

.framework-flow {
  flex: 1;

  display: flex;
  flex-direction: column;
  justify-content: center;

  gap: 15px;

  min-height: 0;
}

.framework-item {
  display: grid;

  grid-template-columns: 54px minmax(0, 1fr);

  column-gap: 16px;

  padding: 15px 20px 15px 14px;

  background: #ffffff;

  border: 1px solid #dce4e9;

  border-radius: 9px;

  box-sizing: border-box;
}

/* ============================================================
   Number
   ============================================================ */

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

/* ============================================================
   Content
   ============================================================ */

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

.framework-item h3 {
  margin: 0 0 5px;

  font-size: 16px;
  line-height: 1.25;

  font-weight: 700;

  color: #173f5f;
}

.framework-item p {
  margin: 0;

  max-width: 930px;

  font-size: 12px;
  line-height: 1.45;

  color: #64748b;
}

.framework-item strong {
  color: #24313a;

  font-weight: 700;
}

/* ============================================================
   Validation item
   ============================================================ */

.framework-item.validation {
  border-color: #b8dcd7;

  background: #f8fbfb;
}

.framework-item.validation .number {
  background: #e7f4f2;

  border-color: #a9d4ce;

  color: #247f76;
}

.framework-item.validation .label {
  color: #2a9d8f;
}

/* ============================================================
   Framework message
   ============================================================ */

.framework-message {
  display: flex;
  align-items: center;
  justify-content: center;

  flex-wrap: wrap;

  gap: 8px;

  margin-top: 12px;

  padding: 11px 12px;

  border-top: 1px solid #dce4e9;
}

.message-node {
  padding: 6px 10px;

  border: 1px solid #dce4e9;

  border-radius: 5px;

  background: #ffffff;

  font-size: 10px;
  font-weight: 600;

  color: #64748b;

  white-space: nowrap;
}

.message-node.highlight {
  border-color: #a9d4ce;

  background: #e7f4f2;

  color: #247f76;
}

.message-arrow {
  font-size: 15px;

  font-weight: 700;

  color: #2a9d8f;
}

/* ============================================================
   Progress
   ============================================================ */

.progress {
  display: flex;
  align-items: center;
  justify-content: flex-end;

  gap: 7px;

  height: 18px;

  margin-top: 8px;
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