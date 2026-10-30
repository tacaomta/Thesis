<script setup>
import { ref, computed, watch, onMounted, onBeforeUnmount } from 'vue'
import { useNav } from '@slidev/client'

const { currentPage } = useNav()

watch(currentPage, () => {
  visibleCount.value = 0
})
const visibleCount = ref(0)
const totalItems = 4

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
  window.addEventListener('keydown', handleKeydown, true)
})

onBeforeUnmount(() => {
  window.removeEventListener('keydown', handleKeydown, true)
})
</script>

<template>
  <div class="setup-slide">

    <div class="setup-grid">

      <!-- =========================
           01 · CORE ACHIEVEMENT
      ========================== -->

      <Transition name="reveal">
        <section v-if="visibleCount >= 1" class="setup-card corner-br">

          <div class="card-header">
            <span class="number">01</span>
            <h2>Core Achievement</h2>
          </div>

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

        </section>
      </Transition>

      <!-- =========================
           02 · SOLVES DATA SCARCITY
      ========================== -->

      <Transition name="reveal">
        <section v-if="visibleCount >= 2" class="setup-card corner-bl">

          <div class="card-header">
            <span class="number">02</span>
            <h2>Solves Data Scarcity</h2>
          </div>

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

        </section>
      </Transition>

      <!-- =========================
           03 · ROBUST IMPROVEMENT
      ========================== -->

      <Transition name="reveal">
        <section v-if="visibleCount >= 3" class="setup-card corner-tr">

          <div class="card-header">
            <span class="number">03</span>
            <h2>Robust Improvement</h2>
          </div>

          <div class="keyword-chips">
            <span class="chip">N = 50, 100</span>
            <span class="chip">binary / ternary</span>
            <span class="chip">K = 10, 20</span>
          </div>

          <svg viewBox="0 0 160 70" class="visual-svg">
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

        </section>
      </Transition>

      <!-- =========================
           04 · PRACTICAL VALUE
      ========================== -->

      <Transition name="reveal">
        <section v-if="visibleCount >= 4" class="setup-card corner-tl">

          <div class="card-header" style="padding-left: 20px;">
            <span class="number">04</span>
            <h2>Practical Value</h2>
          </div>

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

        </section>
      </Transition>

      <!-- =========================
           CENTER KEY — doubles as a
           pie-chart progress indicator:
           each quarter fills in as an
           item is revealed via SPACE.
      ========================== -->

      <div
        class="center-gear"
        :style="{ background: `conic-gradient(#198754 0deg ${progressDeg}deg, #FFFFFF ${progressDeg}deg 360deg)` }"
        role="img"
        :aria-label="`${visibleCount} of ${totalItems} points revealed`"
      >
        <div class="center-gear-inner">
          <svg viewBox="0 0 24 24" class="key-icon" aria-hidden="true">
            <circle cx="7" cy="14.5" r="4.5" />
            <path d="M10.8 11.2 L20 2" />
            <path d="M16 6 L19 9" />
            <path d="M13 9 L16 12" />
          </svg>
        </div>
      </div>

    </div>

  </div>
</template>

<style scoped>
.setup-slide {
  width: 100%;
  height: 100%;
  box-sizing: border-box;

  display: flex;
  flex-direction: column;
}

/* =========================
   GRID
========================= */

.setup-grid {
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

.setup-card {
  min-width: 0;
  min-height: 0;

  position: relative;

  padding: 16px 18px;
  box-sizing: border-box;

  display: flex;
  flex-direction: column;

  background: #ffffff;
  border: 1px solid #dce4e9;
  border-top: 4px solid #B3CEDF;
  border-radius: 10px;

  box-shadow: 0 4px 12px rgba(23, 63, 95, 0.05);

  transition:
    box-shadow 0.22s ease,
    border-top-color 0.22s ease;
}

.setup-card:hover {
  border-top-color: #2A9D8F;

  box-shadow:
    0 7px 16px rgba(23, 63, 95, 0.12),
    0 2px 5px rgba(23, 63, 95, 0.06);

  /* z-index: 6; */
}

/* =========================
   INNER CORNERS — notched inward
   so the four concave cuts together
   form one full circle at the
   middle of the 2x2 grid.
========================= */

:root {
  --notch-r: 70px;
}

/* Card 01 — inner corner is bottom-right */
.corner-br {
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

/* Card 02 — inner corner is bottom-left */
.corner-bl {
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

/* Card 03 — inner corner is top-right */
.corner-tr {
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

/* Card 04 — inner corner is top-left */
.corner-tl {
  border-top-left-radius: 0;
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
   CENTER KEY + PIE PROGRESS

   The outer circle's background is a
   conic-gradient driven by visibleCount,
   so each revealed card fills in one
   more quarter (90°) of the ring.
   The inner white disk + key icon sit
   on top, unaffected by the progress fill.
========================= */

.center-gear {
  position: absolute;

  top: 50%;
  left: 50%;

  width: 72px;
  height: 72px;

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
  width: 46px;
  height: 46px;

  display: flex;
  align-items: center;
  justify-content: center;

  border-radius: 50%;

  background: #ffffff;
  box-shadow: inset 0 0 0 1px rgba(23, 63, 95, 0.06);
}

.key-icon {
  width: 24px;
  height: 24px;

  fill: none;
  stroke: #09c7ae;
  stroke-width: 1.8;
  stroke-linecap: round;
  stroke-linejoin: round;
}

/* =========================
   HEADER
========================= */

.card-header {
  display: flex;
  align-items: baseline;
  gap: 7px;

  margin-bottom: 9px;
}

.number {
  flex: 0 0 auto;

  color: #2A9D8F;
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 10px;
  font-weight: 700;
  letter-spacing: 0.08em;
}

h2 {
  margin: 0;

  color: #173F5F;
  font-size: 14px;
  line-height: 1.2;
  font-weight: 700;
}

/* =========================================
   KEYWORD CHIPS
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
  .setup-grid {
    grid-template-columns: 1fr;
    grid-template-rows: auto;
    overflow-y: auto;
  }

  .setup-card {
    min-height: 260px;
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

  .center-gear {
    transition: none;
  }
}
</style>