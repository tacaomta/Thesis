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
                    No time-lag assumptions — pairwise encoding.
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
           04. CROSS-SCALE GENERALIZATION
           ===================================================== -->
        <Transition name="fade-up">
            <section v-if="visibleCount >= 2" class="condition-card">

                <div class="card-header">
                    <span class="step">02</span>
                    <span class="tag generalization">GENERALIZATION</span>
                </div>

                <h2>Cross-Scale Generalization</h2>

                <p>
                    Train small, infer large — strong performance.
                </p>

                <div class="transfer-visual">

                    <div class="transfer-row">
                        <div class="transfer-icon small-net">
                            <span class="transfer-node"></span>
                            <span class="transfer-node"></span>
                            <span class="transfer-node"></span>
                        </div>

                        <span class="transfer-arrow">→</span>

                        <div class="transfer-icon large-net">
                            <span class="transfer-node"></span>
                            <span class="transfer-node"></span>
                            <span class="transfer-node"></span>
                            <span class="transfer-node"></span>
                            <span class="transfer-node"></span>
                            <span class="transfer-node"></span>
                        </div>
                    </div>

                    <div class="transfer-caption">
                        <span class="transfer-tag train">train (N=10)</span>
                        <span class="transfer-sep">→</span>
                        <span class="transfer-tag infer">infer (N=100+)</span>
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
                    Flexible, efficient GRN inference.
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
        <!-- =====================================================
           04. CLASS IMBALANCE MITIGATION
           ===================================================== -->
        <Transition name="fade-up">
            <section v-if="visibleCount >= 4" class="condition-card">

                <div class="card-header">
                    <span class="step">04</span>
                    <span class="tag mitigation">MITIGATION</span>
                </div>

                <h2>Class Imbalance Mitigation</h2>

                <p>
                    Resolves sparsity via cross-scale augmentation.
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
        

    </div>

    <!-- =====================================================
         SPACE HINT
         ===================================================== -->
    <div v-if="visibleCount < 4" class="space-hint">
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

    if (visibleCount.value < 4) {
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
    grid-template-columns: repeat(4, 1fr);

    gap: 14px;
    margin-top: 60px;
}

/* =========================================================
   CARD
   ========================================================= */

.condition-card {
    min-width: 0;
    min-height: 0;

    padding: 15px 14px 13px;

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

    gap: 8px;
    margin-bottom: 11px;
}

.step {
    font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;

    font-size: 12px;
    font-weight: 600;

    color: #64748b;
}

.tag {
    font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;

    font-size: 9px;
    font-weight: 600;

    letter-spacing: 0.06em;

    padding: 4px 6px;

    border-radius: 4px;

    white-space: nowrap;
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

.generalization {
    color: #7a5af8;
    background: #f1eefe;
}

/* =========================================================
   TYPOGRAPHY
   ========================================================= */

.condition-card h2 {
    margin: 0 0 9px;

    color: #24313a;

    font-size: 14.5px;
    line-height: 1.25;

    font-weight: 650;
}

.condition-card p {
    margin: 0;

    color: #64748b;

    font-size: 11.5px;
    line-height: 1.5;
    font-weight: 600;
}

/* =========================================================
   01. PAIRWISE INTERACTION VISUAL
   ========================================================= */

.pair-visual {
    margin-top: auto;
    padding-top: 12px;

    display: flex;
    flex-direction: column;
    align-items: center;

    gap: 9px;
}

.pair-nodes {
    display: flex;
    align-items: center;

    gap: 7px;
}

.pair-node {
    width: 28px;
    height: 28px;

    border: 1.5px solid #20639b;
    border-radius: 50%;

    background: #f4f8fb;

    display: flex;
    align-items: center;
    justify-content: center;

    color: #173f5f;

    font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;

    font-size: 11px;
    font-weight: 600;
}

.pair-link {
    width: 22px;
    height: 1.5px;

    background: #20639b;
}

.pair-encode {
    display: flex;
    align-items: center;

    gap: 5px;

    color: #64748b;

    font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;

    font-size: 9px;
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
    padding-top: 12px;

    display: flex;
    flex-direction: column;
    align-items: center;

    gap: 9px;
}

.augment-scales {
    display: flex;
    align-items: center;

    gap: 5px;
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

    font-size: 8px;
    font-weight: 600;
}

.scale-box.tiny {
    width: 19px;
    height: 19px;
}

.scale-box.small {
    width: 24px;
    height: 24px;
}

.scale-box.mid {
    width: 29px;
    height: 29px;
}

.augment-arrow {
    color: #94a3b8;
    font-size: 13px;

    transform: rotate(90deg);
}

.augment-pool {
    display: grid;
    grid-template-columns: repeat(3, 1fr);

    gap: 4px;
}

.pool-dot {
    width: 8px;
    height: 8px;

    border-radius: 50%;

    background: #b6560c;
    opacity: 0.85;
}

/* =========================================================
   03. DEPLOYMENT VISUAL
   ========================================================= */

.deploy-visual {
    margin-top: auto;
    padding-top: 12px;

    display: flex;
    align-items: center;
    justify-content: center;

    gap: 16px;
}

.deploy-item {
    display: flex;
    flex-direction: column;
    align-items: center;

    gap: 7px;
}

.deploy-icon {
    width: 44px;
    height: 36px;

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
    width: 4px;
    height: 16px;

    border-radius: 2px;

    background: #2a9d8f;
}

.deploy-icon.flex span:nth-child(1) {
    height: 10px;
}

.deploy-icon.flex span:nth-child(2) {
    height: 19px;
}

.deploy-icon.flex span:nth-child(3) {
    height: 14px;
}

.deploy-icon.fast .bolt {
    font-size: 16px;
    color: #2a9d8f;
}

.deploy-label {
    color: #64748b;

    font-size: 9px;
    font-weight: 600;
}

/* =========================================================
   04. CROSS-SCALE TRANSFER VISUAL
   ========================================================= */

.transfer-visual {
    margin-top: auto;
    padding-top: 12px;

    display: flex;
    flex-direction: column;
    align-items: center;

    gap: 9px;
}

.transfer-row {
    display: flex;
    align-items: center;

    gap: 7px;
}

.transfer-icon {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-wrap: wrap;

    gap: 3px;

    padding: 6px;

    border-radius: 6px;

    box-sizing: border-box;
}

.transfer-icon.small-net {
    width: 34px;
    height: 34px;

    border: 1px solid #cdc3fb;
    background: #f1eefe;
}

.transfer-icon.large-net {
    width: 44px;
    height: 34px;

    border: 1.5px solid #7a5af8;
    background: #f1eefe;
}

.transfer-node {
    width: 5px;
    height: 5px;

    border-radius: 50%;

    background: #7a5af8;
}

.small-net .transfer-node {
    opacity: 0.7;
}

.transfer-arrow {
    color: #94a3b8;
    font-size: 13px;
}

.transfer-caption {
    display: flex;
    align-items: center;

    gap: 5px;

    font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
    font-size: 8.5px;
    font-weight: 600;
}

.transfer-tag {
    padding: 2px 5px;

    border-radius: 3px;
}

.transfer-tag.train {
    color: #64748b;
    background: #f1f5f8;
}

.transfer-tag.infer {
    color: #7a5af8;
    background: #f1eefe;
}

.transfer-sep {
    color: #94a3b8;
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

@media (max-width: 1100px) {

    .conditions-list {
        grid-template-columns: repeat(2, 1fr);
    }

}

@media (max-width: 600px) {

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