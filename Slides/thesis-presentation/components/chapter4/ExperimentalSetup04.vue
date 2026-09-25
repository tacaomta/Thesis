<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

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
  <div class="setup-slide">

    <div class="setup-grid">

      <!-- =========================
           01 · GROUND TRUTH
      ========================== -->

      <Transition name="reveal">
        <section v-if="visibleCount >= 1" class="setup-card topology-card">

          <div class="card-header">
            <span class="number">01</span>
            <h2>Ground Truth Topologies</h2>
          </div>

          <svg
            class="topology-svg"
            viewBox="0 0 430 180"
            preserveAspectRatio="xMidYMid meet"
            aria-label="Twenty synthetic ground truth networks: ten with 50 genes and ten with 100 genes"
          >
            <!-- Network N=50 -->
            <g transform="translate(105, 88)">
              <line x1="0" y1="0" x2="-45" y2="-38" class="edge" />
              <line x1="0" y1="0" x2="48" y2="-42" class="edge" />
              <line x1="0" y1="0" x2="-55" y2="30" class="edge" />
              <line x1="0" y1="0" x2="58" y2="34" class="edge" />
              <line x1="-45" y1="-38" x2="-70" y2="-5" class="edge" />
              <line x1="48" y1="-42" x2="72" y2="-10" class="edge" />

              <circle cx="0" cy="0" r="13" class="hub" />
              <circle cx="-45" cy="-38" r="7" class="node" />
              <circle cx="48" cy="-42" r="7" class="node" />
              <circle cx="-55" cy="30" r="7" class="node" />
              <circle cx="58" cy="34" r="7" class="node" />
              <circle cx="-70" cy="-5" r="5" class="node" />
              <circle cx="72" cy="-10" r="5" class="node" />

              <text x="0" y="76" class="network-label">
                N = 50
              </text>
            </g>

            <!-- Network N=100 -->
            <g transform="translate(320, 88)">
              <line x1="0" y1="0" x2="-40" y2="-42" class="edge" />
              <line x1="0" y1="0" x2="44" y2="-40" class="edge" />
              <line x1="0" y1="0" x2="-53" y2="30" class="edge" />
              <line x1="0" y1="0" x2="57" y2="32" class="edge" />
              <line x1="-40" y1="-42" x2="-70" y2="-8" class="edge" />
              <line x1="44" y1="-40" x2="72" y2="-6" class="edge" />
              <line x1="-53" y1="30" x2="-70" y2="58" class="edge" />
              <line x1="57" y1="32" x2="75" y2="57" class="edge" />
              <line x1="-70" y1="-8" x2="-78" y2="28" class="edge" />

              <circle cx="0" cy="0" r="13" class="hub" />
              <circle cx="-40" cy="-42" r="7" class="node" />
              <circle cx="44" cy="-40" r="7" class="node" />
              <circle cx="-53" cy="30" r="7" class="node" />
              <circle cx="57" cy="32" r="7" class="node" />
              <circle cx="-70" cy="-8" r="5" class="node" />
              <circle cx="72" cy="-6" r="5" class="node" />
              <circle cx="-70" cy="58" r="5" class="node" />
              <circle cx="75" cy="57" r="5" class="node" />
              <circle cx="-78" cy="28" r="5" class="node" />

              <text x="0" y="76" class="network-label">
                N = 100
              </text>
            </g>
          </svg>

          <div class="topology-count">
            <div>
              <strong>20</strong>
              <span>distinct networks</span>
            </div>

            <div class="count-divider"></div>

            <div>
              <strong>10 + 10</strong>
              <span>networks per size</span>
            </div>
          </div>

          <div class="model-tag">
            Barabási–Albert <span>scale-free model</span>
          </div>

        </section>
      </Transition>

      <!-- =========================
           02 · TIME HORIZON
      ========================== -->

      <Transition name="reveal">
        <section v-if="visibleCount >= 2" class="setup-card">

          <div class="card-header">
            <span class="number">02</span>
            <h2>Time-Series Horizon</h2>
          </div>

          <div class="timeline-wrapper">

            <div class="timeline-value">
              <span class="symbol">T</span>
              <span class="equals">=</span>
              <strong>100</strong>
            </div>

            <div class="timeline">
              <div class="timeline-line"></div>

              <span class="tick start">1</span>
              <span class="tick mid">50</span>
              <span class="tick end">100</span>

              <div class="time-dot start-dot"></div>
              <div class="time-dot mid-dot"></div>
              <div class="time-dot end-dot"></div>
            </div>

            <div class="timeline-caption">
              Total trajectory length
            </div>

          </div>

          <!-- <div class="trajectory">
            <span class="trajectory-label">Observed trajectory</span>

            <div class="trajectory-points">
              <i v-for="i in 12" :key="i"></i>
            </div>

            <span class="trajectory-label">→</span>
          </div> -->

        </section>
      </Transition>

      <!-- =========================
           03 · OBSERVATION WINDOW
      ========================== -->

      <Transition name="reveal">
        <section v-if="visibleCount >= 3" class="setup-card observation-card">

          <div class="card-header">
            <span class="number">03</span>
            <h2>Observation Window</h2>
          </div>

          <div class="window-equation">
            <span>K</span>
            <span>=</span>
            <strong>10 → 90</strong>
          </div>

          <div class="window-scale">

            <div class="scale-line"></div>

            <div
              v-for="value in [10, 20, 30, 40, 50, 60, 70, 80, 90]"
              :key="value"
              class="scale-point"
            >
              <span class="point"></span>
              <label>{{ value }}</label>
            </div>

          </div>
<!-- 
          <div class="window-description">
            <span class="step-badge">ΔK = 10</span>
            <span>systematically varied</span>
          </div>

          <div class="window-highlight">
            <div class="bracket left"></div>
            <span>available observations</span>
            <div class="bracket right"></div>
          </div> -->

        </section>
      </Transition>

      <!-- =========================
           04 · DATA RESOLUTION
      ========================== -->

      <Transition name="reveal">
        <section v-if="visibleCount >= 4" class="setup-card resolution-card">

          <div class="card-header">
            <span class="number">04</span>
            <h2>Data Resolution</h2>
          </div>

          <div class="resolution-visual">

            <!-- Binary -->
            <div class="resolution-option binary">

              <div class="state-title">
                Binary
              </div>

              <div class="state-row">
                <div class="state state-low">0</div>
                <div class="state state-high">1</div>
              </div>

              <div class="state-caption">
                2 discrete states
              </div>

            </div>

            <div class="resolution-divider">
              <span>vs.</span>
            </div>

            <!-- Ternary -->
            <div class="resolution-option ternary">

              <div class="state-title">
                Ternary
              </div>

              <div class="state-row">
                <div class="state state-low">0</div>
                <div class="state state-mid">1</div>
                <div class="state state-high">2</div>
              </div>

              <div class="state-caption">
                3 discrete states
              </div>

            </div>

          </div>

          <div class="resolution-message">
            Compare learning under different
            <strong>discretization levels</strong>
          </div>

        </section>
      </Transition>

    </div>

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
.setup-slide {
  width: 100%;
  height: 100%;
  box-sizing: border-box;

  display: flex;
  flex-direction: column;
}

/* =========================
   GRID
========================= */

.setup-grid {
  flex: 1;
  min-height: 0;

  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  grid-template-rows: repeat(2, minmax(0, 1fr));

  gap: 13px;
}

/* =========================
   CARD
========================= */

.setup-card {
  min-width: 0;
  min-height: 0;

  padding: 16px 18px;
  box-sizing: border-box;

  display: flex;
  flex-direction: column;

  background: #ffffff;
  border: 1px solid #dce4e9;
  border-top: 4px solid #173f5f;
  border-radius: 10px;

  box-shadow: 0 4px 12px rgba(23, 63, 95, 0.05);
}

.topology-card {
  border-top-color: #20639b;
}

.observation-card {
  border-top-color: #2a9d8f;
}

.resolution-card {
  border-top-color: #e9c46a;
}

/* =========================
   HEADER
========================= */

.card-header {
  display: flex;
  align-items: baseline;
  gap: 7px;

  margin-bottom: 5px;
}
.card-content { gap: 6px; }

.number {
  flex: 0 0 auto;

  color: #2a9d8f;
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 12px;
  font-weight: 700;
  letter-spacing: 0.08em;
}

h2 {
  margin: 0;

  color: #173f5f;
  font-size: 18px;
  line-height: 1.2;
  font-weight: 700;
}

/* =========================
   TOPOLOGY
========================= */

.topology-svg {
  width: 100%;
  height: 125px;
  margin-top: 2px;
}

.edge {
  stroke: #b7c4cc;
  stroke-width: 1.5;
}

.node {
  fill: #ffffff;
  stroke: #20639b;
  stroke-width: 1.5;
}

.hub {
  fill: #2a9d8f;
  stroke: #173f5f;
  stroke-width: 2;
}

.network-label {
  fill: #173f5f;
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 12px;
  font-weight: 700;
  text-anchor: middle;
}

.topology-count {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 20px;

  margin-top: 2px;
}

.topology-count > div {
  display: flex;
  align-items: baseline;
  gap: 7px;
}

.topology-count strong {
  color: #20639b;
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 19px;
}

.topology-count span {
  color: #64748b;
  font-size: 10px;
}

.count-divider {
  width: 1px;
  height: 22px;
  background: #dce4e9;
}

.model-tag {
  margin-top: auto;
  padding-top: 7px;

  color: #173f5f;
  font-size: 11px;
  font-weight: 600;
  text-align: center;
}

.model-tag span {
  color: #64748b;
  font-weight: 400;
}

/* =========================
   TIME HORIZON
========================= */

.timeline-wrapper {
  flex: 1;

  display: flex;
  flex-direction: column;
  justify-content: center;
}

.timeline-value {
  display: flex;
  justify-content: center;
  align-items: baseline;
  gap: 8px;

  margin-bottom: 15px;
}

.timeline-value .symbol {
  color: #2a9d8f;
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 25px;
  font-style: italic;
  font-weight: 700;
}

.timeline-value .equals {
  color: #64748b;
  font-size: 18px;
}

.timeline-value strong {
  color: #173f5f;
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 30px;
}

.timeline {
  position: relative;
  height: 45px;
  margin: 0 30px;
}

.timeline-line {
  position: absolute;
  top: 21px;
  left: 0;
  right: 0;

  height: 3px;
  background: #dce4e9;
}

.timeline-line::after {
  content: '';
  position: absolute;
  top: -5px;
  right: 0;

  border-left: 10px solid #94a3b8;
  border-top: 6px solid transparent;
  border-bottom: 6px solid transparent;
}

.tick {
  position: absolute;
  top: 34px;

  color: #64748b;
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 10px;
}

.tick.start {
  left: 0;
}

.tick.mid {
  left: 50%;
  transform: translateX(-50%);
}

.tick.end {
  right: 0;
}

.time-dot {
  position: absolute;
  top: 15px;

  width: 14px;
  height: 14px;

  border-radius: 50%;
  background: #ffffff;
  border: 3px solid #20639b;
}

.start-dot {
  left: 0;
}

.mid-dot {
  left: 50%;
  transform: translateX(-50%);
}

.end-dot {
  right: 0;
  border-color: #2a9d8f;
}

.timeline-caption {
  margin-top: 13px;

  color: #64748b;
  font-size: 11px;
  text-align: center;
}

.trajectory {
  display: flex;
  align-items: center;
  gap: 9px;

  margin-top: auto;
  padding-top: 5px;
}

.trajectory-label {
  color: #64748b;
  font-size: 9px;
  white-space: nowrap;
}

.trajectory-points {
  flex: 1;

  display: flex;
  align-items: center;
  justify-content: space-between;
}

.trajectory-points i {
  width: 5px;
  height: 5px;

  border-radius: 50%;
  background: #20639b;
}

/* =========================
   OBSERVATION WINDOW
========================= */

.window-equation {
  display: flex;
  justify-content: center;
  align-items: baseline;
  gap: 9px;

  margin: 4px 0 13px;
}

.window-equation span:first-child {
  color: #2a9d8f;
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 25px;
  font-style: italic;
  font-weight: 700;
}

.window-equation span:nth-child(2) {
  color: #64748b;
}

.window-equation strong {
  color: #173f5f;
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 25px;
}

.window-scale {
  position: relative;

  display: grid;
  grid-template-columns: repeat(9, 1fr);

  margin: 5px 10px 0;
  padding-top: 17px;
}

.scale-line {
  position: absolute;
  top: 13px;
  left: 0;
  right: 0;

  height: 2px;
  background: #dce4e9;
}

.scale-point {
  position: relative;

  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 7px;

  z-index: 1;
}

.scale-point .point {
  width: 9px;
  height: 9px;

  border-radius: 50%;
  background: #ffffff;
  border: 2px solid #2a9d8f;
}

.scale-point label {
  color: #64748b;
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 9px;
}

.window-description {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 9px;

  margin-top: 15px;
}

.step-badge {
  padding: 4px 8px;

  background: rgba(42, 157, 143, 0.1);
  border-radius: 4px;

  color: #2a9d8f;
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 10px;
  font-weight: 700;
}

.window-description span:last-child {
  color: #64748b;
  font-size: 10px;
}

.window-highlight {
  margin-top: auto;

  display: flex;
  justify-content: center;
  align-items: center;
  gap: 9px;

  color: #64748b;
  font-size: 10px;
}

.bracket {
  width: 30px;
  height: 7px;

  border-top: 2px solid #2a9d8f;
}

.bracket.left {
  border-left: 2px solid #2a9d8f;
}

.bracket.right {
  border-right: 2px solid #2a9d8f;
}

/* =========================
   RESOLUTION
========================= */

.resolution-visual {
  flex: 1;

  display: flex;
  align-items: center;
  justify-content: center;

  gap: 25px;
}

.resolution-option {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 9px;
}

.state-title {
  color: #173f5f;
  font-size: 13px;
  font-weight: 700;
}

.state-row {
  display: flex;
  gap: 8px;
}

.state {
  width: 39px;
  height: 39px;

  display: flex;
  align-items: center;
  justify-content: center;

  border-radius: 7px;

  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 15px;
  font-weight: 700;
}

.state-low {
  background: #f8fafb;
  border: 1.5px solid #94a3b8;
  color: #64748b;
}

.state-mid {
  background: rgba(42, 157, 143, 0.1);
  border: 1.5px solid #2a9d8f;
  color: #2a9d8f;
}

.state-high {
  background: rgba(32, 99, 155, 0.1);
  border: 1.5px solid #20639b;
  color: #20639b;
}

.state-caption {
  color: #64748b;
  font-size: 9px;
}

.resolution-divider {
  color: #94a3b8;
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 11px;
}

.resolution-message {
  padding-top: 6px;

  color: #64748b;
  font-size: 10px;
  text-align: center;
}

.resolution-message strong {
  color: #173f5f;
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
   REVEAL
========================= */

.reveal-enter-active {
  transition:
    opacity 0.35s ease,
    transform 0.35s ease;
}

.reveal-enter-from {
  opacity: 0;
  transform: translateY(10px);
}

/* =========================
   RESPONSIVE
========================= */

@media (max-width: 850px) {
  .setup-grid {
    grid-template-columns: 1fr;
    grid-template-rows: auto;
    overflow-y: auto;
  }

  .setup-card {
    min-height: 260px;
  }
}

@media (prefers-reduced-motion: reduce) {
  .reveal-enter-active {
    transition: none;
  }
}
</style>