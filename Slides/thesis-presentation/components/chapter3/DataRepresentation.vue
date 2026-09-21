<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

const visibleCount = ref(0)

function handleKeydown(event) {
  if (event.code !== 'Space') return

  event.preventDefault()
  event.stopPropagation()

  if (visibleCount.value < 3) {
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
            <h2>Task Transformation</h2>

            <p>
              Reformulates network reconstruction into a
              <strong>pairwise binary classification task</strong>.
            </p>

            <div class="flow">
              <span>Network reconstruction</span>
              <span class="arrow">→</span>
              <span class="highlight">Binary classification</span>
            </div>
          </div>
        </section>
      </Transition>

      <!-- Step 2 -->
      <Transition name="fade-up">
        <section v-if="visibleCount >= 2" class="step-card">
          <div class="step-number">02</div>

          <div class="step-body">
            <h2>Interaction Vector Representation</h2>

            <p>
              Concatenates the expression time series of regulator
              <span class="gene">V<sub>j</sub></span>
              and target
              <span class="gene">V<sub>i</sub></span>.
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
              <strong>2T-dimensional representation</strong>
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
              Each regulator–target pair is assigned a binary label
              according to whether a directed regulatory interaction exists.
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

    </div>

    <div v-if="visibleCount < 3" class="space-hint">
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
  grid-template-columns: repeat(3, 1fr);
  gap: 18px;

  align-items: stretch;
  margin-top: 60px;
}

.step-card {
  position: relative;

  display: flex;
  flex-direction: column;

  min-width: 0;

  padding: 22px 20px;

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
  width: 34px;
  height: 34px;

  display: flex;
  align-items: center;
  justify-content: center;

  margin-bottom: 17px;

  border-radius: 50%;

  background: #f0f5f8;
  color: #173f5f;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 11px;
  font-weight: 600;
}

/* =========================
   Text
   ========================= */

.step-body {
  min-width: 0;
}

.step-body h2 {
  margin: 0 0 13px;

  color: #173f5f;

  font-size: 18px;
  line-height: 1.3;
  font-weight: 650;
}

.step-body p {
  margin: 0;

  color: #64748b;

  font-size: 14px;
  line-height: 1.6;
}

.step-body strong {
  color: #173f5f;
  font-weight: 650;
}

.gene {
  color: #20639b;
  font-weight: 600;
}

/* =========================
   Step 1
   ========================= */

.flow {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;
  gap: 9px;

  margin-top: 24px;
  padding: 14px 10px;

  background: #f8fafb;
  border: 1px solid #e5eaee;
  border-radius: 6px;

  color: #64748b;

  font-size: 12px;
  text-align: center;
}

.arrow {
  color: #94a3b8;
  font-size: 16px;
}

.highlight {
  color: #20639b;
  font-weight: 650;
}

/* =========================
   Step 2
   ========================= */

.formula-box {
  margin-top: 20px;
  padding: 17px 10px;

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
  font-size: 25px;
  white-space: nowrap;
}

.dimension-note {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;
  gap: 7px;

  margin-top: 13px;

  color: #64748b;

  font-size: 11px;
  text-align: center;
}

.connector {
  color: #94a3b8;
}

.dimension-note strong {
  color: #2a9d8f;
}

/* =========================
   Step 3
   ========================= */

.label-box {
  margin-top: 20px;

  display: flex;
  flex-direction: column;

  border: 1px solid #dce4e9;
  border-radius: 6px;

  overflow: hidden;
}

.label-item {
  display: flex;
  align-items: center;
  gap: 12px;

  padding: 14px 15px;
}

.label-item.positive {
  background: #f4faf8;
}

.label-item.negative {
  background: #f8fafb;
}

.label-value {
  flex-shrink: 0;

  min-width: 78px;

  color: #173f5f;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 12px;
  font-weight: 600;
}

.label-description {
  color: #64748b;

  font-size: 12px;
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

@media (max-width: 850px) {
  .steps {
    grid-template-columns: 1fr;
    overflow-y: auto;
  }
}
</style>