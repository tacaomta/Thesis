<script setup>
import { ref, watch, onMounted, onBeforeUnmount } from 'vue'
import { useNav } from '@slidev/client'

const { currentPage } = useNav()

watch(currentPage, () => {
  visibleCount.value = 0
})
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
          <circle cx="385" cy="235" r="18" class="mini-node input-node" />
          <circle cx="445" cy="235" r="13" class="mini-node hidden-node" />
          <circle cx="500" cy="235" r="10" class="mini-node latent-node" />
          <circle cx="540" cy="235" r="13" class="mini-node hidden-node" />

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
.feedback-group.visible,
.termination-group.visible {
  opacity: 1;
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

/* =========================
   FEEDBACK LOOP
========================= */

.feedback-line {
  fill: none;
  stroke: #2a9d8f;
  stroke-width: 2.5;
  stroke-dasharray: 7 5;
}

.feedback-arrow {
  fill: #2a9d8f;
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
   REDUCED MOTION
========================= */

@media (prefers-reduced-motion: reduce) {
  .step-group,
  .model-group,
  .arrow-group,
  .feedback-group,
  .termination-group {
    transition: none;
  }
}
</style>