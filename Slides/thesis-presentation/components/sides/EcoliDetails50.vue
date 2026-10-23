<script setup>
import { computed, ref } from 'vue'

const models = [
  { name: 'LR', values: [0.1619, 0.0703, 0.0931, 0.1441, 0.0732, 0.0955, 0.0761, 0.0663], avg: 0.0976 },
  { name: 'DT', values: [0.1043, 0.2552, 0.1338, 0.1849, 0.1856, 0.3494, 0.1911, 0.1508], avg: 0.1944 },
  { name: 'RF', values: [0.0593, 0.0182, 0.1664, 0.3088, 0.0692, 0.0188, 0.1762, 0.1433], avg: 0.1200, bold: [3] },
  { name: 'KNN', values: [0.1859, 0.0540, 0.0897, 0.0905, 0.0432, 0.0419, 0.1463, 0.1406], avg: 0.0990 },
  { name: 'XGBoost', values: [0.1498, 0.0757, 0.1004, 0.1884, 0.2365, 0.0923, 0.1192, 0.1148], avg: 0.1346, bold: [4] },
  { name: 'LGBM', values: [0.4383, 0.0765, 0.1100, 0.1988, 0.2242, 0.0936, 0.1345, 0.1583], avg: 0.1793, bold: [0] },
  { name: 'MLP', values: [0.2958, 0.0785, 0.1150, 0.1764, 0.0922, 0.0637, 0.1216, 0.1295], avg: 0.1341 },
  { name: 'GNB', values: [0.4207, 0.4790, 0.2996, 0.2929, 0.4240, 0.3910, 0.2697, 0.2657], avg: 0.3553, bold: [1, 2, 4, 5, 6, 7], boldAvg: true },
  { name: 'Baseline', values: [0.0378, 0.0373, 0.0445, 0.0434, 0.0398, 0.0392, 0.0495, 0.0502], avg: 0.0427, baseline: true },
  { name: 'Jump3', values: [0.0451, 0.0451, 0.0475, 0.0475, 0.0589, 0.0589, 0.0492, 0.0492], avg: 0.0502, baseline: true },
  { name: 'Inferelator', values: [0.0406, 0.0352, 0.0477, 0.0517, 0.0293, 0.0387, 0.0400, 0.0364], avg: 0.0400, baseline: true },
  { name: 'CLR-lag', values: [0.0409, 0.0350, 0.0472, 0.0401, 0.0364, 0.0508, 0.0546, 0.0534], avg: 0.0448, baseline: true },
  { name: 'TSNI', values: [0.0482, 0.0334, 0.0498, 0.0451, 0.0442, 0.0590, 0.0506, 0.0471], avg: 0.0472, baseline: true },
  { name: 'G1DBN', values: [0.0400, 0.0373, 0.0439, 0.0450, 0.0387, 0.0396, 0.0481, 0.0490], avg: 0.0427, baseline: true },
]

const search = ref('')
const tableScroll = ref(null)

const filteredModels = computed(() => {
  const query = search.value.trim().toLowerCase()
  if (!query) return models
  return models.filter(model => model.name.toLowerCase().includes(query))
})

function isBold(model, index) {
  return model.bold?.includes(index) ?? false
}

function scrollTable(direction) {
  if (!tableScroll.value) return
  tableScroll.value.scrollBy({
    left: direction * 360,
    behavior: 'smooth',
  })
}
</script>

<template>
  <section class="aupr-slide">

    <div ref="tableScroll" class="table-scroll">
      <table>
        <colgroup>
          <col class="model-col" />
          <col v-for="i in 8" :key="i" class="score-col" />
          <col class="average-col" />
        </colgroup>

        <thead>
          <tr class="group-row">
            <th class="model-header sticky-model" rowspan="3">Model</th>
            <th colspan="8" class="group-heading">Network size 50 · Samples and time series</th>
            <th class="average-header sticky-average" rowspan="3">Average</th>
          </tr>
          <tr class="sample-row">
            <th colspan="2">Sample 1</th>
            <th colspan="2">Sample 2</th>
            <th colspan="2">Sample 3</th>
            <th colspan="2">Sample 4</th>
          </tr>
          <tr class="series-row">
            <th>S1</th>
            <th>S2</th>
            <th>S1</th>
            <th>S2</th>
            <th>S1</th>
            <th>S2</th>
            <th>S1</th>
            <th>S2</th>
          </tr>
        </thead>

        <tbody>
          <tr
            v-for="model in filteredModels"
            :key="model.name"
            :class="{
              'baseline-row': model.baseline,
              'gnb-row': model.name === 'GNB',
            }"
          >
            <th scope="row" class="model-cell sticky-model">
              <span v-if="model.name === 'GNB'" class="model-marker"></span>
              {{ model.name }}
              <span v-if="model.baseline" class="baseline-tag">BASELINE</span>
            </th>

            <td
              v-for="(value, index) in model.values"
              :key="index"
              :class="{
                'best-value': isBold(model, index),
                'baseline-value': model.baseline,
              }"
            >
              {{ value.toFixed(4) }}
            </td>

            <td
              class="average-cell sticky-average"
              :class="{ 'best-value': model.boldAvg }"
            >
              {{ model.avg.toFixed(4) }}
            </td>
          </tr>

          <tr v-if="filteredModels.length === 0">
            <td colspan="10" class="empty-state">No matching models found.</td>
          </tr>
        </tbody>
      </table>
    </div>

    <footer class="table-footer">
      <div class="footer-note">
        <span class="footer-key">READING THE TABLE</span>
        <span>Each sample contains two test time series (S1 and S2).</span>
      </div>
      <div class="footer-legend">
        <span class="legend-swatch"></span>
        <span>Bold values reproduce the emphasis in the source table.</span>
      </div>
      <div class="footer-right">E. COLI · N = 50 GENES</div>
    </footer>
  </section>
</template>

<style scoped>
.aupr-slide {
  --navy: #173f5f;
  --blue: #20639b;
  --teal: #2a9d8f;
  --gold: #e9c46a;
  --bg: #f8fafb;
  --text: #24313a;
  --muted: #64748b;
  --border: #dce4e9;
  --header-bg: #edf3f7;

  color: var(--text);
  width: 100%;
  min-width: 0;
  font-family: Inter, "Segoe UI", sans-serif;
}

.slide-heading {
  margin-bottom: 15px;
}

.eyebrow {
  display: flex;
  align-items: center;
  gap: 7px;
  margin-bottom: 7px;
  color: var(--teal);
  font-size: 10px;
  font-weight: 750;
  letter-spacing: 0.13em;
}

.eyebrow-dot {
  width: 7px;
  height: 7px;
  border-radius: 50%;
  background: var(--teal);
}

.title-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 16px;
}

h2 {
  margin: 0;
  color: var(--navy);
  font-size: 27px;
  line-height: 1.15;
  font-weight: 750;
  letter-spacing: -0.035em;
}

.subtitle {
  margin: 6px 0 0;
  color: var(--muted);
  font-size: 11px;
  line-height: 1.45;
}

.metric-badge {
  flex: 0 0 auto;
  min-width: 76px;
  padding: 8px 12px;
  border: 1px solid #d8e7e5;
  border-radius: 8px;
  background: #f0f8f7;
  text-align: center;
}

.metric-label {
  display: block;
  color: var(--muted);
  font-size: 8px;
  font-weight: 700;
  letter-spacing: 0.08em;
}

.metric-badge strong {
  display: block;
  margin-top: 2px;
  color: var(--teal);
  font-size: 18px;
  letter-spacing: 0.02em;
}

.table-toolbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 12px;
  margin-bottom: 7px;
}

.table-summary {
  display: flex;
  align-items: center;
  gap: 7px;
  color: var(--muted);
  font-size: 10px;
  white-space: nowrap;
}

.summary-count {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-width: 21px;
  height: 21px;
  border-radius: 6px;
  background: #e7eff5;
  color: var(--navy);
  font-weight: 750;
}

.summary-divider {
  color: #b1bdc6;
}

.table-actions {
  display: flex;
  align-items: center;
  gap: 5px;
}

.search-box {
  display: flex;
  align-items: center;
  gap: 5px;
  height: 26px;
  padding: 0 7px;
  border: 1px solid var(--border);
  border-radius: 6px;
  background: white;
}

.search-icon {
  color: var(--muted);
  font-size: 17px;
}

.search-box input {
  width: 105px;
  padding: 0;
  border: 0;
  outline: none;
  background: transparent;
  color: var(--text);
  font: inherit;
  font-size: 10px;
}

.scroll-button {
  width: 27px;
  height: 27px;
  border: 1px solid var(--border);
  border-radius: 6px;
  background: white;
  color: var(--navy);
  cursor: pointer;
  font-size: 14px;
}

.scroll-button:hover {
  border-color: var(--teal);
  background: #f0f8f7;
}

.table-scroll {
  width: 100%;
  max-height: 372px;
  overflow-x: auto;
  overflow-y: auto;
  border: 1px solid var(--border);
  border-radius: 8px 8px 0 0;
  background: white;
  scrollbar-width: auto;
  scrollbar-color: #94a3b8 #edf3f7;
}

.table-scroll::-webkit-scrollbar {
  width: 10px;
  height: 12px;
}

.table-scroll::-webkit-scrollbar-track {
  background: #edf3f7;
}

.table-scroll::-webkit-scrollbar-thumb {
  border: 2px solid #edf3f7;
  border-radius: 8px;
  background: #94a3b8;
}

.table-scroll::-webkit-scrollbar-thumb:hover {
  background: #64748b;
}

table {
  width: max-content;
  min-width: 100%;
  border-collapse: separate;
  border-spacing: 0;
  table-layout: fixed;
  font-size: 10px;
  font-variant-numeric: tabular-nums;
}

.model-col {
  width: 132px;
}

.score-col {
  width: 72px;
}

.average-col {
  width: 80px;
}

th,
td {
  padding: 7px 7px;
  border-right: 1px solid #e7edf1;
  border-bottom: 1px solid #e7edf1;
  text-align: center;
  white-space: nowrap;
}

thead th {
  position: sticky;
  z-index: 3;
  background: var(--header-bg);
  color: var(--navy);
  font-weight: 700;
}

.group-row th {
  top: 0;
  height: 30px;
  font-size: 10px;
}

.sample-row th {
  top: 30px;
  height: 27px;
  font-size: 9px;
}

.series-row th {
  top: 57px;
  height: 25px;
  color: var(--muted);
  font-size: 9px;
  font-weight: 650;
}

.group-heading {
  color: var(--navy);
  letter-spacing: 0.015em;
}

.model-header {
  min-width: 132px;
  text-align: left;
  padding-left: 13px;
}

.average-header {
  color: var(--teal);
  background: #e8f5f3;
}

.sticky-model {
  position: sticky;
  left: 0;
  z-index: 4;
  box-shadow: 1px 0 0 #e1e8ed;
}

thead .sticky-model {
  z-index: 6;
  background: var(--header-bg);
}

.model-cell {
  min-width: 132px;
  padding-left: 13px;
  background: #fff;
  color: var(--navy);
  text-align: left;
  font-weight: 650;
}

.gnb-row .model-cell {
  background: #eff8f6;
}

.gnb-row td {
  background: #f7fbfa;
}

.model-marker {
  display: inline-block;
  width: 6px;
  height: 6px;
  margin-right: 6px;
  border-radius: 50%;
  background: var(--teal);
  vertical-align: 1px;
}

td {
  color: #46545e;
}

tbody tr:hover td,
tbody tr:hover .model-cell {
  background: #f1f7fa;
}

tbody tr.gnb-row:hover td,
tbody tr.gnb-row:hover .model-cell {
  background: #eaf6f3;
}

.best-value {
  color: #176f65 !important;
  font-weight: 800 !important;
  background: #e6f5f1 !important;
}

.baseline-row td {
  color: #71808b;
  background: #fafcfd;
}

.baseline-row .model-cell {
  background: #f5f8fa;
  color: #52636f;
}

.baseline-tag {
  display: inline-block;
  margin-left: 5px;
  padding: 2px 4px;
  border-radius: 3px;
  background: #e9eef2;
  color: #70808c;
  font-size: 7px;
  font-weight: 750;
  letter-spacing: 0.04em;
  vertical-align: 1px;
}

.average-cell {
  position: sticky;
  right: 0;
  z-index: 2;
  background: #f0f8f7;
  color: var(--navy);
  font-weight: 700;
  box-shadow: -1px 0 0 #dce9e7;
}

thead .sticky-average {
  z-index: 6;
  background: #e8f5f3;
}

.baseline-row .average-cell {
  background: #edf4f5;
}

.empty-state {
  padding: 22px;
  color: var(--muted);
  text-align: center;
}

.table-footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
  min-height: 34px;
  padding: 7px 11px;
  border: 1px solid var(--border);
  border-top: 0;
  border-radius: 0 0 8px 8px;
  background: var(--header-bg);
  color: var(--muted);
  font-size: 9px;
  line-height: 1.4;
}

.footer-note,
.footer-legend {
  display: flex;
  align-items: center;
  gap: 6px;
}

.footer-key {
  color: var(--navy);
  font-size: 8px;
  font-weight: 750;
  letter-spacing: 0.05em;
  white-space: nowrap;
}

.legend-swatch {
  width: 7px;
  height: 7px;
  flex: 0 0 auto;
  border-radius: 2px;
  background: var(--teal);
}

.footer-right {
  color: var(--navy);
  font-size: 8px;
  font-weight: 750;
  letter-spacing: 0.06em;
  white-space: nowrap;
}

@media (max-width: 700px) {
  h2 {
    font-size: 22px;
  }

  .title-row {
    align-items: flex-start;
  }

  .table-summary {
    flex-wrap: wrap;
    white-space: normal;
  }

  .footer-legend {
    display: none;
  }
}
</style>