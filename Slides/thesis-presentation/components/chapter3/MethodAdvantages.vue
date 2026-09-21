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

<template>
  <div class="highlights-slide">

    <div class="advantages-grid">

      <!-- 01 -->
      <Transition name="fade-up">
        <section v-if="visibleCount >= 1" class="advantage-card">
          <div class="card-top">
            <span class="card-number">01</span>
            <span class="card-tag">FLEXIBILITY</span>
          </div>

          <h2>Assumption-Free Formulation</h2>

          <p>
            Operates without predefined time-lag heuristics or restricted
            candidate regulator subsets.
          </p>

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
        <section v-if="visibleCount >= 2" class="advantage-card">
          <div class="card-top">
            <span class="card-number">02</span>
            <span class="card-tag">JOINT ENCODING</span>
          </div>

          <h2>Joint Spatiotemporal Encoding</h2>

          <p>
            Captures temporal expression dynamics and local regulatory
            topology simultaneously.
          </p>

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
        <section v-if="visibleCount >= 3" class="advantage-card">
          <div class="card-top">
            <span class="card-number">03</span>
            <span class="card-tag">SCALABILITY</span>
          </div>

          <h2>Scale-Invariant Feature Space</h2>

          <p>
            Enables cross-network data integration independent of overall
            network dimensions.
          </p>

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

  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 18px;

  align-items: stretch;
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

  box-sizing: border-box;
  margin-top: 50px;
}

.advantage-card::before {
  content: '';

  position: absolute;
  top: 0;
  left: 0;
  right: 0;

  height: 4px;

  background: #2a9d8f;

  border-radius: 8px 8px 0 0;
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
  margin: 0 0 12px;

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
  padding-top: 20px;
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
   Conclusion
   ========================= */

.highlight-conclusion {
  flex-shrink: 0;

  display: flex;
  align-items: center;
  gap: 10px;

  margin: 14px auto 4px;
  padding: 9px 16px;

  max-width: 900px;

  background: #f8fafb;
  border: 1px solid #dce4e9;
  border-radius: 6px;

  color: #475569;

  font-size: 13px;
  line-height: 1.45;
}

.highlight-conclusion strong {
  color: #173f5f;
  font-weight: 650;
}

.accent {
  width: 4px;
  align-self: stretch;
  flex-shrink: 0;

  border-radius: 2px;

  background: #2a9d8f;
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
}
</style>