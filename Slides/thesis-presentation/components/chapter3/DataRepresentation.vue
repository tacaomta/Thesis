<script setup>
import { ref, watch, onMounted, onBeforeUnmount } from 'vue'
import { useNav } from '@slidev/client'

const { currentPage } = useNav()

watch(currentPage, () => {
  visibleCount.value = 0
})

const visibleCount = ref(0)

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
  <div class="representation-slide">

    <div class="steps">

      <!-- Step 1 -->
      <Transition name="fade-up">
        <section v-if="visibleCount >= 1" class="step-card">
          <div class="step-number">01</div>

          <div class="step-body">
            <h2>Expression Profile</h2>

            <p>
              Each gene <span class="gene">G<sub>i</sub></span>
              is represented by its
              <strong>time-series expression vector</strong>
              over <em>T</em> observed time points.
            </p>

            <div class="formula-box">
              <span class="formula">
                V<sub>i</sub>
                =
                { v<sub>i</sub><sup>(1)</sup>, v<sub>i</sub><sup>(2)</sup>, ..., v<sub>i</sub><sup>(T)</sup> }
              </span>
            </div>

            <div class="dimension-note">
              <span>v<sub>i</sub><sup>(t)</sup></span>
              <span class="connector">=</span>
              <strong>expression value of G<sub>i</sub> at time t</strong>
            </div>
          </div>
        </section>
      </Transition>

      <!-- Step 2 -->
      <Transition name="fade-up">
        <section v-if="visibleCount >= 2" class="step-card">
          <div class="step-number">02</div>

          <div class="step-body">
            <h2>Pairwise Feature Vector</h2>

            <p>
              Concatenates the expression profiles of regulator
              <span class="gene">G<sub>j</sub></span>
              and target
              <span class="gene">G<sub>i</sub></span>
              into one feature vector.
            </p>

            <div class="formula-box">
              <span class="formula">
                <b>x</b><sup>(j,i)</sup>
                =
                V<sub>j</sub>
                ⊕
                V<sub>i</sub>
                ∈
                ℝ<sup>2T</sup>
              </span>
            </div>

            <div class="dimension-note">
              <span>Regulator</span>
              <span class="connector">⊕</span>
              <span>Target</span>
              <span class="connector">→</span>
              <strong>2T-dimensional feature</strong>
            </div>
          </div>
        </section>
      </Transition>

      <!-- Step 3 -->
      <Transition name="fade-up">
        <section v-if="visibleCount >= 3" class="step-card">
          <div class="step-number">03</div>

          <div class="step-body">
            <h2>Binary Class Labeling</h2>

            <p>
              Each ordered gene pair is labeled according to whether
              a directed regulatory interaction exists in the gold
              standard network.
            </p>

            <div class="label-box">
              <div class="label-item positive">
                <span class="label-value">y<sup>(j,i)</sup> = 1</span>
                <span class="label-description">
                  G<sub>j</sub> → G<sub>i</sub> exists
                </span>
              </div>

              <div class="label-divider"></div>

              <div class="label-item negative">
                <span class="label-value">y<sup>(j,i)</sup> = 0</span>
                <span class="label-description">
                  No directed interaction
                </span>
              </div>
            </div>
          </div>
        </section>
      </Transition>

      <!-- Step 4 -->
      <Transition name="fade-up">
        <section v-if="visibleCount >= 4" class="step-card">
          <div class="step-number">04</div>

          <div class="step-body">
            <h2>Labeled Dataset</h2>

            <p>
              Applying this transformation across all ordered gene
              pairs yields a fully supervised dataset for GRN inference.
            </p>

            <div class="formula-box">
              <span class="formula dataset-formula">
                D
                =
                { ( <b>x</b><sup>(j,i)</sup>, y<sup>(j,i)</sup> ) }
              </span>
            </div>

            <div class="dimension-note">
              <span>Each sample</span>
              <span class="connector">→</span>
              <strong>one candidate regulatory interaction</strong>
            </div>
          </div>
        </section>
      </Transition>

    </div>

    <div v-if="visibleCount < 4" class="space-hint">
      Press SPACE to reveal the next step
    </div>

  </div>
</template>

<style scoped>
.representation-slide {
  width: 100%;
  height: 100%;
  box-sizing: border-box;

  display: flex;
  flex-direction: column;

  padding: 6px 24px 4px;
}

/* =========================
   Steps
   ========================= */

.steps {
  flex: 1;
  min-height: 0;

  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 16px;

  align-items: stretch;
  margin-top: 50px;
}

.step-card {
  position: relative;

  display: flex;
  flex-direction: column;

  min-width: 0;

  padding: 20px 16px;

  background: #ffffff;
  border: 1px solid #dce4e9;
  border-radius: 8px;

  box-sizing: border-box;
}

.step-card::before {
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
   Step number
   ========================= */

.step-number {
  width: 32px;
  height: 32px;

  display: flex;
  align-items: center;
  justify-content: center;

  margin-bottom: 15px;

  border-radius: 50%;

  background: #f0f5f8;
  color: #173f5f;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 10.5px;
  font-weight: 600;
}

/* =========================
   Text
   ========================= */

.step-body {
  min-width: 0;
}

.step-body h2 {
  margin: 0 0 11px;

  color: #173f5f;

  font-size: 16px;
  line-height: 1.3;
  font-weight: 650;
}

.step-body p {
  margin: 0;

  color: #64748b;

  font-size: 12.5px;
  line-height: 1.55;
}

.step-body strong {
  color: #173f5f;
  font-weight: 650;
}

.step-body em {
  color: #173f5f;
  font-style: normal;
  font-weight: 600;
}

.gene {
  color: #20639b;
  font-weight: 600;
}

/* =========================
   Formula box (steps 1, 2, 4)
   ========================= */

.formula-box {
  margin-top: 18px;
  padding: 15px 8px;

  display: flex;
  align-items: center;
  justify-content: center;

  background: #f8fafb;
  border: 1px solid #dce4e9;
  border-radius: 6px;

  overflow: hidden;
}

.formula {
  color: #173f5f;

  font-family: 'Times New Roman', serif;
  font-size: 19px;
  white-space: nowrap;
}

.dataset-formula {
  font-size: 20px;
}

.dimension-note {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;
  gap: 6px;

  margin-top: 12px;

  color: #64748b;

  font-size: 10.5px;
  text-align: center;
}

.connector {
  color: #94a3b8;
}

.dimension-note strong {
  color: #2a9d8f;
}

/* =========================
   Step 3 — label box
   ========================= */

.label-box {
  margin-top: 18px;

  display: flex;
  flex-direction: column;

  border: 1px solid #dce4e9;
  border-radius: 6px;

  overflow: hidden;
}

.label-item {
  display: flex;
  align-items: center;
  gap: 10px;

  padding: 12px 13px;
}

.label-item.positive {
  background: #f4faf8;
}

.label-item.negative {
  background: #f8fafb;
}

.label-value {
  flex-shrink: 0;

  min-width: 68px;

  color: #173f5f;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 11px;
  font-weight: 600;
}

.label-description {
  color: #64748b;

  font-size: 11px;
  line-height: 1.4;
}

.label-divider {
  height: 1px;
  background: #dce4e9;
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
   Animation
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

@media (max-width: 1100px) {
  .steps {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 600px) {
  .steps {
    grid-template-columns: 1fr;
    overflow-y: auto;
  }
}
</style>