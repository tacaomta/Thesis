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

const visibleCount = 2
const totalItems = 2

watch(currentPage, () => {
  visibleCount.value = isExporting ? totalItems : 0
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
  <div class="mi-slide">

    <div class="intro">
      Mutual information quantifies how much knowing one variable reduces
      uncertainty about another — the formulation differs for
      <strong>discrete</strong> and <strong>continuous</strong> data.
    </div>

    <div class="mi-grid">

      <!-- ================= DISCRETE ================= -->
      <Transition name="fade-up">
        <section v-if="visibleCount >= 1" class="mi-card discrete-card">

          <div class="mi-top">
            <div class="mi-index">01</div>
            <div>
              <div class="mi-label">DISCRETE VARIABLES</div>
              <h2>Shannon Mutual Information</h2>
            </div>
            <div class="mi-badge">SUM</div>
          </div>

          <div class="formula-box">
            <div class="formula-main">
              I(X;Y) = <span class="sum-op">Σ</span><span class="sum-op">Σ</span>
              p(x,y) log
              <span class="frac">
                <span class="frac-top">p(x,y)</span>
                <span class="frac-bottom">p(x)p(y)</span>
              </span>
            </div>
            <div class="formula-sub">x∈X&nbsp;&nbsp;y∈Y</div>
          </div>

          <div class="formula-box formula-alt">
            <div class="formula-main small">
              I(X;Y) = H(X) + H(Y) − H(X,Y)
            </div>
          </div>

          <div class="annotations">

            <div class="annotation-row">
              <span class="term">p(x,y)</span>
              <span class="desc">Joint <strong>probability mass</strong> that X = x and Y = y</span>
            </div>

            <div class="annotation-row">
              <span class="term">p(x), p(y)</span>
              <span class="desc"><strong>Marginal probabilities</strong> of X and Y individually</span>
            </div>

            <div class="annotation-row">
              <span class="term">H(X)</span>
              <span class="desc"><strong>Entropy</strong> of X: − Σ p(x) log p(x) — uncertainty in X alone</span>
            </div>

            <div class="annotation-row">
              <span class="term">H(Y)</span>
              <span class="desc"><strong>Entropy</strong> of Y — uncertainty in Y alone</span>
            </div>

            <div class="annotation-row">
              <span class="term">H(X,Y)</span>
              <span class="desc"><strong>Joint entropy</strong> of X and Y together</span>
            </div>

          </div>

          <div class="result-box discrete-result">
            <span class="result-icon">Σ</span>
            <div>
              <span class="result-label">COMPUTED VIA</span>
              <strong>Probability tables / discretized bins</strong>
            </div>
          </div>

        </section>
      </Transition>

      <!-- ================= CONTINUOUS ================= -->
      <Transition name="fade-up">
        <section v-if="visibleCount >= 2" class="mi-card continuous-card">

          <div class="mi-top">
            <div class="mi-index">02</div>
            <div>
              <div class="mi-label">CONTINUOUS VARIABLES</div>
              <h2>Differential Mutual Information</h2>
            </div>
            <div class="mi-badge continuous-badge">INTEGRAL</div>
          </div>

          <div class="formula-box">
            <div class="formula-main">
              I(X;Y) = <span class="sum-op">∫</span><span class="sum-op">∫</span>
              p(x,y) log
              <span class="frac">
                <span class="frac-top">p(x,y)</span>
                <span class="frac-bottom">p(x)p(y)</span>
              </span>
              dx dy
            </div>
          </div>

          <div class="formula-box formula-alt">
            <div class="formula-main small">
              I(X;Y) = h(X) + h(Y) − h(X,Y)
            </div>
          </div>

          <div class="annotations">

            <div class="annotation-row">
              <span class="term">p(x,y)</span>
              <span class="desc">Joint <strong>probability density</strong> of X and Y at (x,y)</span>
            </div>

            <div class="annotation-row">
              <span class="term">p(x), p(y)</span>
              <span class="desc"><strong>Marginal densities</strong> of X and Y individually</span>
            </div>

            <div class="annotation-row">
              <span class="term">h(X)</span>
              <span class="desc"><strong>Differential entropy</strong> of X: − ∫ p(x) log p(x) dx</span>
            </div>

            <div class="annotation-row">
              <span class="term">h(Y)</span>
              <span class="desc"><strong>Differential entropy</strong> of Y</span>
            </div>

            <div class="annotation-row">
              <span class="term">h(X,Y)</span>
              <span class="desc"><strong>Joint differential entropy</strong> of X and Y</span>
            </div>

          </div>

          <div class="result-box continuous-result">
            <span class="result-icon">∫</span>
            <div>
              <span class="result-label">COMPUTED VIA</span>
              <strong>KDE / k-NN density estimators</strong>
            </div>
          </div>

        </section>
      </Transition>

    </div>
  </div>
</template>

<style scoped>
.mi-slide {
  width: 100%;
  height: 100%;
  min-height: 0;

  display: flex;
  flex-direction: column;

  box-sizing: border-box;

  padding: 10px 20px 4px;

  font-family: 'Inter', 'Segoe UI', sans-serif;
  color: #24313a;
}

/* =========================================
   INTRO
========================================= */

.intro {
  flex: 0 0 auto;

  margin: 0 4px 12px;

  max-width: 1100px;

  color: #64748b;

  font-size: 12px;
  line-height: 1.45;
}

.intro strong {
  color: #173f5f;
}

/* =========================================
   GRID
========================================= */

.mi-grid {
  flex: 1 1 auto;
  min-height: 0;
  min-width: 0;

  display: grid;
  grid-template-columns: minmax(0, 1fr) minmax(0, 1fr);

  gap: 16px;
}

/* =========================================
   CARD
========================================= */

.mi-card {
  min-width: 0;
  min-height: 0;

  display: flex;
  flex-direction: column;

  padding: 15px 17px;

  border: 1px solid #dce4e9;
  border-radius: 12px;

  background: #ffffff;

  box-sizing: border-box;
}

.discrete-card {
  border-top: 3px solid #20639b;
}

.continuous-card {
  border-top: 3px solid #2a9d8f;
}

/* =========================================
   HEADER
========================================= */

.mi-top {
  position: relative;

  display: flex;
  align-items: flex-start;

  gap: 10px;

  margin-bottom: 10px;
}

.mi-index {
  display: flex;
  align-items: center;
  justify-content: center;

  flex: 0 0 auto;

  width: 28px;
  height: 28px;

  border-radius: 7px;

  background: #eef3f7;

  color: #20639b;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 10px;
  font-weight: 700;
}

.continuous-card .mi-index {
  background: #f3fbf9;
  color: #2a9d8f;
}

.mi-label {
  margin-bottom: 2px;

  color: #2a9d8f;

  font-size: 8px;
  font-weight: 700;
  letter-spacing: 0.1em;
}

.mi-top h2 {
  margin: 0;

  color: #173f5f;

  font-size: 16px;
  font-weight: 700;
  line-height: 1.15;
}

.mi-badge {
  margin-left: auto;

  padding: 4px 8px;

  border: 1px solid #dce4e9;
  border-radius: 4px;

  background: #f8fafb;

  color: #20639b;

  font-size: 8px;
  font-weight: 700;
  letter-spacing: 0.08em;
}

.continuous-badge {
  border-color: #c9e6e1;
  background: #f3fbf9;
  color: #2a9d8f;
}

/* =========================================
   FORMULA
========================================= */

.formula-box {
  flex: 0 0 auto;

  display: flex;
  flex-direction: column;
  align-items: center;

  margin-bottom: 8px;
  padding: 10px 10px;

  border: 1px solid #dce4e9;
  border-radius: 9px;

  background: #f8fafb;
}

.formula-alt {
  padding: 7px 10px;
  background: #ffffff;
}

.formula-main {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  justify-content: center;

  gap: 6px;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 13.5px;
  font-weight: 600;
  color: #173f5f;
}

.formula-main.small {
  font-size: 12.5px;
  color: #24313a;
}

.sum-op {
  font-size: 17px;
  font-weight: 400;
  color: #20639b;
}

.frac {
  display: inline-flex;
  flex-direction: column;
  align-items: center;

  line-height: 1.15;

  vertical-align: middle;
}

.frac-top {
  padding: 0 2px 1px;
  border-bottom: 1.3px solid #173f5f;
}

.frac-bottom {
  padding: 1px 2px 0;
}

.formula-sub {
  margin-top: 4px;

  color: #94a3b8;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 8.5px;
}

/* =========================================
   ANNOTATIONS
========================================= */

.annotations {
  flex: 1 1 auto;
  min-height: 0;

  display: flex;
  flex-direction: column;

  gap: 6px;

  margin-bottom: 8px;
}

.annotation-row {
  display: grid;
  grid-template-columns: 82px minmax(0, 1fr);

  column-gap: 9px;

  align-items: baseline;

  padding: 6px 9px;

  border: 1px solid #edf1f3;
  border-radius: 7px;

  background: #ffffff;
}

.term {
  flex-shrink: 0;

  color: #20639b;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 11px;
  font-weight: 700;
}

.continuous-card .term {
  color: #2a9d8f;
}

.desc {
  min-width: 0;

  color: #64748b;

  font-size: 10.5px;
  line-height: 1.4;
}

.desc strong {
  color: #173f5f;
}

/* =========================================
   RESULT BOX
========================================= */

.result-box {
  flex: 0 0 auto;

  display: flex;
  align-items: center;

  gap: 9px;

  padding: 7px 10px;

  border-radius: 7px;
}

.discrete-result {
  background: #eef3f7;
}

.continuous-result {
  background: #f3fbf9;
}

.result-icon {
  display: flex;
  align-items: center;
  justify-content: center;

  width: 24px;
  height: 24px;

  flex-shrink: 0;

  border-radius: 50%;

  background: #ffffff;

  color: #20639b;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 12px;
  font-weight: 700;
}

.continuous-result .result-icon {
  color: #2a9d8f;
}

.result-label {
  display: block;

  margin-bottom: 1px;

  color: #94a3b8;

  font-size: 8px;
  font-weight: 700;
  letter-spacing: 0.08em;
}

.result-box strong {
  color: #173f5f;

  font-size: 10.5px;
}

/* =========================================
   SPACE HINT
========================================= */

.space-hint {
  flex-shrink: 0;

  display: flex;
  align-items: center;
  justify-content: center;

  height: 22px;

  margin-top: 6px;

  color: #94a3b8;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 10px;
  letter-spacing: 0.03em;
}

/* =========================================
   BOTTOM MESSAGE
========================================= */

.bottom-message {
  flex-shrink: 0;

  display: flex;
  align-items: center;

  gap: 12px;

  margin: 10px 4px 2px;
  padding: 8px 14px;

  border: 1px solid #dce4e9;
  border-radius: 8px;

  background: #ffffff;
}

.bottom-label {
  flex: 0 0 auto;

  color: #2a9d8f;

  font-size: 8.5px;
  font-weight: 700;
  letter-spacing: 0.1em;
}

.bottom-text {
  color: #64748b;

  font-size: 10.5px;
  line-height: 1.35;
}

.bottom-text strong {
  color: #173f5f;
}

/* =========================================
   ANIMATION
========================================= */

.fade-up-enter-active {
  transition:
    opacity 0.35s ease,
    transform 0.35s ease;
}

.fade-up-enter-from {
  opacity: 0;
  transform: translateY(12px);
}

/* =========================================
   RESPONSIVE
========================================= */

@media (max-width: 900px) {
  .mi-grid {
    grid-template-columns: 1fr;
    overflow-y: auto;
  }

  .annotation-row {
    grid-template-columns: 70px minmax(0, 1fr);
  }
}

@media (prefers-reduced-motion: reduce) {
  .fade-up-enter-active {
    transition: none;
  }
}
</style>