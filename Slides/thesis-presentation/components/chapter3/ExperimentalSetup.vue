<template>
<div class="experimental-slide">

    <div class="setup-grid">

        <!-- =====================================================
           01. SYNTHETIC TOPOLOGICAL DATASETS
           ===================================================== -->
        <Transition name="fade-up">
            <section v-if="visibleCount >= 1" class="setup-card">

                <div class="card-header">
                    <span class="step">01</span>
                    <span class="tag synthetic">SYNTHETIC DATA</span>
                </div>

                <h2>Synthetic Topological Datasets</h2>

                <p>
                    Barabási–Albert (BA) scale-free networks across
                    <span class="formula">|V| ∈ {10, 50, 100}</span>.
                </p>

                <!-- Network sizes -->
                <div class="network-scale">
                    <div class="network-item">
                        <div class="network-circle small">
                            <span>10</span>
                        </div>
                        <span>Genes</span>
                    </div>

                    <div class="network-item">
                        <div class="network-circle medium">
                            <span>50</span>
                        </div>
                        <span>Genes</span>
                    </div>

                    <div class="network-item">
                        <div class="network-circle large">
                            <span>100</span>
                        </div>
                        <span>Genes</span>
                    </div>
                </div>

                <!-- Dataset summary -->
                <div class="dataset-summary">
                    <div class="summary-row">
                        <span class="summary-label">Training</span>
                        <span class="summary-value">
                            20,000 / 2,000 / 2,000
                        </span>
                    </div>

                    <div class="summary-row">
                        <span class="summary-label">Validation</span>
                        <span class="summary-value">
                            2,000 / 400 / 400
                        </span>
                    </div>

                    <div class="summary-row">
                        <span class="summary-label">Testing</span>
                        <span class="summary-value">
                            2,000 / 400 / 400
                        </span>
                    </div>

                    <div class="summary-note">
                        <span class="note-dot"></span>
                        Each network: 1 time-series and 50 time points
                    </div>
                </div>

                <button type="button" class="detail-button" @click="openDetail('synthetic')">
                    <span>VIEW DETAIL</span>
                    <span class="arrow">↗</span>
                </button>

            </section>
        </Transition>

        <!-- =====================================================
           02. BIOLOGICAL BENCHMARK DATASETS
           ===================================================== -->
        <Transition name="fade-up">
            <section v-if="visibleCount >= 2" class="setup-card">

                <div class="card-header">
                    <span class="step">02</span>
                    <span class="tag biological">BIOLOGICAL DATA</span>
                </div>

                <h2>Biological Benchmark Datasets</h2>

                <p>
                    Simulated <em>Escherichia coli</em> networks generated via
                    GeneNetWeaver (GNW).
                </p>

                <!-- Biological network visual -->
                <div class="network-scale2">
                    <div class="network-item2">
                        <div class="network-circle2 small">
                            <span>10</span>
                        </div>
                        <span>Genes</span>
                    </div>

                    <div class="network-item2">
                        <div class="network-circle2 medium">
                            <span>50</span>
                        </div>
                        <span>Genes</span>
                    </div>

                    <div class="network-item2">
                        <div class="network-circle2 large">
                            <span>100</span>
                        </div>
                        <span>Genes</span>
                    </div>
                </div>

                <!-- Dataset summary -->
                <div class="dataset-summary">

                    <div class="summary-row">
                        <span class="summary-label">Training</span>
                        <span class="summary-value">
                            200 / 20 / 20
                        </span>
                    </div>

                    <div class="summary-row">
                        <span class="summary-label">Validation</span>
                        <span class="summary-value">
                            20 / 4 / 4
                        </span>
                    </div>

                    <div class="summary-row">
                        <span class="summary-label">Testing</span>
                        <span class="summary-value">
                            10 / 4 / 4
                        </span>
                    </div>

                    <div class="summary-note">
                        <span class="note-dot biological-dot"></span>
                        Each network: 100 time-series and 50 time points
                    </div>

                </div>

                <button type="button" class="detail-button biological-button" @click="openDetail('ecoli')">
                    <span>VIEW DETAIL</span>
                    <span class="arrow">↗</span>
                </button>

            </section>
        </Transition>

        <!-- =====================================================
           03. EVALUATION METRIC
           ===================================================== -->

        <Transition name="fade-up">
            <section v-if="visibleCount >= 3" class="setup-card">
                <div class="card-header">
                    <span class="step">03</span>
                    <span class="tag metric">EVALUATION</span>
                </div>

                <h2>Evaluation Metric</h2>

                <p>
                    Area Under the Precision-Recall Curve (AUPR) selected due to
                    extreme sparsity in biological networks.
                </p>

                <div class="metric-visual">

                    <!-- Y-axis -->
                    <div class="axis y-axis"></div>

                    <!-- X-axis -->
                    <div class="axis x-axis"></div>

                    <svg viewBox="0 0 240 120" class="pr-curve" aria-label="Precision-recall curve">

                        <!-- Horizontal guide lines -->
                        <line x1="20" y1="18" x2="215" y2="18" class="guide" />

                        <line x1="20" y1="62" x2="215" y2="62" class="guide" />

                        <line x1="20" y1="105" x2="215" y2="105" class="guide" />

                        <!-- Baseline -->
                        <path d="M 20 105 C 65 101, 105 98, 145 99 C 175 100, 195 102, 215 105" class="baseline" />

                        <!-- Precision–Recall curve
             Start: Recall = 0, Precision = 1
             End:   Recall = 1, Precision ≈ 0 -->
                        <path d="M 20 18 C 38 18, 52 21, 68 27 C 86 34, 101 44, 117 55 C 135 68, 151 79, 168 88 C 185 97, 201 102, 215 105" class="curve" />

                        <!-- Start point: Precision = 1 -->
                        <circle cx="20" cy="18" r="3" class="curve-point" />

                        <!-- End point: Recall = 1 -->
                        <circle cx="215" cy="105" r="3" class="curve-point" />

                    </svg>

                    <!-- Axis labels -->
                    <span class="axis-label precision">
                        Precision
                    </span>

                    <span class="axis-label recall">
                        Recall
                    </span>

                    <span class="axis-value y-top">1.0</span>
                    <span class="axis-value y-bottom">0</span>

                    <span class="axis-value x-left"></span>
                    <span class="axis-value x-right">1.0</span>

                    <span class="aupr-label">
                        AUPR
                    </span>

                </div>

                <div class="metric-note">
                    <span class="note-dot metric-dot"></span>
                    Robust to highly imbalanced positive and negative classes
                </div>
            </section>
        </Transition>

    </div>

    <!-- =====================================================
         SPACE HINT
         ===================================================== -->
    <div v-if="visibleCount < 3" class="space-hint">
        Press SPACE to reveal
        {{ visibleCount < 3
        ? 'the next experimental component'
        : 'the experimental summary'
      }}
    </div>

    <!-- =====================================================
         DETAIL MODAL
         ===================================================== -->
    <Transition name="modal-fade">
        <div v-if="detailType" class="detail-overlay" @click.self="closeDetail">

            <div class="detail-modal">

                <div class="modal-header">

                    <div>
                        <span class="modal-eyebrow">
                            EXPERIMENTAL SETUP
                        </span>

                        <h3>
                            {{
                  detailType === 'synthetic'
                    ? 'Synthetic Topological Dataset'
                    : 'E. coli Benchmark Dataset'
                }}
                        </h3>
                    </div>

                    <button type="button" class="close-button" aria-label="Close detail" @click="closeDetail">
                        ×
                    </button>

                </div>

                <div class="modal-content">

                    <!-- Synthetic statistic image -->
                    <img v-if="detailType === 'synthetic'" src="/images/synthetic_dataset_statistics.png" alt="Synthetic topological dataset statistics" class="detail-image" />

                    <!-- E. coli statistic image -->
                    <img v-else src="/images/ecoli_dataset_statistics.png" alt="E. coli benchmark dataset statistics" class="detail-image" />

                </div>

                <div class="modal-footer">

                    <span>
                        Click outside or press ESC to close
                    </span>

                </div>

            </div>

        </div>
    </Transition>

</div>
</template>

<script setup>
import {
    ref,
    onMounted,
    onBeforeUnmount
} from 'vue'

const visibleCount = ref(0)
const detailType = ref(null)

/* =========================================================
   SPACE NAVIGATION
   ========================================================= */

function handleKeydown(event) {
    /* Close modal with ESC */
    if (event.code === 'Escape' && detailType.value) {
        event.preventDefault()
        closeDetail()
        return
    }

    /* Do not advance slide content while modal is open */
    if (detailType.value) return

    if (event.code !== 'Space') return

    event.preventDefault()
    event.stopPropagation()

    if (visibleCount.value < 4) {
        visibleCount.value += 1
    }
}

/* =========================================================
   DETAIL MODAL
   ========================================================= */

function openDetail(type) {
    detailType.value = type
}

function closeDetail() {
    detailType.value = null
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

.experimental-slide {
    width: 100%;
    height: 100%;
    box-sizing: border-box;

    display: flex;
    flex-direction: column;

    padding: 8px 20px 0;

    position: relative;
}

/* =========================================================
   MAIN GRID
   ========================================================= */

.setup-grid {
    flex: 1;
    min-height: 0;

    display: grid;
    grid-template-columns: repeat(3, 1fr);

    gap: 18px;
}

/* =========================================================
   CARD
   ========================================================= */

.setup-card {
    min-width: 0;
    min-height: 0;

    padding: 15px 15px 14px;

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
    margin-bottom: 17px;
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

.synthetic {
    color: #20639b;
    background: #eef5fa;
}

.biological {
    color: #2a9d8f;
    background: #edf8f6;
}

.metric {
    color: #8a6a00;
    background: #fff8df;
}

/* =========================================================
   TYPOGRAPHY
   ========================================================= */

.setup-card h2 {
    margin: 0 0 10px;

    color: #24313a;

    font-size: 18px;
    line-height: 1.25;

    font-weight: 650;
}

.setup-card p {
    margin: 0;

    color: #64748b;

    font-size: 12.5px;
    line-height: 1.55;
}

.formula {
    font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;

    color: #173f5f;

    font-size: 11.5px;

    white-space: nowrap;
}

/* =========================================================
   NETWORK SIZE VISUAL
   ========================================================= */

.network-scale,
.network-scale2 {
    min-height: 120px;

    display: flex;
    align-items: center;
    justify-content: space-around;

    gap: 8px;

    margin-top: 8px;
}

.network-item {
    display: flex;
    flex-direction: column;
    align-items: center;

    gap: 5px;

    color: #64748b;
    font-size: 10px;
}

.network-circle {
    border: 1.5px solid #20639b;
    border-radius: 50%;

    display: flex;
    align-items: center;
    justify-content: center;

    color: #173f5f;
    background: #f4f8fb;

    font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;

    font-size: 11px;
    font-weight: 600;
}

.network-item2 {
    display: flex;
    flex-direction: column;
    align-items: center;

    gap: 5px;

    color: #64748b;
    font-size: 10px;
}

.network-circle2 {
    border: 1.5px solid #2a9d8f;
    border-radius: 50%;

    display: flex;
    align-items: center;
    justify-content: center;

    color: #173f5f;
    background: #f4f8fb;

    font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;

    font-size: 11px;
    font-weight: 600;
}

.network-circle.small {
    width: 35px;
    height: 35px;
}

.network-circle.medium {
    width: 55px;
    height: 55px;
}

.network-circle.large {
    width: 75px;
    height: 75px;
}

.network-circle2.small {
    width: 35px;
    height: 35px;
}

.network-circle2.medium {
    width: 55px;
    height: 55px;
}

.network-circle2.large {
    width: 75px;
    height: 75px;
}

/* =========================================================
   DATASET SUMMARY
   ========================================================= */

.dataset-summary {
    margin-top: 5px;

    padding: 9px 10px;

    border-top: 1px solid #edf1f3;

    display: flex;
    flex-direction: column;

    gap: 5px;
}

.summary-row {
    display: flex;
    align-items: center;
    justify-content: space-between;

    gap: 10px;
}

.summary-label {
    color: #64748b;
    font-size: 10.5px;
}

.summary-value {
    color: #24313a;

    font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;

    font-size: 10.5px;
    font-weight: 600;

    white-space: nowrap;
}

.summary-note {
    display: flex;
    align-items: center;

    gap: 6px;

    margin-top: 2px;

    color: #64748b;

    font-size: 10px;
}

.note-dot {
    width: 6px;
    height: 6px;

    flex-shrink: 0;

    border-radius: 50%;

    background: #20639b;
}

.biological-dot {
    background: #2a9d8f;
}

.metric-dot {
    background: #e9c46a;
}

/* =========================================================
   VIEW DETAIL BUTTON
   ========================================================= */

.detail-button {
    align-self: flex-end;

    display: inline-flex;
    align-items: center;
    gap: 7px;

    margin-top: 8px;

    padding: 6px 9px;

    border: 1px solid #dce4e9;
    border-radius: 4px;

    background: #ffffff;

    color: #20639b;

    font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;

    font-size: 9px;
    font-weight: 600;

    letter-spacing: 0.05em;

    cursor: pointer;

    transition:
        background 0.2s ease,
        border-color 0.2s ease,
        transform 0.2s ease;
}

.detail-button:hover {
    background: #f4f8fb;
    border-color: #b9cad6;
    transform: translateY(-1px);
}

.biological-button {
    color: #2a9d8f;
}

.arrow {
    font-size: 12px;
    line-height: 1;
}

/* =========================================================
   BIOLOGICAL VISUAL
   ========================================================= */

.biological-visual {
    min-height: 120px;

    display: flex;
    align-items: center;
    justify-content: center;

    gap: 7px;

    margin-top: 8px;
}

.gene-node {
    width: 46px;
    height: 46px;

    border: 1.5px solid #2a9d8f;
    border-radius: 50%;

    background: #f0faf8;

    color: #236f66;

    display: flex;
    align-items: center;
    justify-content: center;

    text-align: center;

    font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;

    font-size: 9px;
    line-height: 1.2;
}

.gene-node.central {
    width: 58px;
    height: 58px;

    background: #eaf7f5;

    font-weight: 600;
}

.gene-link {
    width: 23px;
    height: 1.5px;

    background: #8abdb7;

    position: relative;
}

.gene-link::after {
    content: '';

    position: absolute;

    right: 0;
    top: -3px;

    width: 6px;
    height: 6px;

    border-top: 1.5px solid #2a9d8f;
    border-right: 1.5px solid #2a9d8f;

    transform: rotate(45deg);
}

/* =========================================================
   METRIC VISUAL
   ========================================================= */
.metric-visual {
  position: relative;
  width: 100%;
  height: 150px;
  margin-top: 16px;
}

/* Axes */

.axis {
  position: absolute;
  background: #94a3b8;
}

.y-axis {
  left: 28px;
  top: 10px;
  bottom: 25px;
  width: 1px;
}

.x-axis {
  left: 28px;
  right: 12px;
  bottom: 25px;
  height: 1px;
}

/* PR curve */

.pr-curve {
  position: absolute;
  left: 28px;
  top: 10px;
  width: calc(100% - 40px);
  height: calc(100% - 35px);
  overflow: visible;
}

.curve {
  fill: none;
  stroke: #20639b;
  stroke-width: 3;
  stroke-linecap: round;
  stroke-linejoin: round;
}

.baseline {
  fill: none;
  stroke: #cbd5e1;
  stroke-width: 1.5;
  stroke-dasharray: 4 4;
}

/* Horizontal reference guides */

.guide {
  stroke: #e2e8f0;
  stroke-width: 0.8;
  stroke-dasharray: 3 4;
}

/* Curve endpoints */

.curve-point {
  fill: #20639b;
  stroke: #ffffff;
  stroke-width: 1.5;
}

/* Axis labels */

.axis-label {
  position: absolute;
  color: #64748b;
  font-size: 10px;
  font-weight: 500;
}

.axis-label.precision {
  left: 0;
  top: 50%;
  transform: rotate(-90deg);
  transform-origin: left top;
}

.axis-label.recall {
  right: 50%;
  bottom: 2px;
}

/* Axis values */

.axis-value {
  position: absolute;
  color: #94a3b8;
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 8px;
}

.y-top {
  left: 13px;
  top: 6px;
}

.y-bottom {
  left: 13px;
  bottom: 20px;
}

.x-left {
  left: 24px;
  bottom: 8px;
}

.x-right {
  right: 8px;
  bottom: 8px;
}

/* AUPR label */

.aupr-label {
  position: absolute;
  left: 40%;
  top: 43%;
  color: #20639b;
  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 0.08em;
}

.metric-note {
    display: flex;
    align-items: center;

    gap: 6px;

    margin-top: 7px;

    color: #64748b;

    font-size: 10px;
}

/* =========================================================
   TAKEAWAY
   ========================================================= */

.takeaway {
    flex-shrink: 0;

    margin: 9px auto 4px;

    max-width: 900px;

    display: flex;
    align-items: stretch;

    gap: 10px;

    padding: 8px 16px;

    box-sizing: border-box;

    background: #f8fafb;

    border: 1px solid #dce4e9;

    border-radius: 6px;

    color: #475569;

    font-size: 12px;
    line-height: 1.45;
}

.accent {
    width: 4px;

    flex-shrink: 0;

    border-radius: 2px;

    background: #20639b;
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
   DETAIL MODAL
   ========================================================= */

.detail-overlay {
    position: absolute;
    inset: 0;
    z-index: 99999;

    display: flex;
    align-items: center;
    justify-content: center;

    padding: 24px;
    box-sizing: border-box;

    background: rgba(15, 30, 42, 0.55);

    isolation: isolate;
}

.detail-modal {
    position: absolute;
    z-index: 100000;

    width: min(820px, 90%);
    height: min(90%, 800px);

    display: flex;
    flex-direction: column;

    background: #ffffff;

    border: 1px solid #adb5bd;
    border-radius: 6px;

    box-shadow:
        0 8px 24px rgba(0, 0, 0, 0.18),
        0 2px 6px rgba(0, 0, 0, 0.08);

    overflow: hidden;

    user-select: none;
    box-sizing: border-box;
}

.modal-header {
    flex-shrink: 0;

    display: flex;
    align-items: center;
    justify-content: space-between;

    min-height: 54px;
    padding: 10px 16px;

    background: #f8f9fa;

    border-bottom: 1px solid #dee2e6;

    cursor: move;
}

.modal-eyebrow {
    display: block;

    margin-bottom: 2px;

    color: #6c757d;

    font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;

    font-size: 9px;
    font-weight: 600;

    letter-spacing: 0.08em;
}

.modal-header h3 {
    margin: 2px 0 0;

    color: #212529;

    font-size: 17px;
    line-height: 1.3;

    font-weight: 600;
}

.close-button {
    width: 32px;
    height: 32px;

    display: flex;
    align-items: center;
    justify-content: center;

    padding: 0;

    border: 0;
    border-radius: 4px;

    background: transparent;

    color: #6c757d;

    font-size: 24px;
    line-height: 1;

    cursor: pointer;
}

.close-button:hover {
    background: #e9ecef;
    color: #212529;
}

.close-button:hover {
    background: #f8fafb;
    color: #24313a;
}

.modal-content {
    flex: 1 1 auto;
    min-width: 0;
    min-height: 0;

    padding: 12px;
    box-sizing: border-box;

    display: flex;
    align-items: center;
    justify-content: center;

    overflow: hidden;

    background: #ffffff;
}

.detail-image {
    display: block;

    width: auto;
    height: auto;

    max-width: 100%;
    max-height: 100%;

    object-fit: contain;
    object-position: center;

    border: 1px solid #dee2e6;
    border-radius: 3px;

    box-sizing: border-box;
}

.modal-footer {
    flex-shrink: 0;

    min-height: 38px;
    box-sizing: border-box;

    display: flex;
    align-items: center;
    justify-content: flex-end;

    padding: 7px 16px;

    background: #f8f9fa;

    border-top: 1px solid #dee2e6;

    color: #6c757d;

    font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;

    font-size: 9px;
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

.modal-fade-enter-active,
.modal-fade-leave-active {
    transition: opacity 0.2s ease;
}

.modal-fade-enter-from,
.modal-fade-leave-to {
    opacity: 0;
}

/* =========================================================
   RESPONSIVE
   ========================================================= */

@media (max-width: 900px) {

    .setup-grid {
        grid-template-columns: 1fr;

        overflow-y: auto;
    }

    .setup-card {
        min-height: 250px;
    }

    .space-hint {
        display: none;
    }

}
</style>
