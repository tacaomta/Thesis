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
  <div class="future-slide">

    <!-- =========================================
         INTRO
         ========================================= -->

    <div class="future-intro">
      <!-- <span>BEYOND THE CURRENT FRAMEWORK</span>

      <div class="intro-line"></div>

      <p>
        Extending GRN inference toward richer representations,
        generative models, and real-world biological validation
      </p> -->
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

          <div class="keyword-chips">
            <span class="chip">graph representation learning</span>
            <span class="chip">structural topology</span>
          </div>

          <svg viewBox="0 0 160 70" class="visual-svg">
            <!-- small graph -->
            <circle cx="18" cy="20" r="5" class="v-net-node" />
            <circle cx="36" cy="12" r="5" class="v-net-node" />
            <circle cx="40" cy="34" r="5" class="v-net-node" />
            <circle cx="20" cy="42" r="5" class="v-net-node" />
            <line x1="18" y1="20" x2="36" y2="12" class="v-net-edge" />
            <line x1="18" y1="20" x2="40" y2="34" class="v-net-edge" />
            <line x1="18" y1="20" x2="20" y2="42" class="v-net-edge" />
            <line x1="40" y1="34" x2="20" y2="42" class="v-net-edge" />
            <text x="29" y="62" text-anchor="middle" class="v-caption">topology</text>

            <path d="M52 30 L70 30" class="v-arrow" marker-end="url(#g1)" />

            <!-- GNN box with internal layers -->
            <rect x="74" y="12" width="76" height="36" rx="6" class="v-gnn-box" />
            <circle cx="90" cy="22" r="3" class="v-gnn-unit" />
            <circle cx="90" cy="32" r="3" class="v-gnn-unit" />
            <circle cx="90" cy="42" r="3" class="v-gnn-unit" />
            <circle cx="112" cy="26" r="3" class="v-gnn-unit" />
            <circle cx="112" cy="36" r="3" class="v-gnn-unit" />
            <circle cx="134" cy="30" r="3.4" class="v-gnn-unit out" />
            <line x1="90" y1="22" x2="112" y2="26" class="v-gnn-link" />
            <line x1="90" y1="22" x2="112" y2="36" class="v-gnn-link" />
            <line x1="90" y1="32" x2="112" y2="26" class="v-gnn-link" />
            <line x1="90" y1="32" x2="112" y2="36" class="v-gnn-link" />
            <line x1="90" y1="42" x2="112" y2="36" class="v-gnn-link" />
            <line x1="112" y1="26" x2="134" y2="30" class="v-gnn-link" />
            <line x1="112" y1="36" x2="134" y2="30" class="v-gnn-link" />
            <text x="112" y="62" text-anchor="middle" class="v-caption synth-label">GNN</text>

            <defs>
              <marker id="g1" markerWidth="8" markerHeight="8" refX="6" refY="4" orient="auto">
                <path d="M0 0 L8 4 L0 8 Z" class="v-arrow-head" />
              </marker>
            </defs>
          </svg>
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

          <div class="keyword-chips">
            <span class="chip warn">no discretization loss</span>
            <span class="chip">continuous datasets</span>
          </div>

          <svg viewBox="0 0 160 70" class="visual-svg">
            <!-- discretized steps -->
            <path d="M6 50 H22 V42 H38 V46 H54 V34 H68" class="v-step-line" />
            <text x="37" y="62" text-anchor="middle" class="v-caption">discretized</text>

            <path d="M78 36 L96 36" class="v-arrow" marker-end="url(#g2)" />

            <!-- smooth continuous curve -->
            <path d="M104 48 C 112 20, 122 56, 132 28 C 138 12, 146 34, 154 20" class="v-smooth-line" />
            <text x="128" y="62" text-anchor="middle" class="v-caption synth-label">continuous</text>

            <defs>
              <marker id="g2" markerWidth="8" markerHeight="8" refX="6" refY="4" orient="auto">
                <path d="M0 0 L8 4 L0 8 Z" class="v-arrow-head" />
              </marker>
            </defs>
          </svg>
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

          <div class="keyword-chips">
            <span class="chip">conditional GAN</span>
            <span class="chip">diffusion models</span>
          </div>

          <svg viewBox="0 0 160 70" class="visual-svg">
            <!-- noise dots -->
            <circle cx="14" cy="18" r="2" class="v-noise-dot" />
            <circle cx="22" cy="30" r="2.2" class="v-noise-dot" />
            <circle cx="12" cy="40" r="1.8" class="v-noise-dot" />
            <circle cx="26" cy="46" r="2" class="v-noise-dot" />
            <circle cx="30" cy="16" r="1.6" class="v-noise-dot" />
            <circle cx="18" cy="52" r="2.2" class="v-noise-dot" />
            <text x="21" y="64" text-anchor="middle" class="v-caption">noise</text>

            <path d="M40 34 L56 34" class="v-arrow" marker-end="url(#g3)" />

            <!-- denoising steps toward clean trajectory -->
            <path d="M62 44 C 74 24, 86 48, 98 26" class="v-diff-step step1" />
            <path d="M62 40 C 74 22, 86 44, 98 24" class="v-diff-step step2" />
            <path d="M62 36 C 74 20, 86 40, 98 22" class="v-smooth-line" />

            <path d="M104 30 L120 30" class="v-arrow" marker-end="url(#g3)" />

            <!-- generated node -->
            <circle cx="138" cy="24" r="5" class="v-net-node" />
            <circle cx="150" cy="36" r="5" class="v-net-node" />
            <line x1="138" y1="24" x2="150" y2="36" class="v-net-edge" />
            <text x="130" y="64" text-anchor="middle" class="v-caption synth-label">generated</text>

            <defs>
              <marker id="g3" markerWidth="8" markerHeight="8" refX="6" refY="4" orient="auto">
                <path d="M0 0 L8 4 L0 8 Z" class="v-arrow-head" />
              </marker>
            </defs>
          </svg>
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

          <div class="keyword-chips">
            <span class="chip">rare disease transcriptomics</span>
            <span class="chip">single-cell RNA-seq</span>
          </div>

          <svg viewBox="0 0 160 70" class="visual-svg">
            <!-- cell / dataset icon -->
            <circle cx="26" cy="32" r="18" class="v-cell" />
            <circle cx="20" cy="26" r="3" class="v-cell-nucleus" />
            <circle cx="32" cy="36" r="2.2" class="v-cell-nucleus" />
            <circle cx="22" cy="40" r="2" class="v-cell-nucleus" />
            <text x="26" y="62" text-anchor="middle" class="v-caption">patient data</text>

            <path d="M50 32 L68 32" class="v-arrow" marker-end="url(#g4)" />

            <!-- validation report with checkmark -->
            <rect x="74" y="12" width="54" height="40" rx="6" class="v-report" />
            <line x1="82" y1="22" x2="112" y2="22" class="v-report-line" />
            <line x1="82" y1="30" x2="108" y2="30" class="v-report-line" />
            <line x1="82" y1="38" x2="112" y2="38" class="v-report-line" />
            <circle cx="138" cy="42" r="11" class="v-check-circle" />
            <path d="M133 42 L137 46 L144 37" class="v-check-mark" />
            <text x="106" y="62" text-anchor="middle" class="v-caption synth-label">validated</text>

            <defs>
              <marker id="g4" markerWidth="8" markerHeight="8" refX="6" refY="4" orient="auto">
                <path d="M0 0 L8 4 L0 8 Z" class="v-arrow-head" />
              </marker>
            </defs>
          </svg>
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

  display: flex;
  flex-direction: column;
}

.horizon-content h3 {
  margin: 0 0 8px;

  color: #173F5F;

  font-size: 14px;
  line-height: 1.2;

  font-weight: 700;

  transition: color 0.22s ease;
}

.horizon.visible:hover .horizon-content h3 {
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

.chip.warn {
  background: #FDF1E7;
  border-color: #F0D0AB;
  color: #B6560C;
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

/* --- shared: network nodes --- */

.v-net-node {
  fill: #EDF8F6;
  stroke: #2A9D8F;
  stroke-width: 1.3;
}

.v-net-edge {
  stroke: #2A9D8F;
  stroke-width: 1.2;
  opacity: 0.75;
}

/* --- 01: GNN --- */

.v-gnn-box {
  fill: #F4F8FB;
  stroke: #20639B;
  stroke-width: 1.4;
}

.v-gnn-unit {
  fill: #EEF5FA;
  stroke: #20639B;
  stroke-width: 1.2;
}

.v-gnn-unit.out {
  fill: #EDF8F6;
  stroke: #2A9D8F;
}

.v-gnn-link {
  stroke: #9BBFD2;
  stroke-width: 1;
  opacity: 0.8;
}

/* --- 02: discretized vs continuous --- */

.v-step-line {
  fill: none;
  stroke: #94A3B8;
  stroke-width: 1.8;
  stroke-linejoin: round;
}

.v-smooth-line {
  fill: none;
  stroke: #2A9D8F;
  stroke-width: 2;
  stroke-linecap: round;
}

/* --- 03: diffusion --- */

.v-noise-dot {
  fill: #CBD5E1;
  opacity: 0.8;
}

.v-diff-step {
  fill: none;
  stroke-width: 1.4;
  stroke-linecap: round;
}

.v-diff-step.step1 {
  stroke: #E2E8F0;
}

.v-diff-step.step2 {
  stroke: #B9D7E8;
}

/* --- 04: clinical validation --- */

.v-cell {
  fill: #FDF1E7;
  stroke: #E9C46A;
  stroke-width: 1.4;
}

.v-cell-nucleus {
  fill: #B5860C;
  opacity: 0.75;
}

.v-report {
  fill: #F4F8FB;
  stroke: #94A3B8;
  stroke-width: 1.3;
}

.v-report-line {
  stroke: #CBD5E1;
  stroke-width: 1.6;
  stroke-linecap: round;
}

.v-check-circle {
  fill: #EDF8F6;
  stroke: #2A9D8F;
  stroke-width: 1.4;
}

.v-check-mark {
  fill: none;
  stroke: #2A9D8F;
  stroke-width: 2;
  stroke-linecap: round;
  stroke-linejoin: round;
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