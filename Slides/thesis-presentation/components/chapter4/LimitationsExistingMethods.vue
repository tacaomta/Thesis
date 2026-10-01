<script setup>
import { ref, watch, onMounted, onBeforeUnmount } from 'vue'
import { useNav } from '@slidev/client'

const { currentPage } = useNav()

watch(currentPage, () => {
  visibleCount.value = 0
})

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
  <div class="limitations-slide">

    <!-- Limitations -->
    <div class="limitations-flow">

      <!-- 01 -->
      <Transition name="reveal">
        <div
          v-if="visibleCount >= 1"
          class="limitation-item"
        >
          <div class="number">01</div>

          <div class="content">
            <div class="label">
              GENERATIVE ADVERSARIAL NETWORKS
            </div>

            <h3>
              GANs require large-scale training samples
            </h3>

            <p>
              GAN-based approaches require
              <strong>large-scale training samples</strong>
              and can suffer from training instability,
              including <strong>mode collapse</strong>,
              when only a small number of samples are available.
            </p>
          </div>
        </div>
      </Transition>

      <!-- 02 -->
      <Transition name="reveal">
        <div
          v-if="visibleCount >= 2"
          class="limitation-item"
        >
          <div class="number">02</div>

          <div class="content">
            <div class="label">
              ARTIFICIAL GENE NETWORK SIMULATORS
            </div>

            <h3>
              AGN simulators rely on rigid assumptions
            </h3>

            <p>
              Artificial Gene Network simulators have been
              phased out due to
              <strong>rigid assumptions</strong>
              and their inability to capture
              <strong>non-linear temporal dynamics</strong>
              from restricted real-world samples.
            </p>
          </div>
        </div>
      </Transition>

      <!-- 03 -->
      <Transition name="reveal">
        <div
          v-if="visibleCount >= 3"
          class="limitation-item unmet"
        >
          <div class="number">03</div>

          <div class="content">
            <div class="label">
              UNMET NEED
            </div>

            <h3>
              A robust architecture is still missing
            </h3>

            <p>
              There is a lack of a robust generative architecture
              capable of synthesizing
              <strong>temporal gene expression profiles</strong>
              from <strong>very limited initial observation steps</strong>.
            </p>
          </div>
        </div>
      </Transition>

    </div>

    <!-- Bottom message -->
    <Transition name="reveal">
      <div
        v-if="visibleCount >= 3"
        class="bottom-message"
      >
        <span class="arrow">→</span>

        <span>
          This motivates a generative framework designed
          specifically for limited temporal observations.
        </span>
      </div>
    </Transition>

  </div>
</template>

<style scoped>
.limitations-slide {
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
   Main limitation flow
   ============================================================ */

.limitations-flow {
  flex: 1;

  display: flex;
  flex-direction: column;
  justify-content: center;

  gap: 5px;

  min-height: 0;
}

/* ============================================================
   Limitation item
   ============================================================ */

.limitation-item {
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

.limitation-item h3 {
  margin: 0 0 5px;

  font-size: 16px;
  line-height: 1.25;

  font-weight: 700;

  color: #173f5f;
}

.limitation-item p {
  margin: 0;

  max-width: 900px;

  font-size: 12px;
  line-height: 1.45;

  color: #64748b;
}

.limitation-item strong {
  color: #24313a;
  font-weight: 700;
}

/* ============================================================
   Unmet need
   ============================================================ */

.limitation-item.unmet {
  border-color: #b8dcd7;

  background: #f8fbfb;
}

.limitation-item.unmet .number {
  background: #e7f4f2;

  border-color: #a9d4ce;

  color: #247f76;
}

.limitation-item.unmet .label {
  color: #2a9d8f;
}

.limitation-item.unmet h3 {
  color: #173f5f;
}

/* ============================================================
   Bottom message
   ============================================================ */

.bottom-message {
  display: flex;
  align-items: center;

  gap: 3px;

  margin-top: 0px;

  padding: 10px 14px;

  border-top: 1px solid #dce4e9;

  font-size: 11px;
  line-height: 1.4;

  color: #64748b;
}

.bottom-message .arrow {
  font-size: 17px;
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