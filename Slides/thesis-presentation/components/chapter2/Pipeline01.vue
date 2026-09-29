<template>
  <div class="proposed-model-slide">
    <div class="intro">
      A four-stage framework that connects gene expression representation,
      network inference, and performance evaluation.
    </div>

    <div class="pipeline">

      <!-- Stage 1: Input -->
      <section class="stage stage-1">
        <div class="stage-number">01</div>

        <div class="stage-icon data-icon">
          <svg viewBox="0 0 64 64" aria-hidden="true">
            <line x1="10" y1="52" x2="56" y2="52" class="axis" />
            <line x1="10" y1="52" x2="10" y2="10" class="axis" />

            <path
              d="M14 43 C20 38 22 25 28 30
                 C34 35 36 18 43 23
                 C48 27 51 17 55 14"
              class="expression-line"
            />

            <circle cx="14" cy="43" r="2.5" class="data-point" />
            <circle cx="28" cy="30" r="2.5" class="data-point" />
            <circle cx="43" cy="23" r="2.5" class="data-point" />
            <circle cx="55" cy="14" r="2.5" class="data-point" />
          </svg>
        </div>

        <div class="stage-content">
          <div class="stage-label">INPUT</div>

          <h2>Gene Expression Data</h2>

          <p>
            Time-series gene expression profiles
            containing quantitative measurements
            across multiple time points.
          </p>

          <div class="stage-tags">
            <span>Continuous values</span>
            <span>Time-series</span>
          </div>
        </div>
      </section>

      <!-- Arrow 1 -->
      <div class="pipeline-arrow">
        <span></span>
      </div>

      <!-- Stage 2: Discretization -->
      <section class="stage stage-2">
        <div class="stage-number">02</div>

        <div class="stage-icon discretization-icon">
          <svg viewBox="0 0 64 64" aria-hidden="true">
            <line x1="10" y1="52" x2="56" y2="52" class="axis" />

            <circle
              cx="16"
              cy="39"
              r="4"
              class="level level-low"
            />

            <circle
              cx="32"
              cy="27"
              r="4"
              class="level level-mid"
            />

            <circle
              cx="48"
              cy="16"
              r="4"
              class="level level-high"
            />

            <path
              d="M16 39 L32 27 L48 16"
              class="discretization-line"
            />

            <path
              d="M16 46 H48"
              class="level-line"
            />

            <text x="12" y="59" class="level-text">L</text>
            <text x="29" y="59" class="level-text">M</text>
            <text x="46" y="59" class="level-text">H</text>
          </svg>
        </div>

        <div class="stage-content">
          <div class="stage-label">REPRESENTATION</div>

          <h2>Multiple-Level Discretization</h2>

          <p>
            Transform continuous expression values
            into multiple discrete states while
            preserving more information than Boolean models.
          </p>

          <div class="stage-tags">
            <span class="highlight-tag">2 + 3 levels</span>
            <span>Discrete states</span>
            <span>Noise-aware</span>
          </div>
        </div>

        <div class="contribution-badge">
          KEY CONTRIBUTION
        </div>
      </section>

      <!-- Arrow 2 -->
      <div class="pipeline-arrow">
        <span></span>
      </div>

      <!-- Stage 3: Inference -->
      <section class="stage stage-3">
        <div class="stage-number">03</div>

        <div class="stage-icon inference-icon">
          <svg viewBox="0 0 64 64" aria-hidden="true">
            <defs>
              <marker
                id="pipeline-network-arrow"
                markerWidth="7"
                markerHeight="7"
                refX="6"
                refY="3.5"
                orient="auto"
                markerUnits="userSpaceOnUse"
              >
                <path
                  d="M0 0 L7 3.5 L0 7 Z"
                  fill="#20639B"
                />
              </marker>
            </defs>

            <circle
              cx="15"
              cy="31"
              r="6"
              class="network-node regulator"
            />

            <circle
              cx="32"
              cy="17"
              r="6"
              class="network-node"
            />

            <circle
              cx="32"
              cy="45"
              r="6"
              class="network-node"
            />

            <circle
              cx="49"
              cy="31"
              r="6"
              class="network-node target"
            />

            <path
              d="M20 27 L27 21"
              class="network-edge"
              marker-end="url(#pipeline-network-arrow)"
            />

            <path
              d="M20 35 L27 41"
              class="network-edge"
              marker-end="url(#pipeline-network-arrow)"
            />

            <path
              d="M38 17 L44 27"
              class="network-edge"
              marker-end="url(#pipeline-network-arrow)"
            />

            <path
              d="M38 45 L44 35"
              class="network-edge"
              marker-end="url(#pipeline-network-arrow)"
            />
          </svg>
        </div>

        <div class="stage-content">
          <div class="stage-label">INFERENCE</div>

          <h2>Discretization Network Inference</h2>

          <p>
            Infer regulatory relationships from
            discretized time-series profiles using
            information-based feature selection.
          </p>

          <div class="stage-tags">
            <span>MIFS</span>
            <span>SWAP</span>
            <span>Network reconstruction</span>
          </div>
        </div>
        <div class="contribution-badge">
          KEY CONTRIBUTION
        </div>
      </section>

      <!-- Arrow 3 -->
      <div class="pipeline-arrow">
        <span></span>
      </div>

      <!-- Stage 4: Evaluation -->
      <section class="stage stage-4">
        <div class="stage-number">04</div>

        <div class="stage-icon evaluation-icon">
          <svg viewBox="0 0 64 64" aria-hidden="true">
            <path
              d="M10 50 L20 39 L29 43 L42 25 L54 14"
              class="evaluation-line"
            />

            <path
              d="M46 14 H54 V22"
              class="evaluation-arrow"
            />

            <line
              x1="10"
              y1="53"
              x2="55"
              y2="53"
              class="evaluation-axis"
            />
          </svg>
        </div>

        <div class="stage-content">
          <div class="stage-label">EVALUATION</div>

          <h2>Performance Evaluation</h2>

          <p>
            Evaluate the inferred network from
            both structural and dynamic perspectives.
          </p>

          <div class="stage-tags">
            <span>Structural accuracy</span>
            <span>Dynamics accuracy</span>
          </div>
        </div>
      </section>
    </div>

    <div class="bottom-message">
      <span class="message-mark">→</span>

      <p>
        From
        <strong>continuous expression</strong>
        to a
        <strong>more informative discrete representation</strong>,
        then to
        <strong>GRN reconstruction and evaluation</strong>.
      </p>
    </div>
  </div>
</template>

<style scoped>
.proposed-model-slide {
  position: relative;
  width: 100%;
  height: 100%;
  min-height: 0;

  display: flex;
  flex-direction: column;

  overflow: hidden;
  box-sizing: border-box;
}

.intro {
  flex: 0 0 auto;

  margin: 0 4px 14px;

  color: #64748b;
  font-size: 13px;
  line-height: 1.45;
}

/* =========================
   PIPELINE
   ========================= */

.pipeline {
  flex: 0 0 auto;

  display: grid;

  grid-template-columns:
    minmax(0, 1fr)
    30px
    minmax(0, 1.15fr)
    30px
    minmax(0, 1.15fr)
    30px
    minmax(0, 1.05fr);

  align-items: stretch;

  min-width: 0;
  min-height: 285px;
}

/* =========================
   STAGES
   ========================= */

.stage {
  position: relative;

  display: flex;
  flex-direction: column;
  align-items: center;

  min-width: 0;
  min-height: 285px;

  padding: 18px 14px;

  border: 1px solid #dce4e9;
  border-radius: 12px;

  background: #ffffff;

  box-sizing: border-box;
  text-align: center;
}

.stage-2 {
  border-color: #2a9d8f;

  box-shadow:
    0 3px 14px rgba(42, 157, 143, 0.08);
}

.stage-number {
  position: absolute;
  top: 10px;
  left: 12px;

  color: #cbd5dc;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 12px;
  font-weight: 700;
}

/* =========================
   ICONS
   ========================= */

.stage-icon {
  display: flex;
  align-items: center;
  justify-content: center;

  width: 64px;
  height: 64px;

  margin-top: 4px;
  margin-bottom: 12px;

  border-radius: 11px;

  background: #f8fafb;
}

.stage-icon svg {
  display: block;

  width: 50px;
  height: 50px;

  overflow: visible;
}

/* Input */

.data-icon .axis {
  fill: none;

  stroke: #94a3b8;
  stroke-width: 1.5;

  stroke-linecap: round;
}

.data-icon .expression-line {
  fill: none;

  stroke: #20639b;
  stroke-width: 2.5;

  stroke-linecap: round;
  stroke-linejoin: round;
}

.data-icon .data-point {
  fill: #2a9d8f;
}

/* Discretization */

.discretization-icon .axis {
  stroke: #94a3b8;
  stroke-width: 1.5;
}

.discretization-icon .level {
  fill: #ffffff;
  stroke-width: 2;
}

.discretization-icon .level-low {
  stroke: #94a3b8;
}

.discretization-icon .level-mid {
  stroke: #20639b;
}

.discretization-icon .level-high {
  stroke: #2a9d8f;
}

.discretization-icon .discretization-line {
  fill: none;

  stroke: #20639b;
  stroke-width: 2;

  stroke-linecap: round;
  stroke-linejoin: round;
}

.discretization-icon .level-line {
  fill: none;

  stroke: #e9c46a;
  stroke-width: 2;

  stroke-dasharray: 3 3;
}

.discretization-icon .level-text {
  fill: #64748b;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 6px;
  font-weight: 700;
}

/* Inference */

.inference-icon {
  overflow: visible;
}

.inference-icon svg {
  overflow: visible;
}

.inference-icon .network-node {
  fill: #ffffff;

  stroke: #20639b;
  stroke-width: 2;
}

.inference-icon .network-node.regulator {
  stroke: #20639b;
}

.inference-icon .network-node.target {
  stroke: #2a9d8f;
}

.inference-icon .network-edge {
  fill: none;

  stroke: #20639b;
  stroke-width: 1.8;

  stroke-linecap: round;
}

/* Evaluation */

.evaluation-icon {
  overflow: visible;
}

.evaluation-icon svg {
  overflow: visible;
}

.evaluation-icon .evaluation-line {
  fill: none;

  stroke: #2a9d8f;
  stroke-width: 2.5;

  stroke-linecap: round;
  stroke-linejoin: round;
}

.evaluation-icon .evaluation-arrow {
  fill: none;

  stroke: #20639b;
  stroke-width: 2;

  stroke-linecap: round;
  stroke-linejoin: round;
}

.evaluation-icon .evaluation-axis {
  stroke: #94a3b8;
  stroke-width: 1.5;
}

/* =========================
   STAGE CONTENT
   ========================= */

.stage-label {
  margin-bottom: 5px;

  color: #2a9d8f;

  font-size: 7px;
  font-weight: 700;

  letter-spacing: 0.11em;
}

.stage-content h2 {
  margin: 0 0 8px;

  color: #173f5f;

  font-size: 15px;
  font-weight: 700;

  line-height: 1.25;
  letter-spacing: -0.015em;
}

.stage-content p {
  margin: 0;

  max-width: 210px;

  color: #475569;

  font-size: 9.5px;
  line-height: 1.45;
}

.stage-tags {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 4px;

  margin-top: 11px;
}

.stage-tags span {
  display: inline-flex;
  align-items: center;

  min-height: 18px;

  padding: 2px 6px;

  border: 1px solid #dce4e9;
  border-radius: 4px;

  background: #f8fafb;

  color: #64748b;

  font-size: 7px;
  font-weight: 600;
}

.stage-tags .highlight-tag {
  border-color: #e9c46a;

  background: #fff9e8;

  color: #8a6a12;
}

/* =========================
   KEY CONTRIBUTION
   ========================= */

.contribution-badge {
  position: absolute;

  top: -8px;
  right: 10px;

  padding: 3px 6px;

  border-radius: 4px;

  background: #e9c46a;

  color: #173f5f;

  font-size: 6px;
  font-weight: 800;

  letter-spacing: 0.07em;
}

/* =========================
   PIPELINE ARROWS
   ========================= */

.pipeline-arrow {
  display: flex;
  align-items: center;
  justify-content: center;
}

.pipeline-arrow span {
  position: relative;

  display: block;

  width: 20px;
  height: 2px;

  background: #94a3b8;
}

.pipeline-arrow span::after {
  content: '';

  position: absolute;

  right: -1px;
  top: 50%;

  width: 6px;
  height: 6px;

  border-top: 2px solid #20639b;
  border-right: 2px solid #20639b;

  transform:
    translateY(-50%)
    rotate(45deg);
}

/* =========================
   BOTTOM MESSAGE
   ========================= */

.bottom-message {
  display: flex;
  align-items: center;

  gap: 10px;

  min-height: 43px;

  margin: 11px 4px 0;
  padding: 7px 14px;

  border: 1px solid #dce4e9;
  border-radius: 9px;

  background: #ffffff;

  box-sizing: border-box;
}

.message-mark {
  display: flex;
  align-items: center;
  justify-content: center;

  flex: 0 0 auto;

  width: 27px;
  height: 27px;

  border-radius: 50%;

  background: #e9c46a;

  color: #173f5f;

  font-size: 16px;
  font-weight: 700;
}

.bottom-message p {
  margin: 0;

  color: #475569;

  font-size: 10.5px;
  line-height: 1.35;
}

.bottom-message strong {
  color: #173f5f;
  font-weight: 700;
}

/* =========================
   RESPONSIVE
   ========================= */

@media (max-width: 950px) {
  .pipeline {
    grid-template-columns: 1fr 1fr;
    gap: 8px;
  }

  .pipeline-arrow {
    display: none;
  }

  .stage {
    min-height: 150px;
  }
}
</style>