<script setup>
import { ref, watch, onMounted, onBeforeUnmount } from 'vue'
import { useNav } from '@slidev/client'

const { currentPage } = useNav()

watch(currentPage, () => {
  visibleCount.value = 0
})
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
  <div class="summary-slide">

    <section class="implications">

      <!-- 01 -->
      <article
        class="implication"
        :class="{ visible: visibleCount >= 1 }"
      >
        <div class="implication-number">01</div>

        <div class="implication-content">
          <h3>Core Achievement</h3>

          <p>
            Demonstrates the first autoencoder-based temporal data synthesis
            method specifically engineered for GRN inference.
          </p>
        </div>
      </article>

      <!-- 02 -->
      <article
        class="implication"
        :class="{ visible: visibleCount >= 2 }"
      >
        <div class="implication-number">02</div>

        <div class="implication-content">
          <h3>Solves Data Scarcity</h3>

          <p>
            Successfully extends time-series expression data without requiring
            complex, unstable GAN models.
          </p>
        </div>
      </article>

      <!-- 03 -->
      <article
        class="implication"
        :class="{ visible: visibleCount >= 3 }"
      >
        <div class="implication-number">03</div>

        <div class="implication-content">
          <h3>Robust Improvement</h3>

          <p>
            Substantially improves precision and recall across network scales
            (<em>N</em> = 50, 100), discretization levels (binary/ternary),
            and low sample regimes (<em>K</em> = 10, 20).
          </p>
        </div>
      </article>

      <!-- 04 -->
      <article
        class="implication"
        :class="{ visible: visibleCount >= 4 }"
      >
        <div class="implication-number">04</div>

        <div class="implication-content">
          <h3>Practical Value</h3>

          <p>
            Allows researchers to infer higher-quality gene networks without
            running costly long-term laboratory experiments.
          </p>
        </div>
      </article>

    </section>

    <div
      v-if="visibleCount < totalItems"
      class="reveal-hint"
    >
      Press <kbd>Space</kbd> to reveal
    </div>

  </div>
</template>

<style scoped>
.summary-slide {
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

.summary-intro {
  display: flex;
  align-items: center;

  gap: 12px;

  margin-bottom: 18px;
}

.summary-intro > span {
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

.summary-intro p {
  margin: 0;

  color: #64748B;

  font-size: 11px;
  line-height: 1.3;
}

/* =========================================
   IMPLICATIONS
   ========================================= */

.implications {
  width: 100%;

  display: grid;
  grid-template-columns: repeat(4, 1fr);

  gap: 12px;

  flex: 1;
  min-height: 0;
}

.implication {
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

.implication.visible {
  opacity: 1;
  transform: translateY(0);
}

/* =========================================
   HOVER
   ========================================= */

.implication.visible:hover {
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

.implication-number {
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

.implication.visible:hover .implication-number {
  transform: translateX(2px);
  color: #20639B;
}

/* =========================================
   CONTENT
   ========================================= */

.implication-content {
  min-width: 0;
}

.implication-content h3 {
  margin: 0 0 7px;

  color: #173F5F;

  font-size: 14px;
  line-height: 1.2;

  font-weight: 700;

  transition: color 0.22s ease;
}

.implication.visible:hover .implication-content h3 {
  color: #20639B;
}

.implication-content p {
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
  .implications {
    grid-template-columns: repeat(2, 1fr);
  }
}
</style>