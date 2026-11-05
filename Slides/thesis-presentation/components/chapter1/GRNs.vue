<template>
  <div class="thesis-network">

    <div class="slide-body">

      <!-- LEFT: FOUR PROGRESSIVE CARDS -->
      <section class="grn-definition">

        <!-- Card 1: Definition -->

        <!-- Card 2: Node -->
        <Transition name="fade-up">
          <div v-if="visibleCount >= 1" class="concept-card node-card">
            <div class="card-heading">
              <span class="card-number">01</span>
              <h2>Node (Gene)</h2>
            </div>
            <div class="node-visual">
              <div class="node-item">
                <div class="gene-node regulator-node">A</div>
                <span>Regulator</span>
              </div>

              <div class="node-plus">+</div>

              <div class="node-item">
                <div class="gene-node target-node">B</div>
                <span>Target</span>
              </div>
            </div>

            <!-- connector reaching toward the figure -->
            <div class="link-arrow link-arrow-node" aria-hidden="true">
              <svg viewBox="0 0 60 16" class="link-arrow-svg">
                <line x1="2" y1="8" x2="48" y2="8" class="link-arrow-line" />
                <path d="M40 2 L52 8 L40 14" class="link-arrow-head" />
              </svg>
            </div>
          </div>
        </Transition>

        <!-- Card 3: Directed Edge -->
        <Transition name="fade-up">
          <div v-if="visibleCount >= 2" class="concept-card edge-card">
            <div class="card-heading">
              <span class="card-number">02</span>
              <h2>Directed Edge (Regulatory influence)</h2>
            </div>

            <div class="edge-visual">

              <div class="edge-item">
                <div class="edge-diagram">
                  <span class="edge-node">A</span>
                  <svg viewBox="0 0 70 20" class="edge-svg">
                    <path d="M3 10 H62" class="enhancer-line" />
                    <path d="M54 3 L63 10 L54 17" class="enhancer-head" />
                  </svg>
                  <span class="edge-node">B</span>
                </div>
                <span class="edge-label enhancer-label">Enhancer</span>
              </div>

              <div class="edge-item">
                <div class="edge-diagram">
                  <span class="edge-node">A</span>
                  <svg viewBox="0 0 70 20" class="edge-svg">
                    <path d="M3 10 H59" class="inhibitor-line" />
                    <path d="M59 3 V17" class="inhibitor-head" />
                  </svg>
                  <span class="edge-node">B</span>
                </div>
                <span class="edge-label inhibitor-label">Inhibitor</span>
              </div>

            </div>

            <!-- connector reaching toward the figure -->
            <div class="link-arrow link-arrow-edge" aria-hidden="true">
              <svg viewBox="0 0 60 16" class="link-arrow-svg">
                <line x1="2" y1="8" x2="48" y2="8" class="link-arrow-line" />
                <path d="M40 2 L52 8 L40 14" class="link-arrow-head" />
              </svg>
            </div>
          </div>
        </Transition>

        <!-- Card 4: Key takeaway -->
        <Transition name="fade-up">
          <div v-if="visibleCount >= 3" class="takeaway-card">
            <span class="takeaway-label">KEY TAKEAWAY</span>

            <p>
              GRN = Genes
              <span class="takeaway-plus">+</span>
              directed regulatory relationships
            </p>
          </div>
        </Transition>

        <!-- Space hint -->
        <div v-if="visibleCount < 3" class="space-hint">
          Press SPACE to reveal
          {{ visibleCount === 0 ? 'the definition' : 'the next concept' }}
        </div>

      </section>

      <!-- RIGHT: ORIGINAL NETWORK IMAGE -->
      <section class="grn-visual">
        <figure class="network-figure">

          <div class="image-frame">

            <img
              src="../../public/images/GRN.png"
              alt="An example of GRNs, size of 100"
              class="network-image"
            />

            <!-- legend overlay, synced with the left cards:
                 tells the viewer what to look for in the figure -->
            <div class="image-legend">

              <Transition name="legend-fade">
                <div v-if="visibleCount >= 1" class="legend-row">
                  <span class="legend-dot legend-dot-regulator"></span>
                  <span class="legend-dot legend-dot-target"></span>
                  <span>Nodes = genes</span>
                </div>
              </Transition>

              <Transition name="legend-fade">
                <div v-if="visibleCount >= 2" class="legend-row">
                  <span class="legend-dot legend-dot-enhancer"></span>
                  <span>Enhancer</span>
                  <span class="legend-dot legend-dot-inhibitor"></span>
                  <span>Inhibitor</span>
                </div>
              </Transition>

            </div>

          </div>

          <figcaption class="network-caption">
            An example of GRNs, size of 100
          </figcaption>
        </figure>
      </section>

    </div>

  </div>
</template>

<script setup>
import { ref, watch, onMounted, onBeforeUnmount } from 'vue'
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
const totalItems = 4

watch(currentPage, () => {
  visibleCount.value = isExporting ? totalItems : 0
})

/* =========================================================
   SPACE NAVIGATION
   ========================================================= */

function handleKeydown(event) {
  if (event.code !== 'Space') return

  const target = event.target
  const isEditable =
    target?.isContentEditable ||
    ['INPUT', 'TEXTAREA', 'SELECT', 'BUTTON'].includes(target?.tagName)

  if (isEditable || event.repeat) return

  event.preventDefault()
  event.stopPropagation()

  if (visibleCount.value < totalItems) {
    visibleCount.value += 1
  }
}

/* =========================================================
   LIFECYCLE
   ========================================================= */

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

<style scoped>
/* =========================================================
   ROOT
   ========================================================= */

.thesis-network {
  position: relative;

  width: 100%;
  height: 100%;

  background: #F8FAFB;
  color: #24313A;

  overflow: hidden;
  box-sizing: border-box;
}

/* =========================================================
   MAIN LAYOUT
   ========================================================= */

.slide-body {
  position: absolute;

  top: 10px;
  left: 64px;
  right: 64px;

  height: calc(100% - 55px);

  display: flex;
  align-items: stretch;

  gap: 46px;
}

/* =========================================================
   LEFT — FOUR CARDS
   ========================================================= */

.grn-definition {
  width: 40%;
  min-width: 0;

  display: flex;
  flex-direction: column;

  gap: 11px;

  padding: 12px 0 30px;

  box-sizing: border-box;
}

/* =========================================================
   CARD 1 — DEFINITION
   ========================================================= */

.definition-card {
  flex-shrink: 0;

  padding: 15px 17px;

  background: #ffffff;
  border: 1px solid #dce4e9;
  border-left: 4px solid #20639B;

  border-radius: 7px;
  box-sizing: border-box;
}

.card-label {
  display: block;

  margin-bottom: 7px;

  color: #20639B;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 10px;
  font-weight: 700;

  letter-spacing: 0.1em;
}

.definition {
  margin: 0;

  color: #173F5F;

  font-size: 16px;
  line-height: 1.45;
  font-weight: 600;
}

/* =========================================================
   CARD 2 & 3 — CONCEPT CARDS
   ========================================================= */

.concept-card {
  position: relative;

  flex-shrink: 0;

  padding: 13px 17px 12px;

  background: #ffffff;
  border: 1px solid #dce4e9;

  border-radius: 7px;
  box-sizing: border-box;
}

.card-heading {
  display: flex;
  align-items: center;

  gap: 9px;

  margin-bottom: 5px;
}

.card-number {
  width: 23px;
  height: 23px;

  display: flex;
  align-items: center;
  justify-content: center;

  flex-shrink: 0;

  border-radius: 50%;

  background: #f0f5f8;
  color: #20639B;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 10px;
  font-weight: 700;
}

.card-heading h2 {
  margin: 0;

  color: #173F5F;

  font-size: 16px;
  line-height: 1.3;
  font-weight: 700;
}

.card-description {
  margin: 0 0 10px;

  color: #64748B;

  font-size: 13px;
  line-height: 1.4;
  font-weight: 500;
}

/* =========================================================
   LINK ARROW — connects a concept card to the figure,
   reaching across the gap between the two columns
   ========================================================= */

.link-arrow {
  position: absolute;

  top: 50%;
  right: -46px;

  width: 54px;

  transform: translateY(-50%);

  pointer-events: none;

  opacity: 0;
  animation: linkArrowIn 0.4s ease 0.15s forwards;
}

.link-arrow-svg {
  width: 100%;
  height: 16px;

  overflow: visible;
}

.link-arrow-line {
  stroke-width: 2;
  stroke-linecap: round;
  stroke-dasharray: 3 3;
}

.link-arrow-head {
  fill: none;
  stroke-width: 2;
  stroke-linecap: round;
  stroke-linejoin: round;
}

.link-arrow-node .link-arrow-line,
.link-arrow-node .link-arrow-head {
  stroke: #20639B;
}

.link-arrow-edge .link-arrow-line,
.link-arrow-edge .link-arrow-head {
  stroke: #E76F51;
}

@keyframes linkArrowIn {
  from {
    opacity: 0;
    transform: translateY(-50%) translateX(-6px);
  }
  to {
    opacity: 1;
    transform: translateY(-50%) translateX(0);
  }
}

/* =========================================================
   NODE VISUALIZATION
   ========================================================= */

.node-visual {
  display: flex;
  align-items: center;
  justify-content: center;

  gap: 20px;

  padding: 3px 0 2px;
}

.node-item {
  display: flex;
  align-items: center;
  flex-direction: column;

  gap: 5px;

  color: #64748B;

  font-size: 10px;
  font-weight: 600;
}

.gene-node {
  width: 30px;
  height: 30px;

  display: flex;
  align-items: center;
  justify-content: center;

  border-radius: 50%;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 12px;
  font-weight: 700;
}

.regulator-node {
  color: #20639B;
  background: #eef5fa;
  border: 1.5px solid #20639B;
}

.target-node {
  color: #2A9D8F;
  background: #edf8f6;
  border: 1.5px solid #2A9D8F;
}

.node-plus {
  color: #94A3B8;

  font-size: 19px;
  font-weight: 500;
}

/* =========================================================
   DIRECTED EDGE VISUALIZATION
   ========================================================= */

.edge-visual {
  display: flex;
  align-items: center;
  justify-content: center;

  gap: 24px;

  padding: 2px 0;
}

.edge-item {
  display: flex;
  align-items: center;
  flex-direction: column;

  gap: 5px;
}

.edge-diagram {
  display: flex;
  align-items: center;

  gap: 3px;
}

.edge-node {
  width: 22px;
  height: 22px;

  display: flex;
  align-items: center;
  justify-content: center;

  border: 1px solid #cbd5e1;
  border-radius: 50%;

  background: #f8fafb;
  color: #173F5F;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 9px;
  font-weight: 700;
}

.edge-svg {
  width: 48px;
  height: 20px;

  overflow: visible;
}

.enhancer-line {
  stroke: #20639B;
  stroke-width: 2;
  stroke-linecap: round;
}

.enhancer-head {
  fill: none;
  stroke: #20639B;
  stroke-width: 2;
  stroke-linecap: round;
  stroke-linejoin: round;
}

.inhibitor-line {
  stroke: #E76F51;
  stroke-width: 2;
  stroke-linecap: round;
}

.inhibitor-head {
  stroke: #E76F51;
  stroke-width: 2.5;
  stroke-linecap: round;
}

.edge-label {
  font-size: 10px;
  font-weight: 600;
}

.enhancer-label {
  color: #20639B;
}

.inhibitor-label {
  color: #E76F51;
}

/* =========================================================
   CARD 4 — KEY TAKEAWAY
   ========================================================= */

.takeaway-card {
  flex-shrink: 0;

  margin-top: auto;

  padding: 14px 17px;

  background: #edf8f6;
  border: 1px solid #b9e4dc;
  border-left: 4px solid #2A9D8F;

  border-radius: 7px;
  box-sizing: border-box;
}

.takeaway-label {
  display: block;

  margin-bottom: 6px;

  color: #2A9D8F;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 10px;
  font-weight: 700;

  letter-spacing: 0.1em;
}

.takeaway-card p {
  margin: 0;

  color: #173F5F;

  font-size: 15px;
  line-height: 1.4;
  font-weight: 750;
}

.takeaway-plus {
  color: #2A9D8F;
  padding: 0 3px;
}

/* =========================================================
   RIGHT — ORIGINAL NETWORK IMAGE
   ========================================================= */

.grn-visual {
  position: relative;

  width: 60%;
  height: 100%;

  display: flex;
  align-items: center;
  justify-content: center;

  box-sizing: border-box;
}

.network-figure {
  width: 100%;
  height: 100%;

  margin: 0;

  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;

  gap: 5px;
}

.image-frame {
  position: relative;

  display: flex;
  align-items: center;
  justify-content: center;

  max-width: 100%;
  max-height: calc(100% - 25px);
}

.network-image {
  display: block;

  max-width: 100%;
  max-height: 100%;

  object-fit: contain;

  border-radius: 10px;
  background: #FFFFFF;
}

/* =========================================================
   IMAGE LEGEND — mirrors the concept-card colors, confirming
   that the cards on the left describe elements in this figure
   ========================================================= */

.image-legend {
  position: absolute;

  top: 10px;
  left: -90px;

  display: flex;
  flex-direction: column;
  gap: 5px;

  padding: 7px 10px;

  background: rgba(255, 255, 255, 0.92);
  border: 1px solid #dce4e9;
  border-radius: 7px;

  box-shadow: 0 3px 10px rgba(23, 63, 95, 0.08);

  backdrop-filter: blur(2px);
}

.legend-row {
  display: flex;
  align-items: center;

  gap: 5px;

  color: #475569;

  font-size: 9.5px;
  font-weight: 600;

  white-space: nowrap;
}

.legend-dot {
  width: 8px;
  height: 8px;
  flex-shrink: 0;

  border-radius: 50%;
}

.legend-dot-regulator {
  background: #20639B;
}

.legend-dot-target {
  background: #2A9D8F;
}

.legend-dot-enhancer {
  background: #20639B;
}

.legend-dot-inhibitor {
  background: #E76F51;
}

.legend-fade-enter-active {
  transition:
    opacity 0.3s ease,
    transform 0.3s ease;
}

.legend-fade-enter-from {
  opacity: 0;
  transform: translateX(-6px);
}

.network-caption {
  color: #64748B;

  font-size: 11.5px;
  font-style: italic;
  text-align: center;
}

/* =========================================================
   SPACE HINT
   ========================================================= */

.space-hint {
  margin-top: auto;

  color: #94A3B8;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 9px;

  letter-spacing: 0.03em;
  text-align: left;
}

/* =========================================================
   ANIMATIONS
   ========================================================= */

.fade-up-enter-active {
  transition:
    opacity 0.35s ease,
    transform 0.35s ease;
}

.fade-up-enter-from {
  opacity: 0;
  transform: translateY(10px);
}

/* =========================================================
   RESPONSIVE
   ========================================================= */

@media (max-width: 900px) {
  .slide-body {
    left: 30px;
    right: 30px;

    gap: 24px;
  }

  .grn-definition {
    width: 45%;
  }

  .grn-visual {
    width: 55%;
  }

  .definition {
    font-size: 14px;
  }

  .card-heading h2 {
    font-size: 14px;
  }

  .card-description {
    font-size: 11px;
  }

  .link-arrow {
    width: 20px;
    right: -22px;
  }
}

@media (max-width: 650px) {
  .thesis-network {
    overflow-y: auto;
  }

  .slide-body {
    position: relative;

    top: auto;
    left: auto;
    right: auto;

    height: auto;

    padding: 15px;
    flex-direction: column;
  }

  .grn-definition,
  .grn-visual {
    width: 100%;
  }

  .grn-visual {
    min-height: 300px;
  }

  .network-figure {
    min-height: 280px;
  }

  .network-image {
    max-height: 250px;
  }

  .link-arrow {
    display: none;
  }
}
</style>