<template>
  <div class="methodology-slide">
    <div class="intro">
      The experimental pipeline transforms a real-valued network into a
      <strong>discretized representation</strong>, infers regulatory interactions,
      and evaluates the resulting network from both structural and dynamic perspectives.
    </div>

    <div class="pipeline">

      <!-- 01 INPUT -->
      <section class="stage input-stage">
        <div class="stage-number">01</div>

        <div class="stage-icon">
          <svg viewBox="0 0 72 62" aria-hidden="true">
            <path
              d="M12 49 C12 37 18 29 28 29 C38 29 45 37 45 49"
              class="input-line"
            />
            <circle cx="28" cy="18" r="9" class="input-node" />

            <path
              d="M42 18 C50 18 57 24 57 32"
              class="input-line secondary"
            />
            <circle cx="58" cy="35" r="7" class="input-node secondary-node" />

            <path
              d="M15 55 L61 55"
              class="input-axis"
            />
          </svg>
        </div>

        <div class="stage-label">INPUT</div>

        <h2>Real-valued Network</h2>

        <p>
          Time-series gene expression data with
          <strong>continuous expression values</strong>.
        </p>

        <div class="stage-tag">
          Continuous values
        </div>
      </section>


      <!-- ARROW -->
      <div class="pipeline-arrow">
        <svg viewBox="0 0 40 24" aria-hidden="true">
          <line x1="3" y1="12" x2="31" y2="12" />
          <path d="M27 6 L34 12 L27 18" />
        </svg>
      </div>


      <!-- 02 DISCRETIZATION -->
      <section class="stage contribution-stage">
        <div class="stage-number">02</div>

        <div class="contribution-badge">
          KEY STEP
        </div>

        <div class="stage-icon">
          <svg viewBox="0 0 72 62" aria-hidden="true">

            <!-- continuous points -->
            <circle cx="10" cy="45" r="2.5" class="point" />
            <circle cx="17" cy="38" r="2.5" class="point" />
            <circle cx="24" cy="41" r="2.5" class="point" />
            <circle cx="31" cy="31" r="2.5" class="point" />
            <circle cx="38" cy="34" r="2.5" class="point" />
            <circle cx="45" cy="23" r="2.5" class="point" />
            <circle cx="52" cy="26" r="2.5" class="point" />
            <circle cx="59" cy="16" r="2.5" class="point" />

            <!-- threshold / clustering -->
            <line
              x1="8"
              y1="32"
              x2="61"
              y2="32"
              class="cluster-line"
            />

            <!-- discrete states -->
            <rect x="12" y="44" width="12" height="7" rx="2" class="state state-0" />
            <rect x="30" y="32" width="12" height="7" rx="2" class="state state-1" />
            <rect x="48" y="19" width="12" height="7" rx="2" class="state state-2" />
          </svg>
        </div>

        <div class="stage-label">DISCRETIZATION</div>

        <h2>K-means + Validity Index</h2>

        <p>
          Determine the appropriate number of states and transform
          continuous expression values into a
          <strong>discrete representation</strong>.
        </p>

        <div class="stage-tags">
          <span>K-means</span>
          <span>Validity Index</span>
        </div>
      </section>


      <!-- ARROW -->
      <div class="pipeline-arrow">
        <svg viewBox="0 0 40 24" aria-hidden="true">
          <line x1="3" y1="12" x2="31" y2="12" />
          <path d="M27 6 L34 12 L27 18" />
        </svg>
      </div>


      <!-- 03 FEATURE SELECTION -->
      <section class="stage contribution-stage">
        <div class="stage-number">03</div>

        <div class="contribution-badge">
          KEY STEP
        </div>

        <div class="stage-icon">
          <svg viewBox="0 0 72 62" aria-hidden="true">

            <!-- candidate regulators -->
            <circle cx="15" cy="16" r="6" class="feature-node" />
            <circle cx="15" cy="31" r="6" class="feature-node" />
            <circle cx="15" cy="46" r="6" class="feature-node" />

            <!-- target -->
            <circle cx="56" cy="31" r="9" class="feature-target" />

            <!-- candidate edges -->
            <path d="M21 16 C32 16 39 24 47 28" class="feature-edge faded" />
            <path d="M21 31 L47 31" class="feature-edge selected" />
            <path d="M21 46 C32 46 39 38 47 34" class="feature-edge faded" />
          </svg>
        </div>

        <div class="stage-label">FEATURE SELECTION</div>

        <h2>MIFS + SWAP Routine</h2>

        <p>
          Select informative regulatory genes and refine the
          <strong>candidate regulator set</strong> for each target gene.
        </p>

        <div class="stage-tags">
          <span>MIFS</span>
          <span>SWAP</span>
        </div>
      </section>


      <!-- ARROW -->
      <div class="pipeline-arrow">
        <svg viewBox="0 0 40 24" aria-hidden="true">
          <line x1="3" y1="12" x2="31" y2="12" />
          <path d="M27 6 L34 12 L27 18" />
        </svg>
      </div>


      <!-- 04 PREDICTED NETWORK -->
      <section class="stage predicted-stage">
        <div class="stage-number">04</div>

        <div class="stage-icon">
          <svg viewBox="0 0 72 62" aria-hidden="true">

            <defs>
              <marker
                id="method-network-arrow"
                markerWidth="8"
                markerHeight="8"
                refX="7"
                refY="4"
                orient="auto"
                markerUnits="userSpaceOnUse"
              >
                <path
                  d="M0 0 L8 4 L0 8 Z"
                  fill="#20639B"
                />
              </marker>
            </defs>

            <path
              d="M19 17 C28 17 34 23 42 28"
              class="network-edge"
              marker-end="url(#method-network-arrow)"
            />

            <path
              d="M19 45 C29 45 34 38 42 34"
              class="network-edge"
              marker-end="url(#method-network-arrow)"
            />

            <path
              d="M51 28 C57 23 60 20 63 17"
              class="network-edge"
              marker-end="url(#method-network-arrow)"
            />

            <path
              d="M51 35 C57 40 60 43 63 46"
              class="network-edge"
              marker-end="url(#method-network-arrow)"
            />

            <circle cx="13" cy="15" r="7" class="network-node" />
            <circle cx="13" cy="47" r="7" class="network-node" />
            <circle cx="47" cy="31" r="8" class="network-node target" />
            <circle cx="66" cy="14" r="7" class="network-node" />
            <circle cx="66" cy="49" r="7" class="network-node" />
          </svg>
        </div>

        <div class="stage-label">INFERENCE</div>

        <h2>Predicted Network</h2>

        <p>
          Regulatory interactions inferred from the
          <strong>discretized time-series profiles</strong>.
        </p>

        <div class="stage-tag">
          GRN reconstruction
        </div>
      </section>


      <!-- ARROW -->
      <div class="pipeline-arrow">
        <svg viewBox="0 0 40 24" aria-hidden="true">
          <line x1="3" y1="12" x2="31" y2="12" />
          <path d="M27 6 L34 12 L27 18" />
        </svg>
      </div>


      <!-- 05 EVALUATION -->
      <section class="stage evaluation-stage">
        <div class="stage-number">05</div>

        <div class="stage-icon">
          <svg viewBox="0 0 72 62" aria-hidden="true">

            <!-- structural -->
            <rect
              x="8"
              y="12"
              width="24"
              height="38"
              rx="4"
              class="evaluation-box"
            />

            <line x1="14" y1="23" x2="26" y2="23" class="metric-line" />
            <line x1="14" y1="31" x2="26" y2="31" class="metric-line" />
            <line x1="14" y1="39" x2="23" y2="39" class="metric-line" />

            <!-- dynamics -->
            <path
              d="M43 45 C48 38 50 29 55 33 C59 36 62 20 67 16"
              class="dynamic-line"
            />

            <circle cx="43" cy="45" r="2.5" class="metric-point" />
            <circle cx="55" cy="33" r="2.5" class="metric-point" />
            <circle cx="67" cy="16" r="2.5" class="metric-point" />
          </svg>
        </div>

        <div class="stage-label">EVALUATION</div>

        <h2>Network Evaluation</h2>

        <div class="metric-list">
          <div>
            <span class="metric-dot"></span>
            <strong>Structural</strong>
            accuracy
          </div>

          <div>
            <span class="metric-dot dynamics"></span>
            <strong>Dynamics</strong>
            accuracy
          </div>
        </div>
      </section>

    </div>

    <div class="bottom-message">
      <span class="bottom-label">EXPERIMENTAL PIPELINE</span>

      <span class="bottom-text">
        From <strong>continuous expression</strong>
        → <strong>discrete states</strong>
        → <strong>selected regulators</strong>
        → <strong>predicted GRN</strong>
        → <strong>structural + dynamic evaluation</strong>
      </span>
    </div>
  </div>
</template>

<script setup>
</script>

<style scoped>
.methodology-slide {
  width: 100%;
  height: 100%;
  min-height: 0;
  display: flex;
  flex-direction: column;
  box-sizing: border-box;
}

/* ---------- INTRO ---------- */

.intro {
  flex: 0 0 auto;
  margin: 0 8px 13px;
  color: #64748b;
  font-size: 10.5px;
  line-height: 1.45;
  max-width: 1050px;
}

.intro strong {
  color: #173f5f;
}


/* ---------- PIPELINE ---------- */

.pipeline {
  flex: 1 1 auto;
  min-height: 0;

  display: grid;

  grid-template-columns:
    minmax(0, 1fr)
    28px
    minmax(0, 1.18fr)
    28px
    minmax(0, 1.18fr)
    28px
    minmax(0, 1fr)
    28px
    minmax(0, 1fr);

  gap: 7px;

  align-items: stretch;
}


/* ---------- STAGE ---------- */

.stage {
  position: relative;

  display: flex;
  flex-direction: column;
  align-items: center;

  min-width: 0;
  min-height: 0;

  padding: 17px 11px 13px;

  border: 1px solid #dce4e9;
  border-radius: 12px;

  background: #ffffff;

  box-sizing: border-box;

  text-align: center;
}

.stage-number {
  position: absolute;
  top: 9px;
  left: 10px;

  color: #cbd5dc;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 10px;
  font-weight: 700;
}


/* ---------- CONTRIBUTION STAGES ---------- */

.contribution-stage {
  border-color: #2a9d8f;

  box-shadow:
    0 4px 16px rgba(42, 157, 143, 0.08);
}

.contribution-badge {
  position: absolute;
  top: 9px;
  right: 9px;

  padding: 3px 6px;

  border: 1px solid #e9c46a;
  border-radius: 4px;

  background: #fff9e8;
  color: #8a6a12;

  font-size: 6px;
  font-weight: 700;
  letter-spacing: 0.08em;
}


/* ---------- ICON ---------- */

.stage-icon {
  display: flex;
  align-items: center;
  justify-content: center;

  width: 61px;
  height: 58px;

  margin-top: 6px;
  margin-bottom: 10px;

  border-radius: 10px;

  background: #f8fafb;
}

.stage-icon svg {
  display: block;

  width: 49px;
  height: 46px;

  overflow: visible;
}


/* ---------- LABEL ---------- */

.stage-label {
  margin-bottom: 5px;

  color: #2a9d8f;

  font-size: 7px;
  font-weight: 700;

  letter-spacing: 0.11em;
}


/* ---------- TITLE ---------- */

.stage h2 {
  margin: 0 0 8px;

  color: #173f5f;

  font-size: 13px;
  font-weight: 700;

  line-height: 1.25;

  letter-spacing: -0.015em;
}


/* ---------- DESCRIPTION ---------- */

.stage p {
  margin: 0;

  max-width: 175px;

  color: #475569;

  font-size: 8.8px;
  line-height: 1.45;
}

.stage p strong {
  color: #24313a;
}


/* ---------- TAGS ---------- */

.stage-tag,
.stage-tags {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;

  gap: 4px;

  margin-top: 11px;
}

.stage-tag,
.stage-tags span {
  display: inline-flex;
  align-items: center;
  justify-content: center;

  min-height: 17px;

  padding: 2px 6px;

  border: 1px solid #dce4e9;
  border-radius: 4px;

  background: #f8fafb;

  color: #64748b;

  font-size: 6.8px;
  font-weight: 600;
}

.contribution-stage .stage-tags span {
  border-color: #c9e6e1;
  background: #f3fbf9;
  color: #287c73;
}


/* ---------- PIPELINE ARROWS ---------- */

.pipeline-arrow {
  display: flex;
  align-items: center;
  justify-content: center;
}

.pipeline-arrow svg {
  display: block;

  width: 27px;
  height: 18px;

  overflow: visible;
}

.pipeline-arrow line,
.pipeline-arrow path {
  fill: none;

  stroke: #94a3b8;

  stroke-width: 1.8;
  stroke-linecap: round;
  stroke-linejoin: round;
}


/* ---------- INPUT ICON ---------- */

.input-line {
  fill: none;
  stroke: #20639b;
  stroke-width: 2;
  stroke-linecap: round;
}

.input-line.secondary {
  stroke: #2a9d8f;
}

.input-node {
  fill: #ffffff;
  stroke: #20639b;
  stroke-width: 2;
}

.input-node.secondary-node {
  stroke: #2a9d8f;
}

.input-axis {
  stroke: #cbd5dc;
  stroke-width: 1.5;
  stroke-linecap: round;
}


/* ---------- DISCRETIZATION ICON ---------- */

.point {
  fill: #64748b;
}

.cluster-line {
  stroke: #e9c46a;
  stroke-width: 1.5;
  stroke-dasharray: 3 3;
}

.state {
  stroke-width: 1.5;
}

.state-0 {
  fill: #ffffff;
  stroke: #20639b;
}

.state-1 {
  fill: #f3fbf9;
  stroke: #2a9d8f;
}

.state-2 {
  fill: #fff9e8;
  stroke: #e9c46a;
}


/* ---------- FEATURE SELECTION ICON ---------- */

.feature-node {
  fill: #ffffff;
  stroke: #20639b;
  stroke-width: 1.8;
}

.feature-target {
  fill: #f3fbf9;
  stroke: #2a9d8f;
  stroke-width: 2.2;
}

.feature-edge {
  fill: none;
  stroke: #20639b;
  stroke-width: 1.8;
  stroke-linecap: round;
}

.feature-edge.faded {
  opacity: 0.25;
}

.feature-edge.selected {
  stroke-width: 2.5;
}


/* ---------- NETWORK ICON ---------- */

.network-edge {
  fill: none;
  stroke: #20639b;
  stroke-width: 1.7;
  stroke-linecap: round;
  stroke-linejoin: round;
}

.network-node {
  fill: #ffffff;
  stroke: #20639b;
  stroke-width: 1.8;
}

.network-node.target {
  fill: #f3fbf9;
  stroke: #2a9d8f;
  stroke-width: 2.2;
}


/* ---------- EVALUATION ICON ---------- */

.evaluation-box {
  fill: #ffffff;
  stroke: #20639b;
  stroke-width: 1.8;
}

.metric-line {
  stroke: #64748b;
  stroke-width: 1.8;
  stroke-linecap: round;
}

.dynamic-line {
  fill: none;
  stroke: #2a9d8f;
  stroke-width: 2.2;
  stroke-linecap: round;
  stroke-linejoin: round;
}

.metric-point {
  fill: #ffffff;
  stroke: #2a9d8f;
  stroke-width: 1.8;
}


/* ---------- METRICS ---------- */

.metric-list {
  display: flex;
  flex-direction: column;

  width: 100%;

  margin-top: 5px;

  gap: 8px;

  color: #64748b;

  font-size: 8.5px;
  line-height: 1.3;

  text-align: left;
}

.metric-list > div {
  display: flex;
  align-items: center;
  gap: 5px;
}

.metric-list strong {
  color: #24313a;
}

.metric-dot {
  flex: 0 0 auto;

  width: 6px;
  height: 6px;

  border-radius: 50%;

  background: #20639b;
}

.metric-dot.dynamics {
  background: #2a9d8f;
}


/* ---------- BOTTOM ---------- */

.bottom-message {
  flex: 0 0 auto;

  display: flex;
  align-items: center;

  min-height: 39px;

  margin: 12px 8px 0;
  padding: 7px 14px;

  border: 1px solid #dce4e9;
  border-radius: 9px;

  background: #ffffff;

  box-sizing: border-box;
}

.bottom-label {
  flex: 0 0 auto;

  margin-right: 12px;

  color: #2a9d8f;

  font-size: 7px;
  font-weight: 700;

  letter-spacing: 0.1em;
}

.bottom-text {
  color: #64748b;

  font-size: 8.5px;
  line-height: 1.3;
}

.bottom-text strong {
  color: #173f5f;
}
</style>