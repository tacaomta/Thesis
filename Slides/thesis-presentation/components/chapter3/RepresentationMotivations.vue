<script setup>
import { ref,watch, onMounted, onBeforeUnmount } from 'vue'
import { useNav } from '@slidev/client'

const { currentPage } = useNav()

const visibleCount = ref(0)

watch(currentPage, () => {
  visibleCount.value = 0
})
function handleKeydown(event) {
  if (event.code !== 'Space') return

  event.preventDefault()
  event.stopPropagation()

  if (visibleCount.value < 4) {
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
  <div class="research-gap-slide">

    <!-- Three limitations -->
    <div class="limitations-grid">

      <!-- 01 -->
      <Transition name="fade-up">
        <section v-if="visibleCount >= 1" class="gap-card">
          <div class="card-header">
            <span class="card-number">01</span>
            <h2>Separated Encoding</h2>
          </div>

          <svg class="gap-visual" viewBox="0 0 260 130" aria-label="Temporal dynamics and local structure encoded separately">

            <!-- Temporal stream -->
            <g class="viz-group">
              <rect x="10" y="18" width="110" height="38" rx="8" class="viz-box box-a" />
              <path d="M22 37 L34 30 L46 42 L58 28 L70 40 L82 32 L94 38 L106 34" class="viz-wave" />
              <text x="65" y="70" text-anchor="middle" class="viz-label">Temporal dynamics</text>
            </g>

            <!-- Structural stream -->
            <g class="viz-group">
              <rect x="140" y="18" width="110" height="38" rx="8" class="viz-box box-b" />
              <circle cx="163" cy="37" r="5" class="viz-node" />
              <circle cx="188" cy="30" r="5" class="viz-node" />
              <circle cx="188" cy="46" r="5" class="viz-node" />
              <circle cx="213" cy="37" r="5" class="viz-node" />
              <line x1="163" y1="37" x2="188" y2="30" class="viz-edge" />
              <line x1="163" y1="37" x2="188" y2="46" class="viz-edge" />
              <line x1="188" y1="30" x2="213" y2="37" class="viz-edge" />
              <line x1="188" y1="46" x2="213" y2="37" class="viz-edge" />
              <text x="195" y="70" text-anchor="middle" class="viz-label">Local structure</text>
            </g>

            <!-- broken link in the middle -->
            <line x1="124" y1="37" x2="136" y2="37" class="viz-broken" />
            <text x="130" y="97" text-anchor="middle" class="viz-caption">encoded independently, no shared representation</text>
          </svg>
        </section>
      </Transition>

      <!-- 02 -->
      <Transition name="fade-up">
        <section v-if="visibleCount >= 2" class="gap-card">
          <div class="card-header">
            <span class="card-number">02</span>
            <h2>Rigid Hyperparameter Assumptions</h2>
          </div>

          <svg class="gap-visual" viewBox="0 0 260 130" aria-label="Models locked to fixed time delay, candidate set and kernel choice">

            <g class="viz-group">
              <rect x="8"   y="22" width="72" height="48" rx="8" class="viz-box box-c" />
              <text x="44" y="42" text-anchor="middle" class="viz-mono">Δt</text>
              <text x="44" y="56" text-anchor="middle" class="viz-mono-sub">fixed lag</text>

              <rect x="94" y="22" width="72" height="48" rx="8" class="viz-box box-c" />
              <text x="130" y="42" text-anchor="middle" class="viz-mono">{g}</text>
              <text x="130" y="56" text-anchor="middle" class="viz-mono-sub">candidate set</text>

              <rect x="180" y="22" width="72" height="48" rx="8" class="viz-box box-c" />
              <text x="216" y="42" text-anchor="middle" class="viz-mono">K(·)</text>
              <text x="216" y="56" text-anchor="middle" class="viz-mono-sub">kernel</text>

              <!-- lock icons on top -->
              <g class="viz-lock" transform="translate(37,6)">
                <rect x="0" y="5" width="14" height="10" rx="2" />
                <path d="M3 5 V2.5 a4 4 0 0 1 8 0 V5" />
              </g>
              <g class="viz-lock" transform="translate(123,6)">
                <rect x="0" y="5" width="14" height="10" rx="2" />
                <path d="M3 5 V2.5 a4 4 0 0 1 8 0 V5" />
              </g>
              <g class="viz-lock" transform="translate(209,6)">
                <rect x="0" y="5" width="14" height="10" rx="2" />
                <path d="M3 5 V2.5 a4 4 0 0 1 8 0 V5" />
              </g>
            </g>

            <text x="130" y="97" text-anchor="middle" class="viz-caption">locked to pre-defined, dataset-specific settings</text>
          </svg>
        </section>
      </Transition>

      <!-- 03 -->
      <Transition name="fade-up">
        <section v-if="visibleCount >= 3" class="gap-card">
          <div class="card-header">
            <span class="card-number">03</span>
            <h2>Severe Class Imbalance</h2>
          </div>

          <svg class="gap-visual" viewBox="0 0 260 130" aria-label="Positive regulatory interactions become rarer as network size grows">

            <!-- small network -->
            <g class="viz-group">
              <text x="48" y="20" text-anchor="middle" class="viz-mono-sub">N = 10</text>
              <rect x="18" y="30" width="60" height="20" rx="10" class="ratio-bar">
                <title>small network ratio</title>
              </rect>
              <rect x="18" y="30" width="22" height="20" rx="10" class="ratio-bar-pos" />
              <text x="48" y="63" text-anchor="middle" class="viz-mono-sub pos-color">~35% positive</text>
            </g>

            <!-- large network -->
            <g class="viz-group">
              <text x="195" y="20" text-anchor="middle" class="viz-mono-sub">N = 200</text>
              <rect x="150" y="30" width="90" height="20" rx="10" class="ratio-bar" />
              <rect x="150" y="30" width="6"  height="20" rx="10" class="ratio-bar-pos" />
              <text x="195" y="63" text-anchor="middle" class="viz-mono-sub pos-color">~3% positive</text>
            </g>

            <path d="M86 40 L142 40" class="viz-arrow-line" marker-end="url(#gapArrow)" />
            <defs>
              <marker id="gapArrow" markerWidth="8" markerHeight="8" refX="6" refY="4" orient="auto">
                <path d="M0 0 L8 4 L0 8 Z" class="viz-arrow-head" />
              </marker>
            </defs>

            <text x="130" y="97" text-anchor="middle" class="viz-caption">positive interactions grow sparser as N increases</text>
          </svg>
        </section>
      </Transition>

    </div>

    <!-- Research gap -->
    <Transition name="fade-up">
      <section v-if="visibleCount >= 4" class="research-gap-box">
        <div class="gap-label">
          RESEARCH GAP
        </div>

        <div class="gap-statement">
          Existing frameworks lack a unified and generalizable
          representation of regulatory relationships from
          time-series expression data.
        </div>
      </section>
    </Transition>

    <!-- Space hint -->
    <div v-if="visibleCount < 4" class="space-hint">
      Press SPACE to reveal the next limitation
    </div>

  </div>
</template>

<style scoped>
.research-gap-slide {
  width: 100%;
  height: 100%;
  box-sizing: border-box;

  display: flex;
  flex-direction: column;

  padding: 10px 24px 4px;
}

/* =========================
   Limitations
   ========================= */

.limitations-grid {
  flex: 1;
  min-height: 0;

  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 18px;

  align-items: stretch;
  margin-top: 60px;
}

.gap-card {
  position: relative;

  display: flex;
  flex-direction: column;

  min-width: 0;

  padding: 24px 22px 22px;

  background: #ffffff;
  border: 1px solid #dce4e9;
  border-radius: 8px;

  box-sizing: border-box;
}

.gap-card::before {
  content: '';

  position: absolute;
  top: 0;
  left: 0;
  right: 0;

  height: 4px;

  background: #20639b;

  border-radius: 8px 8px 0 0;
}

/* =========================
   Card header
   ========================= */

.card-header {
  display: flex;
  align-items: center;
  gap: 13px;

  margin-bottom: 20px;
}

.card-number {
  width: 36px;
  height: 36px;

  flex-shrink: 0;

  display: flex;
  align-items: center;
  justify-content: center;

  border-radius: 50%;

  background: #f0f5f8;
  color: #173f5f;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 12px;
  font-weight: 600;
}

.card-header h2 {
  margin: 0;

  color: #173f5f;

  font-size: 19px;
  line-height: 1.25;
  font-weight: 650;
}

/* =========================
   Visualization (replaces <p>)
   ========================= */

.gap-visual {
  flex: 1;
  width: 100%;
  min-height: 0;

  margin-top: 4px;
}

.viz-box {
  fill: #f8fafb;
  stroke: #dce4e9;
  stroke-width: 1.5;
}

.box-a {
  stroke: #20639b;
}

.box-b {
  stroke: #2a9d8f;
}

.box-c {
  stroke: #e9c46a;
}

.viz-wave {
  fill: none;
  stroke: #20639b;
  stroke-width: 2;
  stroke-linecap: round;
  stroke-linejoin: round;
}

.viz-node {
  fill: #eafaf7;
  stroke: #2a9d8f;
  stroke-width: 1.5;
}

.viz-edge {
  stroke: #2a9d8f;
  stroke-width: 1.3;
  opacity: 0.6;
}

.viz-broken {
  stroke: #cbd5e1;
  stroke-width: 2;
  stroke-dasharray: 3 4;
}

.viz-label {
  fill: #64748b;
  font-family: 'Inter', 'Segoe UI', sans-serif;
  font-size: 9.5px;
  font-weight: 600;
}

.viz-caption {
  fill: #94a3b8;
  font-family: 'Inter', 'Segoe UI', sans-serif;
  font-size: 10px;
  font-style: italic;
}

.viz-mono {
  fill: #173f5f;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 13px;
  font-weight: 700;
}

.viz-mono-sub {
  fill: #64748b;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 8px;
  font-weight: 600;
}

.pos-color {
  fill: #e76f51;
}

.viz-lock {
  fill: none;
  stroke: #b5860c;
  stroke-width: 1.6;
  stroke-linecap: round;
  stroke-linejoin: round;
}

.viz-lock rect {
  fill: #fdf8ec;
}

.ratio-bar {
  fill: #eef3f6;
  stroke: #dce4e9;
  stroke-width: 1;
}

.ratio-bar-pos {
  fill: #e76f51;
  opacity: 0.85;
}

.viz-arrow-line {
  stroke: #94a3b8;
  stroke-width: 1.6;
}

.viz-arrow-head {
  fill: #94a3b8;
}

/* =========================
   Research gap
   ========================= */

.research-gap-box {
  flex-shrink: 0;

  display: flex;
  align-items: center;
  gap: 20px;

  margin: 18px auto 4px;
  padding: 14px 20px;

  width: min(920px, 100%);
  box-sizing: border-box;

  background: #f8fafb;
  border: 1px solid #dce4e9;
  border-left: 4px solid #2a9d8f;

  border-radius: 6px;
}

.gap-label {
  flex-shrink: 0;

  color: #2a9d8f;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.05em;
}

.gap-statement {
  color: #24313a;

  font-size: 15px;
  line-height: 1.45;
  font-weight: 500;
}

/* =========================
   Space hint
   ========================= */

.space-hint {
  flex-shrink: 0;

  height: 20px;

  display: flex;
  align-items: center;
  justify-content: center;

  margin-top: 6px;

  color: #94a3b8;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 10px;
  letter-spacing: 0.04em;
}

/* =========================
   Animations
   ========================= */

.fade-up-enter-active {
  transition:
    opacity 0.35s ease,
    transform 0.35s ease;
}

.fade-up-enter-from {
  opacity: 0;
  transform: translateY(12px);
}

/* =========================
   Responsive
   ========================= */

@media (max-width: 850px) {
  .limitations-grid {
    grid-template-columns: 1fr;
    overflow-y: auto;
  }

  .gap-card {
    min-height: 220px;
  }

  .research-gap-box {
    width: 100%;
  }
}
</style>