<template>
  <div class="discretization-slide">

    <div class="intro">
      MIDNI evaluates both <strong>two-level</strong> and
      <strong>three-level</strong> discretization and selects the level
      that minimizes the validity index.
    </div>

    <div class="content-grid">

      <!-- LEFT: VALIDITY INDEX -->
      <section class="explanation">

        <!-- <div class="motivation-box">
          <div class="box-label">WHY NOT ONLY BOOLEAN?</div>

          <div class="comparison-row">
            <div class="comparison-item">
              <span class="state-badge boolean">2</span>
              <div>
                <strong>Boolean</strong>
                <p>Fast, but may lose expression-level information.</p>
              </div>
            </div>

            <div class="comparison-item">
              <span class="state-badge three">3</span>
              <div>
                <strong>Higher-level</strong>
                <p>Preserves more variation in gene expression.</p>
              </div>
            </div>
          </div>
        </div> -->


        <div class="validity-card">

          <div class="card-header">
            <div>
              <div class="card-label">VALIDITY INDEX</div>
              <h2>Select the optimal number of clusters</h2>
            </div>

            <div class="minimize-badge">
              MINIMIZE
            </div>
          </div>

          <div class="formula">
            <span class="formula-main">
              Validity =
            </span>

            <span class="fraction">
              <span class="top">Intra</span>
              <span class="bottom">Inter</span>
            </span>
          </div>

          <div class="definition-grid">

            <div class="definition">
              <div class="definition-icon intra-icon">
                <span>↔</span>
              </div>

              <div>
                <strong>Intra</strong>
                <p>
                  Average within-cluster dispersion
                  around each cluster center.
                </p>
              </div>
            </div>

            <div class="definition">
              <div class="definition-icon inter-icon">
                <span>↕</span>
              </div>

              <div>
                <strong>Inter</strong>
                <p>
                  Minimum distance between
                  different cluster centers.
                </p>
              </div>
            </div>

          </div>

          <div class="rule-box">
            <span class="rule-icon">✓</span>

            <div>
              <span class="rule-label">SELECTION RULE</span>
              <strong>Choose K that minimizes the Validity Index.</strong>
            </div>
          </div>

        </div>


        <div class="process-box">

          <div class="process-title">
            Discretization procedure
          </div>

          <div class="process">

            <div class="process-step">
              <span>1</span>
              <strong>Cluster</strong>
              <small>K-means</small>
            </div>

            <div class="process-arrow">→</div>

            <div class="process-step">
              <span>2</span>
              <strong>Evaluate</strong>
              <small>Validity Index</small>
            </div>

            <div class="process-arrow">→</div>

            <div class="process-step selected-step">
              <span>3</span>
              <strong>Select</strong>
              <small>Minimum value</small>
            </div>

          </div>

        </div>

      </section>


      <!-- RIGHT: SCATTER CHARTS -->
      <section class="charts">

        <!-- K = 2 -->
        <div class="chart-card">

          <div class="chart-header">
            <div>
              <span class="chart-k">K = 2</span>
              <strong>Two-level discretization</strong>
            </div>

            <div class="validity-value">
              <span>Validity</span>
              <strong>0.0633</strong>
            </div>
          </div>

          <svg
            class="scatter-chart"
            viewBox="0 0 500 220"
            aria-label="K equals 2 discretization"
          >

            <!-- horizontal grid -->
            <line x1="52" y1="25" x2="478" y2="25" class="grid-line" />
            <line x1="52" y1="65" x2="478" y2="65" class="grid-line" />
            <line x1="52" y1="105" x2="478" y2="105" class="grid-line" />
            <line x1="52" y1="145" x2="478" y2="145" class="grid-line" />
            <line x1="52" y1="185" x2="478" y2="185" class="grid-line" />

            <!-- axes -->
            <line x1="52" y1="185" x2="478" y2="185" class="axis-line" />
            <line x1="52" y1="25" x2="52" y2="185" class="axis-line" />

            <!-- y labels -->
            <text x="43" y="29" text-anchor="end" class="axis-label">1.0</text>
            <text x="43" y="69" text-anchor="end" class="axis-label">0.75</text>
            <text x="43" y="109" text-anchor="end" class="axis-label">0.50</text>
            <text x="43" y="149" text-anchor="end" class="axis-label">0.25</text>
            <text x="43" y="189" text-anchor="end" class="axis-label">0</text>

            <!-- x labels -->
            <text x="52" y="202" text-anchor="middle" class="axis-label">0</text>
            <text x="265" y="202" text-anchor="middle" class="axis-label">125</text>
            <text x="478" y="202" text-anchor="middle" class="axis-label">250</text>

            <!-- y axis title -->
            <text
              x="12"
              y="105"
              text-anchor="middle"
              transform="rotate(-90 12 105)"
              class="axis-title"
            >
              Gene expression value
            </text>

            <!-- x axis title -->
            <text x="265" y="217" text-anchor="middle" class="axis-title">
              Time point
            </text>

            <!-- K=2 clusters -->
            <g>
              <circle cx="72" cy="159.4" r="5" class="point cluster-a" />
              <circle cx="94" cy="156.2" r="5" class="point cluster-a" />
              <circle cx="116" cy="149.8" r="5" class="point cluster-a" />
              <circle cx="138" cy="109.8" r="5" class="point cluster-a" />
              <circle cx="160" cy="106.6" r="5" class="point cluster-a" />
              <circle cx="182" cy="101.8" r="5" class="point cluster-a" />
              <circle cx="204" cy="58.6" r="5" class="point cluster-b" />
              <circle cx="226" cy="53.8" r="5" class="point cluster-b" />
              <circle cx="248" cy="50.6" r="5" class="point cluster-b" />
              <circle cx="270" cy="156.2" r="5" class="point cluster-a" />
              <circle cx="292" cy="153.0" r="5" class="point cluster-a" />
              <circle cx="314" cy="108.2" r="5" class="point cluster-a" />
              <circle cx="336" cy="103.4" r="5" class="point cluster-a" />
              <circle cx="358" cy="57.0" r="5" class="point cluster-b" />
              <circle cx="380" cy="52.2" r="5" class="point cluster-b" />
              <circle cx="402" cy="47.4" r="5" class="point cluster-b" />
              <circle cx="424" cy="157.8" r="5" class="point cluster-a" />
              <circle cx="446" cy="105.0" r="5" class="point cluster-a" />
              <circle cx="468" cy="55.4" r="5" class="point cluster-b" />
            </g>

            <!-- cluster centers -->
            <line x1="60" y1="130" x2="470" y2="130" class="center-line-a" />
            <line x1="60" y1="57" x2="470" y2="57" class="center-line-b" />

            <text x="466" y="126" text-anchor="end" class="center-label-a">
              Cluster 1
            </text>

            <text x="466" y="53" text-anchor="end" class="center-label-b">
              Cluster 2
            </text>

          </svg>

        </div>


        <!-- K = 3 -->
        <div class="chart-card selected-chart">

          <div class="chart-header">
            <div>
              <span class="chart-k">K = 3</span>
              <strong>Three-level discretization</strong>
            </div>

            <div class="validity-value selected-validity">
              <span>Validity</span>
              <strong>0.0041</strong>
            </div>
          </div>

          <svg
            class="scatter-chart"
            viewBox="0 0 500 220"
            aria-label="K equals 3 discretization"
          >

            <!-- horizontal grid -->
            <line x1="52" y1="25" x2="478" y2="25" class="grid-line" />
            <line x1="52" y1="65" x2="478" y2="65" class="grid-line" />
            <line x1="52" y1="105" x2="478" y2="105" class="grid-line" />
            <line x1="52" y1="145" x2="478" y2="145" class="grid-line" />
            <line x1="52" y1="185" x2="478" y2="185" class="grid-line" />

            <!-- axes -->
            <line x1="52" y1="185" x2="478" y2="185" class="axis-line" />
            <line x1="52" y1="25" x2="52" y2="185" class="axis-line" />

            <!-- y labels -->
            <text x="43" y="29" text-anchor="end" class="axis-label">1.0</text>
            <text x="43" y="69" text-anchor="end" class="axis-label">0.75</text>
            <text x="43" y="109" text-anchor="end" class="axis-label">0.50</text>
            <text x="43" y="149" text-anchor="end" class="axis-label">0.25</text>
            <text x="43" y="189" text-anchor="end" class="axis-label">0</text>

            <!-- x labels -->
            <text x="52" y="202" text-anchor="middle" class="axis-label">0</text>
            <text x="265" y="202" text-anchor="middle" class="axis-label">125</text>
            <text x="478" y="202" text-anchor="middle" class="axis-label">250</text>

            <!-- y axis title -->
            <text
              x="12"
              y="105"
              text-anchor="middle"
              transform="rotate(-90 12 105)"
              class="axis-title"
            >
              Gene expression value
            </text>

            <!-- x axis title -->
            <text x="265" y="217" text-anchor="middle" class="axis-title">
              Time point
            </text>

            <!-- K=3 clusters -->
            <g>
              <!-- low -->
              <circle cx="72" cy="159.4" r="5" class="point cluster-low" />
              <circle cx="94" cy="156.2" r="5" class="point cluster-low" />
              <circle cx="116" cy="149.8" r="5" class="point cluster-low" />
              <circle cx="270" cy="156.2" r="5" class="point cluster-low" />
              <circle cx="292" cy="153.0" r="5" class="point cluster-low" />
              <circle cx="424" cy="157.8" r="5" class="point cluster-low" />

              <!-- middle -->
              <circle cx="138" cy="109.8" r="5" class="point cluster-mid" />
              <circle cx="160" cy="106.6" r="5" class="point cluster-mid" />
              <circle cx="182" cy="101.8" r="5" class="point cluster-mid" />
              <circle cx="314" cy="108.2" r="5" class="point cluster-mid" />
              <circle cx="336" cy="103.4" r="5" class="point cluster-mid" />
              <circle cx="446" cy="105.0" r="5" class="point cluster-mid" />

              <!-- high -->
              <circle cx="204" cy="58.6" r="5" class="point cluster-high" />
              <circle cx="226" cy="53.8" r="5" class="point cluster-high" />
              <circle cx="248" cy="50.6" r="5" class="point cluster-high" />
              <circle cx="358" cy="57.0" r="5" class="point cluster-high" />
              <circle cx="380" cy="52.2" r="5" class="point cluster-high" />
              <circle cx="402" cy="47.4" r="5" class="point cluster-high" />
              <circle cx="468" cy="55.4" r="5" class="point cluster-high" />
            </g>

            <!-- cluster centers -->
            <line x1="60" y1="155" x2="470" y2="155" class="center-line-low" />
            <line x1="60" y1="106" x2="470" y2="106" class="center-line-mid" />
            <line x1="60" y1="53" x2="470" y2="53" class="center-line-high" />

            <text x="466" y="151" text-anchor="end" class="center-label-low">
              Low
            </text>

            <text x="466" y="102" text-anchor="end" class="center-label-mid">
              Medium
            </text>

            <text x="466" y="49" text-anchor="end" class="center-label-high">
              High
            </text>

          </svg>

        </div>

      </section>

    </div>


    <div class="takeaway">
      <div class="takeaway-label">KEY OBSERVATION</div>

      <div class="takeaway-content">
        <span>
          K = 3 produces
          <strong>tighter and better-separated clusters</strong>,
          resulting in a lower validity index.
        </span>

        <span class="result">
          0.0041 &lt; 0.0633
        </span>
      </div>
    </div>

  </div>
</template>

<script setup>
</script>

<style scoped>
.discretization-slide {
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

  margin: 0 8px 11px;

  max-width: 1050px;

  color: #64748b;

  font-size: 10.5px;
  line-height: 1.4;
}

.intro strong {
  color: #173f5f;
}


/* ---------- MAIN GRID ---------- */

.content-grid {
  flex: 1 1 auto;

  min-height: 0;
  min-width: 0;

  display: grid;

  grid-template-columns:
    minmax(0, 0.9fr)
    minmax(0, 1.35fr);

  gap: 15px;
}


/* ---------- LEFT ---------- */

.explanation {
  min-width: 0;
  min-height: 0;

  display: flex;
  flex-direction: column;

  gap: 10px;
}


/* ---------- MOTIVATION ---------- */

.motivation-box {
  flex: 0 0 auto;

  padding: 10px 12px;

  border: 1px solid #dce4e9;
  border-radius: 10px;

  background: #ffffff;
}

.box-label {
  margin-bottom: 8px;

  color: #2a9d8f;

  font-size: 7px;
  font-weight: 700;

  letter-spacing: 0.12em;
}

.comparison-row {
  display: grid;

  grid-template-columns: 1fr 1fr;

  gap: 8px;
}

.comparison-item {
  display: flex;
  align-items: center;

  gap: 7px;

  min-width: 0;
}

.state-badge {
  flex: 0 0 auto;

  display: flex;
  align-items: center;
  justify-content: center;

  width: 27px;
  height: 27px;

  border-radius: 7px;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 11px;
  font-weight: 700;
}

.state-badge.boolean {
  border: 1px solid #dce4e9;

  background: #f8fafb;

  color: #64748b;
}

.state-badge.three {
  border: 1px solid #c9e6e1;

  background: #f3fbf9;

  color: #2a9d8f;
}

.comparison-item strong {
  display: block;

  color: #173f5f;

  font-size: 9px;
}

.comparison-item p {
  margin: 2px 0 0;

  color: #64748b;

  font-size: 7.3px;
  line-height: 1.3;
}


/* ---------- VALIDITY CARD ---------- */

.validity-card {
  flex: 1 1 auto;

  min-height: 0;

  padding: 12px 13px;

  border: 1px solid #2a9d8f;
  border-radius: 11px;

  background: #ffffff;

  box-shadow:
    0 4px 16px rgba(42, 157, 143, 0.07);
}

.card-header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;

  gap: 8px;
}

.card-label {
  margin-bottom: 3px;

  color: #2a9d8f;

  font-size: 7px;
  font-weight: 700;

  letter-spacing: 0.11em;
}

.card-header h2 {
  margin: 0;

  color: #173f5f;

  font-size: 12px;
  line-height: 1.25;
}

.minimize-badge {
  flex: 0 0 auto;

  padding: 4px 7px;

  border: 1px solid #e9c46a;
  border-radius: 4px;

  background: #fff9e8;

  color: #8a6a12;

  font-size: 6.5px;
  font-weight: 700;

  letter-spacing: 0.08em;
}


/* ---------- FORMULA ---------- */

.formula {
  display: flex;
  align-items: center;
  justify-content: center;

  gap: 7px;

  margin: 11px 0 12px;

  color: #173f5f;

  font-family: 'IBM Plex Mono', monospace;
}

.formula-main {
  font-size: 15px;
  font-weight: 600;
}

.fraction {
  display: inline-flex;
  flex-direction: column;

  align-items: center;

  font-size: 11px;
  line-height: 1.1;
}

.fraction .top {
  padding: 0 9px 3px;

  border-bottom: 1.5px solid #173f5f;
}

.fraction .bottom {
  padding-top: 3px;
}


/* ---------- DEFINITIONS ---------- */

.definition-grid {
  display: grid;

  grid-template-columns: 1fr 1fr;

  gap: 8px;
}

.definition {
  display: flex;

  gap: 7px;

  min-width: 0;

  padding: 8px;

  border-radius: 7px;

  background: #f8fafb;
}

.definition-icon {
  flex: 0 0 auto;

  display: flex;
  align-items: center;
  justify-content: center;

  width: 25px;
  height: 25px;

  border-radius: 6px;

  font-size: 13px;
  font-weight: 700;
}

.intra-icon {
  background: #eef3f7;
  color: #20639b;
}

.inter-icon {
  background: #f3fbf9;
  color: #2a9d8f;
}

.definition strong {
  display: block;

  color: #173f5f;

  font-size: 8.5px;
}

.definition p {
  margin: 3px 0 0;

  color: #64748b;

  font-size: 6.8px;
  line-height: 1.35;
}


/* ---------- RULE ---------- */

.rule-box {
  display: flex;
  align-items: center;

  gap: 8px;

  margin-top: 9px;
  padding: 8px;

  border-radius: 7px;

  background: #f3fbf9;
}

.rule-icon {
  flex: 0 0 auto;

  display: flex;
  align-items: center;
  justify-content: center;

  width: 23px;
  height: 23px;

  border-radius: 50%;

  background: #2a9d8f;

  color: #ffffff;

  font-size: 11px;
  font-weight: 700;
}

.rule-label {
  display: block;

  margin-bottom: 2px;

  color: #2a9d8f;

  font-size: 6.5px;
  font-weight: 700;

  letter-spacing: 0.08em;
}

.rule-box strong {
  color: #173f5f;

  font-size: 8px;
}


/* ---------- PROCEDURE ---------- */

.process-box {
  flex: 0 0 auto;

  padding: 8px 10px;

  border: 1px solid #dce4e9;
  border-radius: 9px;

  background: #ffffff;
}

.process-title {
  margin-bottom: 7px;

  color: #173f5f;

  font-size: 8px;
  font-weight: 700;
}

.process {
  display: flex;
  align-items: center;

  gap: 5px;
}

.process-step {
  flex: 1;

  display: grid;

  grid-template-columns: 20px 1fr;

  column-gap: 5px;

  align-items: center;

  min-width: 0;
}

.process-step > span {
  grid-row: span 2;

  display: flex;
  align-items: center;
  justify-content: center;

  width: 20px;
  height: 20px;

  border-radius: 50%;

  background: #eef3f7;

  color: #20639b;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 7px;
  font-weight: 700;
}

.process-step strong {
  color: #173f5f;

  font-size: 7px;
}

.process-step small {
  color: #64748b;

  font-size: 6px;
}

.selected-step > span {
  background: #2a9d8f;
  color: #ffffff;
}

.process-arrow {
  flex: 0 0 auto;

  color: #94a3b8;

  font-size: 12px;
}


/* ---------- CHARTS ---------- */

.charts {
  min-width: 0;
  min-height: 0;

  display: grid;

  grid-template-rows: 1fr 1fr;

  gap: 10px;
}

.chart-card {
  min-width: 0;
  min-height: 0;

  display: flex;
  flex-direction: column;

  padding: 8px 10px 4px;

  border: 1px solid #dce4e9;
  border-radius: 10px;

  background: #ffffff;

  box-sizing: border-box;
}

.selected-chart {
  border-color: #2a9d8f;

  box-shadow:
    0 3px 12px rgba(42, 157, 143, 0.08);
}

.chart-header {
  flex: 0 0 auto;

  display: flex;
  align-items: center;
  justify-content: space-between;

  margin-bottom: 2px;

  gap: 8px;
}

.chart-header > div:first-child {
  display: flex;
  align-items: center;

  gap: 7px;

  min-width: 0;
}

.chart-k {
  display: inline-flex;
  align-items: center;
  justify-content: center;

  min-width: 28px;
  height: 18px;

  border-radius: 4px;

  background: #eef3f7;

  color: #20639b;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 7px;
  font-weight: 700;
}

.selected-chart .chart-k {
  background: #f3fbf9;
  color: #2a9d8f;
}

.chart-header strong {
  color: #173f5f;

  font-size: 8.5px;
}

.validity-value {
  flex: 0 0 auto;

  display: flex;
  align-items: baseline;

  gap: 4px;
}

.validity-value span {
  color: #64748b;

  font-size: 6.5px;
}

.validity-value strong {
  color: #20639b;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 8px;
}

.selected-validity strong {
  color: #2a9d8f;
}


/* ---------- SVG ---------- */

.scatter-chart {
  display: block;

  width: 100%;
  height: auto;

  min-height: 0;

  overflow: visible;
}

.grid-line {
  stroke: #edf1f3;
  stroke-width: 1;
}

.axis-line {
  stroke: #94a3b8;
  stroke-width: 1.2;
}

.axis-label {
  fill: #94a3b8;

  font-family: 'IBM Plex Mono', monospace;

  font-size: 7px;
}

.axis-title {
  fill: #64748b;

  font-size: 7px;
  font-weight: 600;
}


/* ---------- POINTS ---------- */

.point {
  stroke: #ffffff;
  stroke-width: 1.3;
}

.cluster-a {
  fill: #20639b;
}

.cluster-b {
  fill: #2a9d8f;
}

.cluster-low {
  fill: #20639b;
}

.cluster-mid {
  fill: #2a9d8f;
}

.cluster-high {
  fill: #e9c46a;
}


/* ---------- CENTERS ---------- */

.center-line-a,
.center-line-b,
.center-line-low,
.center-line-mid,
.center-line-high {
  stroke-width: 1;

  stroke-dasharray: 4 4;

  opacity: 0.6;
}

.center-line-a {
  stroke: #20639b;
}

.center-line-b {
  stroke: #2a9d8f;
}

.center-line-low {
  stroke: #20639b;
}

.center-line-mid {
  stroke: #2a9d8f;
}

.center-line-high {
  stroke: #e9c46a;
}

.center-label-a,
.center-label-b,
.center-label-low,
.center-label-mid,
.center-label-high {
  font-size: 6px;
  font-weight: 600;
}

.center-label-a {
  fill: #20639b;
}

.center-label-b {
  fill: #2a9d8f;
}

.center-label-low {
  fill: #20639b;
}

.center-label-mid {
  fill: #2a9d8f;
}

.center-label-high {
  fill: #9a7b19;
}


/* ---------- TAKEAWAY ---------- */

.takeaway {
  flex: 0 0 auto;

  display: flex;
  align-items: center;

  min-height: 37px;

  margin: 10px 8px 0;
  padding: 6px 13px;

  border: 1px solid #dce4e9;
  border-radius: 9px;

  background: #ffffff;
}

.takeaway-label {
  flex: 0 0 auto;

  margin-right: 12px;

  color: #2a9d8f;

  font-size: 6.5px;
  font-weight: 700;

  letter-spacing: 0.1em;
}

.takeaway-content {
  flex: 1;

  display: flex;
  align-items: center;
  justify-content: space-between;

  gap: 10px;

  color: #64748b;

  font-size: 8px;
}

.takeaway-content strong {
  color: #173f5f;
}

.result {
  flex: 0 0 auto;

  padding: 4px 8px;

  border-radius: 4px;

  background: #f3fbf9;

  color: #2a9d8f;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 8px;
  font-weight: 700;
}
</style>