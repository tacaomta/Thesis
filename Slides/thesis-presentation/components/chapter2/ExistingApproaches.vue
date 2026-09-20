<template>
  <div class="approaches-slide">

    <div class="approach-comparison">
      <section
        class="approach-group real-valued"
        :class="{ visible: visibleCount >= 1 }"
      >
        <div class="group-header">
          <div class="group-icon">
            <svg viewBox="0 0 48 48" aria-hidden="true">
              <line x1="8" y1="38" x2="42" y2="38" class="axis" />
              <line x1="8" y1="38" x2="8" y2="8" class="axis" />
              <path
                d="M10 32 C16 27 18 18 24 22 C29 26 31 12 39 14"
                class="curve"
              />
            </svg>
          </div>

          <div>
            <h2>Real-valued approaches</h2>
            <p class="group-subtitle">
              Preserve the continuous expression values
            </p>
          </div>
        </div>

        <div class="representation">
          <span class="representation-label">Representation</span>

          <div class="expression-values">
            <span>0.21</span>
            <span>0.38</span>
            <span>0.74</span>
            <span>0.61</span>
            <span>0.89</span>
          </div>
        </div>

        <div class="methods">
          <span class="section-label">Representative methods</span>

          <div class="method-list">
            <div class="method">
              <span class="method-name">GENIE3</span>
              <span class="method-type">
                Tree-based ensemble learning
              </span>
            </div>

            <div class="method">
              <span class="method-name">TIGRESS</span>
              <span class="method-type">
                Regression + stability selection
              </span>
            </div>

            <div class="method">
              <span class="method-name">ODE-based models</span>
              <span class="method-type">
                Continuous dynamic modeling
              </span>
            </div>
          </div>
        </div>

        <div class="pros-cons">
          <div class="advantage">
            <span class="label">Advantage</span>
            <p>
              Retain rich quantitative information and expression variation.
            </p>
          </div>

          <div class="limitation">
            <span class="label">Limitation</span>
            <p>
                More sensitive to
                <span class="keyword">noise</span>
                and often
                <span class="keyword">computationally demanding</span>.
            </p>
          </div>
        </div>
      </section>

      <section
        class="approach-group boolean"
        :class="{ visible: visibleCount >= 2 }"
      >
        <div class="group-header">
          <div class="group-icon">
            <svg viewBox="0 0 48 48" aria-hidden="true">
              <rect
                x="7"
                y="8"
                width="34"
                height="13"
                rx="3"
                class="binary-box"
              />
              <rect
                x="7"
                y="27"
                width="34"
                height="13"
                rx="3"
                class="binary-box"
              />

              <text x="13" y="18" class="binary-text">0</text>
              <text x="31" y="18" class="binary-text">1</text>
              <text x="13" y="37" class="binary-text">0</text>
              <text x="31" y="37" class="binary-text">1</text>
            </svg>
          </div>

          <div>
            <h2>Boolean approaches</h2>
            <p class="group-subtitle">
              Convert expression into discrete ON / OFF states
            </p>
          </div>
        </div>

        <div class="representation">
          <span class="representation-label">Representation</span>

          <div class="expression-values boolean-values">
            <span>0</span>
            <span>0</span>
            <span>1</span>
            <span>1</span>
            <span>1</span>
          </div>
        </div>

        <div class="methods">
          <span class="section-label">Representative methods</span>

          <div class="method-list">
            <div class="method">
              <span class="method-name">Boolean Network</span>
              <span class="method-type">
                Binary regulatory states
              </span>
            </div>

            <div class="method">
              <span class="method-name">REVEAL</span>
              <span class="method-type">
                Information-based Boolean inference
              </span>
            </div>
            <div class="method">
              <span class="method-name">MIBNI</span>
              <span class="method-type">
                Information-based Boolean inference
              </span>
            </div>
          </div>
        </div>

        <div class="pros-cons">
          <div class="advantage">
            <span class="label">Advantage</span>
            <p>
              Simple representation, lower computational cost, and less
              sensitive to small fluctuations.
            </p>
          </div>

          <div class="limitation">
            <span class="label">Limitation</span>
            <p>
                Binary states can
                <span class="keyword">discard important expression-level information</span>
                and
                <span class="keyword">dynamic variation</span>.
            </p>
          </div>
        </div>
      </section>
    </div>

    <div
      class="bottom-question"
      :class="{ visible: visibleCount >= 3 }"
    >
      <span class="question-mark">?</span>

      <div>
        <span class="question-label">The trade-off</span>

        <p>
          Can we preserve more information than Boolean models while remaining
          efficient and robust to noise?
        </p>
      </div>
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
.approaches-slide {
  position: relative;
  width: 100%;
  height: 100%;
  min-height: 0;
  display: flex;
  flex-direction: column;
  overflow: hidden;
  box-sizing: border-box;
  top: 50px;
}

.intro {
  flex: 0 0 auto;
  margin: 0 4px 10px;
  color: #64748b;
  font-size: 13px;
  line-height: 1.45;
}

.approach-comparison {
  flex: 0 0 auto;
  display: grid;
  grid-template-columns: minmax(0, 1fr) minmax(0, 1fr);
  gap: 10px;
  min-width: 0;
}

.approach-group {
  min-width: 0;
  display: flex;
  flex-direction: column;
  padding: 11px 13px;
  border: 1px solid #dce4e9;
  border-radius: 11px;
  background: #ffffff;
  box-sizing: border-box;

  opacity: 0;
  transform: translateY(12px);
  pointer-events: none;

  transition:
    opacity 0.4s ease,
    transform 0.4s ease;
}

.approach-group.visible {
  opacity: 1;
  transform: translateY(0);
  pointer-events: auto;
}

.group-header {
  display: grid;
  grid-template-columns: 46px minmax(0, 1fr);
  align-items: center;
  gap: 9px;
  margin-bottom: 9px;
}

.group-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 46px;
  height: 46px;
  border-radius: 9px;
  background: #f8fafb;
}

.group-icon svg {
  display: block;
  width: 38px;
  height: 38px;
  overflow: visible;
}

.real-valued .axis {
  fill: none;
  stroke: #94a3b8;
  stroke-width: 1.5;
  stroke-linecap: round;
}

.real-valued .curve {
  fill: none;
  stroke: #20639b;
  stroke-width: 2.5;
  stroke-linecap: round;
  stroke-linejoin: round;
}

.boolean .binary-box {
  fill: #ffffff;
  stroke: #2a9d8f;
  stroke-width: 1.5;
}

.boolean .binary-text {
  fill: #173f5f;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 9px;
  font-weight: 600;
}

.group-header h2 {
  margin: 0 0 3px;
  color: #173f5f;
  font-size: 17px;
  font-weight: 700;
  line-height: 1.2;
  letter-spacing: -0.01em;
}

.group-subtitle {
  margin: 0;
  color: #64748b;
  font-size: 10px;
  line-height: 1.35;
}

.representation {
  display: flex;
  align-items: center;
  gap: 9px;
  margin-bottom: 9px;
  padding: 7px 9px;
  border-radius: 7px;
  background: #f8fafb;
}

.representation-label {
  flex: 0 0 auto;
  color: #64748b;
  font-size: 8px;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.08em;
}

.expression-values {
  display: flex;
  align-items: center;
  gap: 5px;
  min-width: 0;
}

.expression-values span {
  display: flex;
  align-items: center;
  justify-content: center;
  min-width: 39px;
  height: 22px;
  padding: 0 5px;
  border: 1px solid #dce4e9;
  border-radius: 4px;
  background: #ffffff;
  color: #20639b;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 9px;
  font-weight: 600;
}

.boolean-values span {
  min-width: 25px;
  color: #2a9d8f;
}

.methods {
  margin-bottom: 8px;
}

.section-label {
  display: block;
  margin-bottom: 5px;
  color: #64748b;
  font-size: 8px;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.08em;
}

.method-list {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.method {
  display: grid;
  grid-template-columns: 145px minmax(0, 1fr);
  align-items: center;
  gap: 7px;
  min-width: 0;
  padding: 5px 7px;
  border-left: 2px solid #20639b;
  background: #f8fafb;
  box-sizing: border-box;
}

.boolean .method {
  border-left-color: #2a9d8f;
}

.method-name {
  color: #24313a;
  font-size: 10px;
  font-weight: 700;
}

.method-type {
  min-width: 0;
  color: #64748b;
  font-size: 9px;
  line-height: 1.25;
}

.pros-cons {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 8px;
  margin-top: auto;
}

.pros-cons > div {
  min-width: 0;
  padding-top: 6px;
  border-top: 1px solid #eef2f4;
}

.label {
  display: block;
  margin-bottom: 3px;
  font-size: 8px;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.08em;
}

.advantage .label {
  color: #2a9d8f;
}

.limitation .label {
  color: #e76f51;
}

.pros-cons p {
  margin: 0;
  color: #475569;
  font-size: 9.5px;
  line-height: 1.35;
}

.bottom-question {
  flex: 0 0 auto;
  display: grid;
  grid-template-columns: 32px minmax(0, 1fr);
  align-items: center;
  gap: 9px;
  min-height: 43px;
  margin: 9px 4px 0;
  padding: 7px 12px;
  border: 1px solid #dce4e9;
  border-radius: 9px;
  background: #ffffff;
  box-sizing: border-box;

  opacity: 0;
  transform: translateY(8px);
  pointer-events: none;

  transition:
    opacity 0.4s ease,
    transform 0.4s ease;
}

.bottom-question.visible {
  opacity: 1;
  transform: translateY(0);
  pointer-events: auto;
}

.question-mark {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 30px;
  height: 30px;
  border-radius: 50%;
  background: #e9c46a;
  color: #173f5f;
  font-size: 16px;
  font-weight: 700;
}

.question-label {
  display: block;
  margin-bottom: 1px;
  color: #173f5f;
  font-size: 9px;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.08em;
}

.bottom-question p {
  margin: 0;
  color: #475569;
  font-size: 10.5px;
  line-height: 1.3;
}
.limitation .keyword {
  color: #c2412d;
  font-weight: 700;
  text-decoration-line: underline;
  text-decoration-color: #e76f51;
  text-decoration-thickness: 2px;
  text-underline-offset: 3px;
}

@media (max-width: 800px) {
  .approach-comparison {
    grid-template-columns: 1fr;
  }

  .approach-group {
    min-height: 0;
  }

  .method {
    grid-template-columns: 125px minmax(0, 1fr);
  }
}
</style>