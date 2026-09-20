<template>
  <div class="datasets-slide">

    <div class="intro">
      Two complementary datasets are used to evaluate the proposed GRN inference method.
    </div>

    <div class="datasets-grid">

      <!-- ========================= -->
      <!-- Artificial Discretized -->
      <!-- ========================= -->
      <section class="dataset-card">

        <div class="card-header">
          <div>
            <div class="dataset-index">01</div>
            <h2>Artificial Discretized Dataset</h2>
          </div>

          <div class="data-type discrete">
            DISCRETE
          </div>
        </div>

        <div class="dataset-description">
          Gene expression profiles represented by three discrete levels:
          <strong>0, 1, and 2</strong>.
        </div>

        <!-- Expression table -->
        <div class="expression-wrapper">
          <div class="table-label">
            Gene expression profile
          </div>

          <table class="expression-table">
            <thead>
              <tr>
                <th>Time</th>
                <th>Gene 1</th>
                <th>Gene 2</th>
                <th>Gene 3</th>
                <th>Gene 4</th>
                <th>Gene 5</th>
              </tr>
            </thead>

            <tbody>
              <tr>
                <th>t₁</th>
                <td class="level-0">0</td>
                <td class="level-2">2</td>
                <td class="level-1">1</td>
                <td class="level-0">0</td>
                <td class="level-2">2</td>
              </tr>

              <tr>
                <th>t₂</th>
                <td class="level-1">1</td>
                <td class="level-2">2</td>
                <td class="level-1">1</td>
                <td class="level-1">1</td>
                <td class="level-0">0</td>
              </tr>

              <tr>
                <th>t₃</th>
                <td class="level-2">2</td>
                <td class="level-1">1</td>
                <td class="level-0">0</td>
                <td class="level-2">2</td>
                <td class="level-1">1</td>
              </tr>

              <tr>
                <th>t₄</th>
                <td class="level-2">2</td>
                <td class="level-0">0</td>
                <td class="level-1">1</td>
                <td class="level-2">2</td>
                <td class="level-2">2</td>
              </tr>

              <tr>
                <th>t₅</th>
                <td class="level-1">1</td>
                <td class="level-0">0</td>
                <td class="level-2">2</td>
                <td class="level-1">1</td>
                <td class="level-0">0</td>
              </tr>
            </tbody>
          </table>

          <div class="value-legend">
            <span>
              <i class="legend-box level-0"></i>
              0
            </span>
            <span>
              <i class="legend-box level-1"></i>
              1
            </span>
            <span>
              <i class="legend-box level-2"></i>
              2
            </span>
          </div>
        </div>

        <!-- Dataset statistics -->
        <div class="stats-grid">
          <div class="stat">
            <span class="stat-value">20</span>
            <span class="stat-label">Network groups</span>
          </div>

          <div class="stat">
            <span class="stat-value">10–200</span>
            <span class="stat-label">Network size</span>
          </div>

          <div class="stat">
            <span class="stat-value">20</span>
            <span class="stat-label">Networks / group</span>
          </div>

          <div class="stat total">
            <span class="stat-value">400</span>
            <span class="stat-label">Total networks</span>
          </div>
        </div>

      </section>


      <!-- ========================= -->
      <!-- GWN -->
      <!-- ========================= -->
      <section class="dataset-card">

        <div class="card-header">
          <div>
            <div class="dataset-index">02</div>
            <h2>GWN Dataset</h2>
          </div>

          <div class="data-type continuous">
            CONTINUOUS
          </div>
        </div>

        <div class="dataset-description">
          Gene expression profiles generated using
          <strong>GeneNetWeaver (GNW)</strong>, represented as continuous values.
        </div>

        <!-- Expression table -->
        <div class="expression-wrapper">
          <div class="table-label">
            Gene expression profile
          </div>

          <table class="expression-table continuous-table">
            <thead>
              <tr>
                <th>Time</th>
                <th>Gene 1</th>
                <th>Gene 2</th>
                <th>Gene 3</th>
                <th>Gene 4</th>
                <th>Gene 5</th>
              </tr>
            </thead>

            <tbody>
              <tr>
                <th>t₁</th>
                <td>0.37</td>
                <td>1.82</td>
                <td>0.64</td>
                <td>2.15</td>
                <td>1.04</td>
              </tr>

              <tr>
                <th>t₂</th>
                <td>0.52</td>
                <td>1.67</td>
                <td>0.81</td>
                <td>2.03</td>
                <td>1.26</td>
              </tr>

              <tr>
                <th>t₃</th>
                <td>0.91</td>
                <td>1.31</td>
                <td>1.08</td>
                <td>1.74</td>
                <td>1.53</td>
              </tr>

              <tr>
                <th>t₄</th>
                <td>1.24</td>
                <td>1.05</td>
                <td>1.42</td>
                <td>1.38</td>
                <td>1.71</td>
              </tr>

              <tr>
                <th>t₅</th>
                <td>1.58</td>
                <td>0.82</td>
                <td>1.73</td>
                <td>1.12</td>
                <td>1.89</td>
              </tr>
            </tbody>
          </table>

          <div class="continuous-note">
            Continuous expression values
          </div>
        </div>

        <!-- Dataset statistics -->
        <div class="stats-grid">
          <div class="stat">
            <span class="stat-value">4</span>
            <span class="stat-label">Network groups</span>
          </div>

          <div class="stat">
            <span class="stat-value">50–300</span>
            <span class="stat-label">Network size</span>
          </div>

          <div class="stat">
            <span class="stat-value">20</span>
            <span class="stat-label">Networks / group</span>
          </div>

          <div class="stat total">
            <span class="stat-value">80</span>
            <span class="stat-label">Total networks</span>
          </div>
        </div>

      </section>

    </div>

    <!-- Bottom message -->
    <!-- <div class="bottom-message">
      <span class="bottom-label">EVALUATION DATASETS</span>

      <span class="bottom-text">
        <strong>400 artificial networks</strong>
        +
        <strong>80 GWN networks</strong>
        provide complementary evaluation settings:
        <span class="emphasis">discrete</span> vs.
        <span class="emphasis">continuous</span> expression data.
      </span>
    </div> -->

  </div>
</template>


<style scoped>
.datasets-slide {
  width: 100%;
  height: 100%;
  min-height: 0;
  display: flex;
  flex-direction: column;
  box-sizing: border-box;
  overflow: hidden;
}

/* =========================
   Intro
   ========================= */

.intro {
  margin-bottom: 14px;
  color: #64748b;
  font-size: 14px;
  line-height: 1.45;
}


/* =========================
   Main grid
   ========================= */

.datasets-grid {
  flex: 1 1 auto;
  min-height: 0;

  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
}


/* =========================
   Dataset card
   ========================= */

.dataset-card {
  min-width: 0;
  min-height: 0;

  display: flex;
  flex-direction: column;

  padding: 18px 20px;

  background: #ffffff;
  border: 1px solid #dce4e9;
  border-radius: 12px;

  box-sizing: border-box;

  box-shadow:
    0 2px 8px rgba(23, 63, 95, 0.04);
}


/* =========================
   Header
   ========================= */

.card-header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;

  margin-bottom: 8px;
}

.dataset-index {
  margin-bottom: 3px;

  color: #20639b;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 10px;
  font-weight: 700;
  letter-spacing: 0.08em;
}

.card-header h2 {
  margin: 0;

  color: #173f5f;

  font-size: 20px;
  font-weight: 700;
  line-height: 1.2;
}


/* =========================
   Data type badge
   ========================= */

.data-type {
  padding: 5px 9px;

  border-radius: 5px;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 9px;
  font-weight: 700;
  letter-spacing: 0.08em;
}

.data-type.discrete {
  color: #20639b;
  background: #eaf2f8;
  border: 1px solid #cbddea;
}

.data-type.continuous {
  color: #2a7f72;
  background: #eaf6f4;
  border: 1px solid #c9e5df;
}


/* =========================
   Description
   ========================= */

.dataset-description {
  min-height: 38px;

  margin-bottom: 10px;

  color: #64748b;

  font-size: 12px;
  line-height: 1.45;
}

.dataset-description strong {
  color: #24313a;
  font-weight: 700;
}


/* =========================
   Expression table
   ========================= */

.expression-wrapper {
  flex: 1 1 auto;
  min-height: 0;

  display: flex;
  flex-direction: column;
}

.table-label {
  margin-bottom: 5px;

  color: #64748b;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 9px;
  font-weight: 600;
  letter-spacing: 0.04em;
  text-transform: uppercase;
}

.expression-table {
  width: 100%;

  border-collapse: separate;
  border-spacing: 0;

  table-layout: fixed;

  border: 1px solid #dce4e9;
  border-radius: 7px;

  overflow: hidden;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 10px;
}

.expression-table th,
.expression-table td {
  height: 27px;

  padding: 0 4px;

  text-align: center;

  border-right: 1px solid #e5eaee;
  border-bottom: 1px solid #e5eaee;

  box-sizing: border-box;
}

.expression-table th:last-child,
.expression-table td:last-child {
  border-right: none;
}

.expression-table tbody tr:last-child th,
.expression-table tbody tr:last-child td {
  border-bottom: none;
}

.expression-table thead th {
  color: #173f5f;
  background: #f1f5f7;

  font-size: 9px;
  font-weight: 700;
}

.expression-table tbody th {
  width: 48px;

  color: #64748b;
  background: #f8fafb;

  font-size: 9px;
  font-weight: 600;
}

.expression-table td {
  color: #24313a;
  background: #ffffff;

  font-weight: 600;
}


/* =========================
   Discrete values
   ========================= */

.expression-table .level-0 {
  background: #f4f7f9;
  color: #64748b;
}

.expression-table .level-1 {
  background: #e7f0f6;
  color: #20639b;
}

.expression-table .level-2 {
  background: #cfe1ed;
  color: #173f5f;
}


/* =========================
   Continuous table
   ========================= */

.continuous-table td {
  color: #2a6f67;
  background: #f4faf9;

  font-weight: 500;
}

.continuous-table tbody tr:nth-child(even) td {
  background: #eef7f5;
}


/* =========================
   Legends
   ========================= */

.value-legend {
  display: flex;
  align-items: center;
  gap: 12px;

  margin-top: 6px;

  color: #64748b;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 9px;
}

.value-legend span {
  display: flex;
  align-items: center;
  gap: 4px;
}

.legend-box {
  width: 9px;
  height: 9px;

  border: 1px solid #d0d9df;
  border-radius: 2px;
  box-sizing: border-box;
}

.legend-box.level-0 {
  background: #f4f7f9;
}

.legend-box.level-1 {
  background: #e7f0f6;
}

.legend-box.level-2 {
  background: #cfe1ed;
}

.continuous-note {
  margin-top: 6px;

  color: #64748b;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 9px;
}


/* =========================
   Statistics
   ========================= */

.stats-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);

  margin-top: 12px;

  border-top: 1px solid #e5eaee;
  padding-top: 10px;
}

.stat {
  min-width: 0;

  display: flex;
  flex-direction: column;
  align-items: center;

  padding: 0 5px;

  border-right: 1px solid #e5eaee;
}

.stat:last-child {
  border-right: none;
}

.stat-value {
  color: #173f5f;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 14px;
  font-weight: 700;
  line-height: 1.2;
}

.stat-label {
  margin-top: 3px;

  color: #64748b;

  font-size: 8px;
  line-height: 1.2;
  text-align: center;
}

.stat.total .stat-value {
  color: #20639b;
}


/* =========================
   Bottom message
   ========================= */

.bottom-message {
  flex-shrink: 0;

  display: flex;
  align-items: center;
  gap: 12px;

  margin-top: 12px;
  padding: 9px 13px;

  background: #f1f5f7;
  border-left: 3px solid #20639b;
  border-radius: 5px;

  color: #64748b;

  font-size: 10px;
  line-height: 1.35;
}

.bottom-label {
  flex-shrink: 0;

  color: #20639b;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 9px;
  font-weight: 700;
  letter-spacing: 0.06em;
}

.bottom-text strong {
  color: #24313a;
}

.emphasis {
  color: #20639b;
  font-weight: 700;
}
</style>