<template>
  <div class="conclusion-slide">
    <div class="content-grid">
      <Transition name="fade-up">
        <section v-if="visibleCount >= 1" class="panel achieved-panel">
          <div class="panel-header">
            <div class="panel-icon achieved-icon">✓</div>
            <div>
              <div class="panel-kicker">ISSUE 1</div>
              <h2>What We Achieved</h2>
            </div>
          </div>
          <div class="items">
            <div class="result-item">
              <div class="item-marker"></div>
              <div>
                <h3>Multiple-Level Discretization</h3>
                <p>Infer regulatory networks using a multiple-level representation beyond Boolean states.</p>
              </div>
            </div>
            <div class="result-item">
              <div class="item-marker"></div>
              <div>
                <h3>Accurate Inference</h3>
                <p>Achieve higher structural and dynamic accuracy than the compared methods.</p>
              </div>
            </div>
            <div class="result-item">
              <div class="item-marker"></div>
              <div>
                <h3>Scalability to Dense Networks</h3>
                <p>Maintain reliable inference performance as network size and connectivity increase.</p>
              </div>
            </div>
            <div class="result-item">
              <div class="item-marker"></div>
              <div>
                <h3>Competitive Inference Time</h3>
                <p>Achieve inference times comparable to the evaluated methods.</p>
              </div>
            </div>
          </div>
        </section>
      </Transition>
      <Transition name="fade-up">
        <section v-if="visibleCount >= 2" class="panel limitation-panel">
          <div class="panel-header">
            <div class="panel-icon limitation-icon">△</div>
            <div>
              <div class="panel-kicker">FUTURE IMPROVEMENT</div>
              <h2>Limitations</h2>
            </div>
          </div>
          <div class="items">
            <div class="result-item">
              <div class="item-marker limitation-marker"></div>
              <div>
                <h3>Interaction Type and Direction</h3>
                <p>Rely on correlation coefficients to determine the type and direction of regulatory interactions.</p>
              </div>
            </div>
            <div class="result-item">
              <div class="item-marker limitation-marker"></div>
              <div>
                <h3>Greedy Feature Selection</h3>
                <p>MIFS and SWAP are greedy algorithms and may not guarantee a globally optimal feature subset.</p>
              </div>
            </div>
          </div>
        </section>
      </Transition>
    </div>
    <div v-if="visibleCount === 0" class="space-hint">
      <span>Press</span>
      <kbd>SPACE</kbd>
      <span>to reveal the achievements</span>
    </div>
    <div v-else-if="visibleCount === 1" class="space-hint">
      <span>Press</span>
      <kbd>SPACE</kbd>
      <span>to reveal the limitations</span>
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
  if (visibleCount.value < 2) {
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
.conclusion-slide {
  width: 100%;
  height: 100%;
  position: relative;
  box-sizing: border-box;
  display: flex;
  align-items: center;
  justify-content: center;
}
.content-grid {
  width: 100%;
  display: grid;
  grid-template-columns: 1.45fr 1fr;
  gap: 24px;
  align-items: stretch;
}
.panel {
  min-height: 390px;
  padding: 24px 26px;
  box-sizing: border-box;
  border: 1px solid #dce4e9;
  border-radius: 10px;
  background: #ffffff;
}
.achieved-panel {
  border-top: 4px solid #2a9d8f;
}
.limitation-panel {
  border-top: 4px solid #e9c46a;
}
.panel-header {
  display: flex;
  align-items: center;
  gap: 13px;
  padding-bottom: 18px;
  border-bottom: 1px solid #e8edf1;
}
.panel-icon {
  width: 34px;
  height: 34px;
  flex-shrink: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  font-size: 18px;
  font-weight: 700;
}
.achieved-icon {
  color: #2a9d8f;
  background: #e8f5f3;
}
.limitation-icon {
  color: #b58105;
  background: #fbf3d9;
}
.panel-kicker {
  margin-bottom: 3px;
  color: #64748b;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 9px;
  font-weight: 600;
  letter-spacing: 0.12em;
}
h2 {
  margin: 0;
  color: #173f5f;
  font-size: 24px;
  font-weight: 700;
  line-height: 1.15;
}
.items {
  display: flex;
  flex-direction: column;
  gap: 18px;
  padding-top: 20px;
}
.result-item {
  display: grid;
  grid-template-columns: 7px 1fr;
  gap: 12px;
  align-items: start;
}
.item-marker {
  width: 7px;
  height: 7px;
  margin-top: 7px;
  border-radius: 50%;
  background: #2a9d8f;
}
.limitation-marker {
  background: #e9c46a;
}
h3 {
  margin: 0 0 4px;
  color: #24313a;
  font-size: 14px;
  font-weight: 700;
  line-height: 1.25;
}
p {
  margin: 0;
  color: #64748b;
  font-size: 11.5px;
  line-height: 1.5;
}
.space-hint {
  position: absolute;
  left: 50%;
  bottom: 6px;
  transform: translateX(-50%);
  display: flex;
  align-items: center;
  gap: 7px;
  color: #94a3b8;
  font-size: 10px;
  white-space: nowrap;
}
kbd {
  min-width: 42px;
  height: 20px;
  padding: 0 8px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  box-sizing: border-box;
  border: 1px solid #cbd5e1;
  border-bottom-width: 2px;
  border-radius: 4px;
  background: #f8fafb;
  color: #475569;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 9px;
  font-weight: 600;
}
.fade-up-enter-active {
  transition: opacity 0.45s ease, transform 0.45s ease;
}
.fade-up-enter-from {
  opacity: 0;
  transform: translateY(18px);
}
@media (max-width: 800px) {
  .content-grid {
    grid-template-columns: 1fr;
  }
  .panel {
    min-height: auto;
  }
}
</style>