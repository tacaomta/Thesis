<script setup>
import { ref,watch, onMounted, onBeforeUnmount } from 'vue'
import { useNav } from '@slidev/client'

const { currentPage } = useNav()

const visibleCount = ref(0)

watch(currentPage, () => {
  visibleCount.value = 0
})
function handleKeydown(event) {
  if (event.code !== 'Space') return

  event.preventDefault()
  event.stopPropagation()

  if (visibleCount.value < 4) {
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
  <div class="research-gap-slide">

    <!-- Three limitations -->
    <div class="limitations-grid">

      <!-- 01 -->
      <Transition name="fade-up">
        <section v-if="visibleCount >= 1" class="gap-card">
          <div class="card-header">
            <span class="card-number">01</span>
            <h2>Separated Encoding</h2>
          </div>

          <p>
            Temporal expression dynamics and local regulatory structures
            are encoded separately or indirectly.
          </p>
        </section>
      </Transition>

      <!-- 02 -->
      <Transition name="fade-up">
        <section v-if="visibleCount >= 2" class="gap-card">
          <div class="card-header">
            <span class="card-number">02</span>
            <h2>Rigid Hyperparameter Assumptions</h2>
          </div>

          <p>
            Models depend heavily on fixed time delays, restricted
            candidate regulator sets, or specific kernel configurations.
          </p>
        </section>
      </Transition>

      <!-- 03 -->
      <Transition name="fade-up">
        <section v-if="visibleCount >= 3" class="gap-card">
          <div class="card-header">
            <span class="card-number">03</span>
            <h2>Severe Class Imbalance</h2>
          </div>

          <p>
            Increasing network scale significantly skews the ratio of
            positive regulatory interactions to non-interactions.
          </p>
        </section>
      </Transition>

    </div>

    <!-- Research gap -->
    <Transition name="fade-up">
      <section v-if="visibleCount >= 4" class="research-gap-box">
        <div class="gap-label">
          RESEARCH GAP
        </div>

        <div class="gap-statement">
          Existing frameworks lack a unified and generalizable
          representation of regulatory relationships from
          time-series expression data.
        </div>
      </section>
    </Transition>

    <!-- Space hint -->
    <div v-if="visibleCount < 4" class="space-hint">
      Press SPACE to reveal the next limitation
    </div>

  </div>
</template>

<style scoped>
.research-gap-slide {
  width: 100%;
  height: 100%;
  box-sizing: border-box;

  display: flex;
  flex-direction: column;

  padding: 10px 24px 4px;
}

/* =========================
   Limitations
   ========================= */

.limitations-grid {
  flex: 1;
  min-height: 0;

  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 18px;

  align-items: stretch;
  margin-top: 60px;
}

.gap-card {
  position: relative;

  display: flex;
  flex-direction: column;

  min-width: 0;

  padding: 24px 22px 22px;

  background: #ffffff;
  border: 1px solid #dce4e9;
  border-radius: 8px;

  box-sizing: border-box;
}

.gap-card::before {
  content: '';

  position: absolute;
  top: 0;
  left: 0;
  right: 0;

  height: 4px;

  background: #20639b;

  border-radius: 8px 8px 0 0;
}

/* =========================
   Card header
   ========================= */

.card-header {
  display: flex;
  align-items: center;
  gap: 13px;

  margin-bottom: 20px;
}

.card-number {
  width: 36px;
  height: 36px;

  flex-shrink: 0;

  display: flex;
  align-items: center;
  justify-content: center;

  border-radius: 50%;

  background: #f0f5f8;
  color: #173f5f;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 12px;
  font-weight: 600;
}

.card-header h2 {
  margin: 0;

  color: #173f5f;

  font-size: 19px;
  line-height: 1.25;
  font-weight: 650;
}

/* =========================
   Card text
   ========================= */

.gap-card p {
  margin: 0;

  color: #64748b;

  font-size: 15px;
  line-height: 1.65;
}

.gap-card sup {
  color: #20639b;

  font-size: 10px;
  font-weight: 600;

  vertical-align: super;
}

/* =========================
   Research gap
   ========================= */

.research-gap-box {
  flex-shrink: 0;

  display: flex;
  align-items: center;
  gap: 20px;

  margin: 18px auto 4px;
  padding: 14px 20px;

  width: min(920px, 100%);
  box-sizing: border-box;

  background: #f8fafb;
  border: 1px solid #dce4e9;
  border-left: 4px solid #2a9d8f;

  border-radius: 6px;
}

.gap-label {
  flex-shrink: 0;

  color: #2a9d8f;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.05em;
}

.gap-statement {
  color: #24313a;

  font-size: 15px;
  line-height: 1.45;
  font-weight: 500;
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
   Animations
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
  .limitations-grid {
    grid-template-columns: 1fr;
    overflow-y: auto;
  }

  .gap-card {
    min-height: 180px;
  }

  .research-gap-box {
    width: 100%;
  }
}
</style>
