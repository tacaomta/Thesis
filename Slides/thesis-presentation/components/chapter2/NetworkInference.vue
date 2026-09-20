<template>
  <div class="performance-slide">

    <div class="intro">
      The inferred network is evaluated from two complementary perspectives:
      <strong>structural correctness</strong> and <strong>dynamic consistency</strong>.
    </div>

    <div class="evaluation-grid">

      <!-- ================================================= -->
      <!-- LEFT: DYNAMICS — 2/3 -->
      <!-- ================================================= -->

      <section class="dynamics-section">

        <div class="section-heading">
          <span class="section-number">01</span>
          <div>
            <div class="section-label">DYNAMICS PERFORMANCE</div>
            <h2>Does the inferred network reproduce gene dynamics?</h2>
          </div>
        </div>

        <div class="dynamics-grid">

          <!-- Gene-wise consistency -->
          <div class="dynamic-card consistency-card">

            <div class="card-icon">
              <svg viewBox="0 0 80 60" aria-hidden="true">
                <path
                  d="M8 43 C20 37 25 28 36 31 C47 34 51 18 70 16"
                  class="trajectory observed"
                />

                <path
                  d="M8 47 C20 40 27 31 37 35 C48 38 54 23 70 21"
                  class="trajectory predicted"
                />

                <circle cx="8" cy="43" r="3" class="point observed-point" />
                <circle cx="23" cy="35" r="3" class="point observed-point" />
                <circle cx="36" cy="31" r="3" class="point observed-point" />
                <circle cx="51" cy="25" r="3" class="point observed-point" />
                <circle cx="70" cy="16" r="3" class="point observed-point" />

                <circle cx="8" cy="47" r="3" class="point predicted-point" />
                <circle cx="23" cy="40" r="3" class="point predicted-point" />
                <circle cx="37" cy="35" r="3" class="point predicted-point" />
                <circle cx="54" cy="23" r="3" class="point predicted-point" />
                <circle cx="70" cy="21" r="3" class="point predicted-point" />
              </svg>
            </div>

            <div class="metric-label">GENE-WISE</div>

            <h3>Dynamics Consistency</h3>

            <p>
              Compare the observed and predicted discretization
              trajectories of each gene.
            </p>

            <div class="comparison">

              <div class="trajectory-row">
                <span class="trajectory-label observed-label">
                  observed
                </span>

                <div class="states">
                  <span class="state match">1</span>
                  <span class="state match">2</span>
                  <span class="state mismatch">1</span>
                  <span class="state match">2</span>
                  <span class="state match">0</span>
                </div>
              </div>

              <div class="trajectory-row">
                <span class="trajectory-label predicted-label">
                  predicted
                </span>

                <div class="states">
                  <span class="state match">1</span>
                  <span class="state match">2</span>
                  <span class="state mismatch">2</span>
                  <span class="state match">2</span>
                  <span class="state match">0</span>
                </div>
              </div>

            </div>

            <div class="consistency-formula">
              <span class="formula-name">C(v, v′)</span>
              <span class="equals">=</span>

              <span class="fraction">
                <span>matching states</span>
                <span class="fraction-line"></span>
                <span>evaluated time steps</span>
              </span>
            </div>

          </div>


          <!-- Network dynamics accuracy -->
          <div class="dynamic-card accuracy-card">

            <div class="card-icon accuracy-icon">
              <div class="gene-bars">

                <div class="gene-bar">
                  <span>v₁</span>
                  <i style="height: 82%"></i>
                </div>

                <div class="gene-bar">
                  <span>v₂</span>
                  <i style="height: 64%"></i>
                </div>

                <div class="gene-bar">
                  <span>v₃</span>
                  <i style="height: 91%"></i>
                </div>

                <div class="gene-bar">
                  <span>...</span>
                  <i style="height: 73%"></i>
                </div>

              </div>
            </div>

            <div class="metric-label">NETWORK-WISE</div>

            <h3>Dynamics Accuracy</h3>

            <p>
              Average the gene-wise dynamics consistency
              across all <strong>N</strong> genes.
            </p>

            <div class="gene-scores">

              <div class="score-row">
                <span>C(v₁,v₁′)</span>
                <div class="score-track">
                  <div
                    class="score-fill"
                    style="width: 82%"
                  ></div>
                </div>
              </div>

              <div class="score-row">
                <span>C(v₂,v₂′)</span>
                <div class="score-track">
                  <div
                    class="score-fill"
                    style="width: 64%"
                  ></div>
                </div>
              </div>

              <div class="score-row">
                <span>C(v₃,v₃′)</span>
                <div class="score-track">
                  <div
                    class="score-fill"
                    style="width: 91%"
                  ></div>
                </div>
              </div>

              <div class="score-row">
                <span>...</span>
                <div class="score-track">
                  <div
                    class="score-fill"
                    style="width: 73%"
                  ></div>
                </div>
              </div>

            </div>

            <div class="accuracy-formula">
              <div class="formula-label">
                DYNAMICS ACCURACY
              </div>

              <div class="main-formula">
                <span>Σ C(vᵢ, vᵢ′)</span>
                <span class="divide">/</span>
                <span>N</span>
              </div>
            </div>

          </div>

        </div>

      </section>


      <!-- ================================================= -->
      <!-- RIGHT: STRUCTURE — 1/3 -->
      <!-- ================================================= -->

      <section class="structure-section">

        <div class="section-heading compact-heading">
          <span class="section-number">02</span>

          <div>
            <div class="section-label">
              STRUCTURAL PERFORMANCE
            </div>

            <h2>
              Does the inferred network recover the true interactions?
            </h2>
          </div>
        </div>


        <div class="structure-metrics">

          <!-- Precision -->
          <div class="structure-card">

            <div class="metric-symbol precision-symbol">
              P
            </div>

            <div class="structure-content">

              <h3>Precision</h3>

              <p>
                How many inferred interactions
                are actually correct?
              </p>

              <div class="structural-formula">
                TP
                <span>/</span>
                TP + FP
              </div>

            </div>

          </div>


          <!-- Recall -->
          <div class="structure-card">

            <div class="metric-symbol recall-symbol">
              R
            </div>

            <div class="structure-content">

              <h3>Recall</h3>

              <p>
                How many true interactions
                are successfully recovered?
              </p>

              <div class="structural-formula">
                TP
                <span>/</span>
                TP + FN
              </div>

            </div>

          </div>


          <!-- Structural Accuracy -->
          <div class="structure-card structural-accuracy-card">

            <div class="metric-symbol accuracy-symbol">
              A
            </div>

            <div class="structure-content">

              <h3>Structural Accuracy</h3>

              <p>
                Overall correctness of the
                inferred network structure.
              </p>

              <div class="structural-formula">
                TP + TN
                <span>/</span>
                All possible edges
              </div>

            </div>

          </div>

        </div>


        <!-- <div class="structure-visual">

          <div class="network-legend">
            <span class="legend-item">
              <i class="legend-dot true"></i>
              True edge
            </span>

            <span class="legend-item">
              <i class="legend-dot inferred"></i>
              Inferred edge
            </span>
          </div>

          <svg
            class="small-network"
            viewBox="0 0 180 115"
            aria-hidden="true"
          >
            <defs>
              <marker
                id="structure-arrow"
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

            <path
              d="M38 28 C61 28 75 39 90 49"
              class="true-edge"
              marker-end="url(#structure-arrow)"
            />

            <path
              d="M38 82 C60 82 74 67 90 57"
              class="true-edge"
              marker-end="url(#structure-arrow)"
            />

            <path
              d="M98 52 C119 40 133 30 148 27"
              class="inferred-edge"
              marker-end="url(#structure-arrow)"
            />

            <path
              d="M98 60 C119 71 134 81 148 84"
              class="inferred-edge"
              marker-end="url(#structure-arrow)"
            />

            <circle
              cx="29"
              cy="26"
              r="10"
              class="network-node"
            />

            <circle
              cx="29"
              cy="84"
              r="10"
              class="network-node"
            />

            <circle
              cx="94"
              cy="55"
              r="12"
              class="network-node target"
            />

            <circle
              cx="157"
              cy="25"
              r="10"
              class="network-node"
            />

            <circle
              cx="157"
              cy="87"
              r="10"
              class="network-node"
            />
          </svg>

        </div> -->

      </section>

    </div>


    <div class="bottom-message">

      <span class="bottom-label">EVALUATION</span>

      <strong>Structure</strong>

      <span class="bottom-plus">+</span>

      <strong>Dynamics</strong>

      <span class="bottom-arrow">→</span>

      <span class="bottom-text">
        A more complete view of inferred network performance
      </span>

    </div>

  </div>
</template>

<script setup>
</script>

<style scoped>
.performance-slide {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  min-width: 0;
  min-height: 0;
  box-sizing: border-box;
  color: #24313a;
}

/* -------------------------------------------------- */
/* INTRO */
/* -------------------------------------------------- */

.intro {
  flex: 0 0 auto;
  max-width: 920px;
  margin: 0 auto 12px;
  text-align: center;
  color: #64748b;
  font-size: 10px;
  line-height: 1.4;
}

.intro strong {
  color: #173f5f;
}

/* -------------------------------------------------- */
/* MAIN LAYOUT */
/* -------------------------------------------------- */

.evaluation-grid {
  flex: 1 1 auto;
  min-height: 0;
  display: grid;
  grid-template-columns: minmax(0, 2fr) minmax(0, 1fr);
  gap: 14px;
}

/* -------------------------------------------------- */
/* SECTION CONTAINERS */
/* -------------------------------------------------- */

.dynamics-section,
.structure-section {
  min-width: 0;
  min-height: 0;
  padding: 13px;
  border: 1px solid #dce4e9;
  border-radius: 12px;
  background: #ffffff;
  box-sizing: border-box;
}

.dynamics-section {
  display: flex;
  flex-direction: column;
}

.structure-section {
  display: flex;
  flex-direction: column;
}

/* -------------------------------------------------- */
/* SECTION HEADING */
/* -------------------------------------------------- */

.section-heading {
  flex: 0 0 auto;
  display: grid;
  grid-template-columns: 25px minmax(0, 1fr);
  gap: 8px;
  align-items: start;
  margin-bottom: 11px;
}

.section-number {
  color: #cbd5dc;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 10px;
  font-weight: 700;
  line-height: 1.3;
}

.section-label {
  margin-bottom: 3px;
  color: #2a9d8f;
  font-size: 6.5px;
  font-weight: 700;
  letter-spacing: 0.12em;
}

.section-heading h2 {
  margin: 0;
  color: #173f5f;
  font-size: 12px;
  font-weight: 700;
  line-height: 1.25;
}

.compact-heading h2 {
  font-size: 11px;
}

/* -------------------------------------------------- */
/* DYNAMICS CARDS */
/* -------------------------------------------------- */

.dynamics-grid {
  flex: 1 1 auto;
  min-height: 0;
  display: grid;
  grid-template-columns: minmax(0, 1fr) minmax(0, 1fr);
  gap: 10px;
}

.dynamic-card {
  position: relative;
  min-width: 0;
  min-height: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 12px 13px;
  border: 1px solid #dce4e9;
  border-radius: 9px;
  background: #fdfefe;
  box-sizing: border-box;
  overflow: hidden;
  text-align: center;
}

.consistency-card {
  border-top: 2px solid #2a9d8f;
}

.accuracy-card {
  border-top: 2px solid #20639b;
}

.card-icon {
  width: 58px;
  height: 46px;
  margin-bottom: 6px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 8px;
  background: #f8fafb;
}

.card-icon svg {
  display: block;
  width: 52px;
  height: 40px;
  overflow: visible;
}

.trajectory {
  fill: none;
  stroke-width: 1.8;
  stroke-linecap: round;
  stroke-linejoin: round;
}

.trajectory.observed {
  stroke: #20639b;
}

.trajectory.predicted {
  stroke: #2a9d8f;
  stroke-dasharray: 4 3;
}

.point {
  fill: #ffffff;
  stroke-width: 1.5;
}

.observed-point {
  stroke: #20639b;
}

.predicted-point {
  stroke: #2a9d8f;
}

.metric-label {
  margin-bottom: 3px;
  color: #2a9d8f;
  font-size: 6px;
  font-weight: 700;
  letter-spacing: 0.11em;
}

.dynamic-card h3 {
  margin: 0 0 6px;
  color: #173f5f;
  font-size: 13px;
  font-weight: 700;
  line-height: 1.2;
}

.dynamic-card > p {
  max-width: 290px;
  margin: 0;
  color: #64748b;
  font-size: 7.5px;
  line-height: 1.4;
}

.dynamic-card > p strong {
  color: #24313a;
}

/* -------------------------------------------------- */
/* CONSISTENCY */
/* -------------------------------------------------- */

.comparison {
  width: 100%;
  margin-top: 10px;
  padding: 8px 9px;
  border: 1px solid #dce4e9;
  border-radius: 7px;
  background: #f8fafb;
  box-sizing: border-box;
}

.trajectory-row {
  display: grid;
  grid-template-columns: 54px minmax(0, 1fr);
  align-items: center;
  gap: 6px;
}

.trajectory-row + .trajectory-row {
  margin-top: 5px;
}

.trajectory-label {
  text-align: right;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 6px;
  font-weight: 600;
}

.observed-label {
  color: #20639b;
}

.predicted-label {
  color: #2a9d8f;
}

.states {
  display: flex;
  justify-content: space-between;
  gap: 3px;
}

.state {
  width: 21px;
  height: 21px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 4px;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 7px;
  font-weight: 700;
  box-sizing: border-box;
}

.state.match {
  border: 1px solid #a9d9d1;
  background: #edf9f6;
  color: #2a9d8f;
}

.state.mismatch {
  border: 1px solid #e9c46a;
  background: #fff9e8;
  color: #8a6a12;
}

.consistency-formula {
  margin-top: 9px;
  padding: 7px 9px;
  display: flex;
  align-items: center;
  gap: 6px;
  border: 1px solid #dce4e9;
  border-radius: 6px;
  background: #ffffff;
  color: #173f5f;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 7px;
}

.formula-name {
  color: #2a9d8f;
  font-weight: 700;
}

.equals {
  color: #94a3b8;
}

.fraction {
  display: flex;
  flex-direction: column;
  align-items: center;
  line-height: 1.1;
  font-size: 5.5px;
  color: #475569;
}

.fraction-line {
  width: 75px;
  margin: 2px 0;
  border-top: 1px solid #94a3b8;
}

/* -------------------------------------------------- */
/* DYNAMICS ACCURACY */
/* -------------------------------------------------- */

.accuracy-icon {
  align-items: flex-end;
  padding: 7px 10px;
  box-sizing: border-box;
}

.gene-bars {
  width: 43px;
  height: 34px;
  display: flex;
  align-items: flex-end;
  justify-content: space-between;
  gap: 4px;
}

.gene-bar {
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  align-items: center;
  gap: 2px;
}

.gene-bar span {
  color: #94a3b8;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 4.5px;
}

.gene-bar i {
  display: block;
  width: 7px;
  min-height: 5px;
  border-radius: 2px 2px 0 0;
  background: #20639b;
}

.gene-scores {
  width: 100%;
  margin-top: 10px;
  padding: 9px 10px;
  border: 1px solid #dce4e9;
  border-radius: 7px;
  background: #f8fafb;
  box-sizing: border-box;
}

.score-row {
  display: grid;
  grid-template-columns: 52px minmax(0, 1fr);
  align-items: center;
  gap: 7px;
}

.score-row + .score-row {
  margin-top: 6px;
}

.score-row > span {
  color: #64748b;
  text-align: right;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 6px;
}

.score-track {
  height: 6px;
  overflow: hidden;
  border-radius: 3px;
  background: #e9eef1;
}

.score-fill {
  height: 100%;
  border-radius: 3px;
  background: #2a9d8f;
}

.accuracy-formula {
  margin-top: 9px;
  padding: 7px 13px;
  border: 1px solid #b9d8e5;
  border-radius: 6px;
  background: #eef7fa;
}

.formula-label {
  margin-bottom: 3px;
  color: #64748b;
  font-size: 5.5px;
  font-weight: 700;
  letter-spacing: 0.08em;
}

.main-formula {
  color: #20639b;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 8px;
  font-weight: 700;
}

/* -------------------------------------------------- */
/* STRUCTURAL METRICS */
/* -------------------------------------------------- */

.structure-metrics {
  flex: 0 0 auto;
  display: flex;
  flex-direction: column;
  gap: 7px;
}

.structure-card {
  display: grid;
  grid-template-columns: 38px minmax(0, 1fr);
  gap: 9px;
  align-items: center;
  padding: 9px 10px;
  border: 1px solid #dce4e9;
  border-radius: 8px;
  background: #fdfefe;
  box-sizing: border-box;
}

.structural-accuracy-card {
  border-color: #b9d8e5;
  background: #f8fcfd;
}

.metric-symbol {
  width: 34px;
  height: 34px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 7px;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 14px;
  font-weight: 700;
  box-sizing: border-box;
}

.precision-symbol {
  border: 1px solid #b9d8e5;
  background: #eef7fa;
  color: #20639b;
}

.recall-symbol {
  border: 1px solid #a9d9d1;
  background: #edf9f6;
  color: #2a9d8f;
}

.accuracy-symbol {
  border: 1px solid #e9c46a;
  background: #fff9e8;
  color: #8a6a12;
}

.structure-content {
  min-width: 0;
}

.structure-content h3 {
  margin: 0 0 3px;
  color: #173f5f;
  font-size: 10px;
  font-weight: 700;
  line-height: 1.2;
}

.structure-content p {
  margin: 0;
  color: #64748b;
  font-size: 6.8px;
  line-height: 1.35;
}

.structural-formula {
  width: fit-content;
  margin-top: 5px;
  padding: 4px 7px;
  border-radius: 4px;
  background: #f8fafb;
  color: #20639b;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 6.5px;
  font-weight: 600;
}

.structural-formula span {
  margin: 0 3px;
  color: #94a3b8;
}

/* -------------------------------------------------- */
/* STRUCTURAL VISUAL */
/* -------------------------------------------------- */

.structure-visual {
  flex: 1 1 auto;
  min-height: 0;
  margin-top: 9px;
  padding: 8px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  border: 1px solid #dce4e9;
  border-radius: 8px;
  background: #f8fafb;
  box-sizing: border-box;
}

.network-legend {
  width: 100%;
  display: flex;
  justify-content: center;
  gap: 12px;
  margin-bottom: 4px;
}

.legend-item {
  display: flex;
  align-items: center;
  gap: 4px;
  color: #64748b;
  font-size: 5.5px;
}

.legend-dot {
  width: 5px;
  height: 5px;
  border-radius: 50%;
}

.legend-dot.true {
  background: #20639b;
}

.legend-dot.inferred {
  background: #2a9d8f;
}

.small-network {
  width: 150px;
  max-width: 100%;
  height: auto;
  overflow: visible;
}

.true-edge {
  fill: none;
  stroke: #20639b;
  stroke-width: 1.7;
  stroke-linecap: round;
}

.inferred-edge {
  fill: none;
  stroke: #2a9d8f;
  stroke-width: 1.7;
  stroke-dasharray: 4 2;
  stroke-linecap: round;
}

.network-node {
  fill: #ffffff;
  stroke: #20639b;
  stroke-width: 1.7;
}

.network-node.target {
  fill: #f3fbf9;
  stroke: #2a9d8f;
  stroke-width: 2;
}

/* -------------------------------------------------- */
/* BOTTOM */
/* -------------------------------------------------- */

.bottom-message {
  flex: 0 0 auto;
  min-height: 36px;
  margin-top: 10px;
  padding: 6px 16px;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 7px;
  border: 1px solid #dce4e9;
  border-radius: 8px;
  background: #ffffff;
  box-sizing: border-box;
  font-size: 7.5px;
}

.bottom-label {
  color: #2a9d8f;
  font-size: 6px;
  font-weight: 700;
  letter-spacing: 0.1em;
}

.bottom-message strong {
  color: #173f5f;
}

.bottom-plus,
.bottom-arrow {
  color: #94a3b8;
  font-size: 10px;
}

.bottom-text {
  color: #64748b;
}
</style>