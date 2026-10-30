<script setup>
import { ref, computed, watch, onMounted, onBeforeUnmount } from 'vue'
import { useNav } from '@slidev/client'

const { currentPage } = useNav()

watch(currentPage, () => {
  visibleCount.value = 0
})

const visibleCount = ref(0)
const totalItems = 3

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
  <div class="research-gap-03">

    <div class="gap-stage">

      <!-- =========================
           LEFT · STACKED CONTENT
      ========================== -->
      <div class="gap-stack">

        <!-- 01 -->
        <Transition name="reveal">
          <div v-if="visibleCount >= 1" class="gap-item">
            <div class="number">01</div>

            <div class="content">
              <div class="label">BIOLOGICAL COMPLEXITY</div>
              <h3>Temporal Observation Requirements</h3>
              <p>
                Requires observing
                <strong>coordinated gene expression trajectories</strong>
              </p>
            </div>
          </div>
        </Transition>

        <!-- 02 -->
        <Transition name="reveal">
          <div v-if="visibleCount >= 2" class="gap-item">
            <div class="number">02</div>

            <div class="content">
              <div class="label">DATA COLLECTION CONSTRAINTS</div>
              <h3>Biological experiments limit temporal sampling</h3>
              <p>
                Experiments facing
                <strong>high costs, measurement noise,</strong>
                and strict environmental constraints
              </p>
            </div>
          </div>
        </Transition>

        <!-- 03 -->
        <Transition name="reveal">
          <div v-if="visibleCount >= 3" class="gap-item impact">
            <div class="number">03</div>

            <div class="content">
              <div class="label">IMPACT ON INFERENCE</div>
              <h3>Short time-series data weakens GRN inference</h3>
              <p>
                Reduces the
                <strong>accuracy and stability</strong>
                of inference algorithms.
              </p>
            </div>
          </div>
        </Transition>

      </div>

      <!-- =========================
           HUB — trunk line, dots,
           branch line, pie-progress
           circle connecting all 4 cards
      ========================== -->
      <div class="hub-gutter">

        <div class="trunk-line"></div>

        <Transition name="dot-fade">
          <span v-if="visibleCount >= 1" class="trunk-dot" style="top: 18%"></span>
        </Transition>

        <Transition name="dot-fade">
          <span v-if="visibleCount >= 3" class="trunk-dot" style="top: 82%"></span>
        </Transition>

        <div class="branch-line"></div>

        <div
          class="hub-circle"
          :style="{ background: `conic-gradient(#2a9d8f ${progressDeg}deg, #ffffff ${progressDeg}deg 360deg)` }"
          role="img"
          :aria-label="`${visibleCount} of ${totalItems} gap points revealed`"
        >
          <div class="hub-inner">
            <svg viewBox="0 0 24 24" class="hub-icon" aria-hidden="true">
              <path d="M8.5 15.5 L15.5 8.5" />
              <path d="M10 4.5h3a4 4 0 0 1 0 8h-2" />
              <path d="M14 19.5h-3a4 4 0 0 1 0-8h2" />
            </svg>
          </div>
        </div>

      </div>

      <!-- =========================
           RIGHT · VISUALIZATION
           always visible, height
           matches the full stack
      ========================== -->
      <div class="viz-card">

        <div class="viz-eyebrow">RESEARCH GAP</div>
        <h4 class="viz-title">From Signal to Weak Inference</h4>

        <svg viewBox="0 0 220 300" class="viz-svg" aria-label="Funnel diagram showing rich biological signal narrowing through constrained sampling into unstable inference">

          <!-- wide top: rich biological signal -->
          <path d="M20 30 L200 30 L150 110 L70 110 Z" class="funnel-wide" />
          <circle cx="45" cy="50" r="3" class="funnel-dot" />
          <circle cx="75" cy="42" r="3" class="funnel-dot" />
          <circle cx="105" cy="52" r="3" class="funnel-dot" />
          <circle cx="135" cy="44" r="3" class="funnel-dot" />
          <circle cx="165" cy="52" r="3" class="funnel-dot" />
          <circle cx="60" cy="75" r="3" class="funnel-dot" />
          <circle cx="95" cy="80" r="3" class="funnel-dot" />
          <circle cx="130" cy="76" r="3" class="funnel-dot" />
          <circle cx="160" cy="82" r="3" class="funnel-dot" />

          <!-- bottleneck neck: constrained sampling -->
          <path d="M70 110 L150 110 L128 165 L92 165 Z" class="funnel-neck" />
          <line x1="100" y1="128" x2="120" y2="128" class="neck-tick" />
          <line x1="97" y1="145" x2="123" y2="145" class="neck-tick" />

          <!-- narrow bottom: weak / noisy inference -->
          <path d="M92 165 L128 165 L118 230 L102 230 Z" class="funnel-narrow" />

          <path
            d="M110 230 C 106 245, 114 250, 108 262 C 104 272, 116 278, 110 290"
            class="noisy-line"
          />

          <!-- zone labels -->
          <text x="110" y="20" text-anchor="middle" class="zone-label wide">rich biological signal</text>
          <text x="110" y="150" text-anchor="middle" class="zone-label neck">constrained sampling</text>
          <text x="110" y="300" text-anchor="middle" class="zone-label narrow">unstable inference</text>

        </svg>

      </div>

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

  font-family: 'Inter', 'Segoe UI', sans-serif;
}

/* ============================================================
   STAGE — left stack / hub gutter / right viz card
   ============================================================ */

.gap-stage {
  flex: 1;
  min-height: 0;

  display: flex;
  align-items: stretch;

  gap: 0;
}

/* ============================================================
   LEFT · STACKED CONTENT
   ============================================================ */

.gap-stack {
  flex: 1 1 58%;
  min-width: 0;

  display: flex;
  flex-direction: column;
  justify-content: center;

  gap: 14px;
}

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

  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 12px;
  font-weight: 700;
}

.content {
  min-width: 0;
}

.label {
  margin-bottom: 4px;

  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
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
   HUB GUTTER — trunk line + dots + branch + circle
   ============================================================ */

.hub-gutter {
  flex: 0 0 86px;

  position: relative;
}

.trunk-line {
  position: absolute;

  left: 50%;
  top: 6%;
  bottom: 6%;

  width: 2px;

  background: #dce4e9;

  transform: translateX(-50%);
}

.trunk-dot {
  position: absolute;

  left: 50%;

  width: 9px;
  height: 9px;

  border-radius: 50%;

  background: #2a9d8f;
  border: 2px solid #ffffff;
  box-shadow: 0 0 0 1px #2a9d8f;

  transform: translate(-50%, -50%);

  z-index: 2;
}

.dot-fade-enter-active {
  transition:
    opacity 0.3s ease,
    transform 0.3s ease;
}

.dot-fade-enter-from {
  opacity: 0;
  transform: translate(-50%, -50%) scale(0.3);
}

.branch-line {
  position: absolute;

  left: 50%;
  top: 50%;

  width: 50%;
  height: 2px;

  background: #dce4e9;

  transform: translateY(-50%);
}

.hub-circle {
  position: absolute;

  left: 50%;
  top: 50%;

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

  z-index: 3;

  transition: background 0.4s ease;
}

.hub-inner {
  width: 50px;
  height: 50px;

  display: flex;
  align-items: center;
  justify-content: center;

  border-radius: 50%;

  background: #ffffff;
  box-shadow: inset 0 0 0 1px rgba(23, 63, 95, 0.06);
}

.hub-icon {
  width: 26px;
  height: 26px;

  fill: none;
  stroke: #173f5f;
  stroke-width: 1.8;
  stroke-linecap: round;
  stroke-linejoin: round;
}

/* ============================================================
   RIGHT · VISUALIZATION CARD
   height matches the full stack via stretch
   ============================================================ */

.viz-card {
  flex: 0 0 34%;
  min-width: 0;

  display: flex;
  flex-direction: column;
  align-items: center;

  padding: 18px 16px 16px;
  box-sizing: border-box;

  background: #ffffff;
  border: 1px solid #dce4e9;
  /* border-top: 4px solid #2a9d8f; */
  border-radius: 10px;

  box-shadow: 0 4px 12px rgba(23, 63, 95, 0.05);
}

.viz-eyebrow {
  align-self: center;

  color: #2a9d8f;

  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 9px;
  font-weight: 700;
  letter-spacing: 0.14em;
}

.viz-title {
  margin: 4px 0 6px;

  color: #173f5f;

  font-size: 14px;
  line-height: 1.25;
  font-weight: 700;

  text-align: center;
}

.viz-svg {
  flex: 1;
  min-height: 0;
  width: 100%;

  margin-top: 4px;
}

/* funnel zones */

.funnel-wide {
  fill: rgba(32, 99, 155, 0.06);
  stroke: #20639b;
  stroke-width: 1.4;
}

.funnel-dot {
  fill: #20639b;
  opacity: 0.6;
}

.funnel-neck {
  fill: rgba(233, 196, 106, 0.1);
  stroke: #e9c46a;
  stroke-width: 1.4;
}

.neck-tick {
  stroke: #b5860c;
  stroke-width: 1.4;
  opacity: 0.6;
}

.funnel-narrow {
  fill: rgba(42, 157, 143, 0.06);
  stroke: #2a9d8f;
  stroke-width: 1.4;
  stroke-dasharray: 3 3;
}

.noisy-line {
  fill: none;
  stroke: #e76f51;
  stroke-width: 1.6;
  stroke-linecap: round;
}

.zone-label {
  fill: #64748b;

  font-family: 'Inter', 'Segoe UI', sans-serif;
  font-size: 9px;
  font-weight: 600;
}

.zone-label.wide {
  fill: #20639b;
}

.zone-label.neck {
  fill: #8a6a12;
}

.zone-label.narrow {
  fill: #247f76;
}

.viz-footnote {
  margin-top: 6px;

  color: #94a3b8;

  font-size: 9.5px;
  line-height: 1.4;
  text-align: center;
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
  .reveal-enter-active,
  .dot-fade-enter-active,
  .hub-circle {
    transition: none;
  }
}

/* ============================================================
   Responsive
   ============================================================ */

@media (max-width: 900px) {
  .gap-stage {
    flex-direction: column;
  }

  .hub-gutter {
    display: none;
  }

  .viz-card {
    flex: 0 0 auto;
  }
}
</style> 