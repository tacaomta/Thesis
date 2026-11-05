<template>
<div class="conditions-slide">

    <div class="conditions-list">

        <!-- =====================================================
           01. TEMPORAL ALIGNMENT CONDITION
           ===================================================== -->
        <Transition name="fade-up">
            <section v-if="visibleCount >= 1" class="condition-card card-1">

                <div class="card-header">
                    <span class="step">01</span>
                    <span class="tag alignment">ALIGNMENT</span>
                </div>

                <h2>Temporal Alignment Condition</h2>

                <p>
                    <span class="formula">T<sub>test</sub></span>
                    must equal or exceed
                    <span class="formula">T<sub>train</sub></span>.
                </p>

                <div class="alignment-visual">

                    <div class="timeline-row">
                        <span class="timeline-label">Training</span>
                        <div class="timeline-track">
                            <div class="timeline-bar train-bar"></div>
                        </div>
                        <span class="timeline-value">T<sub>train</sub></span>
                    </div>

                    <div class="timeline-row">
                        <span class="timeline-label">Testing</span>
                        <div class="timeline-track">
                            <div class="timeline-bar test-bar"></div>
                        </div>
                        <span class="timeline-value">T<sub>test</sub> ≥ T<sub>train</sub></span>
                    </div>

                </div>

            </section>
        </Transition>

        <!-- =====================================================
           02. SHORT-PROFILE HANDLING
           ===================================================== -->
        <Transition name="fade-up">
            <section v-if="visibleCount >= 2" class="condition-card card-2">

                <div class="card-header">
                    <span class="step">02</span>
                    <span class="tag handling">HANDLING</span>
                </div>

                <h2>Short-Profile Handling</h2>

                <p>
                    Requires temporal extension techniques
                </p>

                <div class="extension-visual">

                    <div class="ext-block short">
                        <span>Short profile</span>
                    </div>

                    <span class="ext-arrow">→</span>

                    <div class="ext-block extended">
                        <span>Extended profile</span>
                    </div>

                </div>

            </section>
        </Transition>

        <!-- =====================================================
           03. CROSS-REGIME STABILITY
           ===================================================== -->
        <Transition name="fade-up">
            <section v-if="visibleCount >= 3" class="condition-card card-3">

                <div class="card-header">
                    <span class="step">03</span>
                    <span class="tag stability">STABILITY</span>
                </div>

                <h2>Cross-Regime Stability</h2>

                <p>
                    Operates both discrete and continuous
                    gene expression data
                </p>

                <div class="regime-visual">

                    <div class="regime-item">
                        <div class="regime-icon discrete">
                            <span class="regime-dot"></span>
                            <span class="regime-dot"></span>
                            <span class="regime-dot"></span>
                        </div>
                        <span class="regime-label">Discrete</span>
                    </div>

                    <div class="regime-divider"></div>

                    <div class="regime-item">
                        <div class="regime-icon continuous">
                            <svg viewBox="0 0 60 24" class="regime-wave">
                                <path d="M 2 18 C 12 4, 22 4, 30 12 C 38 20, 48 20, 58 6" />
                            </svg>
                        </div>
                        <span class="regime-label">Continuous</span>
                    </div>

                </div>

            </section>
        </Transition>

        <!-- Connector 1 -> 2, overlapping both cards -->
        <Transition name="connector-pop">
            <div v-if="visibleCount >= 2" class="connector" style="left: 33.333%;">
                <svg viewBox="0 0 24 24" class="connector-icon" aria-hidden="true">
                    <!-- <rect x="4" y="4" width="16" height="16" rx="4" /> -->
                    <path d="M8 12.5 L10.8 15.3 L16 9" />
                </svg>
            </div>
        </Transition>

        <!-- Connector 2 -> 3, overlapping both cards -->
        <Transition name="connector-pop">
            <div v-if="visibleCount >= 3" class="connector" style="left: 66.667%;">
                <svg viewBox="0 0 24 24" class="connector-icon" aria-hidden="true">
                    <!-- <rect x="4" y="4" width="16" height="16" rx="4" /> -->
                    <path d="M8 12.5 L10.8 15.3 L16 9" />
                </svg>
            </div>
        </Transition>

    </div>

    <!-- =====================================================
         SPACE HINT
         ===================================================== -->
    <div v-if="visibleCount < 3" class="space-hint">
        Press SPACE to reveal
        {{ visibleCount === 0 ? 'the first condition' : 'the next condition' }}
    </div>

</div>
</template>

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
const visibleCount = ref(0)
watch(currentPage, () => {
  if (isExporting) {
    visibleCount.value = 3
  }
  else
  {
    visibleCount.value = 0
  }
})
/* =========================================================
   SPACE NAVIGATION
   ========================================================= */

function handleKeydown(event) {
    if (event.code !== 'Space') return

    event.preventDefault()
    event.stopPropagation()

    if (visibleCount.value < 3) {
        visibleCount.value += 1
    }
}

/* =========================================================
   LIFECYCLE
   ========================================================= */

onMounted(() => {
    if(isExporting){
        visibleCount.value = 3
    }
    window.addEventListener('keydown', handleKeydown, true)
})

onBeforeUnmount(() => {
    window.removeEventListener('keydown', handleKeydown, true)
})
</script>

<style scoped>
/* =========================================================
   ROOT
   ========================================================= */

.conditions-slide {
    width: 100%;
    height: 100%;
    box-sizing: border-box;

    display: flex;
    flex-direction: column;

    padding: 12px 10px 0;

    position: relative;
}

/* =========================================================
   LIST — HORIZONTAL, LEFT TO RIGHT
   ========================================================= */

.conditions-list {
    flex: 1;
    min-height: 0;

    position: relative;

    display: grid;
    grid-template-columns: repeat(3, 1fr);

    gap: 6px;
    margin-top: 30px;
}

/* =========================================================
   CARD
   ========================================================= */

:root {
    /* radius of the connector circle AND the matching edge
       notch carved into each card's touching edges */
    --cond-connector-r: 18px;
}

.condition-card {
    position: relative;

    min-width: 0;
    min-height: 0;

    padding: 16px 16px 14px;

    border: 1px solid #dce4e9;
    border-radius: 8px;

    background: #ffffff;

    display: flex;
    flex-direction: column;

    box-sizing: border-box;

    overflow: hidden;
}

/* right-edge notch: cards 1 and 2 */
.card-1::after,
.card-2::after {
    content: '';
    position: absolute;

    top: 50%;
    right: calc(var(--cond-connector-r) * -1);

    width: calc(var(--cond-connector-r) * 2);
    height: calc(var(--cond-connector-r) * 2);

    transform: translateY(-50%);

    background: radial-gradient(
        circle,
        #f8fafb var(--cond-connector-r),
        transparent calc(var(--cond-connector-r) + 1px)
    );

    pointer-events: none;
    z-index: 2;
}

/* left-edge notch: cards 2 and 3 */
.card-2::before,
.card-3::before {
    content: '';
    position: absolute;

    top: 50%;
    left: calc(var(--cond-connector-r) * -1);

    width: calc(var(--cond-connector-r) * 2);
    height: calc(var(--cond-connector-r) * 2);

    transform: translateY(-50%);

    background: radial-gradient(
        circle,
        #f8fafb var(--cond-connector-r),
        transparent calc(var(--cond-connector-r) + 1px)
    );

    pointer-events: none;
    z-index: 2;
}

/* =========================================================
   CONNECTOR — "requirement" icon overlapping both cards,
   centered on the shared column boundary and on the cards'
   vertical center (cards sit at margin-top 60px via the
   list's own margin-top, so 50% is already their true center)
   ========================================================= */

.connector {
    position: absolute;

    top: 50%;

    width: calc(var(--cond-connector-r) * 2);
    height: calc(var(--cond-connector-r) * 2);

    transform: translate(-50%, -50%);

    display: flex;
    align-items: center;
    justify-content: center;

    border-radius: 50%;

    background: #eef5fa;
    border: 1.5px solid #bcd8ec;

    box-shadow: 0 3px 8px rgba(32, 99, 155, 0.14);

    z-index: 10;
}

.connector-icon {
    width: 32px;
    height: 32px;

    fill: none;
    stroke: #20639b;
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

/* =========================================================
   CARD HEADER
   ========================================================= */

.card-header {
    display: flex;
    align-items: center;

    gap: 9px;
    margin-bottom: 12px;
}

.step {
    font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;

    font-size: 12px;
    font-weight: 600;

    color: #64748b;
}

.tag {
    font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;

    font-size: 10px;
    font-weight: 600;

    letter-spacing: 0.08em;

    padding: 4px 7px;

    border-radius: 4px;
}

.alignment {
    color: #20639b;
    background: #eef5fa;
}

.handling {
    color: #b6560c;
    background: #fdf1e7;
}

.stability {
    color: #2a9d8f;
    background: #edf8f6;
}

/* =========================================================
   TYPOGRAPHY
   ========================================================= */

.condition-card h2 {
    margin: 0 0 10px;

    color: #24313a;

    font-size: 16px;
    line-height: 1.25;

    font-weight: 650;
}

.condition-card p {
    margin: 0;

    color: #64748b;

    font-size: 12.5px;
    line-height: 1.55;
}

.formula {
    font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;

    color: #173f5f;

    font-size: 12px;
    font-weight: 600;

    white-space: nowrap;
}

.formula sub {
    font-size: 9px;
}

/* =========================================================
   01. ALIGNMENT VISUAL
   ========================================================= */

.alignment-visual {
    margin-top: auto;
    padding-top: 14px;

    display: flex;
    flex-direction: column;

    gap: 10px;
}

.timeline-row {
    display: flex;
    align-items: center;

    gap: 8px;
}

.timeline-label {
    flex-shrink: 0;
    width: 46px;

    color: #64748b;

    font-size: 10px;
    font-weight: 600;
}

.timeline-track {
    flex: 1;
    min-width: 0;

    height: 14px;

    background: #f4f8fb;
    border: 1px solid #dce4e9;
    border-radius: 4px;

    overflow: hidden;
}

.timeline-bar {
    height: 100%;
    border-radius: 3px;
}

.train-bar {
    width: 55%;
    background: #20639b;
}

.test-bar {
    width: 85%;
    background: #7ab6dd;
}

.timeline-value {
    flex-shrink: 0;

    text-align: right;

    color: #173f5f;

    font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;

    font-size: 9px;
    font-weight: 600;

    white-space: nowrap;
}

/* =========================================================
   02. EXTENSION VISUAL
   ========================================================= */

.extension-visual {
    margin-top: auto;
    padding-top: 14px;

    display: flex;
    flex-direction: column;
    align-items: center;

    gap: 10px;
}

.ext-block {
    width: 100%;

    padding: 10px 8px;

    border-radius: 6px;

    font-size: 11px;
    font-weight: 600;

    text-align: center;

    box-sizing: border-box;
}

.ext-block.short {
    color: #b6560c;
    background: #fdf1e7;
    border: 1px solid #f0d0ab;
}

.ext-block.extended {
    color: #20639b;
    background: #eef5fa;
    border: 1px solid #bcd8ec;
}

.ext-arrow {
    color: #94a3b8;
    font-size: 16px;
    transform: rotate(90deg);
}

/* =========================================================
   03. REGIME VISUAL
   ========================================================= */

.regime-visual {
    margin-top: auto;
    padding-top: 14px;

    display: flex;
    align-items: center;
    justify-content: center;

    gap: 16px;
}

.regime-item {
    display: flex;
    flex-direction: column;
    align-items: center;

    gap: 8px;
}

.regime-icon {
    width: 58px;
    height: 38px;

    display: flex;
    align-items: center;
    justify-content: center;
    gap: 6px;

    border-radius: 6px;

    border: 1px solid #cfe3df;
    background: #edf8f6;
}

.regime-dot {
    width: 7px;
    height: 7px;

    border-radius: 2px;

    background: #2a9d8f;
}

.regime-wave {
    width: 46px;
    height: 20px;
}

.regime-wave path {
    fill: none;
    stroke: #2a9d8f;
    stroke-width: 2;
    stroke-linecap: round;
}

.regime-label {
    color: #64748b;

    font-size: 10px;
    font-weight: 600;
}

.regime-divider {
    width: 1px;
    height: 34px;

    background: #dce4e9;
}

/* =========================================================
   SPACE HINT
   ========================================================= */

.space-hint {
    position: absolute;

    right: 4px;
    bottom: -2px;

    color: #94a3b8;

    font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;

    font-size: 10px;

    letter-spacing: 0.02em;
}

/* =========================================================
   ANIMATIONS
   ========================================================= */

.fade-up-enter-active {
    transition:
        opacity 0.35s ease,
        transform 0.35s ease;
}

.fade-up-enter-from {
    opacity: 0;
    transform: translateY(10px);
}

/* =========================================================
   RESPONSIVE
   ========================================================= */

@media (max-width: 900px) {

    .conditions-list {
        grid-template-columns: 1fr;

        overflow-y: auto;
    }

    .condition-card {
        min-height: 220px;
    }

    .condition-card::after,
    .condition-card::before {
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

    .space-hint {
        display: none;
    }

}
</style>