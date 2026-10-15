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

          <div class="keyword-chips">
            <span class="chip first">first of its kind</span>
            <span class="chip">autoencoder-based</span>
            <span class="chip">temporal synthesis</span>
          </div>

          <svg viewBox="0 0 160 70" class="visual-svg">
            <rect x="4" y="27" width="34" height="16" rx="4" class="v-io" />
            <text x="21" y="37" text-anchor="middle" class="v-io-text">input</text>

            <path d="M40 35 L58 35" class="v-arrow" marker-end="url(#a1)" />

            <path d="M62 15 L82 35 L62 55 Z" class="v-ae v-ae-enc" />
            <path d="M98 15 L78 35 L98 55 Z" class="v-ae v-ae-dec" />
            <text x="80" y="64" text-anchor="middle" class="v-caption">autoencoder</text>

            <path d="M100 35 L120 35" class="v-arrow" marker-end="url(#a1)" />

            <rect x="122" y="27" width="34" height="16" rx="4" class="v-io v-io-out" />
            <text x="139" y="37" text-anchor="middle" class="v-io-text out">synthetic</text>

            <defs>
              <marker id="a1" markerWidth="8" markerHeight="8" refX="6" refY="4" orient="auto">
                <path d="M0 0 L8 4 L0 8 Z" class="v-arrow-head" />
              </marker>
            </defs>
          </svg>
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

          <div class="keyword-chips">
            <span class="chip">extends time-series data</span>
            <span class="chip warn">no GAN instability</span>
          </div>

          <svg viewBox="0 0 160 70" class="visual-svg">
            <!-- few real samples -->
            <circle cx="18" cy="48" r="4" class="v-dot-real" />
            <circle cx="32" cy="42" r="4" class="v-dot-real" />
            <circle cx="46" cy="50" r="4" class="v-dot-real" />
            <text x="32" y="64" text-anchor="middle" class="v-caption">few samples</text>

            <path d="M58 40 L76 40" class="v-arrow" marker-end="url(#a2)" />

            <!-- GAN crossed out -->
            <g class="v-gan-cross">
              <rect x="80" y="10" width="24" height="16" rx="3" class="v-gan-box" />
              <text x="92" y="21" text-anchor="middle" class="v-gan-text">GAN</text>
              <line x1="78" y1="8" x2="106" y2="28" class="v-cross" />
              <line x1="106" y1="8" x2="78" y2="28" class="v-cross" />
            </g>

            <!-- expanded samples -->
            <circle cx="112" cy="48" r="4" class="v-dot-synth" />
            <circle cx="124" cy="40" r="4" class="v-dot-synth" />
            <circle cx="136" cy="50" r="4" class="v-dot-synth" />
            <circle cx="148" cy="42" r="4" class="v-dot-synth" />
            <text x="130" y="64" text-anchor="middle" class="v-caption synth-label">more samples</text>

            <defs>
              <marker id="a2" markerWidth="8" markerHeight="8" refX="6" refY="4" orient="auto">
                <path d="M0 0 L8 4 L0 8 Z" class="v-arrow-head" />
              </marker>
            </defs>
          </svg>
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

          <div class="keyword-chips">
            <span class="chip">N = 50, 100</span>
            <span class="chip">binary / ternary</span>
            <span class="chip">K = 10, 20</span>
          </div>

          <svg viewBox="0 0 160 70" class="visual-svg">
            <!-- paired bars: baseline vs improved, across 3 dimensions -->
            <g v-for="(bar, i) in 3" :key="i"></g>

            <!-- dimension 1: network size -->
            <rect x="12" y="46" width="10" height="14" class="v-bar-base" />
            <rect x="24" y="30" width="10" height="30" class="v-bar-up" />
            <text x="23" y="66" text-anchor="middle" class="v-caption small">size</text>

            <!-- dimension 2: discretization -->
            <rect x="68" y="42" width="10" height="18" class="v-bar-base" />
            <rect x="80" y="24" width="10" height="36" class="v-bar-up" />
            <text x="79" y="66" text-anchor="middle" class="v-caption small">levels</text>

            <!-- dimension 3: low-K -->
            <rect x="124" y="50" width="10" height="10" class="v-bar-base" />
            <rect x="136" y="18" width="10" height="42" class="v-bar-up" />
            <text x="135" y="66" text-anchor="middle" class="v-caption small">low-K</text>

            <line x1="4" y1="60" x2="156" y2="60" class="v-baseline" />
          </svg>
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

          <div class="keyword-chips">
            <span class="chip">higher-quality networks</span>
            <span class="chip unmet-chip">no costly lab experiments</span>
          </div>

          <svg viewBox="0 0 160 70" class="visual-svg">
            <!-- lab flask, crossed out -->
            <g class="v-gan-cross">
              <path d="M24 12 L24 24 L14 44 a4 4 0 0 0 4 6 h24 a4 4 0 0 0 4 -6 L36 24 L36 12" class="v-flask" />
              <line x1="18" y1="10" x2="42" y2="10" class="v-flask-top" />
              <line x1="10" y1="8" x2="42" y2="46" class="v-cross" />
              <line x1="42" y1="8" x2="10" y2="46" class="v-cross" />
            </g>
            <text x="26" y="64" text-anchor="middle" class="v-caption">lab experiments</text>

            <path d="M54 32 L72 32" class="v-arrow" marker-end="url(#a4)" />

            <!-- computed network -->
            <circle cx="100" cy="20" r="5" class="v-net-node" />
            <circle cx="118" cy="16" r="5" class="v-net-node" />
            <circle cx="132" cy="30" r="5" class="v-net-node" />
            <circle cx="112" cy="38" r="5" class="v-net-node" />
            <line x1="100" y1="20" x2="118" y2="16" class="v-net-edge" />
            <line x1="118" y1="16" x2="132" y2="30" class="v-net-edge" />
            <line x1="100" y1="20" x2="112" y2="38" class="v-net-edge" />
            <line x1="112" y1="38" x2="132" y2="30" class="v-net-edge" />
            <text x="116" y="64" text-anchor="middle" class="v-caption synth-label">inferred network</text>

            <defs>
              <marker id="a4" markerWidth="8" markerHeight="8" refX="6" refY="4" orient="auto">
                <path d="M0 0 L8 4 L0 8 Z" class="v-arrow-head" />
              </marker>
            </defs>
          </svg>
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

  display: flex;
  flex-direction: column;
}

.implication-content h3 {
  margin: 0 0 8px;

  color: #173F5F;

  font-size: 14px;
  line-height: 1.2;

  font-weight: 700;

  transition: color 0.22s ease;
}

.implication.visible:hover .implication-content h3 {
  color: #20639B;
}

/* =========================================
   KEYWORD CHIPS (replaces old <p>)
   ========================================= */

.keyword-chips {
  display: flex;
  flex-wrap: wrap;

  gap: 5px;

  margin-bottom: 10px;
}

.chip {
  padding: 3px 8px;

  border-radius: 999px;

  background: #F1F5F8;
  border: 1px solid #DCE4E9;

  color: #475569;

  font-size: 9.5px;
  font-weight: 600;

  white-space: nowrap;
}

.chip.first {
  background: #EDF8F6;
  border-color: #B8DCD7;
  color: #247F76;
}

.chip.warn {
  background: #FDF1E7;
  border-color: #F0D0AB;
  color: #B6560C;
}

.chip.unmet-chip {
  background: #EDF8F6;
  border-color: #B8DCD7;
  color: #247F76;
}

/* =========================================
   VISUAL
   ========================================= */

.visual-svg {
  width: 100%;
  height: auto;

  margin-top: auto;
}

.v-caption {
  fill: #94A3B8;
  font-family: 'Inter', 'Segoe UI', sans-serif;
  font-size: 7.5px;
}

.v-caption.small {
  font-size: 7px;
}

.v-caption.synth-label {
  fill: #20639B;
  font-weight: 600;
}

.v-arrow {
  stroke: #CBD5E1;
  stroke-width: 1.6;
  fill: none;
}

.v-arrow-head {
  fill: #CBD5E1;
}

/* --- 01: autoencoder --- */

.v-io {
  fill: #EEF5FA;
  stroke: #20639B;
  stroke-width: 1.3;
}

.v-io-out {
  fill: #EDF8F6;
  stroke: #2A9D8F;
}

.v-io-text {
  fill: #173F5F;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 7.5px;
  font-weight: 600;
}

.v-io-text.out {
  fill: #247F76;
}

.v-ae {
  fill: #F4F8FB;
  stroke: #20639B;
  stroke-width: 1.4;
}

.v-ae-dec {
  fill: #EEF5FA;
}

/* --- 02: GAN crossed, more samples --- */

.v-dot-real {
  fill: #EEF5FA;
  stroke: #20639B;
  stroke-width: 1.2;
}

.v-dot-synth {
  fill: #EDF8F6;
  stroke: #2A9D8F;
  stroke-width: 1.2;
}

.synth-label {
  fill: #247F76;
}

.v-gan-box {
  fill: #FDF1E7;
  stroke: #E76F51;
  stroke-width: 1.3;
}

.v-gan-text {
  fill: #B6560C;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 7px;
  font-weight: 700;
}

.v-cross {
  stroke: #E76F51;
  stroke-width: 1.6;
  stroke-linecap: round;
}

/* --- 03: improvement bars --- */

.v-bar-base {
  fill: #E2E8F0;
}

.v-bar-up {
  fill: #2A9D8F;
}

.v-baseline {
  stroke: #CBD5E1;
  stroke-width: 1;
}

/* --- 04: lab vs network --- */

.v-flask {
  fill: #F4F8FB;
  stroke: #94A3B8;
  stroke-width: 1.4;
  stroke-linejoin: round;
}

.v-flask-top {
  stroke: #94A3B8;
  stroke-width: 1.4;
}

.v-net-node {
  fill: #EDF8F6;
  stroke: #2A9D8F;
  stroke-width: 1.4;
}

.v-net-edge {
  stroke: #2A9D8F;
  stroke-width: 1.2;
  opacity: 0.7;
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