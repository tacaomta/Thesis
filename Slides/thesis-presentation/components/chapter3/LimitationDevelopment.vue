<template>
<div class="conditions-slide">

    <div class="conditions-list">

        <!-- =====================================================
           01. TEMPORAL ALIGNMENT CONDITION
           ===================================================== -->
        <Transition name="fade-up">
            <section v-if="visibleCount >= 1" class="condition-card">

                <div class="card-header">
                    <span class="step">01</span>
                    <span class="tag alignment">ALIGNMENT</span>
                </div>

                <h2>Temporal Alignment Condition</h2>

                <p>
                    Test time-series length
                    <span class="formula">T<sub>test</sub></span>
                    must equal or exceed training profile length
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
            <section v-if="visibleCount >= 2" class="condition-card">

                <div class="card-header">
                    <span class="step">02</span>
                    <span class="tag handling">HANDLING</span>
                </div>

                <h2>Short-Profile Handling</h2>

                <p>
                    Requires temporal extension techniques when evaluating
                    shorter time series.
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
            <section v-if="visibleCount >= 3" class="condition-card">

                <div class="card-header">
                    <span class="step">03</span>
                    <span class="tag stability">STABILITY</span>
                </div>

                <h2>Cross-Regime Stability</h2>

                <p>
                    Operates stably across both discrete and continuous
                    gene expression data regimes.
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
import { ref, onMounted, onBeforeUnmount } from 'vue'

const visibleCount = ref(0)

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

    padding: 12px 20px 0;

    position: relative;
}

/* =========================================================
   LIST — HORIZONTAL, LEFT TO RIGHT
   ========================================================= */

.conditions-list {
    flex: 1;
    min-height: 0;

    display: grid;
    grid-template-columns: repeat(3, 1fr);

    gap: 16px;
    margin-top: 60px;
}

/* =========================================================
   CARD
   ========================================================= */

.condition-card {
    min-width: 0;
    min-height: 0;

    padding: 16px 16px 14px;

    border: 1px solid #dce4e9;
    border-radius: 8px;

    background: #ffffff;

    display: flex;
    flex-direction: column;

    box-sizing: border-box;
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

    .space-hint {
        display: none;
    }

}
</style>