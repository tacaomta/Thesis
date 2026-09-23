<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

const visibleCount = ref(0)

const totalItems = 4

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

    <!-- ======================================================
         LEFT: Four phases
         ====================================================== -->
    <div class="phase-panel">

      <div class="phase-list">

        <!-- Phase 1 -->
        <Transition name="reveal">
          <div
            v-if="visibleCount >= 1"
            class="phase-item"
          >
            <div class="phase-number">01</div>

            <div class="phase-content">
              <div class="phase-label">
                PHASE 1 · REPRESENTATION
              </div>

              <p>
                Map the
                <strong>k × n discretized gene expression matrix</strong>
                into adjacent temporal concatenated vectors.
              </p>
            </div>
          </div>
        </Transition>

        <!-- Phase 2 -->
        <Transition name="reveal">
          <div
            v-if="visibleCount >= 2"
            class="phase-item"
          >
            <div class="phase-number">02</div>

            <div class="phase-content">
              <div class="phase-label">
                PHASE 2 · GENERATIVE MODELING
              </div>

              <p>
                Train a
                <strong>3-hidden-layer Autoencoder</strong>
                to reconstruct adjacent state transitions.
              </p>
            </div>
          </div>
        </Transition>

        <!-- Phase 3 -->
        <Transition name="reveal">
          <div
            v-if="visibleCount >= 3"
            class="phase-item"
          >
            <div class="phase-number">03</div>

            <div class="phase-content">
              <div class="phase-label">
                PHASE 3 · AUTO-REGRESSIVE SYNTHESIS
              </div>

              <p>
                Iteratively predict missing temporal trajectories
                from step <strong>k + 1</strong> up to <strong>m</strong>.
              </p>
            </div>
          </div>
        </Transition>

        <!-- Phase 4 -->
        <Transition name="reveal">
          <div
            v-if="visibleCount >= 4"
            class="phase-item final"
          >
            <div class="phase-number">04</div>

            <div class="phase-content">
              <div class="phase-label">
                PHASE 4 · GRN INFERENCE
              </div>

              <p>
                Feed the combined
                <strong>original + synthetic profiles</strong>
                into the <strong>MIDNI</strong> algorithm.
              </p>
            </div>
          </div>
        </Transition>

      </div>

      <!-- Progress -->
      <div class="progress">
        <span
          v-for="index in totalItems"
          :key="index"
          class="progress-dot"
          :class="{ active: visibleCount >= index }"
        ></span>

        <span class="progress-text">
          {{ visibleCount }} / {{ totalItems }}
        </span>
      </div>

    </div>


    <!-- ======================================================
         RIGHT: Main framework figure
         ====================================================== -->
    <div class="figure-panel">

      <!--
        Replace this path with your actual figure.

        Example:
        /images/chapter3/autoencoder_framework.png
      -->
      <img
        class="framework-image"
        src="../../public/images/frameworkv9.png"
        alt="Autoencoder-based time-series gene expression synthesis framework"
      />

      <!-- Image caption -->
      <div class="figure-caption">
        Autoencoder-based framework for synthesizing
        missing temporal gene expression profiles
      </div>

    </div>

  </div>
</template>

<style scoped>
.framework-slide {
  width: 100%;
  height: 100%;

  display: grid;
  grid-template-columns: 1fr 2fr;

  gap: 24px;

  box-sizing: border-box;

  color: #24313a;
}

/* ============================================================
   LEFT PANEL
   ============================================================ */

.phase-panel {
  min-width: 0;
  min-height: 0;

  display: flex;
  flex-direction: column;

  padding: 4px 0 4px 2px;
}

.phase-list {
  flex: 1;

  display: flex;
  flex-direction: column;

  justify-content: center;

  gap: 12px;

  min-height: 0;
}

/* ============================================================
   Phase item
   ============================================================ */

.phase-item {
  display: grid;

  grid-template-columns: 34px minmax(0, 1fr);

  column-gap: 10px;

  padding: 10px 10px 10px 8px;

  border-left: 3px solid #dce4e9;

  background: #ffffff;

  box-sizing: border-box;
}

/* ============================================================
   Phase number
   ============================================================ */

.phase-number {
  width: 30px;
  height: 30px;

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

  font-size: 9px;
  font-weight: 700;
}

/* ============================================================
   Phase content
   ============================================================ */

.phase-content {
  min-width: 0;
}

.phase-label {
  margin-bottom: 4px;

  font-family:
    'IBM Plex Mono',
    'JetBrains Mono',
    monospace;

  font-size: 8px;
  font-weight: 700;

  letter-spacing: 0.08em;

  color: #20639b;

  line-height: 1.3;
}

.phase-content p {
  margin: 0;

  font-size: 11px;

  line-height: 1.42;

  color: #64748b;
}

.phase-content strong {
  color: #24313a;

  font-weight: 700;
}

/* ============================================================
   Final phase
   ============================================================ */

.phase-item.final {
  border-left-color: #2a9d8f;

  background: #f8fbfb;
}

.phase-item.final .phase-number {
  background: #e7f4f2;

  border-color: #a9d4ce;

  color: #247f76;
}

.phase-item.final .phase-label {
  color: #2a9d8f;
}

/* ============================================================
   Progress
   ============================================================ */

.progress {
  display: flex;

  align-items: center;

  justify-content: flex-start;

  gap: 6px;

  height: 18px;

  margin-top: 5px;

  padding-left: 8px;
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
  margin-left: 3px;

  font-family:
    'IBM Plex Mono',
    'JetBrains Mono',
    monospace;

  font-size: 8px;

  color: #94a3b8;
}

/* ============================================================
   RIGHT PANEL — FIGURE
   ============================================================ */

.figure-panel {
  min-width: 0;
  min-height: 0;

  display: flex;
  flex-direction: column;

  align-items: center;
  justify-content: center;

  padding: 4px 0;
}

.framework-image {
  display: block;

  width: 100%;
  height: auto;

  max-height: calc(100% - 26px);

  object-fit: contain;

  /* Prevent the image from becoming visually small */
  min-width: 0;
}

.figure-caption {
  margin-top: 6px;

  max-width: 92%;

  text-align: center;

  font-size: 9px;

  line-height: 1.3;

  color: #64748b;
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

/* ============================================================
   Smaller screens
   ============================================================ */

@media (max-width: 760px) {
  .framework-slide {
    grid-template-columns: 1fr;
    grid-template-rows: auto 1fr;

    gap: 12px;
  }

  .phase-list {
    justify-content: flex-start;
  }

  .figure-panel {
    min-height: 300px;
  }
}
</style>