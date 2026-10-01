<script setup>
import { ref, watch, onMounted, onBeforeUnmount } from 'vue'
import { useNav } from '@slidev/client'

const { currentPage } = useNav()

watch(currentPage, () => {
  visibleCount.value = 0
})
const visibleCount = ref(0)
const totalItems = 4

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
  <div class="autoencoder-slide">

    <!-- =========================
         ARCHITECTURE
    ========================== -->
    <div class="architecture">

      <!-- Encoder -->
      <Transition name="layer-reveal">
        <g v-if="visibleCount >= 1" class="architecture-group">
          <!-- SVG content is rendered below -->
        </g>
      </Transition>

      <svg
        class="network-svg"
        viewBox="0 0 1100 430"
        preserveAspectRatio="xMidYMid meet"
        role="img"
        aria-label="Symmetrical autoencoder architecture with dimensions 2n, 64, 32, 64, and 2n"
      >

        <!-- =========================
             CONNECTIONS
        ========================== -->

        <!-- Input → Hidden 1 -->
        <g
          class="connection-group"
          :class="{ visible: visibleCount >= 1 }"
        >
          <line x1="155" y1="210" x2="280" y2="210" />
          <polygon points="280,210 268,203 268,217" />
        </g>

        <!-- Hidden 1 → Latent -->
        <g
          class="connection-group"
          :class="{ visible: visibleCount >= 2 }"
        >
          <line x1="365" y1="210" x2="465" y2="210" />
          <polygon points="465,210 453,203 453,217" />
        </g>

        <!-- Latent → Hidden 3 -->
        <g
          class="connection-group"
          :class="{ visible: visibleCount >= 3 }"
        >
          <line x1="635" y1="210" x2="735" y2="210" />
          <polygon points="735,210 723,203 723,217" />
        </g>

        <!-- Hidden 3 → Output -->
        <g
          class="connection-group"
          :class="{ visible: visibleCount >= 3 }"
        >
          <line x1="820" y1="210" x2="945" y2="210" />
          <polygon points="945,210 933,203 933,217" />
        </g>

        <!-- =========================
             INPUT
        ========================== -->

        <g
          class="layer-group"
          :class="{ visible: visibleCount >= 1 }"
        >
          <rect
            class="layer-box input-layer"
            x="55"
            y="145"
            width="100"
            height="130"
            rx="12"
          />

          <text x="105" y="130" class="layer-title">
            Input
          </text>

          <text x="105" y="202" class="dimension">
            2n
          </text>

          <text x="105" y="232" class="layer-subtitle">
            concatenated
          </text>

          <text x="105" y="249" class="layer-subtitle">
            states
          </text>
        </g>

        <!-- =========================
             HIDDEN 1
        ========================== -->

        <g
          class="layer-group"
          :class="{ visible: visibleCount >= 1 }"
        >
          <rect
            class="layer-box encoder-layer"
            x="280"
            y="145"
            width="85"
            height="130"
            rx="12"
          />

          <text x="322.5" y="130" class="layer-title">
            Hidden 1
          </text>

          <text x="322.5" y="202" class="dimension">
            64
          </text>

          <text x="322.5" y="239" class="activation">
            ReLU
          </text>
        </g>

        <!-- =========================
             LATENT
        ========================== -->

        <g
          class="layer-group"
          :class="{ visible: visibleCount >= 2 }"
        >
          <rect
            class="layer-box latent-layer"
            x="465"
            y="125"
            width="170"
            height="170"
            rx="16"
          />

          <text x="550" y="110" class="layer-title">
            Latent Bottleneck
          </text>

          <text x="550" y="208" class="dimension latent-dimension">
            32
          </text>

          <text x="550" y="245" class="activation">
            ReLU
          </text>

          <text x="550" y="270" class="layer-subtitle">
            compressed representation
          </text>
        </g>

        <!-- =========================
             HIDDEN 3
        ========================== -->

        <g
          class="layer-group"
          :class="{ visible: visibleCount >= 3 }"
        >
          <rect
            class="layer-box decoder-layer"
            x="735"
            y="145"
            width="85"
            height="130"
            rx="12"
          />

          <text x="777.5" y="130" class="layer-title">
            Hidden 3
          </text>

          <text x="777.5" y="202" class="dimension">
            64
          </text>

          <text x="777.5" y="239" class="activation">
            ReLU
          </text>
        </g>

        <!-- =========================
             OUTPUT
        ========================== -->

        <g
          class="layer-group"
          :class="{ visible: visibleCount >= 3 }"
        >
          <rect
            class="layer-box output-layer"
            x="945"
            y="145"
            width="100"
            height="130"
            rx="12"
          />

          <text x="995" y="130" class="layer-title">
            Output
          </text>

          <text x="995" y="202" class="dimension">
            2n
          </text>

          <text x="995" y="239" class="activation linear">
            Linear
          </text>
        </g>

        <!-- =========================
             SECTION LABELS
        ========================== -->

        <g
          class="section-label"
          :class="{ visible: visibleCount >= 1 }"
        >
          <line x1="55" y1="335" x2="365" y2="335" />
          <text x="210" y="360">ENCODER</text>
        </g>

        <g
          class="section-label"
          :class="{ visible: visibleCount >= 3 }"
        >
          <line x1="735" y1="335" x2="1045" y2="335" />
          <text x="890" y="360">DECODER</text>
        </g>

      </svg>
    </div>

    <!-- =========================
         TRAINING CONFIGURATION
    ========================== -->

    <Transition name="config-reveal">
      <div
        v-if="visibleCount >= 4"
        class="training-config"
      >
        <div class="config-item">
          <span class="config-label">Hidden activation</span>
          <strong>ReLU</strong>
        </div>

        <div class="config-divider"></div>

        <div class="config-item">
          <span class="config-label">Output activation</span>
          <strong>Linear</strong>
        </div>

        <div class="config-divider"></div>

        <div class="config-item">
          <span class="config-label">Optimizer</span>
          <strong>Adam</strong>
        </div>

        <div class="config-divider"></div>

        <div class="config-item">
          <span class="config-label">Loss function</span>
          <strong>MSE</strong>
        </div>
      </div>
    </Transition>

    <!-- Progress -->
    <div class="progress">
      <span
        v-for="i in totalItems"
        :key="i"
        class="dot"
        :class="{ active: visibleCount >= i }"
      />

      <span v-if="visibleCount < totalItems" class="hint">
        Press <strong>Space</strong> to reveal
      </span>
    </div>

  </div>
</template>

<style scoped>
.autoencoder-slide {
  width: 100%;
  height: 100%;
  box-sizing: border-box;

  display: flex;
  flex-direction: column;
}

/* =========================
   ARCHITECTURE
========================= */

.architecture {
  flex: 1;
  min-height: 0;

  display: flex;
  align-items: center;
  justify-content: center;
}

.network-svg {
  width: 100%;
  max-width: 1080px;
  height: auto;
  max-height: 390px;
  overflow: visible;
}

/* =========================
   CONNECTIONS
========================= */

.connection-group {
  opacity: 0;
  transition: opacity 0.35s ease;
}

.connection-group.visible {
  opacity: 1;
}

.connection-group line {
  stroke: #94a3b8;
  stroke-width: 2.5;
}

.connection-group polygon {
  fill: #94a3b8;
}

/* =========================
   LAYERS
========================= */

.layer-group {
  opacity: 0;
  transform-box: fill-box;
  transform-origin: center;
  transition:
    opacity 0.4s ease,
    transform 0.4s ease;
}

.layer-group.visible {
  opacity: 1;
  transform: scale(1);
}

.layer-box {
  stroke-width: 2;
}

.input-layer {
  fill: #f8fafb;
  stroke: #173f5f;
}

.encoder-layer {
  fill: rgba(32, 99, 155, 0.08);
  stroke: #20639b;
}

.latent-layer {
  fill: rgba(42, 157, 143, 0.12);
  stroke: #2a9d8f;
  stroke-width: 2.5;
}

.decoder-layer {
  fill: rgba(32, 99, 155, 0.08);
  stroke: #20639b;
}

.output-layer {
  fill: #f8fafb;
  stroke: #173f5f;
}

/* =========================
   SVG TYPOGRAPHY
========================= */

.layer-title {
  fill: #173f5f;
  font-family: Inter, 'Segoe UI', sans-serif;
  font-size: 16px;
  font-weight: 700;
  text-anchor: middle;
}

.dimension {
  fill: #24313a;
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 29px;
  font-weight: 700;
  text-anchor: middle;
}

.latent-dimension {
  fill: #2a9d8f;
  font-size: 38px;
}

.layer-subtitle {
  fill: #64748b;
  font-family: Inter, 'Segoe UI', sans-serif;
  font-size: 11px;
  text-anchor: middle;
}

.activation {
  fill: #20639b;
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 14px;
  font-weight: 700;
  text-anchor: middle;
}

.activation.linear {
  fill: #173f5f;
}

.section-label {
  opacity: 0;
  transition: opacity 0.35s ease;
}

.section-label.visible {
  opacity: 1;
}

.section-label line {
  stroke: #dce4e9;
  stroke-width: 1.5;
}

.section-label text {
  fill: #64748b;
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 0.12em;
  text-anchor: middle;
}

/* =========================
   TRAINING CONFIGURATION
========================= */

.training-config {
  flex: 0 0 auto;

  margin: 4px 35px 4px;

  min-height: 68px;

  display: flex;
  align-items: center;
  justify-content: center;

  background: #ffffff;
  border: 1px solid #dce4e9;
  border-radius: 9px;
}

.config-item {
  min-width: 130px;

  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 5px;
}

.config-label {
  color: #64748b;
  font-size: 10px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.05em;
}

.config-item strong {
  color: #173f5f;
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 16px;
}

.config-divider {
  width: 1px;
  height: 32px;
  background: #dce4e9;
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
   TRANSITIONS
========================= */

.config-reveal-enter-active {
  transition:
    opacity 0.4s ease,
    transform 0.4s ease;
}

.config-reveal-enter-from {
  opacity: 0;
  transform: translateY(10px);
}

/* =========================
   REDUCED MOTION
========================= */

@media (prefers-reduced-motion: reduce) {
  .layer-group,
  .connection-group,
  .section-label,
  .config-reveal-enter-active {
    transition: none;
  }
}
</style>
