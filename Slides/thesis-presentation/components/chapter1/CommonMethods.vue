<template>
  <div class="approaches-slide">

    <div class="intro">
      GRN inference methods can be grouped by the type of dependency
      they are designed to capture.
    </div>

    <div class="approach-grid">
      <article
        v-for="(approach, index) in approaches"
        :key="approach.title"
        class="approach-card"
        :class="{ 'card-hidden': index >= visibleCount }"
      >
        <div class="approach-visual">
          <div class="approach-number">
            {{ String(index + 1).padStart(2, '0') }}
          </div>

          <div class="mini-network">
            <svg viewBox="0 0 80 54" aria-hidden="true">

              <defs>
                <marker
                  :id="`arrow-${index}`"
                  markerWidth="7"
                  markerHeight="7"
                  refX="6"
                  refY="3.5"
                  orient="auto"
                  markerUnits="userSpaceOnUse"
                >
                  <path
                    d="M0 0 L7 3.5 L0 7 Z"
                    fill="#20639B"
                  />
                </marker>
              </defs>

              <template v-if="index === 0">
                <line
                  x1="22"
                  y1="27"
                  x2="58"
                  y2="27"
                  class="network-edge"
                  :marker-end="`url(#arrow-${index})`"
                />

                <circle
                  cx="15"
                  cy="27"
                  r="7"
                  class="network-node regulator"
                />

                <circle
                  cx="65"
                  cy="27"
                  r="7"
                  class="network-node target"
                />
              </template>

              <template v-else-if="index === 1">
                <path
                  d="M21 17 C32 10 48 10 59 17"
                  class="network-edge"
                  :marker-end="`url(#arrow-${index})`"
                />

                <path
                  d="M21 37 C32 44 48 44 59 37"
                  class="network-edge"
                  :marker-end="`url(#arrow-${index})`"
                />

                <circle
                  cx="15"
                  cy="17"
                  r="7"
                  class="network-node regulator"
                />

                <circle
                  cx="15"
                  cy="37"
                  r="7"
                  class="network-node regulator"
                />

                <circle
                  cx="65"
                  cy="27"
                  r="8"
                  class="network-node target"
                />
              </template>

              <template v-else-if="index === 2">
                <path
                  d="M22 27 C30 27 35 15 45 15 C52 15 57 21 59 27"
                  class="network-edge"
                  :marker-end="`url(#arrow-${index})`"
                />

                <path
                  d="M22 27 C30 27 35 39 45 39 C52 39 57 33 59 27"
                  class="network-edge"
                  :marker-end="`url(#arrow-${index})`"
                />

                <circle
                  cx="15"
                  cy="27"
                  r="7"
                  class="network-node regulator"
                />

                <circle
                  cx="65"
                  cy="27"
                  r="8"
                  class="network-node target"
                />
              </template>

              <template v-else>
                <path
                  d="M22 27 C30 12 39 12 49 27 C57 39 63 39 69 27"
                  class="network-edge"
                  :marker-end="`url(#arrow-${index})`"
                />

                <circle
                  cx="15"
                  cy="27"
                  r="7"
                  class="network-node regulator"
                />

                <circle
                  cx="39"
                  cy="27"
                  r="7"
                  class="network-node"
                />

                <circle
                  cx="76"
                  cy="27"
                  r="7"
                  class="network-node target"
                />
              </template>

            </svg>
          </div>
        </div>

        <div class="approach-body">
          <h2>{{ approach.title }}</h2>

          <div class="examples">
            <span class="examples-label">Examples</span>

            <span class="example-list">
              {{ approach.examples }}
            </span>
          </div>

          <div class="pros-cons">
            <div class="pro">
              <span class="label">Strength</span>
              <p>{{ approach.strength }}</p>
            </div>

            <div class="con">
              <span class="label">Limitation</span>
              <p>{{ approach.limitation }}</p>
            </div>
          </div>
        </div>
      </article>
    </div>

    <div
      class="bottom-message"
      :class="{ 'message-hidden': visibleCount < approaches.length }"
    >
      <span class="message-mark">→</span>

      <span>
        Different approaches capture different aspects of regulation,
        but no single family fully resolves the challenges of
        high dimensionality, limited observations, and complex dependencies.
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

  if (visibleCount.value < approaches.length) {
    visibleCount.value += 1
  }
}

onMounted(() => {
  window.addEventListener('keydown', handleKeydown, true)
})

onBeforeUnmount(() => {
  window.removeEventListener('keydown', handleKeydown, true)
})

const approaches = [
  {
    title: 'Correlation-based',
    examples: 'Pearson correlation, Spearman correlation',
    strength: 'Simple, fast, and easy to interpret.',
    limitation: 'Mainly captures pairwise statistical association.'
  },
  {
    title: 'Information-theoretic',
    examples: 'Mutual Information, ARACNe',
    strength: 'Can capture nonlinear statistical dependencies.',
    limitation: 'Sensitive to dependency estimation and threshold selection.'
  },
  {
    title: 'Regression / Machine Learning',
    examples: 'GENIE3, TIGRESS',
    strength: 'Can model multivariate and potentially complex relationships.',
    limitation: 'Model selection and computation can become demanding.'
  },
  {
    title: 'Dynamic / Time-series models',
    examples: 'Dynamic Bayesian Networks, ODE-based models',
    strength: 'Explicitly model temporal dependencies and dynamics.',
    limitation: 'Often require sufficient time points and strong assumptions.'
  }
]
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
}

/* INTRO */

.intro {
  flex: 0 0 auto;
  margin: 0 4px 9px;
  color: #64748b;
  font-size: 13px;
  line-height: 1.45;
}

/* APPROACH GRID */

.approach-grid {
  flex: 0 0 auto;
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: 8px;
  min-width: 0;
}

/* APPROACH CARD */

.approach-card {
  min-width: 0;
  min-height: 108px;
  display: grid;
  grid-template-columns: 78px minmax(0, 1fr);
  gap: 10px;
  padding: 9px 11px;
  border: 1px solid #dce4e9;
  border-radius: 10px;
  background: #ffffff;
  box-sizing: border-box;

  opacity: 1;
  transform: translateY(0);

  transition:
    opacity 0.35s ease,
    transform 0.35s ease;
}

/* HIDDEN CARD */

.approach-card.card-hidden {
  opacity: 0;
  transform: translateY(12px);
  pointer-events: none;
}

/* LEFT VISUAL AREA */

.approach-visual {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-width: 0;
  border-right: 1px solid #eef2f4;
}

/* CARD NUMBER */

.approach-number {
  position: absolute;
  top: 0;
  left: 0;
  color: #94a3b8;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 9px;
  font-weight: 600;
  line-height: 1;
}

/* MINI NETWORK */

.mini-network {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 70px;
  height: 54px;
}

.mini-network svg {
  display: block;
  width: 70px;
  height: 48px;
  overflow: visible;
}

/* NETWORK EDGES */

.network-edge {
  fill: none;
  stroke: #20639b;
  stroke-width: 2;
  stroke-linecap: round;
  stroke-linejoin: round;
}

/* NETWORK NODES */

.network-node {
  fill: #ffffff;
  stroke: #20639b;
  stroke-width: 2;
}

.network-node.regulator {
  stroke: #20639b;
}

.network-node.target {
  stroke: #2a9d8f;
}

/* CARD BODY */

.approach-body {
  min-width: 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

/* TITLE */

.approach-body h2 {
  margin: 0 0 4px;
  color: #173f5f;
  font-size: 15px;
  font-weight: 700;
  line-height: 1.2;
  letter-spacing: -0.01em;
}

/* EXAMPLES */

.examples {
  display: flex;
  align-items: baseline;
  gap: 5px;
  min-width: 0;
  margin-bottom: 6px;
  line-height: 1.25;
}

.examples-label {
  flex: 0 0 auto;
  color: #2a9d8f;
  font-size: 9px;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.08em;
}

.example-list {
  min-width: 0;
  color: #64748b;
  font-size: 10px;
  line-height: 1.25;
}

/* STRENGTH / LIMITATION */

.pros-cons {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 8px;
}

.pros-cons > div {
  min-width: 0;
}

/* LABELS */

.label {
  display: block;
  margin-bottom: 2px;
  font-size: 9px;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.07em;
}

.pro .label {
  color: #2a9d8f;
}

.con .label {
  color: #e76f51;
}

/* DESCRIPTION */

.pros-cons p {
  margin: 0;
  color: #475569;
  font-size: 9.5px;
  line-height: 1.3;
}

/* BOTTOM MESSAGE */

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
    opacity 0.35s ease,
    transform 0.35s ease;
}

/* HIDDEN MESSAGE */

.bottom-message.message-hidden {
  opacity: 0;
  transform: translateY(8px);
  pointer-events: none;
}

/* MESSAGE ICON */

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

/* MESSAGE TEXT */

.bottom-message span:last-child {
  color: #475569;
  font-size: 10.5px;
  line-height: 1.35;
}

/* RESPONSIVE */

@media (max-width: 800px) {
  .approach-grid {
    grid-template-columns: 1fr;
  }

  .approach-card {
    min-height: 96px;
  }
}
</style>