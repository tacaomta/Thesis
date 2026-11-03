<script setup>
import { ref, watch, onMounted, onBeforeUnmount } from 'vue'
import { useNav } from '@slidev/client'

const { currentPage } = useNav()
const isExporting =
  typeof window !== 'undefined' &&
  (
    window.location.pathname.startsWith('/export') ||
    new URLSearchParams(window.location.search).has('print') ||
    new URLSearchParams(window.location.search).has('range')
  )

watch(currentPage, () => {
  if(isExporting)
{
  visibleCount.value = 3
}
else{
  visibleCount.value = 0
}
})
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
  if(isExporting)
{
  visibleCount.value = 3
}
  window.addEventListener('keydown', handleKeydown, true)
})

onBeforeUnmount(() => {
  window.removeEventListener('keydown', handleKeydown, true)
})
</script>

<template>
  <div class="highlights-slide">

    <div class="advantages-grid">

      <!-- 01 -->
      <Transition name="fade-up">
        <section v-if="visibleCount >= 1" class="advantage-card card-1">
          <div class="card-top">
            <span class="card-number">01</span>
            <span class="card-tag">FLEXIBILITY</span>
          </div>

          <h2>Assumption-Free Formulation</h2>

          <div class="visual">
            <div class="visual-row">
              <span>Time-lag</span>
              <span class="cross">×</span>
              <span>Candidate restriction</span>
            </div>

            <div class="visual-result">
              No predefined assumptions
            </div>
          </div>
        </section>
      </Transition>

      <!-- 02 -->
      <Transition name="fade-up">
        <section v-if="visibleCount >= 2" class="advantage-card card-2">
          <div class="card-top">
            <span class="card-number">02</span>
            <span class="card-tag">JOINT ENCODING</span>
          </div>

          <h2>Joint Spatiotemporal Encoding</h2>

          <div class="visual">
            <div class="dual-input">
              <span>Temporal dynamics</span>
              <span class="plus">+</span>
              <span>Local topology</span>
            </div>

            <div class="visual-result">
              Unified representation
            </div>
          </div>
        </section>
      </Transition>

      <!-- 03 -->
      <Transition name="fade-up">
        <section v-if="visibleCount >= 3" class="advantage-card card-3">
          <div class="card-top">
            <span class="card-number">03</span>
            <span class="card-tag">SCALABILITY</span>
          </div>

          <h2>Scale-Invariant Feature Space</h2>

          <div class="visual">
            <div class="network-sizes">
              <span class="network small">10</span>
              <span class="network medium">50</span>
              <span class="network large">100</span>
              <span class="network xlarge">200</span>
            </div>

            <div class="visual-result">
              Shared feature space
            </div>
          </div>
        </section>
      </Transition>

      <!-- Connector 1 -> 2, overlapping both cards -->
      <Transition name="connector-pop">
        <div v-if="visibleCount >= 2" class="connector" style="left: 33.333%;">
          <svg viewBox="0 0 24 24" class="connector-icon" aria-hidden="true">
            <path d="M9 15 L15 9" />
            <path d="M11 6.5 L13 4.5 a3.2 3.2 0 0 1 4.5 4.5 L15.5 11" />
            <path d="M13 17.5 L11 19.5 a3.2 3.2 0 0 1 -4.5 -4.5 L8.5 13" />
          </svg>
        </div>
      </Transition>

      <!-- Connector 2 -> 3, overlapping both cards -->
      <Transition name="connector-pop">
        <div v-if="visibleCount >= 3" class="connector" style="left: 66.667%;">
          <svg viewBox="0 0 24 24" class="connector-icon" aria-hidden="true">
            <path d="M9 15 L15 9" />
            <path d="M11 6.5 L13 4.5 a3.2 3.2 0 0 1 4.5 4.5 L15.5 11" />
            <path d="M13 17.5 L11 19.5 a3.2 3.2 0 0 1 -4.5 -4.5 L8.5 13" />
          </svg>
        </div>
      </Transition>

    </div>


    <div v-if="visibleCount < 3" class="space-hint">
      Press SPACE to reveal the next advantage
    </div>

  </div>
</template>

<style scoped>
.highlights-slide {
  width: 100%;
  height: 100%;
  box-sizing: border-box;

  display: flex;
  flex-direction: column;

  padding: 8px 24px 4px;
}

/* =========================
   Cards
   ========================= */

.advantages-grid {
  flex: 1;
  min-height: 0;

  position: relative;

  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 6px;

  align-items: stretch;
}

:root {
  /* radius of the connector circle AND the matching edge notch
     carved into each card — change this one value to resize both */
  --connector-r: 19px;
}

.advantage-card {
  position: relative;

  display: flex;
  flex-direction: column;

  min-width: 0;

  padding: 21px 20px 19px;

  background: #ffffff;
  border: 1px solid #dce4e9;
  border-radius: 8px;
  border-top: 4px solid #2a9d8f;

  box-sizing: border-box;
  margin-top: 50px;

  overflow: hidden;
}

.card-1::after,
.card-2 .notch-left,
.card-2 .notch-right,
.card-3::after {
  content: '';
}

/* right edge notch: cards 1 and 2 */
.card-1::after,
.card-2::after {
  content: '';
  position: absolute;

  top: 50%;
  right: calc(var(--connector-r) * -1);

  width: calc(var(--connector-r) * 2);
  height: calc(var(--connector-r) * 2);

  transform: translateY(-50%);

  background: radial-gradient(
    circle,
    #f8fafb var(--connector-r),
    transparent calc(var(--connector-r) + 1px)
  );

  pointer-events: none;
  z-index: 3;
}

/* left edge notch: cards 2 and 3 */
.card-2::before,
.card-3::before {
  content: '';
  position: absolute;

  top: 50%;
  left: calc(var(--connector-r) * -1);

  width: calc(var(--connector-r) * 2);
  height: calc(var(--connector-r) * 2);

  transform: translateY(-50%);

  background: radial-gradient(
    circle,
    #f8fafb var(--connector-r),
    transparent calc(var(--connector-r) + 1px)
  );

  pointer-events: none;
  z-index: 3;
}

/* card-2 needs both a left and a right notch, and its top-accent
   bar (::before originally) is reused above for the left notch,
   so give card-2 its top accent via a dedicated element instead */
.card-2 {
  --dummy: 0; /* keep selector grouping simple */
}

/* =========================
   Connector circle — overlaps
   both neighboring cards by
   sitting exactly on the grid
   column boundary, vertically
   centered on the cards' own
   center line.
   ========================= */

.connector {
  position: absolute;

  /* left is set inline per-instance (33.333% / 66.667%) */
  top: calc(50% + 25px); /* 25px = half of the cards' 50px margin-top offset */

  width: calc(var(--connector-r) * 2);
  height: calc(var(--connector-r) * 2);

  transform: translate(-50%, -50%);

  display: flex;
  align-items: center;
  justify-content: center;

  border-radius: 50%;

  background: #eef7f5;
  border: 1.5px solid #bfe3db;

  box-shadow: 0 3px 8px rgba(42, 157, 143, 0.14);

  z-index: 10;
}

.connector-icon {
  width: 30px;
  height: 30px;

  fill: none;
  stroke: #2a7f73;
  stroke-width: 1.8;
  stroke-linecap: round;
  stroke-linejoin: round;
}

.connector-pop-enter-active {
  transition:
    opacity 0.3s ease 0.1s,
    transform 0.3s ease 0.1s;
}

.connector-pop-enter-from {
  opacity: 0;
  transform: translate(-50%, -50%) scale(0.4);
}

/* =========================
   Card top
   ========================= */

.card-top {
  display: flex;
  align-items: center;
  justify-content: space-between;

  margin-bottom: 17px;
}

.card-number {
  width: 34px;
  height: 34px;

  display: flex;
  align-items: center;
  justify-content: center;

  border-radius: 50%;

  background: #f0f5f8;
  color: #173f5f;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 11px;
  font-weight: 600;
}

.card-tag {
  color: #2a9d8f;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 9px;
  font-weight: 600;
  letter-spacing: 0.06em;
}

/* =========================
   Text
   ========================= */

.advantage-card h2 {
  margin: 0 0 10px;

  color: #173f5f;

  font-size: 18px;
  line-height: 1.3;
  font-weight: 650;
}

.advantage-card p {
  margin: 0;

  color: #64748b;

  font-size: 14px;
  line-height: 1.6;
}

.advantage-card sup {
  color: #20639b;

  font-size: 9px;
  font-weight: 600;

  vertical-align: super;
}

/* =========================
   Visual explanation
   ========================= */

.visual {
  margin-top: auto;
  padding-top: 10px;
}

.visual-row,
.dual-input {
  min-height: 45px;

  display: flex;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;
  gap: 7px;

  padding: 8px;

  background: #f8fafb;
  border: 1px solid #e5eaee;
  border-radius: 6px;

  color: #64748b;

  font-size: 10px;
  text-align: center;
}

.cross,
.plus {
  color: #94a3b8;
  font-size: 14px;
}

.visual-result {
  margin-top: 7px;

  padding: 8px;

  border-radius: 5px;

  background: #eef7f5;

  color: #2a7f73;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 10px;
  font-weight: 600;

  text-align: center;
}

/* =========================
   Network size visual
   ========================= */

.network-sizes {
  min-height: 45px;

  display: flex;
  align-items: center;
  justify-content: center;
  gap: 9px;

  padding: 8px;

  background: #f8fafb;
  border: 1px solid #e5eaee;
  border-radius: 6px;
}

.network {
  display: flex;
  align-items: center;
  justify-content: center;

  border-radius: 50%;

  border: 1px solid #20639b;

  color: #20639b;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 8px;
}

.network.small {
  width: 20px;
  height: 20px;
}

.network.medium {
  width: 26px;
  height: 26px;
}

.network.large {
  width: 32px;
  height: 32px;
}

.network.xlarge {
  width: 38px;
  height: 38px;
}

/* =========================
   Space hint
   ========================= */

.space-hint {
  flex-shrink: 0;

  height: 20px;

  display: flex;
  align-items: center;
  justify-content: center;

  margin-top: 6px;

  color: #94a3b8;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 10px;
  letter-spacing: 0.04em;
}

/* =========================
   Animation
   ========================= */

.fade-up-enter-active {
  transition:
    opacity 0.35s ease,
    transform 0.35s ease;
}

.fade-up-enter-from {
  opacity: 0;
  transform: translateY(12px);
}

/* =========================
   Responsive
   ========================= */

@media (max-width: 850px) {
  .advantages-grid {
    grid-template-columns: 1fr;
    overflow-y: auto;
  }

  .advantage-card::after,
  .advantage-card::before {
    display: none;
  }

  .connector {
    position: static;
    margin: 10px auto;
    transform: none;
  }

  .connector-pop-enter-from {
    transform: scale(0.4);
  }
}
</style>