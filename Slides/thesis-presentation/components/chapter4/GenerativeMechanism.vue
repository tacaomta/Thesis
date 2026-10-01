<script setup>
import { ref, watch, onMounted, onBeforeUnmount } from 'vue'
import { useNav } from '@slidev/client'

const { currentPage } = useNav()

const visibleCount = ref(0)
const totalItems = 3
const cycleCount = ref(1)

let cycleTimer = null

function startCycle() {
  if (cycleTimer) return

  cycleTimer = setInterval(() => {
    cycleCount.value = cycleCount.value >= 6 ? 1 : cycleCount.value + 1
  }, 2400)
}

function stopCycle() {
  if (cycleTimer) {
    clearInterval(cycleTimer)
    cycleTimer = null
  }
}

watch(visibleCount, (val) => {
  if (val >= 2) {
    startCycle()
  } else {
    stopCycle()
    cycleCount.value = 1
  }
})

watch(currentPage, () => {
  visibleCount.value = 0
  cycleCount.value = 1
  stopCycle()
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
  window.addEventListener('keydown', handleKeydown, true)
})

onBeforeUnmount(() => {
  window.removeEventListener('keydown', handleKeydown, true)
  stopCycle()
})
</script>

<template>
  <div class="generation-slide">

    <!-- =========================
         MAIN GENERATIVE LOOP
    ========================== -->
    <div class="mechanism">

      <svg
        class="mechanism-svg"
        viewBox="0 0 1120 470"
        preserveAspectRatio="xMidYMid meet"
        role="img"
        aria-label="Auto-regressive generative mechanism for synthesizing future gene expression states"
      >

        <!-- =========================
             STEP 1 · INPUT
        ========================== -->

        <g
          class="step-group"
          :class="{ visible: visibleCount >= 1 }"
        >
          <rect
            x="45"
            y="155"
            width="205"
            height="115"
            rx="12"
            class="input-box"
          />

          <text
            x="147.5"
            y="140"
            class="node-title"
          >
            Current Input
          </text>

          <text
            x="147.5"
            y="205"
            class="equation"
          >
            T(tᵢ ⊕ tᵢ₊₁)
          </text>

          <text
            x="147.5"
            y="238"
            class="node-subtitle"
          >
            observed / generated pair
          </text>
        </g>

        <!-- =========================
             INPUT → MODEL
        ========================== -->

        <g
          class="arrow-group"
          :class="{ visible: visibleCount >= 1 }"
        >
          <line x1="250" y1="212" x2="335" y2="212" />
          <polygon points="335,212 323,205 323,219" />

          <text x="292" y="192" class="arrow-label">
            input
          </text>

          <circle
            v-if="visibleCount >= 1"
            r="4.5"
            class="travel-particle forward-particle"
          >
            <animateMotion
              path="M 250,212 L 330,212"
              dur="1.6s"
              repeatCount="indefinite"
              begin="0s"
            />
          </circle>
        </g>

        <!-- =========================
             AUTOENCODER
        ========================== -->

        <g
          class="model-group"
          :class="{ visible: visibleCount >= 1 }"
        >
          <rect
            x="335"
            y="125"
            width="220"
            height="175"
            rx="16"
            class="model-box"
          />

          <text
            x="445"
            y="162"
            class="model-title"
          >
            Trained
          </text>

          <text
            x="445"
            y="188"
            class="model-title"
          >
            Autoencoder
          </text>

          <!-- mini architecture -->
          <circle cx="385" cy="235" r="18" class="mini-node input-node" style="animation-delay: 0s" />
          <circle cx="445" cy="235" r="13" class="mini-node hidden-node" style="animation-delay: 0.2s" />
          <circle cx="500" cy="235" r="10" class="mini-node latent-node" style="animation-delay: 0.4s" />
          <circle cx="540" cy="235" r="13" class="mini-node hidden-node" style="animation-delay: 0.6s" />

          <line x1="403" y1="235" x2="432" y2="235" class="mini-line" />
          <line x1="458" y1="235" x2="490" y2="235" class="mini-line" />
          <line x1="510" y1="235" x2="527" y2="235" class="mini-line" />

          <text
            x="445"
            y="276"
            class="model-subtitle"
          >
            learned transition mapping
          </text>
        </g>

        <!-- =========================
             MODEL → OUTPUT
        ========================== -->

        <g
          class="arrow-group"
          :class="{ visible: visibleCount >= 1 }"
        >
          <line x1="555" y1="212" x2="640" y2="212" />
          <polygon points="640,212 628,205 628,219" />

          <text x="597" y="192" class="arrow-label">
            reconstruct
          </text>

          <circle
            v-if="visibleCount >= 1"
            r="4.5"
            class="travel-particle forward-particle"
          >
            <animateMotion
              path="M 555,212 L 635,212"
              dur="1.6s"
              repeatCount="indefinite"
              begin="0.3s"
            />
          </circle>
        </g>

        <!-- =========================
             PREDICTED OUTPUT
        ========================== -->

        <g
          class="step-group"
          :class="{ visible: visibleCount >= 1 }"
        >
          <rect
            x="640"
            y="135"
            width="220"
            height="155"
            rx="12"
            class="output-box"
          />

          <text
            x="750"
            y="165"
            class="node-title"
          >
            Predicted Next Pair
          </text>

          <text
            x="750"
            y="215"
            class="equation predicted"
          >
            T̂(tᵢ₊₁ ⊕ tᵢ₊₂)
          </text>

          <line
            x1="665"
            y1="240"
            x2="835"
            y2="240"
            class="split-line"
          />

          <text
            x="707"
            y="263"
            class="half-label"
          >
            V̂(tᵢ₊₁)
          </text>

          <text
            x="793"
            y="263"
            class="half-label future"
          >
            V̂(tᵢ₊₂)
          </text>
        </g>

        <!-- =========================
             FEEDBACK LOOP
        ========================== -->

        <g
          class="feedback-group"
          :class="{ visible: visibleCount >= 2 }"
        >

          <!-- vertical from output -->
          <path
            d="M 750 290
               L 750 355
               L 445 355
               L 445 300"
            class="feedback-line"
          />

          <polygon
            points="445,300 438,312 452,312"
            class="feedback-arrow"
          />

          <circle
            v-if="visibleCount >= 2"
            r="5"
            class="travel-particle loop-particle"
          >
            <animateMotion
              path="M 750,290 L 750,355 L 445,355 L 445,300"
              dur="2.4s"
              repeatCount="indefinite"
              begin="0s"
            />
          </circle>

          <text
            x="600"
            y="345"
            class="feedback-label"
          >
            FEEDBACK / AUTOREGRESSIVE LOOP
          </text>

          <!-- feedback annotation -->
          <rect
            x="875"
            y="160"
            width="195"
            height="125"
            rx="10"
            class="feedback-note"
          />

          <text
            x="972.5"
            y="190"
            class="note-title"
          >
            Next Input
          </text>

          <text
            x="972.5"
            y="220"
            class="note-equation"
          >
            T(tᵢ₊₁ ⊕ tᵢ₊₂)
          </text>

          <text
            x="972.5"
            y="251"
            class="note-text"
          >
            previous prediction
          </text>

          <text
            x="972.5"
            y="268"
            class="note-text"
          >
            becomes the next input
          </text>

        </g>

        <!-- =========================
             TERMINATION
        ========================== -->

        <g
          class="termination-group"
          :class="{ visible: visibleCount >= 3 }"
        >

          <rect
            x="245"
            y="390"
            width="630"
            height="52"
            rx="10"
            class="termination-box"
          />

          <circle
            cx="273"
            cy="416"
            r="10"
            class="termination-dot"
          />

          <text
            x="297"
            y="422"
            class="termination-text"
          >
            Repeat until
          </text>

          <text
            x="395"
            y="422"
            class="termination-equation"
          >
            t = m
          </text>

          <text
            x="455"
            y="422"
            class="termination-text"
          >
            — full temporal length reached
          </text>

          <text
            x="738"
            y="422"
            class="example"
          >
            (e.g., m = 100)
          </text>

        </g>

      </svg>

    </div>

    <!-- =========================
         PROGRESS
    ========================== -->

    <div class="progress">
      <span
        v-for="i in totalItems"
        :key="i"
        class="dot"
        :class="{ active: visibleCount >= i }"
      />

      <span
        v-if="visibleCount >= 2"
        class="cycle-badge"
      >
        <span class="cycle-pulse"></span>
        Iteration {{ cycleCount }}
      </span>

      <span
        v-if="visibleCount < totalItems"
        class="hint"
      >
        Press <strong>Space</strong> to reveal
      </span>
    </div>

  </div>
</template>

<style scoped>
.generation-slide {
  width: 100%;
  height: 100%;
  box-sizing: border-box;

  display: flex;
  flex-direction: column;
}

/* =========================
   MAIN VISUAL
========================= */

.mechanism {
  flex: 1;
  min-height: 0;

  display: flex;
  align-items: center;
  justify-content: center;
}

.mechanism-svg {
  width: 100%;
  max-width: 1120px;
  max-height: 500px;
  height: auto;
  overflow: visible;
}

/* =========================
   REVEAL GROUPS
========================= */

.step-group,
.model-group,
.arrow-group,
.feedback-group,
.termination-group {
  opacity: 0;

  transition:
    opacity 0.4s ease,
    transform 0.4s ease;
}

.step-group.visible,
.model-group.visible,
.arrow-group.visible,
.feedback-group.visible {
  opacity: 1;
}

.termination-group.visible {
  opacity: 1;
  animation: popIn 0.5s ease;
}

@keyframes popIn {
  0% {
    opacity: 0;
    transform: scale(0.92) translateY(6px);
  }
  60% {
    opacity: 1;
    transform: scale(1.015) translateY(0);
  }
  100% {
    opacity: 1;
    transform: scale(1) translateY(0);
  }
}

/* =========================
   INPUT / OUTPUT
========================= */

.input-box {
  fill: #f8fafb;
  stroke: #173f5f;
  stroke-width: 2;
}

.output-box {
  fill: rgba(42, 157, 143, 0.07);
  stroke: #2a9d8f;
  stroke-width: 2;
}

.step-group.visible .output-box {
  animation: breatheGlow 2.4s ease-in-out infinite;
}

@keyframes breatheGlow {
  0%, 100% {
    fill-opacity: 0.07;
  }
  50% {
    fill-opacity: 0.16;
  }
}

.node-title {
  fill: #173f5f;
  font-family: Inter, 'Segoe UI', sans-serif;
  font-size: 15px;
  font-weight: 700;
  text-anchor: middle;
}

.node-subtitle {
  fill: #64748b;
  font-family: Inter, 'Segoe UI', sans-serif;
  font-size: 10px;
  text-anchor: middle;
}

.equation {
  fill: #24313a;
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 22px;
  font-weight: 700;
  text-anchor: middle;
}

.predicted {
  fill: #2a9d8f;
}

.split-line {
  stroke: #dce4e9;
  stroke-width: 1;
  stroke-dasharray: 4 4;
}

.half-label {
  fill: #20639b;
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 11px;
  font-weight: 600;
  text-anchor: middle;
}

.half-label.future {
  fill: #2a9d8f;
}

/* =========================
   AUTOENCODER
========================= */

.model-box {
  fill: #ffffff;
  stroke: #20639b;
  stroke-width: 2;
}

.model-group.visible .model-box {
  animation: pulseGlow 2.4s ease-in-out infinite;
}

@keyframes pulseGlow {
  0%, 100% {
    stroke-width: 2;
    stroke-opacity: 1;
  }
  50% {
    stroke-width: 3;
    stroke-opacity: 0.65;
  }
}

.model-title {
  fill: #173f5f;
  font-family: Inter, 'Segoe UI', sans-serif;
  font-size: 16px;
  font-weight: 700;
  text-anchor: middle;
}

.model-subtitle {
  fill: #64748b;
  font-family: Inter, 'Segoe UI', sans-serif;
  font-size: 10px;
  text-anchor: middle;
}

.mini-node {
  stroke-width: 2;
  transform-box: fill-box;
  transform-origin: center;
}

.model-group.visible .mini-node {
  animation: nodePulse 1.8s ease-in-out infinite;
}

@keyframes nodePulse {
  0%, 100% {
    transform: scale(1);
  }
  40% {
    transform: scale(1.18);
  }
}

.input-node {
  fill: #f8fafb;
  stroke: #173f5f;
}

.hidden-node {
  fill: rgba(32, 99, 155, 0.12);
  stroke: #20639b;
}

.latent-node {
  fill: rgba(42, 157, 143, 0.18);
  stroke: #2a9d8f;
}

.mini-line {
  stroke: #94a3b8;
  stroke-width: 1.5;
}

/* =========================
   ARROWS
========================= */

.arrow-group line {
  stroke: #94a3b8;
  stroke-width: 2.5;
}

.arrow-group polygon {
  fill: #94a3b8;
}

.arrow-label {
  fill: #64748b;
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 10px;
  text-anchor: middle;
}

.travel-particle {
  fill: #20639b;
}

.forward-particle {
  fill: #20639b;
  filter: drop-shadow(0 0 2px rgba(32, 99, 155, 0.5));
}

/* =========================
   FEEDBACK LOOP
========================= */

.feedback-line {
  fill: none;
  stroke: #2a9d8f;
  stroke-width: 2.5;
  stroke-dasharray: 9 6;
}

.feedback-group.visible .feedback-line {
  animation: flowDash 1s linear infinite;
}

@keyframes flowDash {
  to {
    stroke-dashoffset: -30;
  }
}

.feedback-arrow {
  fill: #2a9d8f;
}

.loop-particle {
  fill: #2a9d8f;
  filter: drop-shadow(0 0 3px rgba(42, 157, 143, 0.65));
}

.feedback-label {
  fill: #2a9d8f;
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 10px;
  font-weight: 700;
  letter-spacing: 0.08em;
  text-anchor: middle;
}

.feedback-note {
  fill: rgba(42, 157, 143, 0.06);
  stroke: #b7dcd6;
  stroke-width: 1.5;
}

.feedback-group.visible .feedback-note {
  animation: notePulse 2.4s ease-in-out infinite;
}

@keyframes notePulse {
  0%, 100% {
    stroke: #b7dcd6;
  }
  50% {
    stroke: #2a9d8f;
  }
}

.note-title {
  fill: #2a9d8f;
  font-family: Inter, 'Segoe UI', sans-serif;
  font-size: 13px;
  font-weight: 700;
  text-anchor: middle;
}

.note-equation {
  fill: #24313a;
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 14px;
  font-weight: 700;
  text-anchor: middle;
}

.note-text {
  fill: #64748b;
  font-family: Inter, 'Segoe UI', sans-serif;
  font-size: 9px;
  text-anchor: middle;
}

/* =========================
   TERMINATION
========================= */

.termination-box {
  fill: #ffffff;
  stroke: #dce4e9;
  stroke-width: 1.5;
}

.termination-dot {
  fill: #e9c46a;
}

.termination-group.visible .termination-dot {
  animation: dotBlink 1.6s ease-in-out infinite;
}

@keyframes dotBlink {
  0%, 100% {
    opacity: 1;
  }
  50% {
    opacity: 0.4;
  }
}

.termination-text {
  fill: #64748b;
  font-family: Inter, 'Segoe UI', sans-serif;
  font-size: 12px;
}

.termination-equation {
  fill: #173f5f;
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 14px;
  font-weight: 700;
}

.example {
  fill: #64748b;
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 11px;
}

/* =========================
   PROGRESS
========================= */

.progress {
  height: 26px;
  flex: 0 0 26px;

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
   CYCLE BADGE
========================= */

.cycle-badge {
  display: inline-flex;
  align-items: center;
  gap: 6px;

  margin-left: 12px;
  padding: 3px 10px;

  border-radius: 999px;
  background: rgba(42, 157, 143, 0.09);
  border: 1px solid rgba(42, 157, 143, 0.35);

  color: #2a9d8f;

  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 10px;
  font-weight: 600;
  letter-spacing: 0.03em;
}

.cycle-pulse {
  width: 6px;
  height: 6px;

  border-radius: 50%;
  background: #2a9d8f;

  animation: cyclePulse 1.2s ease-in-out infinite;
}

@keyframes cyclePulse {
  0%, 100% {
    transform: scale(1);
    opacity: 1;
  }
  50% {
    transform: scale(1.5);
    opacity: 0.45;
  }
}

/* =========================
   REDUCED MOTION
========================= */

@media (prefers-reduced-motion: reduce) {
  .step-group,
  .model-group,
  .arrow-group,
  .feedback-group,
  .termination-group,
  .model-box,
  .mini-node,
  .feedback-line,
  .feedback-note,
  .termination-dot,
  .output-box,
  .cycle-pulse {
    animation: none !important;
    transition: none;
  }

  .travel-particle {
    display: none;
  }
}
</style>