<template>
<div class="conditions-slide">

    <div class="conditions-list">

        <!-- =====================================================
           01. UNIFIED TASK REFORMULATION
           ===================================================== -->
        <Transition name="fade-up">
            <section v-if="visibleCount >= 1" class="condition-card">

                <div class="card-header">
                    <span class="step">01</span>
                    <span class="tag reformulation">REFORMULATION</span>
                </div>

                <h2>Unified Task Reformulation</h2>

                <p>
                    Eliminates heuristic time-lag assumptions via
                    pairwise interaction encoding.
                </p>

                <div class="pair-visual">

                    <div class="pair-nodes">
                        <div class="pair-node">A</div>
                        <div class="pair-link"></div>
                        <div class="pair-node">B</div>
                    </div>

                    <div class="pair-encode">
                        <span>[ A, B ]</span>
                        <span class="pair-arrow">→</span>
                        <span class="pair-label">interaction</span>
                    </div>

                </div>

            </section>
        </Transition>

        <!-- =====================================================
           02. CLASS IMBALANCE MITIGATION
           ===================================================== -->
        <Transition name="fade-up">
            <section v-if="visibleCount >= 2" class="condition-card">

                <div class="card-header">
                    <span class="step">02</span>
                    <span class="tag mitigation">MITIGATION</span>
                </div>

                <h2>Class Imbalance Mitigation</h2>

                <p>
                    Resolves data sparsity through cross-scale
                    small-network data augmentation.
                </p>

                <div class="augment-visual">

                    <div class="augment-scales">
                        <div class="scale-box tiny">10</div>
                        <div class="scale-box small">50</div>
                        <div class="scale-box mid">100</div>
                    </div>

                    <span class="augment-arrow">→</span>

                    <div class="augment-pool">
                        <span class="pool-dot"></span>
                        <span class="pool-dot"></span>
                        <span class="pool-dot"></span>
                        <span class="pool-dot"></span>
                        <span class="pool-dot"></span>
                        <span class="pool-dot"></span>
                    </div>

                </div>

            </section>
        </Transition>

        <!-- =====================================================
           03. SCALABLE BIOLOGICAL DEPLOYMENT
           ===================================================== -->
        <Transition name="fade-up">
            <section v-if="visibleCount >= 3" class="condition-card">

                <div class="card-header">
                    <span class="step">03</span>
                    <span class="tag deployment">DEPLOYMENT</span>
                </div>

                <h2>Scalable Biological Deployment</h2>

                <p>
                    Provides a highly flexible, computationally efficient
                    solution for time-series GRN inference.
                </p>

                <div class="deploy-visual">

                    <div class="deploy-item">
                        <div class="deploy-icon flex">
                            <span></span>
                            <span></span>
                            <span></span>
                        </div>
                        <span class="deploy-label">Flexible</span>
                    </div>

                    <div class="deploy-item">
                        <div class="deploy-icon fast">
                            <span class="bolt">⚡</span>
                        </div>
                        <span class="deploy-label">Efficient</span>
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
        {{ visibleCount === 0 ? 'the first point' : 'the next point' }}
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

.reformulation {
    color: #20639b;
    background: #eef5fa;
}

.mitigation {
    color: #b6560c;
    background: #fdf1e7;
}

.deployment {
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

/* =========================================================
   01. PAIRWISE INTERACTION VISUAL
   ========================================================= */

.pair-visual {
    margin-top: auto;
    padding-top: 14px;

    display: flex;
    flex-direction: column;
    align-items: center;

    gap: 10px;
}

.pair-nodes {
    display: flex;
    align-items: center;

    gap: 8px;
}

.pair-node {
    width: 32px;
    height: 32px;

    border: 1.5px solid #20639b;
    border-radius: 50%;

    background: #f4f8fb;

    display: flex;
    align-items: center;
    justify-content: center;

    color: #173f5f;

    font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;

    font-size: 12px;
    font-weight: 600;
}

.pair-link {
    width: 26px;
    height: 1.5px;

    background: #20639b;
}

.pair-encode {
    display: flex;
    align-items: center;

    gap: 6px;

    color: #64748b;

    font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;

    font-size: 10px;
}

.pair-encode span:first-child {
    color: #173f5f;
    font-weight: 600;
}

.pair-arrow {
    color: #94a3b8;
}

.pair-label {
    color: #20639b;
    font-weight: 600;
}

/* =========================================================
   02. AUGMENTATION VISUAL
   ========================================================= */

.augment-visual {
    margin-top: auto;
    padding-top: 14px;

    display: flex;
    flex-direction: column;
    align-items: center;

    gap: 10px;
}

.augment-scales {
    display: flex;
    align-items: center;

    gap: 6px;
}

.scale-box {
    display: flex;
    align-items: center;
    justify-content: center;

    border: 1.5px solid #b6560c;
    border-radius: 4px;

    background: #fdf1e7;

    color: #8a4409;

    font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;

    font-size: 9px;
    font-weight: 600;
}

.scale-box.tiny {
    width: 22px;
    height: 22px;
}

.scale-box.small {
    width: 28px;
    height: 28px;
}

.scale-box.mid {
    width: 34px;
    height: 34px;
}

.augment-arrow {
    color: #94a3b8;
    font-size: 14px;

    transform: rotate(90deg);
}

.augment-pool {
    display: grid;
    grid-template-columns: repeat(3, 1fr);

    gap: 5px;
}

.pool-dot {
    width: 9px;
    height: 9px;

    border-radius: 50%;

    background: #b6560c;
    opacity: 0.85;
}

/* =========================================================
   03. DEPLOYMENT VISUAL
   ========================================================= */

.deploy-visual {
    margin-top: auto;
    padding-top: 14px;

    display: flex;
    align-items: center;
    justify-content: center;

    gap: 20px;
}

.deploy-item {
    display: flex;
    flex-direction: column;
    align-items: center;

    gap: 8px;
}

.deploy-icon {
    width: 50px;
    height: 40px;

    display: flex;
    align-items: center;
    justify-content: center;

    border-radius: 6px;

    border: 1px solid #cfe3df;
    background: #edf8f6;
}

.deploy-icon.flex {
    gap: 4px;
}

.deploy-icon.flex span {
    width: 5px;
    height: 18px;

    border-radius: 2px;

    background: #2a9d8f;
}

.deploy-icon.flex span:nth-child(1) {
    height: 12px;
}

.deploy-icon.flex span:nth-child(2) {
    height: 22px;
}

.deploy-icon.flex span:nth-child(3) {
    height: 16px;
}

.deploy-icon.fast .bolt {
    font-size: 18px;
    color: #2a9d8f;
}

.deploy-label {
    color: #64748b;

    font-size: 10px;
    font-weight: 600;
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