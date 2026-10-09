<template>
<div class="landscape-slide">

    <div class="slide-header">
        <p class="subtitle">
            GRN inference spans several research stages — from data representation
            to inference algorithms. This thesis focuses on two of them.
        </p>
    </div>

    <!-- Zone strip -->
    <div class="zone-strip">
        <div class="zone zone-source">DATA SOURCE</div>
        <div class="zone zone-thesis">THIS THESIS</div>
        <div class="zone zone-downstream">INFERENCE &amp; OUTPUT</div>
    </div>

    <!-- Pipeline -->
    <div class="pipeline">

        <!-- Stage 0: Raw Data -->
        <div class="stage stage-neutral">
            <div class="stage-icon">
                <svg viewBox="0 0 24 24"><path d="M4 6c0-1.1 3.6-2 8-2s8 .9 8 2-3.6 2-8 2-8-.9-8-2z" /><path d="M4 6v12c0 1.1 3.6 2 8 2s8-.9 8-2V6" /><path d="M4 12c0 1.1 3.6 2 8 2s8-.9 8-2" /></svg>
            </div>
            <div class="stage-label">Raw Time-Series<br />Expression Data</div>
            <div class="stage-tags">
                <span>High-dim</span>
                <span>Limited T</span>
                <span>Noisy</span>
                <span>Complex deps</span>
            </div>
        </div>

        <div class="flow-arrow"><svg viewBox="0 0 24 24"><path d="M4 12h15M14 6l6 6-6 6" /></svg></div>

        <!-- Stage 1: Data Representation (THESIS) -->
        <div class="stage stage-thesis" style="--accent: #20639B; --accent2: #7A5AF8;">
            <div class="thesis-badge">THIS THESIS</div>

            <div class="stage-icon dual">
                <svg viewBox="0 0 24 24"><rect x="3" y="3" width="7" height="7" rx="1.5" /><rect x="14" y="3" width="7" height="7" rx="1.5" /><rect x="3" y="14" width="7" height="7" rx="1.5" /><rect x="14" y="14" width="7" height="7" rx="1.5" /></svg>
            </div>

            <div class="stage-label">Data Representation</div>

            <div class="issue-chips">
                <span class="issue-chip" style="--c: #20639B;">
                    <strong>Issue 1</strong> Discretization &amp; MI
                </span>
                <span class="issue-chip" style="--c: #7A5AF8;">
                    <strong>Issue 2</strong> SITTF
                </span>
            </div>
        </div>

        <div class="flow-arrow"><svg viewBox="0 0 24 24"><path d="M4 12h15M14 6l6 6-6 6" /></svg></div>

        <!-- Stage 2: Data Augmentation (THESIS) -->
        <div class="stage stage-thesis" style="--accent: #2A9D8F; --accent2: #2A9D8F;">
            <div class="thesis-badge">THIS THESIS</div>

            <div class="stage-icon">
                <svg viewBox="0 0 24 24"><rect x="4" y="4" width="12" height="12" rx="2" /><path d="M9 20h11V9" /></svg>
            </div>

            <div class="stage-label">Data Augmentation</div>

            <div class="issue-chips">
                <span class="issue-chip" style="--c: #2A9D8F;">
                    <strong>Issue 3</strong> Synthetic Data
                </span>
            </div>
        </div>

        <div class="flow-arrow"><svg viewBox="0 0 24 24"><path d="M4 12h15M14 6l6 6-6 6" /></svg></div>

        <!-- Stage 3: Inference Algorithms -->
        <div class="stage stage-neutral">
            <div class="stage-icon">
                <svg viewBox="0 0 24 24"><rect x="7" y="7" width="10" height="10" rx="1.5" /><path d="M7 3v4M17 3v4M7 17v4M17 17v4M3 7h4M17 7h4M3 17h4M17 17h4" /></svg>
            </div>
            <div class="stage-label">Inference<br />Algorithms</div>
            <div class="stage-tags">
                <span>Correlation</span>
                <span>Info-theoretic</span>
                <span>ML / Regression</span>
                <span>Dynamic models</span>
            </div>
        </div>

        <div class="flow-arrow"><svg viewBox="0 0 24 24"><path d="M4 12h15M14 6l6 6-6 6" /></svg></div>

        <!-- Stage 4: Output -->
        <div class="stage stage-neutral stage-output">
            <div class="stage-icon">
                <svg viewBox="0 0 24 24"><circle cx="6" cy="6" r="2.4" /><circle cx="18" cy="6" r="2.4" /><circle cx="12" cy="18" r="2.4" /><path d="M8 7l7-1M8 8l4 8M16 8l-4 8" /></svg>
            </div>
            <div class="stage-label">Reconstructed<br />GRN</div>
        </div>

    </div>

    <!-- Legend -->
    <div class="legend-footer">
        <span class="legend-item"><i style="--c:#20639B"></i>Issue 1 — Discretization-based GRN inference</span>
        <span class="legend-item"><i style="--c:#7A5AF8"></i>Issue 2 — Scale-independent task transformation</span>
        <span class="legend-item"><i style="--c:#2A9D8F"></i>Issue 3 — Autoencoder-based data synthesis</span>
    </div>

</div>
</template>

<script setup>
</script>

<style scoped>
.landscape-slide {
    width: 100%;
    height: 100%;
    box-sizing: border-box;

    display: flex;
    flex-direction: column;

    padding: 10px 26px 6px;

    background: #f8fafb;
    color: #24313a;

    font-family: 'Inter', 'Segoe UI', sans-serif;
}

/* =========================
   HEADER
========================= */

.slide-header {
    flex-shrink: 0;
    margin-bottom: 10px;
}

.section-label {
    margin-bottom: 5px;

    color: #64748b;

    font-size: 10px;
    font-weight: 700;
    letter-spacing: 0.14em;
}

.slide-header h1 {
    margin: 0;

    color: #173f5f;

    font-size: 22px;
    line-height: 1.25;
    font-weight: 700;
    letter-spacing: -0.01em;
}

.subtitle {
    max-width: 720px;
    margin: 5px 0 0;

    color: #64748b;

    font-size: 12px;
    line-height: 1.45;
}

/* =========================
   ZONE STRIP
========================= */

.zone-strip {
    flex-shrink: 0;

    display: flex;

    margin: 14px 0 6px;

    border-top: 2px solid #dce4e9;
}

.zone {
    position: relative;

    padding-top: 6px;

    text-align: center;

    font-family: 'IBM Plex Mono', monospace;
    font-size: 9px;
    font-weight: 700;
    letter-spacing: 0.1em;

    color: #94a3b8;
}

.zone::before {
    content: '';

    position: absolute;
    top: -2px;
    left: 0;
    right: 0;

    height: 2px;
}

.zone-source {
    flex: 0 0 17%;
}

.zone-thesis {
    flex: 0 0 41%;

    color: #173f5f;
}

.zone-thesis::before {
    background: linear-gradient(90deg, #20639b, #7A5AF8 55%, #2A9D8F);
}

.zone-downstream {
    flex: 0 0 42%;
}

/* =========================
   PIPELINE
========================= */

.pipeline {
    flex: 1;
    min-height: 0;

    display: grid;
    grid-template-columns: 1fr 28px 1.25fr 28px 1.1fr 28px 1fr 28px 0.85fr;

    align-items: stretch;
    gap: 0 6px;
}

/* =========================
   STAGE — base
========================= */

.stage {
    position: relative;
    min-width: 0;

    display: flex;
    flex-direction: column;
    align-items: center;

    padding: 16px 12px 14px;

    border-radius: 12px;

    box-sizing: border-box;
}

.stage-neutral {
    background: #ffffff;
    border: 1px solid #dce4e9;
}

.stage-output {
    background: #f0f5f8;
}

.stage-thesis {
    background:
        linear-gradient(
            180deg,
            #ffffff 0%,
            color-mix(in srgb, var(--accent) 7%, white) 100%
        );

    border: 1.5px solid var(--accent);

    box-shadow: 0 6px 18px color-mix(in srgb, var(--accent) 18%, transparent);
}

.stage:hover {
    transform: translateY(-2px);
}

.stage {
    transition: transform 0.2s ease;
}

/* =========================
   THESIS BADGE
========================= */

.thesis-badge {
    position: absolute;
    top: -10px;

    padding: 3px 10px;

    border-radius: 999px;

    background: var(--accent);
    color: #ffffff;

    font-family: 'IBM Plex Mono', monospace;
    font-size: 8px;
    font-weight: 700;
    letter-spacing: 0.08em;
}

/* =========================
   ICON
========================= */

.stage-icon {
    width: 34px;
    height: 34px;

    margin-bottom: 10px;

    display: flex;
    align-items: center;
    justify-content: center;

    border-radius: 9px;

    background: #f0f5f8;
}

.stage-thesis .stage-icon {
    background: color-mix(in srgb, var(--accent) 14%, white);
}

.stage-icon svg {
    width: 18px;
    height: 18px;

    fill: none;
    stroke: #173f5f;
    stroke-width: 1.8;
    stroke-linecap: round;
    stroke-linejoin: round;
}

.stage-thesis .stage-icon svg {
    stroke: var(--accent);
}

/* =========================
   LABEL
========================= */

.stage-label {
    color: #173f5f;

    font-size: 12.5px;
    font-weight: 700;
    line-height: 1.3;
    text-align: center;
}

/* =========================
   NEUTRAL STAGE TAGS
========================= */

.stage-tags {
    margin-top: 11px;

    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 4px;
}

.stage-tags span {
    padding: 3px 7px;

    border-radius: 999px;
    background: #f1f5f8;

    color: #64748b;

    font-size: 8.5px;
    font-weight: 600;
    white-space: nowrap;
}

/* =========================
   THESIS STAGE — ISSUE CHIPS
========================= */

.issue-chips {
    margin-top: 11px;

    display: flex;
    flex-direction: column;
    gap: 5px;

    width: 100%;
}

.issue-chip {
    display: flex;
    align-items: baseline;
    justify-content: center;
    gap: 5px;

    padding: 4px 8px;

    border-radius: 6px;
    background: color-mix(in srgb, var(--c) 10%, white);
    border: 1px solid color-mix(in srgb, var(--c) 30%, white);

    color: #475569;

    font-size: 9px;
    line-height: 1.3;
    text-align: center;
}

.issue-chip strong {
    color: var(--c);

    font-family: 'IBM Plex Mono', monospace;
    font-size: 8.5px;
    font-weight: 700;
    white-space: nowrap;
}

/* =========================
   ARROWS
========================= */

.flow-arrow {
    display: flex;
    align-items: center;
    justify-content: center;
}

.flow-arrow svg {
    width: 16px;
    height: 16px;

    fill: none;
    stroke: #aab8c2;
    stroke-width: 2;
    stroke-linecap: round;
    stroke-linejoin: round;
}

/* =========================
   LEGEND FOOTER
========================= */

.legend-footer {
    flex-shrink: 0;

    display: flex;
    align-items: center;
    justify-content: center;
    flex-wrap: wrap;

    gap: 18px;

    margin-top: 12px;
    padding-top: 10px;

    border-top: 1px solid #dce4e9;
}

.legend-item {
    display: flex;
    align-items: center;
    gap: 6px;

    color: #64748b;

    font-size: 10.5px;
}

.legend-item i {
    width: 7px;
    height: 7px;
    flex-shrink: 0;

    border-radius: 50%;

    background: var(--c);
}

/* =========================
   RESPONSIVE
========================= */

@media (max-width: 1000px) {
    .pipeline {
        grid-template-columns: 1fr;
        grid-auto-rows: auto;
        gap: 10px 0;
    }

    .flow-arrow {
        transform: rotate(90deg);
    }

    .zone-strip {
        display: none;
    }
}
</style>