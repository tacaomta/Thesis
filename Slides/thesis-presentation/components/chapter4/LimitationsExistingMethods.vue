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

  // Prevent Slidev from advancing to the next slide
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
  <div class="limitations-slide">

    <!-- Limitations -->
    <div class="limitations-flow">

      <!-- 01 -->
      <Transition name="reveal">
        <div
          v-if="visibleCount >= 1"
          class="limitation-item"
        >
          <div class="number">01</div>

          <div class="content">
            <div class="label">
              GENERATIVE ADVERSARIAL NETWORKS
            </div>

            <h3>
              Fails with limited training samples
            </h3>

            <div class="keyword-chips">
              <span class="chip">large-scale training samples</span>
              <span class="chip">training instability</span>
              <span class="chip warn">mode collapse</span>
            </div>
          </div>

          <div class="visual">
            <svg viewBox="0 0 120 90" class="visual-svg">
              <!-- data distribution: many real modes -->
              <circle cx="20" cy="22" r="5" class="mode-real" />
              <circle cx="40" cy="14" r="5" class="mode-real" />
              <circle cx="60" cy="24" r="5" class="mode-real" />
              <circle cx="80" cy="15" r="5" class="mode-real" />
              <circle cx="100" cy="23" r="5" class="mode-real" />

              <text x="60" y="40" text-anchor="middle" class="visual-caption">real data modes</text>

              <path d="M60 46 L60 56" class="visual-arrow" marker-end="url(#ganArrow)" />
              <defs>
                <marker id="ganArrow" markerWidth="8" markerHeight="8" refX="4" refY="7" orient="auto">
                  <path d="M0 0 L8 0 L4 7 Z" class="arrow-head" />
                </marker>
              </defs>

              <!-- collapsed single mode -->
              <circle cx="60" cy="72" r="9" class="mode-collapsed" />

              <text x="60" y="88" text-anchor="middle" class="visual-caption collapsed-label">collapsed to one mode</text>
            </svg>
          </div>
        </div>
      </Transition>

      <!-- 02 -->
      <Transition name="reveal">
        <div
          v-if="visibleCount >= 2"
          class="limitation-item"
        >
          <div class="number">02</div>

          <div class="content">
            <div class="label">
              ARTIFICIAL GENE NETWORK SIMULATORS
            </div>

            <h3>
              Cannot capture non-linear dynamics
            </h3>

            <div class="keyword-chips">
              <span class="chip">rigid assumptions</span>
              <span class="chip warn">non-linear temporal dynamics</span>
              <span class="chip">restricted real-world samples</span>
            </div>
          </div>

          <div class="visual">
            <svg viewBox="0 0 120 90" class="visual-svg">
              <!-- rigid linear assumption -->
              <line x1="12" y1="55" x2="108" y2="25" class="agn-linear" />
              <text x="60" y="18" text-anchor="middle" class="visual-caption">assumed (linear)</text>

              <!-- actual non-linear trajectory -->
              <path d="M12 68 C 35 30, 55 85, 78 40 C 90 20, 98 55, 108 45" class="agn-nonlinear" />
              <text x="60" y="88" text-anchor="middle" class="visual-caption nonlinear-label">actual (non-linear)</text>

              <!-- gap markers -->
              <circle cx="55" cy="47" r="2.6" class="agn-gap-dot" />
              <circle cx="78" cy="40" r="2.6" class="agn-gap-dot" />
            </svg>
          </div>
        </div>
      </Transition>

      <!-- 03 -->
      <Transition name="reveal">
        <div
          v-if="visibleCount >= 3"
          class="limitation-item unmet"
        >
          <div class="number">03</div>

          <div class="content">
            <div class="label">
              UNMET NEED
            </div>

            <h3>
              No robust architecture exists yet
            </h3>

            <div class="keyword-chips">
              <span class="chip unmet-chip">temporal gene expression profiles</span>
              <span class="chip unmet-chip">very limited observation steps</span>
            </div>
          </div>

          <div class="visual">
            <svg viewBox="0 0 120 90" class="visual-svg">
              <!-- few observed points -->
              <circle cx="20" cy="55" r="5" class="unmet-observed" />
              <circle cx="42" cy="48" r="5" class="unmet-observed" />

              <text x="31" y="75" text-anchor="middle" class="visual-caption">observed</text>

              <!-- question-mark gap for the rest of trajectory -->
              <path d="M42 48 C 60 40, 75 60, 92 38 C 98 30, 104 34, 110 28" class="unmet-missing" />

              <circle cx="78" cy="32" r="12" class="unmet-flag" />
              <text x="78" y="37" text-anchor="middle" class="unmet-question">?</text>

              <text x="88" y="75" text-anchor="middle" class="visual-caption missing-label">missing</text>
            </svg>
          </div>
        </div>
      </Transition>

    </div>

    <!-- Bottom message -->
    <!-- <Transition name="reveal">
      <div
        v-if="visibleCount >= 3"
        class="bottom-message"
      >
        <span class="arrow">→</span>

        <span>
          This motivates a generative framework designed
          specifically for limited temporal observations.
        </span>
      </div>
    </Transition> -->

  </div>
</template>

<style scoped>
.limitations-slide {
  width: 100%;
  height: 100%;

  box-sizing: border-box;

  display: flex;
  flex-direction: column;

  color: #24313a;
}

/* ============================================================
   Main limitation flow
   ============================================================ */

.limitations-flow {
  flex: 1;

  display: flex;
  flex-direction: column;
  justify-content: center;

  gap: 8px;

  min-height: 0;
}

/* ============================================================
   Limitation item
   ============================================================ */

.limitation-item {
  display: grid;

  grid-template-columns: 54px minmax(0, 1fr) 128px;

  align-items: center;

  column-gap: 16px;

  padding: 13px 18px 13px 14px;

  background: #ffffff;

  border: 1px solid #dce4e9;

  border-radius: 9px;

  box-sizing: border-box;
}

/* ============================================================
   Number
   ============================================================ */

.number {
  width: 38px;
  height: 38px;

  display: flex;
  align-items: center;
  justify-content: center;

  border-radius: 50%;

  background: #f0f5f7;

  border: 1px solid #cbd8df;

  color: #173f5f;

  font-family:
    'IBM Plex Mono',
    'JetBrains Mono',
    monospace;

  font-size: 12px;
  font-weight: 700;
}

/* ============================================================
   Content
   ============================================================ */

.content {
  min-width: 0;
}

.label {
  margin-bottom: 4px;

  font-family:
    'IBM Plex Mono',
    'JetBrains Mono',
    monospace;

  font-size: 9px;
  font-weight: 700;

  letter-spacing: 0.12em;

  color: #20639b;
}

.limitation-item h3 {
  margin: 0 0 8px;

  font-size: 16px;
  line-height: 1.25;

  font-weight: 700;

  color: #173f5f;
}

/* ============================================================
   Keyword chips (replaces the old <p> sentence)
   ============================================================ */

.keyword-chips {
  display: flex;
  flex-wrap: wrap;

  gap: 6px;
}

.chip {
  padding: 4px 9px;

  border-radius: 999px;

  background: #f1f5f8;
  border: 1px solid #dce4e9;

  color: #475569;

  font-size: 10.5px;
  font-weight: 600;

  white-space: nowrap;
}

.chip.warn {
  background: #fdf1e7;
  border-color: #f0d0ab;
  color: #b6560c;
}

.chip.unmet-chip {
  background: #edf8f6;
  border-color: #b8dcd7;
  color: #247f76;
}

/* ============================================================
   Visual column
   ============================================================ */

.visual {
  display: flex;
  align-items: center;
  justify-content: center;

  width: 128px;
  height: 90px;

  flex-shrink: 0;
}

.visual-svg {
  width: 100%;
  height: 100%;
}

.visual-caption {
  fill: #94a3b8;

  font-family: 'Inter', 'Segoe UI', sans-serif;
  font-size: 7.5px;
}

.visual-arrow {
  stroke: #cbd5e1;
  stroke-width: 1.6;
}

.arrow-head {
  fill: #cbd5e1;
}

/* --- 01: GAN mode collapse --- */

.mode-real {
  fill: #eef5fa;
  stroke: #20639b;
  stroke-width: 1.4;
}

.mode-collapsed {
  fill: #fdf1e7;
  stroke: #e76f51;
  stroke-width: 1.8;
}

.collapsed-label {
  fill: #b6560c;
  font-weight: 600;
}

/* --- 02: AGN rigid vs non-linear --- */

.agn-linear {
  stroke: #cbd5e1;
  stroke-width: 1.8;
  stroke-dasharray: 4 3;
}

.agn-nonlinear {
  fill: none;
  stroke: #20639b;
  stroke-width: 2;
  stroke-linecap: round;
}

.agn-gap-dot {
  fill: #e76f51;
}

.nonlinear-label {
  fill: #20639b;
  font-weight: 600;
}

/* --- 03: unmet need --- */

.unmet-observed {
  fill: #edf8f6;
  stroke: #2a9d8f;
  stroke-width: 1.6;
}

.unmet-missing {
  fill: none;
  stroke: #cbd5e1;
  stroke-width: 1.8;
  stroke-dasharray: 3 4;
}

.unmet-flag {
  fill: #fdf1e7;
  stroke: #e9c46a;
  stroke-width: 1.6;
}

.unmet-question {
  fill: #b5860c;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 11px;
  font-weight: 700;
}

.missing-label {
  fill: #b5860c;
  font-weight: 600;
}

/* ============================================================
   Unmet need
   ============================================================ */

.limitation-item.unmet {
  border-color: #b8dcd7;

  background: #f8fbfb;
}

.limitation-item.unmet .number {
  background: #e7f4f2;

  border-color: #a9d4ce;

  color: #247f76;
}

.limitation-item.unmet .label {
  color: #2a9d8f;
}

.limitation-item.unmet h3 {
  color: #173f5f;
}

/* ============================================================
   Bottom message
   ============================================================ */

.bottom-message {
  display: flex;
  align-items: center;

  gap: 3px;

  margin-top: 0px;

  padding: 10px 14px;

  border-top: 1px solid #dce4e9;

  font-size: 11px;
  line-height: 1.4;

  color: #64748b;
}

.bottom-message .arrow {
  font-size: 17px;
  font-weight: 700;

  color: #2a9d8f;
}

/* ============================================================
   Reveal animation
   ============================================================ */

.reveal-enter-active {
  transition:
    opacity 0.3s ease,
    transform 0.3s ease;
}

.reveal-enter-from {
  opacity: 0;

  transform: translateY(10px);
}

.reveal-enter-to {
  opacity: 1;

  transform: translateY(0);
}

/* ============================================================
   Reduced motion
   ============================================================ */

@media (prefers-reduced-motion: reduce) {
  .reveal-enter-active {
    transition: none;
  }
}

/* ============================================================
   Responsive
   ============================================================ */

@media (max-width: 900px) {
  .limitation-item {
    grid-template-columns: 40px minmax(0, 1fr);
  }

  .visual {
    display: none;
  }
}
</style>