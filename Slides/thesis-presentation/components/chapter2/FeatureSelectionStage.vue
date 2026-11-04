<template>
  <div class="feature-selection-slide">

    <div class="methods-grid">

      <!-- ================= MIFS ================= -->
      <section class="method-card mifs-card">

        <div class="method-top">
          <div class="method-index">01</div>

          <div>
            <div class="method-label">FEATURE SELECTION</div>
            <h2>MIFS</h2>
          </div>

          <div class="method-badge">
            SELECT
          </div>
        </div>

        <!-- target + candidate pool -->
        <!-- <div class="selection-visual">

          <div class="target-column">
            <div class="visual-label">TARGET</div>
            <div class="target-gene">g₀</div>
          </div>

          <div class="selection-arrow">
            <svg viewBox="0 0 45 24" aria-hidden="true">
              <line x1="3" y1="12" x2="34" y2="12" />
              <path d="M29 6 L36 12 L29 18" />
            </svg>
          </div>

          <div class="candidate-pool">
            <div class="visual-label">CANDIDATE GENES</div>
            <div class="gene-pool">
              <span>g₁</span>
              <span>g₂</span>
              <span>g₃</span>
              <span>g₄</span>
              <span>g₅</span>
              <span>…</span>
            </div>
          </div>

        </div> -->

        <!-- ================= PSEUDO-CODE STEPS ================= -->
        <div class="pseudocode" aria-label="MIFS pseudo-code, press 1, 2 or 3 to highlight a step">

          <div class="pseudocode-header">
            <span class="pseudocode-title">MIFS(g₀, k)</span>
            <span class="pseudocode-hint">press <strong>1</strong> · <strong>2</strong> · <strong>3</strong></span>
          </div>

          <div
            v-for="n in 3"
            :key="`mifs-wrap-${n}`"
            class="code-step"
            :class="{ 'is-active': activeStep === n }"
          >
            <div
              :key="`mifs-pulse-${n}-${pulseTick[n]}`"
              class="code-step-pulse"
            >

              <template v-if="n === 1">
                <div class="code-line">
                  <span class="line-no">01</span>
                  <span class="kw">SELECT</span>
                  <span class="code-text">gene <em>g</em> that <span class="kw-inline">MAXIMIZES</span> MI(g, g₀)</span>
                </div>
              </template>

              <template v-else-if="n === 2">
                <div class="code-line indent">
                  <span class="line-no">02</span>
                  <span class="kw">SELECT</span>
                  <span class="code-text">next gene <em>g</em> that <span class="kw-inline">MAXIMIZES</span> MI(g, g₀)</span>
                </div>
                <div class="code-line indent">
                  <span class="line-no">03</span>
                  <span class="code-text spacer"><span class="kw-inline">MINIMIZING</span> redundancy with already-selected genes</span>
                </div>
              </template>

              <template v-else>
                <div class="code-line">
                  <span class="line-no">04</span>
                  <span class="kw">REPEAT</span>
                  <span class="code-text">step 2 <span class="kw-inline">UNTIL</span> k regulators selected</span>
                </div>
              </template>

              <div class="step-caption">
                <span class="step-caption-number">STEP {{ n }}</span>
                <span v-if="n === 1">Pick the single most informative gene</span>
                <span v-else-if="n === 2">Add genes that add new information, not duplicate it</span>
                <span v-else>Stop once k regulators are collected</span>
              </div>

            </div>
          </div>

        </div>

        <div class="result-box mifs-result">
          <span class="result-icon">→</span>
          <div>
            <span class="result-label">OUTPUT</span>
            <strong>Potential regulator set</strong>
          </div>
        </div>

      </section>


      <!-- ================= SWAP ================= -->
      <section class="method-card swap-card">

        <div class="method-top">
          <div class="method-index">02</div>

          <div>
            <div class="method-label">ITERATIVE REFINEMENT</div>
            <h2>SWAP</h2>
          </div>

          <div class="method-badge swap-badge">
            REFINE
          </div>
        </div>

        <div class="method-description">
          MIFS does not compute the <strong>exact multivariate mutual information</strong>
          and may fail to find the optimal regulator set.
        </div>

        <!-- swap visual -->
        <div class="swap-visual">

          <div class="variable-group">
            <div class="visual-label">SELECTED</div>
            <div class="selected-variables">
              <span class="selected-variable">g₁</span>
              <span class="selected-variable">g₃</span>
              <span class="selected-variable">g₇</span>
            </div>
          </div>

          <div class="swap-symbol">
            <svg viewBox="0 0 70 52" aria-hidden="true">
              <defs>
                <marker id="swap-arrow-up" markerWidth="8" markerHeight="8" refX="7" refY="4" orient="auto" markerUnits="userSpaceOnUse">
                  <path d="M0 0 L8 4 L0 8 Z" fill="#2A9D8F" />
                </marker>
                <marker id="swap-arrow-down" markerWidth="8" markerHeight="8" refX="7" refY="4" orient="auto" markerUnits="userSpaceOnUse">
                  <path d="M0 0 L8 4 L0 8 Z" fill="#E9C46A" />
                </marker>
              </defs>
              <path d="M18 18 C32 8 39 8 52 18" class="swap-arrow selected-to-unselected" marker-end="url(#swap-arrow-up)" />
              <path d="M52 34 C39 44 32 44 18 34" class="swap-arrow unselected-to-selected" marker-end="url(#swap-arrow-down)" />
              <text x="35" y="30" text-anchor="middle" class="swap-text">SWAP</text>
            </svg>
          </div>

          <div class="variable-group">
            <div class="visual-label">UNSELECTED</div>
            <div class="unselected-variables">
              <span class="unselected-variable">g₂</span>
              <span class="unselected-variable">g₄</span>
              <span class="unselected-variable">g₆</span>
              <span class="unselected-variable">…</span>
            </div>
          </div>

        </div>

        <!-- ================= PSEUDO-CODE ITERATION ================= -->
        <!-- <div class="pseudocode" aria-label="SWAP pseudo-code, press 1, 2 or 3 to highlight a step">

          <div class="pseudocode-header">
            <span class="pseudocode-title">SWAP(selected, unselected)</span>
            <span class="pseudocode-hint">press <strong>1</strong> · <strong>2</strong> · <strong>3</strong></span>
          </div>

          <div
            v-for="n in 3"
            :key="`swap-wrap-${n}`"
            class="code-step"
            :class="{ 'is-active': activeStep === n }"
          >
            <div
              :key="`swap-pulse-${n}-${pulseTick[n]}`"
              class="code-step-pulse"
            >

              <template v-if="n === 1">
                <div class="code-line">
                  <span class="line-no">01</span>
                  <span class="kw">SWAP</span>
                  <span class="code-text">equal number of selected / unselected genes</span>
                </div>
              </template>

              <template v-else-if="n === 2">
                <div class="code-line">
                  <span class="line-no">02</span>
                  <span class="kw">EVALUATE</span>
                  <span class="code-text">gene-wise dynamics consistency after swap</span>
                </div>
              </template>

              <template v-else>
                <div class="code-line">
                  <span class="line-no">03</span>
                  <span class="kw">KEEP</span>
                  <span class="code-text">swap <span class="kw-inline">IF</span> consistency improves, <span class="kw-inline">ELSE</span> revert</span>
                </div>
              </template>

              <div class="step-caption">
                <span class="step-caption-number">STEP {{ n }}</span>
                <span v-if="n === 1">Try exchanging candidates between the two sets</span>
                <span v-else-if="n === 2">Measure how well dynamics are reproduced</span>
                <span v-else>Only accept changes that help</span>
              </div>

            </div>
          </div>

        </div> -->

        <!-- stopping conditions -->
        <div class="stopping-box">

          <div class="stopping-title">STOP WHEN</div>

          <div class="stopping-conditions">
            <div class="condition">
              <span class="condition-check">✓</span>
              <span>Gene-wise dynamics consistency <strong>reaches 1.0</strong></span>
            </div>

            <div class="condition">
              <span class="condition-check">✓</span>
              <span>Number of potential candidates <strong>equals k</strong></span>
            </div>
          </div>

        </div>

        <div class="result-box swap-result">
          <span class="result-icon">→</span>
          <div>
            <span class="result-label">OUTPUT</span>
            <strong>Refined regulator set</strong>
          </div>
        </div>

      </section>

    </div>


    <div class="bottom-message">
      <span class="bottom-label">FEATURE SELECTION STRATEGY</span>
      <span class="bottom-text">
        <strong>MIFS</strong> identifies potential regulators
        → <strong>SWAP</strong> refines the selected set
        → improved <strong>dynamic consistency</strong>
      </span>
    </div>

  </div>
</template>


<script setup>
import { ref, reactive, onMounted, onBeforeUnmount } from 'vue'

/* currently highlighted step (1, 2 or 3); 0 = none */
const activeStep = ref(0)

/* bumped every time a digit is pressed, even if it's the same
   digit again — forces Vue to recreate the .code-step-pulse
   element (via :key) so the CSS pulse animation always restarts */
const pulseTick = reactive({ 1: 0, 2: 0, 3: 0 })

function handleKeydown(event) {
  const map = { Digit1: 1, Digit2: 2, Digit3: 3, Numpad1: 1, Numpad2: 2, Numpad3: 3 }
  const step = map[event.code]

  if (!step) return

  event.preventDefault()
  event.stopPropagation()

  activeStep.value = step
  pulseTick[step] += 1
}

onMounted(() => {
  window.addEventListener('keydown', handleKeydown, true)
})

onBeforeUnmount(() => {
  window.removeEventListener('keydown', handleKeydown, true)
})
</script>


<style scoped>
.feature-selection-slide {
  width: 100%;
  height: 100%;
  min-height: 0;

  display: flex;
  flex-direction: column;

  box-sizing: border-box;
}


/* =========================================
   INTRO
========================================= */

.intro {
  flex: 0 0 auto;

  margin: 0 8px 11px;

  max-width: 1100px;

  color: #64748b;

  font-size: 10.5px;
  line-height: 1.4;
}

.intro strong {
  color: #173f5f;
}


/* =========================================
   MAIN GRID
========================================= */

.methods-grid {
  flex: 1 1 auto;

  min-height: 0;
  min-width: 0;

  display: grid;

  grid-template-columns:
    minmax(0, 1fr)
    minmax(0, 1fr);

  gap: 14px;
}


/* =========================================
   METHOD CARD
========================================= */

.method-card {
  min-width: 0;
  min-height: 0;

  display: flex;
  flex-direction: column;

  padding: 13px 14px;

  border: 1px solid #dce4e9;
  border-radius: 12px;

  background: #ffffff;

  box-sizing: border-box;
}

.mifs-card {
  border-top: 3px solid #20639b;
}

.swap-card {
  border-top: 3px solid #2a9d8f;
}


/* =========================================
   HEADER
========================================= */

.method-top {
  position: relative;

  display: flex;
  align-items: flex-start;

  gap: 10px;

  margin-bottom: 8px;
}

.method-index {
  display: flex;
  align-items: center;
  justify-content: center;

  flex: 0 0 auto;

  width: 27px;
  height: 27px;

  border-radius: 7px;

  background: #eef3f7;

  color: #20639b;

  font-family: 'IBM Plex Mono', monospace;

  font-size: 9px;
  font-weight: 700;
}

.swap-card .method-index {
  background: #f3fbf9;
  color: #2a9d8f;
}

.method-label {
  margin-bottom: 2px;

  color: #2a9d8f;

  font-size: 6.5px;
  font-weight: 700;

  letter-spacing: 0.11em;
}

.method-top h2 {
  margin: 0;

  color: #173f5f;

  font-size: 19px;
  font-weight: 700;

  line-height: 1.1;
}

.method-badge {
  margin-left: auto;

  padding: 4px 7px;

  border: 1px solid #dce4e9;
  border-radius: 4px;

  background: #f8fafb;

  color: #20639b;

  font-size: 6px;
  font-weight: 700;

  letter-spacing: 0.08em;
}

.swap-badge {
  border-color: #c9e6e1;

  background: #f3fbf9;

  color: #2a9d8f;
}


/* =========================================
   DESCRIPTION
========================================= */

.method-description {
  flex: 0 0 auto;

  padding: 7px 9px;

  border-radius: 7px;

  background: #f8fafb;

  color: #64748b;

  font-size: 8.5px;
  line-height: 1.4;
}

.method-description strong {
  color: #173f5f;
}


/* =========================================
   MIFS SELECTION VISUAL
========================================= */

.selection-visual {
  flex: 0 0 auto;

  display: grid;

  grid-template-columns:
    70px
    45px
    minmax(0, 1fr);

  align-items: center;

  gap: 5px;

  min-height: 60px;

  margin: 8px 0;

  padding: 7px 9px;

  border: 1px solid #dce4e9;
  border-radius: 8px;

  background: #ffffff;
}

.target-column {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.visual-label {
  margin-bottom: 5px;

  color: #94a3b8;

  font-size: 5.8px;
  font-weight: 700;

  letter-spacing: 0.1em;
}

.target-gene {
  display: flex;
  align-items: center;
  justify-content: center;

  width: 32px;
  height: 32px;

  border-radius: 50%;

  border: 2px solid #2a9d8f;

  background: #f3fbf9;

  color: #173f5f;

  font-family: 'IBM Plex Mono', monospace;

  font-size: 11px;
  font-weight: 700;
}

.selection-arrow {
  display: flex;
  align-items: center;
  justify-content: center;
}

.selection-arrow svg {
  width: 38px;
  height: 20px;

  overflow: visible;
}

.selection-arrow line,
.selection-arrow path {
  fill: none;

  stroke: #94a3b8;

  stroke-width: 1.7;

  stroke-linecap: round;
  stroke-linejoin: round;
}

.candidate-pool {
  min-width: 0;
}

.gene-pool {
  display: flex;
  flex-wrap: wrap;

  gap: 5px;
}

.gene-pool span {
  display: flex;
  align-items: center;
  justify-content: center;

  min-width: 23px;
  height: 21px;

  padding: 0 5px;

  border: 1px solid #dce4e9;
  border-radius: 5px;

  background: #f8fafb;

  color: #20639b;

  font-family: 'IBM Plex Mono', monospace;

  font-size: 7px;
  font-weight: 600;
}


/* =========================================
   PSEUDO-CODE BLOCK
========================================= */

.pseudocode {
  flex: 1 1 auto;

  min-height: 0;

  display: flex;
  flex-direction: column;

  gap: 5px;

  margin-top: 8px;

  padding: 8px 9px 9px;

  border-radius: 8px;

  background: #0f1e2b;
}

.pseudocode-header {
  display: flex;
  align-items: center;
  justify-content: space-between;

  margin-bottom: 2px;
}

.pseudocode-title {
  color: #8fd8c9;

  font-family: 'IBM Plex Mono', monospace;

  font-size: 8.5px;
  font-weight: 700;
}

.pseudocode-hint {
  color: #5b7184;

  font-family: 'IBM Plex Mono', monospace;

  font-size: 6.5px;
}

.pseudocode-hint strong {
  color: #b9cadb;

  padding: 1px 3px;

  border: 1px solid #2c3f4f;
  border-radius: 3px;
}

/* ---- step wrapper (border highlight) ---- */

.code-step {
  border-radius: 6px;

  border: 1.5px solid transparent;

  transition: border-color 0.25s ease, background 0.25s ease;
}

.code-step.is-active {
  border-color: #2a9d8f;

  background: rgba(42, 157, 143, 0.08);
}

.code-step-pulse {
  padding: 4px 6px 6px;
}

.code-step.is-active .code-step-pulse {
  animation: stepPulse 0.65s ease-out;
}

@keyframes stepPulse {
  0% {
    box-shadow: 0 0 0 0 rgba(42, 157, 143, 0.55);
  }
  70% {
    box-shadow: 0 0 0 9px rgba(42, 157, 143, 0);
  }
  100% {
    box-shadow: 0 0 0 0 rgba(42, 157, 143, 0);
  }
}

/* ---- code line ---- */

.code-line {
  display: flex;
  align-items: baseline;
  flex-wrap: wrap;

  gap: 6px;

  font-family: 'IBM Plex Mono', monospace;

  font-size: 8px;
  line-height: 1.55;
}

.code-line.indent {
  padding-left: 14px;
}

.line-no {
  flex: 0 0 auto;

  color: #3c5468;

  font-size: 7px;
}

.kw {
  flex: 0 0 auto;

  color: #e9c46a;

  font-weight: 700;
}

.kw-inline {
  color: #7fd4c1;

  font-weight: 700;
}

.code-text {
  min-width: 0;

  color: #c8d6e0;
}

.code-text em {
  color: #8fd8c9;
  font-style: normal;
}

.code-text.spacer {
  padding-left: 0;
}

/* ---- step caption ---- */

.step-caption {
  display: flex;
  align-items: baseline;

  gap: 6px;

  margin-top: 3px;
  padding-top: 3px;

  border-top: 1px dashed #243648;

  color: #7f93a4;

  font-size: 6.6px;
  line-height: 1.35;
}

.step-caption-number {
  flex: 0 0 auto;

  color: #4f94d4;

  font-family: 'IBM Plex Mono', monospace;

  font-size: 6px;
  font-weight: 700;

  letter-spacing: 0.06em;
}


/* =========================================
   SWAP VISUAL
========================================= */

.swap-visual {
  flex: 0 0 auto;

  display: grid;

  grid-template-columns:
    minmax(0, 1fr)
    70px
    minmax(0, 1fr);

  align-items: center;

  min-height: 72px;

  margin: 8px 0;

  padding: 8px;

  border: 1px solid #dce4e9;
  border-radius: 8px;

  background: #ffffff;
}

.variable-group {
  min-width: 0;

  text-align: center;
}

.selected-variables,
.unselected-variables {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;

  gap: 5px;
}

.selected-variable,
.unselected-variable {
  display: flex;
  align-items: center;
  justify-content: center;

  min-width: 27px;
  height: 25px;

  padding: 0 5px;

  border-radius: 5px;

  font-family: 'IBM Plex Mono', monospace;

  font-size: 7px;
  font-weight: 700;
}

.selected-variable {
  border: 1px solid #2a9d8f;

  background: #f3fbf9;

  color: #287c73;
}

.unselected-variable {
  border: 1px solid #e9c46a;

  background: #fff9e8;

  color: #8a6a12;
}

.swap-symbol {
  display: flex;
  align-items: center;
  justify-content: center;
}

.swap-symbol svg {
  display: block;

  width: 62px;
  height: 48px;

  overflow: visible;
}

.swap-arrow {
  fill: none;

  stroke-width: 1.8;

  stroke-linecap: round;
}

.selected-to-unselected {
  stroke: #2a9d8f;
}

.unselected-to-selected {
  stroke: #e9c46a;
}

.swap-text {
  fill: #173f5f;

  font-family: 'IBM Plex Mono', monospace;

  font-size: 7px;
  font-weight: 700;
}


/* =========================================
   STOPPING CONDITIONS
========================================= */

.stopping-box {
  flex: 0 0 auto;

  margin-top: 7px;

  padding: 7px 9px;

  border: 1px solid #c9e6e1;
  border-radius: 7px;

  background: #f3fbf9;
}

.stopping-title {
  margin-bottom: 5px;

  color: #2a9d8f;

  font-size: 9px;
  font-weight: 700;

  letter-spacing: 0.1em;
}

.stopping-conditions {
  display: grid;

  grid-template-columns: 1fr 1fr;

  gap: 6px;
}

.condition {
  display: flex;
  align-items: center;

  gap: 5px;

  color: #64748b;

  font-size: 6.5px;

  line-height: 1.3;
}

.condition-check {
  display: flex;
  align-items: center;
  justify-content: center;

  flex: 0 0 auto;

  width: 16px;
  height: 16px;

  border-radius: 50%;

  background: #2a9d8f;

  color: #ffffff;

  font-size: 7px;
  font-weight: 700;
}

.condition strong {
  color: #173f5f;
}


/* =========================================
   RESULT BOX
========================================= */

.result-box {
  flex: 0 0 auto;

  display: flex;
  align-items: center;

  gap: 7px;

  margin-top: 7px;

  padding: 6px 8px;

  border-radius: 6px;
}

.mifs-result {
  background: #eef3f7;
}

.swap-result {
  background: #f3fbf9;
}

.result-icon {
  display: flex;
  align-items: center;
  justify-content: center;

  width: 20px;
  height: 20px;

  border-radius: 50%;

  background: #ffffff;

  color: #20639b;

  font-size: 10px;
  font-weight: 700;
}

.swap-result .result-icon {
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

  font-size: 7.5px;
}


/* =========================================
   BOTTOM MESSAGE
========================================= */

.bottom-message {
  flex: 0 0 auto;

  display: flex;
  align-items: center;

  min-height: 36px;

  margin: 10px 8px 0;

  padding: 6px 12px;

  border: 1px solid #dce4e9;
  border-radius: 8px;

  background: #ffffff;
}

.bottom-label {
  flex: 0 0 auto;

  margin-right: 12px;

  color: #2a9d8f;

  font-size: 6.5px;
  font-weight: 700;

  letter-spacing: 0.1em;
}

.bottom-text {
  color: #64748b;

  font-size: 7.8px;

  line-height: 1.3;
}

.bottom-text strong {
  color: #173f5f;
}
</style>