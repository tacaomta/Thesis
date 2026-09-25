<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

const visibleCount = ref(0)
const totalItems = 3

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
  <div class="matrix-transformation">
    <div class="blocks">

      <!-- Block 01 -->
      <Transition name="reveal">
        <section v-if="visibleCount >= 1" class="info-block">
          <div class="block-header"><span class="block-number">01</span><h2>Input Matrix</h2></div>

          

          <div class="matrix-box">
            <span class="matrix-label">Observed expression data</span>
            <div class="matrix">
              <span>v₁(t₁)</span>
              <span>v₂(t₁)</span>
              <span>⋯</span>
              <span>vₙ(t₁)</span>

              <span>v₁(t₂)</span>
              <span>v₂(t₂)</span>
              <span>⋯</span>
              <span>vₙ(t₂)</span>

              <span>⋮</span>
              <span>⋮</span>
              <span>⋱</span>
              <span>⋮</span>

              <span>v₁(tₖ)</span>
              <span>v₂(tₖ)</span>
              <span>⋯</span>
              <span>vₙ(tₖ)</span>
            </div>
          </div>

          <div class="dimension">
            <strong>k × n</strong>
            <span>observed time steps × genes</span>
          </div>

          <p>
            The observed time-series expression matrix contains
            <strong>k</strong> time steps for <strong>n</strong> genes.
          </p>
        </section>
      </Transition>

      <!-- Block 02 -->
      <Transition name="reveal">
        <section v-if="visibleCount >= 2" class="info-block highlight">
          <div class="block-header"><span class="block-number">02</span><h2>Vector Formulation</h2></div>

          

          <div class="equation-box">
            <div class="equation">
              T(t<sub>i</sub> ⊕ t<sub>i+1</sub>) =
            </div>

            <div class="vector">
              [
              <span>v₁(t<sub>i</sub>)</span>,
              <span>…</span>,
              <span>vₙ(t<sub>i</sub>)</span>,
              <span class="separator">|</span>
              <span>v₁(t<sub>i+1</sub>)</span>,
              <span>…</span>,
              <span>vₙ(t<sub>i+1</sub>)</span>
              ]
            </div>
          </div>

          <div class="transformation">
            <div class="dimension old">
              <strong>k × n</strong>
            </div>

            <div class="arrow">→</div>

            <div class="dimension new">
              <strong>(k − 1) × 2n</strong>
            </div>
          </div>

          <p>
            Consecutive expression states are concatenated into
            <strong>2n-dimensional transition vectors</strong>.
          </p>
        </section>
      </Transition>

      <!-- Block 03 -->
      <Transition name="reveal">
        <section v-if="visibleCount >= 3" class="info-block">
          <div class="block-header"><span class="block-number">03</span><h2>Why This Transformation?</h2></div>

          

          <div class="transition-visual">
            <div class="state">
              <span class="state-label">t<sub>i</sub></span>
              <div class="gene-row">
                <span>v₁</span>
                <span>v₂</span>
                <span>⋯</span>
                <span>vₙ</span>
              </div>
            </div>

            <div class="transition-arrow">
              <span>transition</span>
              →
            </div>

            <div class="state">
              <span class="state-label">t<sub>i+1</sub></span>
              <div class="gene-row">
                <span>v₁</span>
                <span>v₂</span>
                <span>⋯</span>
                <span>vₙ</span>
              </div>
            </div>
          </div>

          <p class="rationale">
            Explicitly exposes
            <strong>state-transition correlations</strong>
            to the neural network, enabling accurate prediction of
            future gene-expression states.
          </p>

          <div class="key-message">
            <span class="message-icon">→</span>
            <span>
              Learn <strong>how the system changes</strong>,
              not only its individual states.
            </span>
          </div>
        </section>
      </Transition>

    </div>
  </div>
</template>

<style scoped>
.matrix-transformation {
  width: 100%;
  height: 100%;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
}

.blocks {
  min-height: 0;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
}

/* =========================
   BLOCK
========================= */

.info-block {
  min-width: 0;
  height: 100%;
  box-sizing: border-box;

  display: flex;
  flex-direction: column;

  padding: 18px 15px;

  background: #ffffff;
  border: 1px solid #dce4e9;
  border-top: 4px solid #173f5f;
  border-radius: 10px;

  box-shadow: 0 4px 12px rgba(23, 63, 95, 0.06);
  margin-top: 20px;
}

.info-block.highlight {
  border-top-color: #2a9d8f;
}

/* =========================
   HEADER
========================= */

.block-header {
  display: flex;
  align-items: baseline;
  gap: 6px;
  margin-bottom: 10px;
}

.block-number {
  flex: 0 0 auto;

  color: #2a9d8f;
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 13px;
  font-weight: 700;
  letter-spacing: 0.08em;
}

h2 {
  margin: 0;

  color: #173f5f;
  font-size: 20px;
  line-height: 1.2;
  font-weight: 700;
}

p {
  margin: 12px 0 0;
  color: #64748b;
  font-size: 15px;
  line-height: 1.55;
}

p strong {
  color: #24313a;
}

/* =========================
   MATRIX
========================= */

.matrix-box {
  padding: 15px 12px;
  background: #f8fafb;
  border: 1px solid #dce4e9;
  border-radius: 8px;
}

.matrix-label {
  display: block;
  margin-bottom: 12px;

  color: #64748b;
  font-size: 11px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

.matrix {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px 6px;

  color: #24313a;
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 12px;
  text-align: center;
}

.dimension {
  margin-top: 16px;
  display: flex;
  align-items: baseline;
  gap: 9px;
}

.dimension strong {
  color: #20639b;
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 19px;
}

.dimension span {
  color: #64748b;
  font-size: 12px;
}

/* =========================
   EQUATION
========================= */

.equation-box {
  min-height: 125px;
  padding: 18px 12px;

  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 14px;

  background: #f8fafb;
  border: 1px solid #dce4e9;
  border-radius: 8px;

  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  color: #24313a;
}

.equation {
  font-size: 15px;
  color: #173f5f;
  text-align: center;
}

.vector {
  font-size: 11px;
  line-height: 1.8;
  text-align: center;
  word-break: break-word;
}

.vector span {
  color: #20639b;
}

.vector .separator {
  margin: 0 4px;
  color: #2a9d8f;
  font-weight: 700;
}

.transformation {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 14px;

  margin-top: 20px;
}

.transformation .dimension {
  margin: 0;
  padding: 7px 11px;

  background: #f8fafb;
  border: 1px solid #dce4e9;
  border-radius: 6px;
}

.transformation .dimension strong {
  font-size: 16px;
}

.transformation .arrow {
  color: #2a9d8f;
  font-size: 22px;
  font-weight: 700;
}

/* =========================
   TRANSITION VISUAL
========================= */

.transition-visual {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 17px 10px;

  background: #f8fafb;
  border: 1px solid #dce4e9;
  border-radius: 8px;
}

.state {
  flex: 1;
  min-width: 0;
  text-align: center;
}

.state-label {
  display: block;
  margin-bottom: 10px;

  color: #20639b;
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 13px;
  font-weight: 700;
}

.gene-row {
  display: flex;
  justify-content: center;
  gap: 4px;
}

.gene-row span {
  min-width: 25px;
  padding: 5px 2px;

  background: #ffffff;
  border: 1px solid #dce4e9;
  border-radius: 4px;

  color: #24313a;
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 10px;
}

.transition-arrow {
  flex: 0 0 auto;

  display: flex;
  flex-direction: column;
  align-items: center;

  color: #2a9d8f;
  font-size: 20px;
  font-weight: 700;
}

.transition-arrow span {
  margin-bottom: 2px;

  color: #64748b;
  font-family: Inter, 'Segoe UI', sans-serif;
  font-size: 9px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.04em;
}

.rationale {
  margin-top: 18px;
}

/* =========================
   KEY MESSAGE
========================= */

.key-message {
  margin-top: auto;
  padding: 11px 12px;

  display: flex;
  align-items: center;
  gap: 9px;

  background: rgba(42, 157, 143, 0.08);
  border-left: 3px solid #2a9d8f;
  border-radius: 5px;

  color: #24313a;
  font-size: 12px;
  line-height: 1.45;
}

.message-icon {
  color: #2a9d8f;
  font-size: 18px;
  font-weight: 700;
}

/* =========================
   PROGRESS
========================= */

.progress {
  height: 30px;
  flex: 0 0 30px;

  display: flex;
  align-items: center;
  justify-content: center;
  gap: 6px;
}

.dot {
  width: 7px;
  height: 7px;
  border-radius: 50%;
  background: #dce4e9;
  transition: all 0.25s ease;
}

.dot.active {
  background: #2a9d8f;
  transform: scale(1.15);
}

.hint {
  margin-left: 10px;
  color: #94a3b8;
  font-size: 10px;
}

.hint strong {
  color: #64748b;
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
  transform: translateY(12px);
}

/* =========================
   RESPONSIVE
========================= */

@media (max-width: 900px) {
  .blocks {
    grid-template-columns: 1fr;
    overflow-y: auto;
  }

  .info-block {
    min-height: 320px;
  }
}
</style>