<template>
<div class="overview-slide">
    <div class="card-grid">

        <!-- 01. GRN Definition -->
        <article class="topic-card">
            <div class="card-top">
                <span class="card-number">01</span>
                <span class="card-eyebrow">GENE REGULATORY NETWORK</span>
            </div>

            <h2>What is a GRN?</h2>

            <ul class="card-points">
                <li>A set of genes connected by <strong>directed regulatory relationships</strong>.</li>
                <li>Each <strong>node</strong> is a gene — acting as a regulator or a target.</li>
                <li>Each <strong>directed edge</strong> is a regulatory influence: activating or inhibitory.</li>
            </ul>
        </article>

        <!-- 02. Research Problem -->
        <article class="topic-card">
            <div class="card-top">
                <span class="card-number">02</span>
                <span class="card-eyebrow">RESEARCH PROBLEM</span>
            </div>

            <h2>What Are We Trying to Infer?</h2>

            <ul class="card-points">
                <li>A <strong>hidden regulatory network</strong> drives gene expression changes over time.</li>
                <li>We cannot observe regulation directly — only the resulting <strong>expression profiles</strong>.</li>
                <li>Goal: reconstruct the <strong>hidden network</strong> from observed time-series data.</li>
            </ul>
        </article>

        <!-- 03. Why It Matters -->
        <article class="topic-card">
            <div class="card-top">
                <span class="card-number">03</span>
                <span class="card-eyebrow">WHY DOES IT MATTER?</span>
            </div>

            <h2>Why Regulatory Genes Matter?</h2>

            <ul class="card-points">
                <li>Reveals <strong>how genes regulate each other</strong> and coordinate cellular processes.</li>
                <li>Explains <strong>how cells respond</strong> to biological or environmental changes.</li>
                <li>Identifies <strong>key control points</strong> and links to <strong>disease mechanisms</strong>.</li>
            </ul>
        </article>

        <!-- 04. Observed Data -->
        <article class="topic-card">
            <div class="card-top">
                <span class="card-number">04</span>
                <span class="card-eyebrow">EXPERIMENTAL DATA</span>
            </div>

            <h2>What Data Do We Observe?</h2>

            <ul class="card-points">
                <li>Expression data as a matrix — <strong>genes × time points</strong>.</li>
                <li>Time-series captures the <strong>temporal dynamics</strong>, not just a static state.</li>
                <li>Temporal patterns give <strong>clues about regulatory dependencies</strong>.</li>
            </ul>
        </article>

        <!-- 05. Challenges -->
        <article class="topic-card">
            <div class="card-top">
                <span class="card-number">05</span>
                <span class="card-eyebrow">CHALLENGES</span>
            </div>

            <h2>Why Is It Difficult?</h2>

            <ul class="card-points">
                <li><strong>High dimensionality</strong> with <strong>limited observations</strong> over time.</li>
                <li><strong>Noise</strong> and <strong>complex dependencies</strong> — nonlinearity, feedback loops.</li>
                <li>The problem is inherently <strong>ambiguous</strong>: different networks, similar patterns.</li>
            </ul>
        </article>

        <!-- 06. Common Approaches -->
        <article class="topic-card">
            <div class="card-top">
                <span class="card-number">06</span>
                <span class="card-eyebrow">INFERENCE METHODS</span>
            </div>

            <h2>Common GRN Approaches</h2>

            <ul class="card-points">
                <li><strong>Correlation-based</strong> (Pearson, Spearman) — simple but pairwise only.</li>
                <li><strong>Information-theoretic</strong> (ARACNE, MIBNI) — capture nonlinear dependencies.</li>
                <li><strong>Regression/ML</strong> (GENIE3, TIGRESS) and <strong>dynamic models</strong> (DBN, ODE).</li>
            </ul>
        </article>

    </div>

</div>
</template>

<script setup>
</script>

<style scoped>
.overview-slide {
    position: relative;
    width: 100%;
    height: 100%;
    box-sizing: border-box;

    display: flex;
    flex-direction: column;

    padding: 10px 24px 6px;

    background: #f8fafb;
    color: #24313a;

    font-family: 'Inter', 'Segoe UI', sans-serif;
    top:5px;
}

/* =========================
   HEADER
========================= */

.slide-header {
    flex-shrink: 0;
    margin-bottom: 14px;
}

.section-label {
    margin-bottom: 6px;

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

/* =========================
   CARD GRID — 3 cols x 2 rows
========================= */

.card-grid {
    flex: 1;
    min-height: 0;

    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(2, 1fr);
    gap: 5px;
}

/* dim siblings when one card is hovered, to draw focus */
.card-grid:hover .topic-card:not(:hover) {
    opacity: 0.55;
    transform: scale(0.99);
}

/* =========================
   CARD
========================= */

.topic-card {
    position: relative;
    min-width: 0;
    min-height: 0;

    display: flex;
    flex-direction: column;

    padding: 16px 17px 15px;

    background: #ffffff;
    border: 1px solid #dce4e9;
    border-radius: 10px;

    box-sizing: border-box;

    cursor: default;

    transition:
        opacity 0.25s ease,
        transform 0.25s ease,
        border-color 0.25s ease,
        box-shadow 0.25s ease,
        background 0.25s ease;
}

.topic-card::before {
    content: '';

    position: absolute;
    top: 0;
    left: 0;
    right: 0;    

    border-radius: 10px 10px 0 0;

    background: #cbd9e1;

    transition: background 0.25s ease;
}

.topic-card:hover {
    transform: translateY(-4px) scale(1.015);

    border-color: #20639b;
    border-top: 4px solid #2a9d8f;
    background: #fbfdfe;

    box-shadow:
        0 12px 24px rgba(23, 63, 95, 0.12),
        0 2px 6px rgba(23, 63, 95, 0.08);

    z-index: 2;
}

.topic-card:hover::before {
    background: linear-gradient(90deg, #20639b, #2a9d8f);
}

/* =========================
   CARD TOP
========================= */

.card-top {
    display: flex;
    align-items: center;
    gap: 8px;

    margin-bottom: 10px;
}

.card-number {
    flex-shrink: 0;

    width: 22px;
    height: 22px;

    display: flex;
    align-items: center;
    justify-content: center;

    border-radius: 6px;

    background: #f0f5f8;
    color: #173f5f;

    font-family: 'IBM Plex Mono', monospace;
    font-size: 9px;
    font-weight: 700;

    transition: background 0.25s ease, color 0.25s ease;
}

.topic-card:hover .card-number {
    background: #20639b;
    color: #ffffff;
}

.card-eyebrow {
    min-width: 0;

    color: #64748b;

    font-size: 9px;
    font-weight: 700;
    letter-spacing: 0.1em;

    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
}

/* =========================
   TITLE
========================= */

.topic-card h2 {
    margin: 0 0 10px;

    color: #173f5f;

    font-size: 14.5px;
    line-height: 1.25;
    font-weight: 700;
}

/* =========================
   POINTS
========================= */

.card-points {
    margin: 0;
    padding: 0;

    list-style: none;

    display: flex;
    flex-direction: column;
    gap: 7px;
}

.card-points li {
    position: relative;

    padding-left: 13px;

    color: #64748b;

    font-size: 10.5px;
    line-height: 1.42;

    transition: color 0.25s ease;
}

.card-points li::before {
    content: '';

    position: absolute;
    left: 0;
    top: 6px;

    width: 5px;
    height: 5px;

    border-radius: 50%;

    background: #c3d2da;

    transition: background 0.25s ease;
}

.topic-card:hover .card-points li {
    color: #475569;
}

.topic-card:hover .card-points li::before {
    background: #2a9d8f;
}

.card-points strong {
    color: #24313a;
    font-weight: 650;

    transition: color 0.25s ease;
}

.topic-card:hover .card-points strong {
    color: #173f5f;
}

/* =========================
   RESPONSIVE
========================= */

@media (max-width: 900px) {
    .card-grid {
        grid-template-columns: repeat(2, 1fr);
        grid-template-rows: repeat(3, 1fr);

        overflow-y: auto;
    }
}
</style>