<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

const visibleCount = ref(0)
const totalItems = 4

function handleKeydown(event) {
  if (event.code !== 'Space') return

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
  <div class="future-slide">

    <!-- =========================================
         INTRO
         ========================================= -->

    <div class="future-intro">
      <span>BEYOND THE CURRENT FRAMEWORK</span>

      <div class="intro-line"></div>

      <p>
        Extending GRN inference toward richer representations,
        generative models, and real-world biological validation
      </p>
    </div>

    <!-- =========================================
         FUTURE HORIZONS
         ========================================= -->

    <section class="horizons">

      <!-- 01 -->
      <article
        class="horizon"
        :class="{ visible: visibleCount >= 1 }"
      >
        <div class="horizon-number">01</div>

        <div class="horizon-content">
          <h3>Graph Neural Networks</h3>

          <p>
            Integrating graph representation learning to capture
            structural topology directly.
          </p>
        </div>
      </article>

      <!-- 02 -->
      <article
        class="horizon"
        :class="{ visible: visibleCount >= 2 }"
      >
        <div class="horizon-number">02</div>

        <div class="horizon-content">
          <h3>Continuous-Valued Data</h3>

          <p>
            Extending the framework to operate directly on continuous
            datasets without discretization loss.
          </p>
        </div>
      </article>

      <!-- 03 -->
      <article
        class="horizon"
        :class="{ visible: visibleCount >= 3 }"
      >
        <div class="horizon-number">03</div>

        <div class="horizon-content">
          <h3>Advanced Generative Architectures</h3>

          <p>
            Exploring conditional GANs or Diffusion Models for
            continuous dynamics.
          </p>
        </div>
      </article>

      <!-- 04 -->
      <article
        class="horizon"
        :class="{ visible: visibleCount >= 4 }"
      >
        <div class="horizon-number">04</div>

        <div class="horizon-content">
          <h3>Clinical Validation</h3>

          <p>
            Benchmarking on real-world biological datasets, rare disease
            transcriptomics, and temporal single-cell RNA-seq.
          </p>
        </div>
      </article>

    </section>

    <!-- =========================================
         REVEAL HINT
         ========================================= -->

    <div
      v-if="visibleCount < totalItems"
      class="reveal-hint"
    >
      Press <kbd>Space</kbd> to reveal
    </div>

  </div>
</template>

<style scoped>
.future-slide {
  width: 100%;
  height: 100%;
  box-sizing: border-box;

  display: flex;
  flex-direction: column;

  color: #24313A;
}

/* =========================================
   INTRO
   ========================================= */

.future-intro {
  display: flex;
  align-items: center;

  gap: 12px;

  margin-bottom: 18px;
}

.future-intro > span {
  flex: 0 0 auto;

  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;

  font-size: 10px;
  font-weight: 700;

  letter-spacing: .08em;

  color: #2A9D8F;
}

.intro-line {
  width: 42px;
  height: 1px;

  background: #B3CEDF;
}

.future-intro p {
  margin: 0;

  color: #64748B;

  font-size: 11px;
  line-height: 1.3;
}

/* =========================================
   HORIZONS
   ========================================= */

.horizons {
  width: 100%;

  display: grid;
  grid-template-columns: repeat(4, 1fr);

  gap: 12px;

  flex: 1;
  min-height: 0;
}

.horizon {
  min-width: 0;

  box-sizing: border-box;

  padding: 13px 13px;

  display: flex;
  flex-direction: column;

  border-top: 3px solid #B3CEDF;

  background: #FFFFFF;

  opacity: 0;

  transform: translateY(10px);

  transition:
    opacity 0.3s ease,
    transform 0.3s ease,
    box-shadow 0.22s ease,
    border-top-color 0.22s ease;
}

.horizon.visible {
  opacity: 1;
  transform: translateY(0);
}

/* =========================================
   HOVER
   ========================================= */

.horizon.visible:hover {
  transform: translateY(-4px);

  border-top-color: #2A9D8F;

  box-shadow:
    0 7px 16px rgba(23, 63, 95, 0.12),
    0 2px 5px rgba(23, 63, 95, 0.06);

  z-index: 5;
}

/* =========================================
   NUMBER
   ========================================= */

.horizon-number {
  margin-bottom: 10px;

  color: #2A9D8F;

  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;

  font-size: 10px;
  font-weight: 700;

  letter-spacing: .08em;

  transition:
    transform 0.22s ease,
    color 0.22s ease;
}

.horizon.visible:hover .horizon-number {
  transform: translateX(2px);
  color: #20639B;
}

/* =========================================
   CONTENT
   ========================================= */

.horizon-content {
  min-width: 0;
}

.horizon-content h3 {
  margin: 0 0 7px;

  color: #173F5F;

  font-size: 14px;
  line-height: 1.2;

  font-weight: 700;

  transition: color 0.22s ease;
}

.horizon.visible:hover .horizon-content h3 {
  color: #20639B;
}

.horizon-content p {
  margin: 0;

  color: #64748B;

  font-size: 11px;
  line-height: 1.45;
}

/* =========================================
   REVEAL HINT
   ========================================= */

.reveal-hint {
  align-self: flex-end;

  margin-top: 8px;

  font-size: 10px;

  color: #94A3B8;
}

kbd {
  display: inline-block;

  padding: 1px 5px;

  border: 1px solid #CBD5E1;
  border-bottom-width: 2px;

  border-radius: 4px;

  background: #F8FAFB;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 10px;

  color: #475569;
}

/* =========================================
   RESPONSIVE
   ========================================= */

@media (max-width: 900px) {
  .horizons {
    grid-template-columns: repeat(2, 1fr);
  }
}
</style>