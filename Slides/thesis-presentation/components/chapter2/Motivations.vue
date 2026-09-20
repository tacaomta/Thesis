<template>
  <div class="motivation-slide">
    <div class="intro">
      The limitations of existing representations suggest three directions
      for improvement.
    </div>

    <div class="goals">
      <!-- Goal 1 -->
      <section
        class="goal-card goal-1"
        :class="{ visible: visibleCount >= 1 }"
      >
        <div class="goal-number">01</div>

        <div class="goal-icon">
          <svg viewBox="0 0 56 56" aria-hidden="true">
            <circle cx="28" cy="28" r="19" class="icon-circle" />
            <path
              d="M28 17 L28 29 L36 34"
              class="clock-hand"
            />
            <path
              d="M18 39 L23 34 L28 39 L34 31 L39 34"
              class="trend-line"
            />
          </svg>
        </div>

        <div class="goal-content">
          <div class="goal-label">GOAL 1</div>
          <h2>Efficiency &amp; Robustness</h2>
          <p>
            Reduce computational cost while being
            <strong>less sensitive to noise</strong>
            in gene expression measurements.
          </p>
        </div>
      </section>

      <!-- Goal 2 -->
      <section
        class="goal-card goal-2"
        :class="{ visible: visibleCount >= 2 }"
      >
        <div class="goal-number">02</div>

        <div class="goal-icon">
          <svg viewBox="0 0 56 56" aria-hidden="true">
            <rect
              x="10"
              y="15"
              width="10"
              height="26"
              rx="2"
              class="bar bar-low"
            />
            <rect
              x="23"
              y="10"
              width="10"
              height="31"
              rx="2"
              class="bar bar-mid"
            />
            <rect
              x="36"
              y="6"
              width="10"
              height="35"
              rx="2"
              class="bar bar-high"
            />
            <path
              d="M8 44 H48"
              class="baseline"
            />
          </svg>
        </div>

        <div class="goal-content">
          <div class="goal-label">GOAL 2</div>
          <h2>Information Preservation</h2>
          <p>
            Preserve more
            <strong>expression-level information</strong>
            than conventional Boolean representations.
          </p>
        </div>
      </section>

      <!-- Goal 3 -->
      <section
        class="goal-card goal-3"
        :class="{ visible: visibleCount >= 3 }"
      >
        <div class="goal-number">03</div>

        <div class="goal-icon">
          <svg viewBox="0 0 56 56" aria-hidden="true">
            <circle cx="13" cy="28" r="5" class="network-node" />
            <circle cx="29" cy="15" r="5" class="network-node" />
            <circle cx="29" cy="41" r="5" class="network-node" />
            <circle cx="45" cy="28" r="5" class="network-node target" />

            <path
              d="M17 25 L25 18"
              class="network-edge"
            />
            <path
              d="M17 31 L25 38"
              class="network-edge"
            />
            <path
              d="M34 15 L41 25"
              class="network-edge"
            />
            <path
              d="M34 41 L41 31"
              class="network-edge"
            />
          </svg>
        </div>

        <div class="goal-content">
          <div class="goal-label">GOAL 3</div>
          <h2>Structure &amp; Dynamics</h2>
          <p>
            Improve both
            <strong>network structure</strong>
            and
            <strong>dynamic behavior</strong>
            accuracy.
          </p>
        </div>
      </section>
    </div>

    <div
      class="bottom-message"
      :class="{ visible: visibleCount >= 3 }"
    >
      <span class="message-mark">→</span>

      <p>
        Find a representation that balances
        <strong>information, efficiency, and robustness</strong>.
      </p>
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
.motivation-slide {
  position: relative;
  width: 100%;
  height: 100%;
  min-height: 0;
  display: flex;
  flex-direction: column;
  overflow: hidden;
  box-sizing: border-box;
}

.intro {
  flex: 0 0 auto;
  margin: 0 4px 12px;
  color: #64748b;
  font-size: 13px;
  line-height: 1.45;
}

.goals {
  flex: 1 1 auto;
  min-height: 0;
  display: flex;
  flex-direction: column;
  gap: 9px;
}

.goal-card {
  flex: 1 1 0;
  min-height: 0;
  display: grid;
  grid-template-columns: 38px 58px minmax(0, 1fr);
  align-items: center;
  gap: 14px;

  padding: 12px 18px;

  border: 1px solid #dce4e9;
  border-radius: 11px;
  background: #ffffff;
  box-sizing: border-box;

  opacity: 0;
  transform: translateY(14px);
  pointer-events: none;

  transition:
    opacity 0.4s ease,
    transform 0.4s ease;
}

.goal-card.visible {
  opacity: 1;
  transform: translateY(0);
  pointer-events: auto;
}

.goal-number {
  color: #cbd5dc;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 17px;
  font-weight: 700;
  letter-spacing: -0.03em;
}

.goal-icon {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 54px;
  height: 54px;
  border-radius: 10px;
  background: #f8fafb;
}

.goal-icon svg {
  display: block;
  width: 42px;
  height: 42px;
  overflow: visible;
}

/* Goal 1 icon */

.goal-1 .icon-circle {
  fill: none;
  stroke: #20639b;
  stroke-width: 2;
}

.goal-1 .clock-hand {
  fill: none;
  stroke: #20639b;
  stroke-width: 2;
  stroke-linecap: round;
  stroke-linejoin: round;
}

.goal-1 .trend-line {
  fill: none;
  stroke: #2a9d8f;
  stroke-width: 2;
  stroke-linecap: round;
  stroke-linejoin: round;
}

/* Goal 2 icon */

.goal-2 .bar {
  fill: #20639b;
}

.goal-2 .bar-low {
  opacity: 0.45;
}

.goal-2 .bar-mid {
  opacity: 0.7;
}

.goal-2 .bar-high {
  opacity: 0.95;
}

.goal-2 .baseline {
  fill: none;
  stroke: #94a3b8;
  stroke-width: 1.5;
  stroke-linecap: round;
}

/* Goal 3 icon */

.goal-3 .network-node {
  fill: #ffffff;
  stroke: #20639b;
  stroke-width: 2;
}

.goal-3 .network-node.target {
  stroke: #2a9d8f;
}

.goal-3 .network-edge {
  fill: none;
  stroke: #20639b;
  stroke-width: 1.8;
  stroke-linecap: round;
  stroke-linejoin: round;
}

.goal-content {
  min-width: 0;
}

.goal-label {
  margin-bottom: 3px;
  color: #2a9d8f;
  font-size: 8px;
  font-weight: 700;
  letter-spacing: 0.12em;
}

.goal-content h2 {
  margin: 0 0 5px;
  color: #173f5f;
  font-size: 19px;
  font-weight: 700;
  line-height: 1.2;
  letter-spacing: -0.015em;
}

.goal-content p {
  margin: 0;
  max-width: 760px;
  color: #475569;
  font-size: 11px;
  line-height: 1.45;
}

.goal-content strong {
  color: #24313a;
  font-weight: 700;
  background: linear-gradient(
    180deg,
    transparent 48%,
    rgba(233, 196, 106, 0.65) 48%,
    rgba(233, 196, 106, 0.65) 90%,
    transparent 90%
  );
  padding: 0 2px;
  box-decoration-break: clone;
  -webkit-box-decoration-break: clone;
}

.bottom-message {
  flex: 0 0 auto;

  display: flex;
  align-items: center;
  gap: 10px;

  min-height: 43px;
  margin: 10px 4px 0;
  padding: 7px 14px;

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

.bottom-message.visible {
  opacity: 1;
  transform: translateY(0);
  pointer-events: auto;
}

.message-mark {
  display: flex;
  align-items: center;
  justify-content: center;

  width: 27px;
  height: 27px;

  border-radius: 50%;
  background: #e9c46a;

  color: #173f5f;
  font-size: 16px;
  font-weight: 700;
}

.bottom-message p {
  margin: 0;
  color: #475569;
  font-size: 10.5px;
  line-height: 1.35;
}

.bottom-message strong {
  color: #173f5f;
  font-weight: 700;
}

@media (max-width: 800px) {
  .goal-card {
    grid-template-columns: 32px 48px minmax(0, 1fr);
    gap: 10px;
    padding: 10px 12px;
  }

  .goal-icon {
    width: 46px;
    height: 46px;
  }

  .goal-icon svg {
    width: 36px;
    height: 36px;
  }

  .goal-content h2 {
    font-size: 16px;
  }

  .goal-content p {
    font-size: 10px;
  }
}
</style>