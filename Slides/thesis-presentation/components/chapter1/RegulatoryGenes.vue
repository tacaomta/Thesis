<script setup>
import { ref, computed, watch, onMounted, onBeforeUnmount } from 'vue'
import { useNav } from '@slidev/client'

const { currentPage } = useNav()
const isExporting =
  typeof window !== 'undefined' &&
  (
    window.location.pathname.startsWith('/export') ||
    new URLSearchParams(window.location.search).has('print') ||
    new URLSearchParams(window.location.search).has('range')
  )

const visibleCount = ref(0)
const totalItems = 5

const progressDeg = computed(() => (visibleCount.value / totalItems) * 360)

watch(currentPage, () => {
  if (isExporting) {
    visibleCount.value = totalItems
  } else {
    visibleCount.value = 0
  }
})

function handleKeydown(event) {
  if (event.code !== 'Space') return

  event.preventDefault()
  event.stopPropagation()

  if (visibleCount.value < totalItems) {
    visibleCount.value += 1
  }
}

onMounted(() => {
  if (isExporting) {
    visibleCount.value = totalItems
  }
  window.addEventListener('keydown', handleKeydown, true)
})

onBeforeUnmount(() => {
  window.removeEventListener('keydown', handleKeydown, true)
})
</script>

<template>
  <div class="regulatory-slide">

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
              <div class="label">GENE-TO-GENE CONTROL</div>
              <h3>One gene can switch another on or off</h3>
              <p>
                Just like <strong>a switch</strong>, one gene can tell another to start
                or stop working.
              </p>
            </div>
          </div>
        </Transition>

        <!-- 02 -->
        <Transition name="reveal">
          <div v-if="visibleCount >= 2" class="gap-item">
            <div class="number">02</div>

            <div class="content">
              <div class="label">COORDINATED RESPONSE</div>
              <h3>Genes act together, not alone</h3>
              <p>
                Many genes work as <strong>a team</strong> so the cell can do
                complex tasks correctly.
              </p>
            </div>
          </div>
        </Transition>

        <!-- 03 -->
        <Transition name="reveal">
          <div v-if="visibleCount >= 3" class="gap-item">
            <div class="number">03</div>

            <div class="content">
              <div class="label">ADAPTING TO CHANGE</div>
              <h3>Cells react to heat, stress, and surroundings</h3>
              <p>
                Gene control lets the body <strong>adjust quickly</strong> when
                conditions change.
              </p>
            </div>
          </div>
        </Transition>

        <!-- 04 -->
        <Transition name="reveal">
          <div v-if="visibleCount >= 4" class="gap-item">
            <div class="number">04</div>

            <div class="content">
              <div class="label">MASTER REGULATORS</div>
              <h3>A few genes control many others</h3>
              <p>
                Finding these <strong>key switches</strong> explains a lot about
                how the whole system behaves.
              </p>
            </div>
          </div>
        </Transition>

        <!-- 05 -->
        <Transition name="reveal">
          <div v-if="visibleCount >= 5" class="gap-item impact">
            <div class="number">05</div>

            <div class="content">
              <div class="label">DISEASE &amp; DRUG TARGETS</div>
              <h3>Faulty control often leads to disease</h3>
              <p>
                Knowing which gene <strong>broke the switch</strong> helps
                scientists design better treatments.
              </p>
            </div>
          </div>
        </Transition>

      </div>

      <!-- =========================
           HUB — trunk line, dots,
           branch line, pie-progress
           circle connecting the stack
           to the visualization
      ========================== -->
      <div class="hub-gutter">

        <div class="trunk-line"></div>

        <Transition name="dot-fade">
          <span v-if="visibleCount >= 1" class="trunk-dot" style="top: 10%"></span>
        </Transition>

        <Transition name="dot-fade">
          <span v-if="visibleCount >= 2" class="trunk-dot" style="top: 30%"></span>
        </Transition>

        <Transition name="dot-fade">
          <span v-if="visibleCount >= 4" class="trunk-dot" style="top: 70%"></span>
        </Transition>

        <Transition name="dot-fade">
          <span v-if="visibleCount >= 5" class="trunk-dot" style="top: 90%"></span>
        </Transition>

        <div class="branch-line"></div>

        <div
          class="hub-circle"
          :style="{ background: `conic-gradient(#2a9d8f ${progressDeg}deg, #ffffff ${progressDeg}deg 360deg)` }"
          role="img"
          :aria-label="`${visibleCount} of ${totalItems} points revealed`"
        >
          <div class="hub-inner">
            <svg viewBox="0 0 24 24" class="hub-icon" aria-hidden="true">
              <circle cx="7" cy="7" r="2.6" />
              <circle cx="17" cy="7" r="2.6" />
              <circle cx="12" cy="18" r="2.6" />
              <path d="M9.3 8.7 L10.7 15.5" />
              <path d="M14.7 8.7 L13.3 15.5" />
              <path d="M9.6 7 L14.4 7" />
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

        <div class="viz-eyebrow">REGULATORY CONTROL</div>
        <h4 class="viz-title">Why Finding These Genes Matters</h4>

        <svg class="regulation-svg" viewBox="0 0 620 330" aria-label="Regulatory genes control the expression of target genes and cellular response">
          <defs>
            <marker id="regulatory-arrow" markerWidth="12" markerHeight="12" refX="10" refY="6" orient="auto" markerUnits="userSpaceOnUse">
              <path d="M1 1 L11 6 L1 11" fill="none" stroke="#20639B" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round" />
            </marker>
            <marker id="response-arrow" markerWidth="12" markerHeight="12" refX="10" refY="6" orient="auto" markerUnits="userSpaceOnUse">
              <path d="M1 1 L11 6 L1 11" fill="none" stroke="#2A9D8F" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round" />
            </marker>
          </defs>
          <path d="M155 165 C190 165 205 165 238 165" class="flow-edge regulatory-edge" marker-end="url(#regulatory-arrow)" />
          <path d="M155 165 C188 125 205 102 238 102" class="flow-edge regulatory-edge" marker-end="url(#regulatory-arrow)" />
          <path d="M155 165 C188 205 205 228 238 228" class="flow-edge regulatory-edge" marker-end="url(#regulatory-arrow)" />
          <path d="M338 102 C370 102 386 125 414 142" class="flow-edge response-edge" marker-end="url(#response-arrow)" />
          <path d="M338 175 C370 175 388 165 414 165" class="flow-edge response-edge" marker-end="url(#response-arrow)" />
          <path d="M338 248 C370 248 386 205 414 188" class="flow-edge response-edge" marker-end="url(#response-arrow)" />
          <g class="regulator-node">
            <circle cx="105" cy="175" r="50" />
            <circle cx="105" cy="175" r="40" class="inner-ring" />
            <text x="105" y="167" text-anchor="middle">Regulatory</text>
            <text x="105" y="187" text-anchor="middle">genes</text>
            <text x="105" y="208" text-anchor="middle" class="node-subtitle">CONTROL</text>
          </g>
          <g class="target-node">
            <rect x="238" y="72" width="100" height="60" rx="12" />
            <text x="288" y="107" text-anchor="middle">Gene A</text>
          </g>
          <g class="target-node">
            <rect x="238" y="145" width="100" height="60" rx="12" />
            <text x="288" y="180" text-anchor="middle">Gene B</text>
          </g>
          <g class="target-node">
            <rect x="238" y="218" width="100" height="60" rx="12" />
            <text x="288" y="253" text-anchor="middle">Gene C</text>
          </g>
          <g class="response-node">
            <rect x="414" y="125" width="155" height="80" rx="16" />
            <circle cx="445" cy="165" r="19" class="response-circle" />
            <path d="M436 165 L443 172 L455 157" class="response-check" />
            <text x="490" y="158" text-anchor="middle">Cellular</text>
            <text x="490" y="178" text-anchor="middle">response</text>
          </g>
          <text x="105" y="285" text-anchor="middle" class="group-label">UPSTREAM CONTROL</text>
          <text x="288" y="295" text-anchor="middle" class="group-label">TARGET GENES</text>
          <text x="491" y="285" text-anchor="middle" class="group-label">BIOLOGICAL OUTCOME</text>
        </svg>

        <div class="viz-footnote">
          Reveal
          <strong>disease mechanisms</strong> and point toward
          <strong>potential therapeutic targets</strong>.
        </div>

      </div>

    </div>

  </div>
</template>

<style scoped>
.regulatory-slide {
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

  gap: 8px;
}

.gap-item {
  display: grid;
  grid-template-columns: 46px minmax(0, 1fr);

  column-gap: 14px;

  padding: 10px 16px 10px 12px;

  background: #ffffff;

  border: 1px solid #dce4e9;
  border-radius: 9px;

  box-sizing: border-box;
}

.number {
  width: 32px;
  height: 32px;

  display: flex;
  align-items: center;
  justify-content: center;

  border-radius: 50%;

  background: #f0f5f7;
  border: 1px solid #cbd8df;

  color: #173f5f;

  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 11px;
  font-weight: 700;
}

.content {
  min-width: 0;
}

.label {
  margin-bottom: 2px;

  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 8px;
  font-weight: 700;
  letter-spacing: 0.1em;

  color: #20639b;
}

.gap-item h3 {
  margin: 0 0 3px;

  font-size: 13.5px;
  line-height: 1.22;
  font-weight: 700;

  color: #173f5f;
}

.gap-item p {
  margin: 0;

  max-width: 900px;

  font-size: 10.5px;
  line-height: 1.38;

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
  flex: 0 0 38%;
  min-width: 0;

  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;

  padding: 18px 16px 16px;
  box-sizing: border-box;

  background: #ffffff;
  border: 1px solid #dce4e9;
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

.regulation-svg {
  width: 100%;
  max-width: 560px;
  height: auto;
  overflow: visible;
}

.flow-edge {
  fill: none;
  stroke-width: 3;
  stroke-linecap: round;
}

.regulatory-edge {
  stroke: #20639b;
}

.response-edge {
  stroke: #2a9d8f;
}

.regulator-node circle {
  fill: #edf5f9;
  stroke: #20639b;
  stroke-width: 2.5;
}

.regulator-node .inner-ring {
  fill: none;
  stroke: #9bbfd2;
  stroke-width: 1;
  stroke-dasharray: 3 4;
}

.regulator-node text {
  fill: #173f5f;
  font-size: 12px;
  font-weight: 700;
}

.regulator-node .node-subtitle {
  fill: #64748b;
  font-size: 7px;
  font-weight: 700;
  letter-spacing: 0.12em;
}

.target-node rect {
  fill: #ffffff;
  stroke: #20639b;
  stroke-width: 2;
}

.target-node text {
  fill: #173f5f;
  font-size: 14px;
  font-weight: 700;
}

.response-node rect {
  fill: #f1faf8;
  stroke: #2a9d8f;
  stroke-width: 2;
}

.response-circle {
  fill: #2a9d8f;
  stroke: none;
}

.response-check {
  fill: none;
  stroke: #ffffff;
  stroke-width: 2.5;
  stroke-linecap: round;
  stroke-linejoin: round;
}

.response-node text {
  fill: #206b63;
  font-size: 13px;
  font-weight: 700;
}

.group-label {
  fill: #94a3b8;
  font-size: 8px;
  font-weight: 700;
  letter-spacing: 0.12em;
}

.viz-footnote {
  margin-top: 6px;

  max-width: 500px;

  color: #64748b;

  font-size: 10.5px;
  line-height: 1.4;
  text-align: center;
}

.viz-footnote strong {
  color: #173f5f;
  font-weight: 700;
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