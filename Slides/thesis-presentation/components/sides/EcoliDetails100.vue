<script setup>
import { computed, ref } from 'vue'

const models = [
  { name: 'LR', values: [0.0332, 0.0307, 0.0391, 0.0374, 0.0521, 0.0563, 0.0336, 0.0374], avg: 0.0400 },
  { name: 'DT', values: [0.3146, 0.2220, 0.1845, 0.2078, 0.1674, 0.1553, 0.1695, 0.2176], avg: 0.2048 },
  { name: 'RF', values: [0.1745, 0.0461, 0.1309, 0.1546, 0.1171, 0.1357, 0.1024, 0.1019], avg: 0.1204 },
  { name: 'KNN', values: [0.0124, 0.0124, 0.0858, 0.0124, 0.0124, 0.1394, 0.1163, 0.0123], avg: 0.0504 },
  { name: 'XGBoost', values: [0.0595, 0.0312, 0.0600, 0.0446, 0.0469, 0.0645, 0.0473, 0.0515], avg: 0.0507 },
  { name: 'LGBM', values: [0.0611, 0.0325, 0.0493, 0.0462, 0.0582, 0.0576, 0.0428, 0.0458], avg: 0.0492 },
  { name: 'MLP', values: [0.0454, 0.0317, 0.0430, 0.0422, 0.0490, 0.0522, 0.0489, 0.0628], avg: 0.0469 },
  { name: 'GNB', values: [0.3579, 0.3511, 0.3086, 0.3018, 0.3817, 0.3897, 0.2571, 0.2424], avg: 0.3238, bold: [0, 1, 2, 3, 4, 5, 6, 7], boldAvg: true },
  { name: 'Baseline', values: [0.0254, 0.0251, 0.0254, 0.0251, 0.0252, 0.0249, 0.0250, 0.0252], avg: 0.0252, baseline: true },
  { name: 'Jump3', values: [0.0390, 0.0390, 0.0281, 0.0281, 0.0280, 0.0280, 0.0282, 0.0282], avg: 0.0308, baseline: true },
  { name: 'Inferelator', values: [0.0280, 0.0239, 0.0281, 0.0255, 0.0212, 0.0364, 0.0244, 0.0275], avg: 0.0269, baseline: true },
  { name: 'CLR-lag', values: [0.0235, 0.0251, 0.0269, 0.0270, 0.0260, 0.0254, 0.0238, 0.0233], avg: 0.0251, baseline: true },
  { name: 'TSNI', values: [0.0279, 0.0250, 0.0266, 0.0290, 0.0330, 0.0259, 0.0285, 0.0264], avg: 0.0278, baseline: true },
  { name: 'G1DBN', values: [0.0255, 0.0249, 0.0261, 0.0262, 0.0277, 0.0324, 0.0246, 0.0255], avg: 0.0266, baseline: true },
]

const search = ref('')
const tableScroll = ref(null)

const filteredModels = computed(() => {
  const query = search.value.trim().toLowerCase()
  return query
    ? models.filter(model => model.name.toLowerCase().includes(query))
    : models
})

function isBold(model, index) {
  return model.bold?.includes(index) ?? false
}

function scrollTable(direction) {
  tableScroll.value?.scrollBy({
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
            <th colspan="8" class="group-heading">Network size 100 · Samples and time series</th>
            <th class="average-header sticky-average" rowspan="3">Average</th>
          </tr>
          <tr class="sample-row">
            <th colspan="2">Sample 1</th>
            <th colspan="2">Sample 2</th>
            <th colspan="2">Sample 3</th>
            <th colspan="2">Sample 4</th>
          </tr>
          <tr class="series-row">
            <th>S1</th><th>S2</th>
            <th>S1</th><th>S2</th>
            <th>S1</th><th>S2</th>
            <th>S1</th><th>S2</th>
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
      <div class="footer-right">E. COLI · N = 100 GENES</div>
    </footer>
  </section>
</template>

<style scoped>
.aupr-slide {
  --navy: #173f5f;
  --blue: #20639b;
  --teal: #2a9d8f;
  --bg: #f8fafb;
  --text: #24313a;
  --muted: #64748b;
  --border: #dce4e9;
  --header-bg: #edf3f7;

  width: 100%;
  min-width: 0;
  color: var(--text);
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
  align-items: center;
  justify-content: space-between;
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
}

.table-toolbar {
  display: flex;
  align-items: center;
  justify-content: space-between;
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

.model-col { width: 132px; }
.score-col { width: 72px; }
.average-col { width: 80px; }

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
  padding-left: 13px;
  text-align: left;
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
  h2 { font-size: 22px; }
  .title-row { align-items: flex-start; }
  .table-summary { flex-wrap: wrap; white-space: normal; }
  .footer-legend { display: none; }
}
</style>