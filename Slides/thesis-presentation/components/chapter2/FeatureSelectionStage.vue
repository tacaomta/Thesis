<template>
  <div class="feature-selection-slide">

    <div class="intro">
      MIFS first selects potential regulators for each target gene.
      SWAP then iteratively refines the selected set to improve
      <strong>gene-wise dynamics consistency</strong>.
    </div>

    <div class="methods-grid">

      <!-- ================= MIFS ================= -->
      <section class="method-card mifs-card">

        <div class="method-top">
          <div class="method-index">01</div>

          <div>
            <div class="method-label">FEATURE SELECTION</div>
            <h2>MIFS</h2>
          </div>

          <div class="method-badge">
            SELECT
          </div>
        </div>


        <div class="method-description">
          For each target gene <strong>g₀</strong>, MIFS selects
          a set of <strong>k potential regulator genes</strong>.
        </div>


        <!-- target + candidate pool -->
        <div class="selection-visual">

          <div class="target-column">

            <div class="visual-label">
              TARGET
            </div>

            <div class="target-gene">
              g₀
            </div>

          </div>


          <div class="selection-arrow">
            <svg viewBox="0 0 45 24" aria-hidden="true">
              <line x1="3" y1="12" x2="34" y2="12" />
              <path d="M29 6 L36 12 L29 18" />
            </svg>
          </div>


          <div class="candidate-pool">

            <div class="visual-label">
              CANDIDATE GENES
            </div>

            <div class="gene-pool">
              <span>g₁</span>
              <span>g₂</span>
              <span>g₃</span>
              <span>g₄</span>
              <span>g₅</span>
              <span>…</span>
            </div>

          </div>

        </div>


        <!-- three steps -->
        <div class="steps">

          <div class="step">

            <div class="step-number">1</div>

            <div class="step-content">
              <strong>Select the first regulator</strong>

              <p>
                Choose the gene that maximizes
                <strong>mutual information</strong>
                with the target gene g₀.
              </p>
            </div>

          </div>


          <div class="step">

            <div class="step-number">2</div>

            <div class="step-content">
              <strong>Select the next regulator</strong>

              <p>
                Select the candidate that maximizes
                its information with g₀ while considering
                its dependency on already selected genes.
              </p>
            </div>

          </div>


          <div class="step">

            <div class="step-number">3</div>

            <div class="step-content">
              <strong>Repeat until k regulators</strong>

              <p>
                Continue the selection process until the
                desired number <strong>k</strong> of candidates
                has been chosen.
              </p>
            </div>

          </div>

        </div>


        <!-- k parameter -->
        <div class="parameter-box">

          <div class="parameter-symbol">
            k
          </div>

          <div>
            <span class="parameter-label">
              USER-DEFINED PARAMETER
            </span>

            <strong>Maximum k = 8</strong>
          </div>

        </div>


        <div class="result-box mifs-result">

          <span class="result-icon">→</span>

          <div>
            <span class="result-label">OUTPUT</span>
            <strong>Potential regulator set</strong>
          </div>

        </div>

      </section>


      <!-- ================= SWAP ================= -->
      <section class="method-card swap-card">

        <div class="method-top">
          <div class="method-index">02</div>

          <div>
            <div class="method-label">ITERATIVE REFINEMENT</div>
            <h2>SWAP</h2>
          </div>

          <div class="method-badge swap-badge">
            REFINE
          </div>
        </div>


        <div class="method-description">
          MIFS may fail to find the optimal regulator set because
          it does not compute the exact
          <strong>multivariate mutual information</strong>.
        </div>


        <!-- swap visual -->
        <div class="swap-visual">

          <div class="variable-group">

            <div class="visual-label">
              SELECTED
            </div>

            <div class="selected-variables">
              <span class="selected-variable">g₁</span>
              <span class="selected-variable">g₃</span>
              <span class="selected-variable">g₇</span>
            </div>

          </div>


          <div class="swap-symbol">

            <svg viewBox="0 0 70 52" aria-hidden="true">

              <defs>
                <marker
                  id="swap-arrow-up"
                  markerWidth="8"
                  markerHeight="8"
                  refX="7"
                  refY="4"
                  orient="auto"
                  markerUnits="userSpaceOnUse"
                >
                  <path
                    d="M0 0 L8 4 L0 8 Z"
                    fill="#2A9D8F"
                  />
                </marker>

                <marker
                  id="swap-arrow-down"
                  markerWidth="8"
                  markerHeight="8"
                  refX="7"
                  refY="4"
                  orient="auto"
                  markerUnits="userSpaceOnUse"
                >
                  <path
                    d="M0 0 L8 4 L0 8 Z"
                    fill="#E9C46A"
                  />
                </marker>
              </defs>

              <path
                d="M18 18 C32 8 39 8 52 18"
                class="swap-arrow selected-to-unselected"
                marker-end="url(#swap-arrow-up)"
              />

              <path
                d="M52 34 C39 44 32 44 18 34"
                class="swap-arrow unselected-to-selected"
                marker-end="url(#swap-arrow-down)"
              />

              <text
                x="35"
                y="30"
                text-anchor="middle"
                class="swap-text"
              >
                SWAP
              </text>

            </svg>

          </div>


          <div class="variable-group">

            <div class="visual-label">
              UNSELECTED
            </div>

            <div class="unselected-variables">
              <span class="unselected-variable">g₂</span>
              <span class="unselected-variable">g₄</span>
              <span class="unselected-variable">g₆</span>
              <span class="unselected-variable">…</span>
            </div>

          </div>

        </div>


        <!-- iterative process -->
        <div class="iteration-box">

          <div class="iteration-title">
            Iterative improvement
          </div>

          <div class="iteration-flow">

            <div class="iteration-step">
              <span class="iteration-number">1</span>
              <strong>Swap variables</strong>
            </div>

            <div class="iteration-arrow">→</div>

            <div class="iteration-step">
              <span class="iteration-number">2</span>
              <strong>Evaluate dynamics</strong>
            </div>

            <div class="iteration-arrow">→</div>

            <div class="iteration-step">
              <span class="iteration-number">3</span>
              <strong>Keep improvement</strong>
            </div>

          </div>

        </div>


        <!-- stopping conditions -->
        <div class="stopping-box">

          <div class="stopping-title">
            STOP WHEN
          </div>

          <div class="stopping-conditions">

            <div class="condition">
              <span class="condition-check">✓</span>

              <span>
                Gene-wise dynamics consistency
                <strong>reaches 1.0</strong>
              </span>
            </div>

            <div class="condition">
              <span class="condition-check">✓</span>

              <span>
                Number of potential candidates
                <strong>equals k</strong>
              </span>
            </div>

          </div>

        </div>


        <div class="result-box swap-result">

          <span class="result-icon">→</span>

          <div>
            <span class="result-label">OUTPUT</span>
            <strong>Refined regulator set</strong>
          </div>

        </div>

      </section>

    </div>


    <!-- <div class="bottom-message">

      <span class="bottom-label">
        FEATURE SELECTION STRATEGY
      </span>

      <span class="bottom-text">
        <strong>MIFS</strong> identifies potential regulators
        → <strong>SWAP</strong> refines the selected set
        → improved <strong>dynamic consistency</strong>
      </span>

    </div> -->

  </div>
</template>


<script setup>
</script>


<style scoped>
.feature-selection-slide {
  width: 100%;
  height: 100%;
  min-height: 0;

  display: flex;
  flex-direction: column;

  box-sizing: border-box;
}


/* =========================================
   INTRO
========================================= */

.intro {
  flex: 0 0 auto;

  margin: 0 8px 11px;

  max-width: 1100px;

  color: #64748b;

  font-size: 10.5px;
  line-height: 1.4;
}

.intro strong {
  color: #173f5f;
}


/* =========================================
   MAIN GRID
========================================= */

.methods-grid {
  flex: 1 1 auto;

  min-height: 0;
  min-width: 0;

  display: grid;

  grid-template-columns:
    minmax(0, 1fr)
    minmax(0, 1fr);

  gap: 14px;
}


/* =========================================
   METHOD CARD
========================================= */

.method-card {
  min-width: 0;
  min-height: 0;

  display: flex;
  flex-direction: column;

  padding: 13px 14px;

  border: 1px solid #dce4e9;
  border-radius: 12px;

  background: #ffffff;

  box-sizing: border-box;
}

.mifs-card {
  border-top: 3px solid #20639b;
}

.swap-card {
  border-top: 3px solid #2a9d8f;
}


/* =========================================
   HEADER
========================================= */

.method-top {
  position: relative;

  display: flex;
  align-items: flex-start;

  gap: 10px;

  margin-bottom: 8px;
}

.method-index {
  display: flex;
  align-items: center;
  justify-content: center;

  flex: 0 0 auto;

  width: 27px;
  height: 27px;

  border-radius: 7px;

  background: #eef3f7;

  color: #20639b;

  font-family: 'IBM Plex Mono', monospace;

  font-size: 9px;
  font-weight: 700;
}

.swap-card .method-index {
  background: #f3fbf9;
  color: #2a9d8f;
}

.method-label {
  margin-bottom: 2px;

  color: #2a9d8f;

  font-size: 6.5px;
  font-weight: 700;

  letter-spacing: 0.11em;
}

.method-top h2 {
  margin: 0;

  color: #173f5f;

  font-size: 19px;
  font-weight: 700;

  line-height: 1.1;
}

.method-badge {
  margin-left: auto;

  padding: 4px 7px;

  border: 1px solid #dce4e9;
  border-radius: 4px;

  background: #f8fafb;

  color: #20639b;

  font-size: 6px;
  font-weight: 700;

  letter-spacing: 0.08em;
}

.swap-badge {
  border-color: #c9e6e1;

  background: #f3fbf9;

  color: #2a9d8f;
}


/* =========================================
   DESCRIPTION
========================================= */

.method-description {
  flex: 0 0 auto;

  min-height: 42px;

  padding: 7px 9px;

  border-radius: 7px;

  background: #f8fafb;

  color: #64748b;

  font-size: 8.5px;

  line-height: 1.4;
}

.method-description strong {
  color: #173f5f;
}


/* =========================================
   MIFS SELECTION VISUAL
========================================= */

.selection-visual {
  flex: 0 0 auto;

  display: grid;

  grid-template-columns:
    70px
    45px
    minmax(0, 1fr);

  align-items: center;

  gap: 5px;

  min-height: 67px;

  margin: 8px 0;

  padding: 7px 9px;

  border: 1px solid #dce4e9;
  border-radius: 8px;

  background: #ffffff;
}

.target-column {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.visual-label {
  margin-bottom: 5px;

  color: #94a3b8;

  font-size: 5.8px;
  font-weight: 700;

  letter-spacing: 0.1em;
}

.target-gene {
  display: flex;
  align-items: center;
  justify-content: center;

  width: 35px;
  height: 35px;

  border-radius: 50%;

  border: 2px solid #2a9d8f;

  background: #f3fbf9;

  color: #173f5f;

  font-family: 'IBM Plex Mono', monospace;

  font-size: 11px;
  font-weight: 700;
}

.selection-arrow {
  display: flex;
  align-items: center;
  justify-content: center;
}

.selection-arrow svg {
  width: 38px;
  height: 20px;

  overflow: visible;
}

.selection-arrow line,
.selection-arrow path {
  fill: none;

  stroke: #94a3b8;

  stroke-width: 1.7;

  stroke-linecap: round;
  stroke-linejoin: round;
}

.candidate-pool {
  min-width: 0;
}

.gene-pool {
  display: flex;
  flex-wrap: wrap;

  gap: 5px;
}

.gene-pool span {
  display: flex;
  align-items: center;
  justify-content: center;

  min-width: 25px;
  height: 23px;

  padding: 0 5px;

  border: 1px solid #dce4e9;
  border-radius: 5px;

  background: #f8fafb;

  color: #20639b;

  font-family: 'IBM Plex Mono', monospace;

  font-size: 7px;
  font-weight: 600;
}


/* =========================================
   MIFS STEPS
========================================= */

.steps {
  flex: 1 1 auto;

  min-height: 0;

  display: flex;
  flex-direction: column;

  gap: 6px;
}

.step {
  display: grid;

  grid-template-columns: 23px minmax(0, 1fr);

  gap: 7px;

  min-width: 0;

  padding: 6px 7px;

  border: 1px solid #edf1f3;
  border-radius: 7px;

  background: #ffffff;
}

.step-number {
  display: flex;
  align-items: center;
  justify-content: center;

  width: 21px;
  height: 21px;

  border-radius: 50%;

  background: #eef3f7;

  color: #20639b;

  font-family: 'IBM Plex Mono', monospace;

  font-size: 7px;
  font-weight: 700;
}

.step-content {
  min-width: 0;
}

.step-content strong {
  display: block;

  margin-bottom: 2px;

  color: #173f5f;

  font-size: 8px;
}

.step-content p {
  margin: 0;

  color: #64748b;

  font-size: 6.9px;

  line-height: 1.35;
}

.step-content p strong {
  display: inline;

  color: #20639b;

  font-size: inherit;
}


/* =========================================
   PARAMETER
========================================= */

.parameter-box {
  flex: 0 0 auto;

  display: flex;
  align-items: center;

  gap: 8px;

  margin-top: 7px;

  padding: 6px 8px;

  border-radius: 7px;

  background: #f8fafb;
}

.parameter-symbol {
  display: flex;
  align-items: center;
  justify-content: center;

  width: 25px;
  height: 25px;

  border-radius: 5px;

  background: #173f5f;

  color: #ffffff;

  font-family: 'IBM Plex Mono', monospace;

  font-size: 10px;
  font-weight: 700;
}

.parameter-label {
  display: block;

  margin-bottom: 1px;

  color: #94a3b8;

  font-size: 5.5px;
  font-weight: 700;

  letter-spacing: 0.08em;
}

.parameter-box strong {
  color: #173f5f;

  font-size: 7.5px;
}


/* =========================================
   SWAP VISUAL
========================================= */

.swap-visual {
  flex: 0 0 auto;

  display: grid;

  grid-template-columns:
    minmax(0, 1fr)
    70px
    minmax(0, 1fr);

  align-items: center;

  min-height: 82px;

  margin: 8px 0;

  padding: 8px;

  border: 1px solid #dce4e9;
  border-radius: 8px;

  background: #ffffff;
}

.variable-group {
  min-width: 0;

  text-align: center;
}

.selected-variables,
.unselected-variables {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;

  gap: 5px;
}

.selected-variable,
.unselected-variable {
  display: flex;
  align-items: center;
  justify-content: center;

  min-width: 27px;
  height: 25px;

  padding: 0 5px;

  border-radius: 5px;

  font-family: 'IBM Plex Mono', monospace;

  font-size: 7px;
  font-weight: 700;
}

.selected-variable {
  border: 1px solid #2a9d8f;

  background: #f3fbf9;

  color: #287c73;
}

.unselected-variable {
  border: 1px solid #e9c46a;

  background: #fff9e8;

  color: #8a6a12;
}

.swap-symbol {
  display: flex;
  align-items: center;
  justify-content: center;
}

.swap-symbol svg {
  display: block;

  width: 62px;
  height: 48px;

  overflow: visible;
}

.swap-arrow {
  fill: none;

  stroke-width: 1.8;

  stroke-linecap: round;
}

.selected-to-unselected {
  stroke: #2a9d8f;
}

.unselected-to-selected {
  stroke: #e9c46a;
}

.swap-text {
  fill: #173f5f;

  font-family: 'IBM Plex Mono', monospace;

  font-size: 7px;
  font-weight: 700;
}


/* =========================================
   ITERATION
========================================= */

.iteration-box {
  flex: 0 0 auto;

  padding: 7px 9px;

  border-radius: 7px;

  background: #f8fafb;
}

.iteration-title {
  margin-bottom: 6px;

  color: #173f5f;

  font-size: 7.5px;
  font-weight: 700;
}

.iteration-flow {
  display: flex;
  align-items: center;

  gap: 5px;
}

.iteration-step {
  flex: 1;

  display: flex;
  align-items: center;

  gap: 5px;

  min-width: 0;
}

.iteration-number {
  display: flex;
  align-items: center;
  justify-content: center;

  flex: 0 0 auto;

  width: 18px;
  height: 18px;

  border-radius: 50%;

  background: #f3fbf9;

  color: #2a9d8f;

  font-family: 'IBM Plex Mono', monospace;

  font-size: 6.5px;
  font-weight: 700;
}

.iteration-step strong {
  color: #475569;

  font-size: 6.7px;

  line-height: 1.2;
}

.iteration-arrow {
  flex: 0 0 auto;

  color: #94a3b8;

  font-size: 10px;
}


/* =========================================
   STOPPING CONDITIONS
========================================= */

.stopping-box {
  flex: 0 0 auto;

  margin-top: 7px;

  padding: 7px 9px;

  border: 1px solid #c9e6e1;
  border-radius: 7px;

  background: #f3fbf9;
}

.stopping-title {
  margin-bottom: 5px;

  color: #2a9d8f;

  font-size: 6px;
  font-weight: 700;

  letter-spacing: 0.1em;
}

.stopping-conditions {
  display: grid;

  grid-template-columns: 1fr 1fr;

  gap: 6px;
}

.condition {
  display: flex;
  align-items: center;

  gap: 5px;

  color: #64748b;

  font-size: 6.5px;

  line-height: 1.3;
}

.condition-check {
  display: flex;
  align-items: center;
  justify-content: center;

  flex: 0 0 auto;

  width: 16px;
  height: 16px;

  border-radius: 50%;

  background: #2a9d8f;

  color: #ffffff;

  font-size: 7px;
  font-weight: 700;
}

.condition strong {
  color: #173f5f;
}


/* =========================================
   RESULT BOX
========================================= */

.result-box {
  flex: 0 0 auto;

  display: flex;
  align-items: center;

  gap: 7px;

  margin-top: 7px;

  padding: 6px 8px;

  border-radius: 6px;
}

.mifs-result {
  background: #eef3f7;
}

.swap-result {
  background: #f3fbf9;
}

.result-icon {
  display: flex;
  align-items: center;
  justify-content: center;

  width: 20px;
  height: 20px;

  border-radius: 50%;

  background: #ffffff;

  color: #20639b;

  font-size: 10px;
  font-weight: 700;
}

.swap-result .result-icon {
  color: #2a9d8f;
}

.result-label {
  display: block;

  margin-bottom: 1px;

  color: #94a3b8;

  font-size: 5.5px;
  font-weight: 700;

  letter-spacing: 0.08em;
}

.result-box strong {
  color: #173f5f;

  font-size: 7.5px;
}


/* =========================================
   BOTTOM MESSAGE
========================================= */

.bottom-message {
  flex: 0 0 auto;

  display: flex;
  align-items: center;

  min-height: 36px;

  margin: 10px 8px 0;

  padding: 6px 12px;

  border: 1px solid #dce4e9;
  border-radius: 8px;

  background: #ffffff;
}

.bottom-label {
  flex: 0 0 auto;

  margin-right: 12px;

  color: #2a9d8f;

  font-size: 6.5px;
  font-weight: 700;

  letter-spacing: 0.1em;
}

.bottom-text {
  color: #64748b;

  font-size: 7.8px;

  line-height: 1.3;
}

.bottom-text strong {
  color: #173f5f;
}
</style>