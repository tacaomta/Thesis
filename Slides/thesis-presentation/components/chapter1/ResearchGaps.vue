<template>
  <div class="research-gaps-slide">

    <div class="gaps-list">

      <!-- GAP 1 -->
      <article
        class="gap-card"
        :class="{ 'gap-hidden': visibleCount < 1 }"
      >
        <div class="gap-index">
          01
        </div>

        <div class="gap-visual">
          <div class="state-comparison">
            <div class="state-group">
              <span class="state-label">Conventional</span>

              <div class="states boolean">
                <span>0</span>
                <span>1</span>
              </div>
            </div>

            <div class="state-arrow">→</div>

            <div class="state-group proposed">
              <span class="state-label">This thesis</span>

              <div class="states hybrid">
                <span>0</span>
                <span>1</span>
                <span>2</span>
              </div>
            </div>
          </div>
        </div>

        <div class="gap-content">
          <div class="gap-meta">
            <span class="gap-tag">GAP 01</span>
            <span class="publication">Publication 1</span>
          </div>

          <h2>Limited regulatory-state representation</h2>

          <p>
            Many existing inference models represent gene regulation using
            binary states, which may oversimplify the expression dynamics
            observed in time-series data.
          </p>

          <div class="solution">
            <span class="solution-label">Addressed by</span>

            <span class="solution-text">
              A mixed Boolean–ternary discretization strategy that preserves
              more regulatory-state information.
            </span>
          </div>
        </div>
      </article>


      <!-- GAP 2 -->
      <article
        class="gap-card"
        :class="{ 'gap-hidden': visibleCount < 2 }"
      >
        <div class="gap-index">
          02
        </div>

        <div class="gap-visual">
          <div class="representation-flow">

            <div class="data-box">
              <span class="box-icon">D</span>
              <span>Expression<br>data</span>
            </div>

            <div class="flow-line"></div>

            <div class="feature-box">
              <span class="box-icon">R</span>
              <span>Learnable<br>representation</span>
            </div>

            <div class="flow-line"></div>

            <div class="model-box">
              <span class="box-icon">M</span>
              <span>ML model</span>
            </div>

          </div>
        </div>

        <div class="gap-content">
          <div class="gap-meta">
            <span class="gap-tag">GAP 02</span>
            <span class="publication">Publication 2</span>
          </div>

          <h2>Limited representation for machine learning</h2>

          <p>
            The availability of large expression datasets is not always
            matched by representations that allow machine-learning models
            to effectively exploit the available information.
          </p>

          <div class="solution">
            <span class="solution-label">Addressed by</span>

            <span class="solution-text">
              A representation learning framework that transforms expression
              profiles into features suitable for GRN inference.
            </span>
          </div>
        </div>
      </article>


      <!-- GAP 3 -->
      <article
        class="gap-card"
        :class="{ 'gap-hidden': visibleCount < 3 }"
      >
        <div class="gap-index">
          03
        </div>

        <div class="gap-visual">
          <div class="data-generation">

            <div class="real-data">
              <span class="data-dot"></span>
              <span class="data-dot"></span>
              <span class="data-dot"></span>
              <span class="data-dot"></span>
              <span class="data-dot"></span>
              <span class="data-dot"></span>
              <span class="data-label">Observed data</span>
            </div>

            <div class="generation-arrow">
              <span>+</span>
              <div class="arrow-line"></div>
            </div>

            <div class="synthetic-data">
              <span class="data-dot"></span>
              <span class="data-dot"></span>
              <span class="data-dot"></span>
              <span class="data-dot"></span>
              <span class="data-dot"></span>
              <span class="data-dot"></span>
              <span class="data-label">Synthetic data</span>
            </div>

          </div>
        </div>

        <div class="gap-content">
          <div class="gap-meta">
            <span class="gap-tag">GAP 03</span>
            <span class="publication">Publication 3</span>
          </div>

          <h2>Limited observations for GRN inference</h2>

          <p>
            Time-series gene expression datasets often contain only a limited
            number of observations, making it difficult to learn reliable
            regulatory relationships.
          </p>

          <div class="solution">
            <span class="solution-label">Addressed by</span>

            <span class="solution-text">
              A data-generation approach that synthesizes additional
              time-series expression data to improve inference performance.
            </span>
          </div>
        </div>
      </article>

    </div>

    <div
      class="bottom-message"
      :class="{ 'message-hidden': visibleCount < 3 }"
    >
      <span class="message-mark">→</span>

      <span>
        These three gaps motivate the three research directions of this thesis:
        <strong>better representation, better learning, and better data.</strong>
      </span>
    </div>

  </div>
</template>


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


<style scoped>
.research-gaps-slide {
  position: relative;
  width: 100%;
  height: 100%;
  min-height: 0;
  display: flex;
  flex-direction: column;
  overflow: hidden;
  box-sizing: border-box;
}


/* INTRO */

.intro {
  flex: 0 0 auto;
  margin: 0 4px 10px;
  color: #64748b;
  font-size: 13px;
  line-height: 1.45;
}


/* GAPS */

.gaps-list {
  flex: 0 0 auto;
  display: flex;
  flex-direction: column;
  gap: 8px;
  min-width: 0;
}


/* GAP CARD */

.gap-card {
  min-width: 0;
  min-height: 110px;

  display: grid;
  grid-template-columns: 32px 170px minmax(0, 1fr);
  gap: 10px;

  padding: 5px 12px;

  border: 1px solid #dce4e9;
  border-radius: 10px;

  background: #ffffff;
  box-sizing: border-box;

  opacity: 1;
  transform: translateY(0);

  transition:
    opacity 0.4s ease,
    transform 0.4s ease;
}


/* HIDDEN */

.gap-card.gap-hidden {
  opacity: 0;
  transform: translateY(12px);
  pointer-events: none;
}


/* INDEX */

.gap-index {
  padding-top: 2px;

  color: #94a3b8;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 10px;
  font-weight: 600;
  line-height: 1;
}


/* VISUAL */

.gap-visual {
  min-width: 0;

  display: flex;
  align-items: center;
  justify-content: center;

  border-right: 1px solid #eef2f4;
}


/* CONTENT */

.gap-content {
  min-width: 0;

  display: flex;
  flex-direction: column;
  justify-content: center;
}


/* META */

.gap-meta {
  display: flex;
  align-items: center;
  gap: 7px;
  margin-bottom: 3px;
}

.gap-tag {
  color: #2a9d8f;

  font-size: 8.5px;
  font-weight: 700;

  text-transform: uppercase;
  letter-spacing: 0.08em;
}

.publication {
  padding-left: 7px;

  border-left: 1px solid #dce4e9;

  color: #94a3b8;

  font-size: 8.5px;
  font-weight: 600;
}


/* TITLE */

.gap-content h2 {
  margin: 0 0 4px;

  color: #173f5f;

  font-size: 14px;
  font-weight: 700;

  line-height: 1.2;
}


/* DESCRIPTION */

.gap-content p {
  margin: 0 0 6px;

  color: #475569;

  font-size: 9.5px;
  line-height: 1.35;
}


/* SOLUTION */

.solution {
  display: flex;
  align-items: baseline;
  gap: 6px;

  min-width: 0;
}

.solution-label {
  flex: 0 0 auto;

  color: #e76f51;

  font-size: 8.5px;
  font-weight: 700;

  text-transform: uppercase;
  letter-spacing: 0.07em;
}

.solution-text {
  min-width: 0;

  color: #64748b;

  font-size: 9px;
  line-height: 1.3;
}


/* ------------------------------------------------ */
/* GAP 01 — DISCRETIZATION */
/* ------------------------------------------------ */

.state-comparison {
  display: flex;
  align-items: center;
  gap: 8px;
}

.state-group {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 4px;
}

.state-label {
  color: #94a3b8;

  font-size: 7.5px;
  font-weight: 600;

  text-transform: uppercase;
  letter-spacing: 0.04em;
}

.states {
  display: flex;
  align-items: center;
  gap: 3px;
}

.states span {
  width: 20px;
  height: 20px;

  display: flex;
  align-items: center;
  justify-content: center;

  border: 1px solid #cbd5e1;
  border-radius: 5px;

  color: #475569;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 9px;
  font-weight: 600;

  background: #f8fafb;
}

.states.hybrid span {
  border-color: #2a9d8f;
  color: #20639b;
  background: #f3fbfa;
}

.state-arrow {
  color: #e9c46a;
  font-size: 15px;
  font-weight: 700;
}


/* ------------------------------------------------ */
/* GAP 02 — REPRESENTATION */
/* ------------------------------------------------ */

.representation-flow {
  display: flex;
  align-items: center;
  gap: 3px;
}

.data-box,
.feature-box,
.model-box {
  width: 43px;
  height: 39px;

  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;

  border: 1px solid #dce4e9;
  border-radius: 6px;

  background: #f8fafb;

  color: #475569;

  font-size: 7px;
  line-height: 1.1;
  text-align: center;
}

.feature-box {
  border-color: #2a9d8f;
  background: #f3fbfa;
  width: 50px;
}

.model-box {
  border-color: #20639b;
  background: #f4f8fb;
}

.box-icon {
  margin-bottom: 3px;

  color: #173f5f;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 10px;
  font-weight: 700;
}

.flow-line {
  width: 8px;
  height: 1px;

  background: #cbd5e1;
}


/* ------------------------------------------------ */
/* GAP 03 — DATA LIMITATION */
/* ------------------------------------------------ */

.data-generation {
  display: flex;
  align-items: center;
  gap: 7px;
}

.real-data,
.synthetic-data {
  position: relative;

  display: grid;
  grid-template-columns: repeat(3, 7px);
  gap: 3px;

  width: 32px;
  padding-bottom: 13px;
}

.data-dot {
  width: 7px;
  height: 7px;

  border-radius: 50%;

  background: #20639b;
}

.synthetic-data .data-dot {
  background: #2a9d8f;
}

.data-label {
  position: absolute;
  left: 50%;
  bottom: 0;

  transform: translateX(-50%);

  white-space: nowrap;

  color: #94a3b8;

  font-size: 7px;
}

.generation-arrow {
  display: flex;
  align-items: center;
  gap: 2px;

  color: #e9c46a;
  font-size: 11px;
  font-weight: 700;
}

.arrow-line {
  width: 14px;
  height: 1px;

  background: #cbd5e1;
}


/* ------------------------------------------------ */
/* BOTTOM MESSAGE */
/* ------------------------------------------------ */

.bottom-message {
  flex: 0 0 auto;

  display: grid;
  grid-template-columns: 28px minmax(0, 1fr);

  align-items: center;
  gap: 8px;

  min-height: 42px;

  margin: 8px 4px 0;
  padding: 7px 12px;

  border: 1px solid #dce4e9;
  border-radius: 9px;

  background: #f8fafb;

  box-sizing: border-box;

  opacity: 1;
  transform: translateY(0);

  transition:
    opacity 0.4s ease,
    transform 0.4s ease;
}

.bottom-message.message-hidden {
  opacity: 0;
  transform: translateY(8px);
  pointer-events: none;
}

.message-mark {
  display: flex;
  align-items: center;
  justify-content: center;

  width: 28px;
  height: 28px;

  border-radius: 50%;

  background: #e9c46a;

  color: #173f5f;

  font-size: 15px;
  font-weight: 700;
}

.bottom-message span:last-child {
  color: #475569;

  font-size: 10.5px;
  line-height: 1.35;
}


/* RESPONSIVE */

@media (max-width: 800px) {
  .gap-card {
    grid-template-columns: 25px 145px minmax(0, 1fr);
  }
}
</style>