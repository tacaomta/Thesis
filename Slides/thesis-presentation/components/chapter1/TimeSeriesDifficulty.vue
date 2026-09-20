<template>
  <div class="difficulty-slide">
    <div class="difficulty-content">

      <div class="challenge-grid">

        <!-- Challenge 1 -->
        <div
          v-if="visibleCount >= 1"
          class="challenge-card"
          :class="{ 'card-enter': visibleCount === 1 }"
        >
          <div class="challenge-visual">
            <div class="challenge-number">01</div>

            <svg viewBox="0 0 72 72" aria-hidden="true">
              <circle cx="36" cy="36" r="25" class="icon-ring"/>
              <circle cx="27" cy="28" r="4" class="icon-node"/>
              <circle cx="46" cy="25" r="4" class="icon-node"/>
              <circle cx="22" cy="46" r="4" class="icon-node"/>
              <circle cx="43" cy="48" r="4" class="icon-node"/>

              <path d="M30 29 L42 26" class="icon-edge"/>
              <path d="M28 31 L23 43" class="icon-edge"/>
              <path d="M27 46 L39 48" class="icon-edge"/>
              <path d="M46 29 L44 44" class="icon-edge"/>
            </svg>
          </div>

          <div class="challenge-body">
            <h3>High dimensionality</h3>

            <p>
              Thousands of genes create a huge number of possible regulatory
              interactions compared with the available observations.
            </p>

            <div class="challenge-example">
              <strong>Example:</strong>
              10,000 genes × 50–100 time points
              → <span>O(N²)</span> possible interactions
            </div>
          </div>
        </div>


        <!-- Challenge 2 -->
        <div
          v-if="visibleCount >= 2"
          class="challenge-card"
          :class="{ 'card-enter': visibleCount === 2 }"
        >
          <div class="challenge-visual">
            <div class="challenge-number">02</div>

            <svg viewBox="0 0 72 72" aria-hidden="true">
              <line
                x1="15"
                y1="54"
                x2="60"
                y2="54"
                class="axis"
              />

              <line
                x1="15"
                y1="54"
                x2="15"
                y2="15"
                class="axis"
              />

              <circle cx="22" cy="43" r="3.5" class="data-point"/>
              <circle cx="34" cy="31" r="3.5" class="data-point"/>
              <circle cx="47" cy="40" r="3.5" class="data-point"/>
              <circle cx="58" cy="23" r="3.5" class="data-point"/>

              <path
                d="M22 43 L34 31 L47 40 L58 23"
                class="data-line"
              />
            </svg>
          </div>

          <div class="challenge-body">
            <h3>Limited observations</h3>

            <p>
              Time-series experiments often contain only a small number of
              time points and biological replicates.
            </p>

            <div class="challenge-example">
              <strong>Typical constraint:</strong>
              Few time points + few biological replicates
            </div>
          </div>
        </div>


        <!-- Challenge 3 -->
        <div
          v-if="visibleCount >= 3"
          class="challenge-card"
          :class="{ 'card-enter': visibleCount === 3 }"
        >
          <div class="challenge-visual">
            <div class="challenge-number">03</div>

            <svg viewBox="0 0 72 72" aria-hidden="true">
              <path
                d="M12 38
                   C18 20 25 55 32 36
                   S45 20 52 37
                   S62 50 64 29"
                class="signal"
              />

              <path
                d="M12 45
                   C20 33 26 51 34 42
                   S47 31 55 44
                   S61 39 64 35"
                class="noise"
              />
            </svg>
          </div>

          <div class="challenge-body">
            <h3>Noise &amp; biological variability</h3>

            <p>
              Observed expression combines regulatory signal with measurement
              noise and biological variation between samples.
            </p>

            <div class="challenge-example">
              <strong>Observed data:</strong>
              True signal + measurement noise + biological variation
            </div>
          </div>
        </div>


        <!-- Challenge 4 -->
        <div
          v-if="visibleCount >= 4"
          class="challenge-card"
          :class="{ 'card-enter': visibleCount === 4 }"
        >
          <div class="challenge-visual">
            <div class="challenge-number">04</div>

            <svg viewBox="0 0 72 72" aria-hidden="true">

              <defs>
                <marker
                  id="complex-arrow"
                  markerWidth="7"
                  markerHeight="7"
                  refX="6"
                  refY="3.5"
                  orient="auto"
                >
                  <path
                    d="M0 0 L7 3.5 L0 7 Z"
                    class="marker"
                  />
                </marker>
              </defs>

              <circle
                cx="19"
                cy="23"
                r="6"
                class="network-node"
              />

              <circle
                cx="51"
                cy="23"
                r="6"
                class="network-node"
              />

              <circle
                cx="51"
                cy="51"
                r="6"
                class="network-node"
              />

              <circle
                cx="19"
                cy="51"
                r="6"
                class="network-node"
              />

              <path
                d="M25 23 L45 23"
                class="network-edge"
                marker-end="url(#complex-arrow)"
              />

              <path
                d="M51 29 L51 45"
                class="network-edge"
                marker-end="url(#complex-arrow)"
              />

              <path
                d="M45 51 L25 51"
                class="network-edge"
                marker-end="url(#complex-arrow)"
              />

              <path
                d="M19 45 L19 29"
                class="network-edge"
                marker-end="url(#complex-arrow)"
              />

            </svg>
          </div>

          <div class="challenge-body">
            <h3>Complex dependencies</h3>

            <p>
              Regulatory systems involve nonlinear effects, feedback loops,
              indirect dependencies, and time-dependent interactions.
            </p>

            <div class="challenge-example">
              <strong>Challenge:</strong>
              Correlation does not directly reveal the underlying mechanism
            </div>
          </div>
        </div>


        <!-- Challenge 5 -->
        <div
          v-if="visibleCount >= 5"
          class="challenge-card challenge-wide"
          :class="{ 'card-enter': visibleCount === 5 }"
        >
          <div class="challenge-visual">
            <div class="challenge-number">05</div>

            <svg viewBox="0 0 72 72" aria-hidden="true">
              <circle
                cx="36"
                cy="36"
                r="25"
                class="icon-ring"
              />

              <path
                d="M23 36
                   C23 28 29 23 36 23
                   C43 23 49 28 49 36"
                class="uncertain"
              />

              <path
                d="M49 36
                   C49 44 43 49 36 49
                   C29 49 23 44 23 36"
                class="uncertain"
              />

              <text
                x="36"
                y="40"
                text-anchor="middle"
                class="question"
              >
                ?
              </text>
            </svg>
          </div>

          <div class="challenge-body">
            <h3>Underdetermined inference</h3>

            <p>
              With limited observations, different network structures can
              produce similar expression patterns, leaving multiple plausible
              regulatory explanations.
            </p>

            <div class="challenge-example">
              <strong>Implication:</strong>
              One observed dataset may support multiple plausible network structures
            </div>
          </div>
        </div>

      </div>


      <!-- Bottom message -->
      <div
        v-if="visibleCount >= 6"
        class="bottom-message"
        :class="{ 'message-enter': visibleCount === 6 }"
      >
        <span class="message-mark"></span>

        <span>
          The challenge is not only to model the dynamics —
          <strong>
            it is to recover reliable regulatory relationships from limited,
            noisy observations.
          </strong>
        </span>
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

  if (visibleCount.value < 6) {
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
.difficulty-slide {
  width: 100%;
  height: 100%;
  min-width: 0;
  min-height: 0;
  overflow: hidden;
  box-sizing: border-box;
  background: #f8fafb;
  color: #24313a;
  font-family: 'Inter', 'Segoe UI', sans-serif;
}

.difficulty-content {
  width: 100%;
  height: 100%;
  min-width: 0;
  min-height: 0;
  display: flex;
  flex-direction: column;
  overflow: hidden;
  box-sizing: border-box;
}

.intro {
  flex: 0 0 auto;
  margin: 0 0 7px;
  padding: 0;
}

.intro p {
  margin: 0;
  max-width: 900px;
  color: #64748b;
  font-size: 10px;
  line-height: 1.3;
}

/* ================================
   CHALLENGE GRID
   ================================ */

.challenge-grid {
  flex: 0 0 auto;
  width: 100%;
  min-width: 0;
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  grid-auto-rows: minmax(78px, auto);
  gap: 7px;
  overflow: hidden;
  box-sizing: border-box;
}

/* ================================
   CARD
   ================================ */

.challenge-card {
  min-width: 0;
  min-height: 78px;
  display: grid;
  grid-template-columns: 76px minmax(0, 1fr);
  align-items: center;
  gap: 10px;
  padding: 8px 11px;
  border: 1px solid #dce4e9;
  border-radius: 8px;
  background: #ffffff;
  box-sizing: border-box;
  overflow: hidden;
}

.challenge-wide {
  grid-column: 1 / -1;
}

/* ================================
   LEFT VISUAL
   ================================ */

.challenge-visual {
  height: 100%;
  min-height: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  border-right: 1px solid #edf1f3;
  padding-right: 8px;
  box-sizing: border-box;
}

.challenge-number {
  margin-bottom: 2px;
  color: #2a9d8f;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 8px;
  font-weight: 700;
  letter-spacing: 0.04em;
}

.challenge-visual svg {
  width: 48px;
  height: 48px;
  display: block;
  overflow: visible;
}

/* ================================
   RIGHT BODY
   ================================ */

.challenge-body {
  min-width: 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
  overflow: hidden;
}

.challenge-body h3 {
  margin: 0 0 3px;
  color: #173f5f;
  font-size: 12px;
  font-weight: 700;
  line-height: 1.15;
}

.challenge-body p {
  margin: 0;
  color: #526273;
  font-size: 8.8px;
  line-height: 1.3;
}

.challenge-example {
  margin-top: 4px;
  padding: 4px 7px;
  border-radius: 5px;
  background: #f5f8fa;
  color: #64748b;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 7.7px;
  line-height: 1.25;
  box-sizing: border-box;
}

.challenge-example strong {
  color: #526273;
}

.challenge-example span {
  color: #20639b;
  font-weight: 700;
}

/* ================================
   ICONS
   ================================ */

.icon-ring {
  fill: none;
  stroke: #dce4e9;
  stroke-width: 2;
}

.icon-node {
  fill: #ffffff;
  stroke: #20639b;
  stroke-width: 2;
}

.icon-edge {
  fill: none;
  stroke: #20639b;
  stroke-width: 1.7;
  stroke-linecap: round;
}

.axis {
  stroke: #94a3b8;
  stroke-width: 1.5;
}

.data-point {
  fill: #2a9d8f;
}

.data-line {
  fill: none;
  stroke: #20639b;
  stroke-width: 1.8;
  stroke-linecap: round;
  stroke-linejoin: round;
}

.signal {
  fill: none;
  stroke: #20639b;
  stroke-width: 2;
  stroke-linecap: round;
}

.noise {
  fill: none;
  stroke: #e76f51;
  stroke-width: 1.4;
  stroke-linecap: round;
  opacity: 0.75;
}

.marker {
  fill: #20639b;
}

.network-node {
  fill: #ffffff;
  stroke: #20639b;
  stroke-width: 1.8;
}

.network-edge {
  fill: none;
  stroke: #20639b;
  stroke-width: 1.5;
  stroke-linecap: round;
}

.uncertain {
  fill: none;
  stroke: #94a3b8;
  stroke-width: 2;
  stroke-dasharray: 3 3;
}

.question {
  fill: #e76f51;
  font-size: 16px;
  font-weight: 700;
}

/* ================================
   BOTTOM MESSAGE
   ================================ */

.bottom-message {
    flex: 0 0 auto;
    min-width: 0;
    display: flex;
    align-items: center;
    gap: 12px;
    margin-top: 9px;
    padding: 8px 16px;
    border: 1px solid #dce4e9;
    border-radius: 8px;
    background: #ffffff;
    box-sizing: border-box;
    color: #526273;
    font-size: 10px;
    line-height: 1.35;
}

.message-mark {
    flex: 0 0 auto;
    width: 4px;
    height: 25px;
    border-radius: 4px;
    background: #e9c46a;
}

.bottom-message strong {
    color: #173f5f;
}
.card-enter {
  animation: challenge-enter 0.45s ease-out both;
}

.message-enter {
  animation: message-enter 0.5s ease-out both;
}

@keyframes challenge-enter {
  from {
    opacity: 0;
    transform: translateY(12px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes message-enter {
  from {
    opacity: 0;
    transform: translateY(8px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }
}

</style>