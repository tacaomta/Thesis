<script setup>
const models = [
  {
    name: 'LR',
    group: 'learning',
    values: [
      '0.3077', '0.3852', '0.5803', '0.6818', '0.8626', '0.9311',
      '0.9292', '0.9760', '0.5277', '0.5162',
      '0.6400', '0.7022', '0.6465', '0.2051', '0.7677', '0.7876',
      '0.1254', '0.1089', '0.2276', '0.2083',
    ],
    bold: [10, 11],
    average: '0.5559',
  },
  {
    name: 'DT',
    group: 'learning',
    values: [
      '0.3000', '0.3179', '0.3558', '0.3808', '0.6778', '0.4760',
      '0.1714', '0.2722', '0.4174', '0.3253',
      '0.2808', '0.3344', '0.1381', '0.6106', '0.3804', '0.5342',
      '0.1263', '0.1208', '0.2428', '0.2059',
    ],
    bold: [13],
    average: '0.3334',
  },
  {
    name: 'RF',
    group: 'learning',
    values: [
      '0.6873', '0.2810', '0.5460', '0.7145', '0.9111', '0.8111',
      '0.9111', '0.9167', '0.6778', '0.5242',
      '0.4399', '0.5709', '0.6183', '0.1548', '0.7376', '0.7376',
      '0.4000', '0.0500', '0.1056', '0.1056',
    ],
    bold: [0, 3],
    average: '0.5450',
  },
  {
    name: 'KNN',
    group: 'learning',
    values: [
      '0.5315', '0.2683', '0.3705', '0.6684', '0.5639', '0.4861',
      '0.8017', '0.6222', '0.7485', '0.4899',
      '0.4915', '0.3535', '0.4240', '0.1464', '0.7614', '0.6126',
      '0.2611', '0.2000', '0.1680', '0.1819',
    ],
    bold: [8],
    average: '0.4576',
  },
  {
    name: 'XGBoost',
    group: 'learning',
    values: [
      '0.6236', '0.6370', '0.5338', '0.6964', '0.9229', '0.9826',
      '0.9271', '1.0000', '0.4439', '0.4576',
      '0.3621', '0.5192', '0.3097', '0.2175', '0.9007', '0.8931',
      '0.1266', '0.1104', '0.1735', '0.1800',
    ],
    bold: [5, 7],
    average: '0.5509',
  },
  {
    name: 'LGBM',
    group: 'learning',
    values: [
      '0.6603', '0.6395', '0.5915', '0.6998', '0.9181', '0.9602',
      '0.9404', '0.9905', '0.4429', '0.5047',
      '0.4043', '0.5452', '0.9024', '0.2299', '0.9106', '0.8946',
      '0.1278', '0.1170', '0.1632', '0.1873',
    ],
    bold: [1, 12, 14],
    average: '0.5915',
    averageBold: true,
  },
  {
    name: 'MLP',
    group: 'learning',
    values: [
      '0.4376', '0.3069', '0.6487', '0.6322', '0.9322', '0.7100',
      '0.9247', '0.9826', '0.5258', '0.5920',
      '0.5673', '0.5815', '0.3363', '0.3082', '0.9075', '0.9180',
      '0.1129', '0.1128', '0.1645', '0.1847',
    ],
    bold: [4, 15],
    average: '0.5443',
  },
  {
    name: 'GNB',
    group: 'learning',
    values: [
      '0.5099', '0.5099', '0.6327', '0.6327', '0.6356', '0.6107',
      '0.9556', '0.9556', '0.5148', '0.5503',
      '0.4207', '0.4551', '0.6061', '0.6094', '0.6309', '0.6550',
      '0.4017', '0.2877', '0.3713', '0.3773',
    ],
    bold: [6, 7, 18, 19],
    average: '0.5661',
  },
  {
    name: 'Baseline',
    group: 'baseline',
    values: [
      '0.1663', '0.1746', '0.1572', '0.1594', '0.1398', '0.1360',
      '0.1368', '0.1356', '0.2696', '0.2639',
      '0.2107', '0.2017', '0.1019', '0.0988', '0.2187', '0.2160',
      '0.1234', '0.1164', '0.2266', '0.2368',
    ],
    bold: [],
    average: '0.1745',
  },
  {
    name: 'Jump3',
    group: 'baseline',
    values: [
      '0.1946', '0.1946', '0.1398', '0.1398', '0.1097', '0.1097',
      '0.1041', '0.1041', '0.2373', '0.2373',
      '0.3195', '0.3195', '0.0907', '0.0907', '0.2077', '0.2077',
      '0.0924', '0.0924', '0.2430', '0.2430',
    ],
    bold: [],
    average: '0.1739',
  },
  {
    name: 'Inferelator',
    group: 'baseline',
    values: [
      '0.1439', '0.1213', '0.1679', '0.1905', '0.0970', '0.1161',
      '0.1153', '0.1815', '0.2518', '0.2945',
      '0.1793', '0.2938', '0.0389', '0.0624', '0.2762', '0.1179',
      '0.1323', '0.0936', '0.2135', '0.2925',
    ],
    bold: [],
    average: '0.1690',
  },
  {
    name: 'CLR-lag',
    group: 'baseline',
    values: [
      '0.1653', '0.1829', '0.2138', '0.2177', '0.1145', '0.1702',
      '0.1136', '0.1993', '0.2820', '0.2561',
      '0.2192', '0.3492', '0.0829', '0.1050', '0.2123', '0.2171',
      '0.1212', '0.1261', '0.2857', '0.2662',
    ],
    bold: [],
    average: '0.1950',
  },
  {
    name: 'TSNI',
    group: 'baseline',
    values: [
      '0.1429', '0.1537', '0.1732', '0.1434', '0.1982', '0.2621',
      '0.3033', '0.1701', '0.3154', '0.2206',
      '0.3722', '0.2487', '0.1820', '0.1231', '0.2666', '0.2784',
      '0.1306', '0.1296', '0.2241', '0.2351',
    ],
    bold: [],
    average: '0.2137',
  },
  {
    name: 'G1DBN',
    group: 'baseline',
    values: [
      '0.1485', '0.1803', '0.1590', '0.1443', '0.1736', '0.1115',
      '0.2633', '0.1287', '0.2523', '0.3205',
      '0.2808', '0.2084', '0.1033', '0.0825', '0.2297', '0.2759',
      '0.1000', '0.1000', '0.2331', '0.1983',
    ],
    bold: [],
    average: '0.1847',
  },
]

const samples = Array.from({ length: 10 }, (_, i) => ({
  number: i + 1,
  rows: [
    { state: 'S1', index: i * 2 },
    { state: 'S2', index: i * 2 + 1 },
  ],
}))

function isBold(model, index) {
  return model.bold.includes(index)
}
</script>

<template>
  <section class="aupr-slide">

    <div class="table-container">
      <div class="table-scroll">
        <table>
          <thead>
            <tr>
              <th class="sample-heading">Sample</th>
              <th
                v-for="model in models"
                :key="model.name"
                :class="[
                  'model-heading',
                  model.group === 'baseline' ? 'baseline-column' : '',
                ]"
              >
                {{ model.name }}
              </th>
            </tr>
          </thead>

          <tbody>
            <template v-for="sample in samples" :key="sample.number">
              <tr
                v-for="row in sample.rows"
                :key="`${sample.number}-${row.state}`"
                :class="{ 'sample-start': row.state === 'S1' }"
              >
                <td class="sample-cell">
                  <span class="sample-number">{{ sample.number }}</span>
                  <span class="sample-state">{{ row.state }}</span>
                </td>

                <td
                  v-for="model in models"
                  :key="model.name"
                  :class="[
                    'value-cell',
                    model.group === 'baseline' ? 'baseline-column' : '',
                  ]"
                >
                  <strong v-if="isBold(model, row.index)">
                    {{ model.values[row.index] }}
                  </strong>
                  <span v-else>{{ model.values[row.index] }}</span>
                </td>
              </tr>
            </template>

            <tr class="average-row">
              <td class="sample-cell average-label">Average</td>

              <td
                v-for="model in models"
                :key="model.name"
                :class="[
                  'value-cell',
                  model.group === 'baseline' ? 'baseline-column' : '',
                ]"
              >
                <strong v-if="model.averageBold">{{ model.average }}</strong>
                <span v-else>{{ model.average }}</span>
              </td>
            </tr>
          </tbody>
        </table>
      </div>

      <footer class="table-footer">
        <span class="footer-label">EXPERIMENT DETAILS</span>

        <div class="footer-content">
          <span><strong>Network size:</strong> 10 genes</span>
          <span class="footer-separator">·</span>
          <span><strong>Samples:</strong> 10</span>
          <span class="footer-separator">·</span>
          <span><strong>Profiles:</strong> S1 and S2 per sample</span>
          <span class="footer-separator">·</span>
          <span>Bold values reproduce the emphasis in the source table.</span>
        </div>
      </footer>
    </div>
  </section>
</template>

<style scoped>
.aupr-slide {
  --navy: #173f5f;
  --blue: #20639b;
  --teal: #2a9d8f;
  --text: #24313a;
  --muted: #64748b;
  --border: #dce4e9;
  --header-bg: #edf3f7;

  width: 100%;
  color: var(--text);
  font-family: Inter, "Segoe UI", sans-serif;
}

.table-heading {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
  margin-bottom: 12px;
}

.section-label {
  margin-bottom: 5px;
  color: var(--teal);
  font-family: "IBM Plex Mono", monospace;
  font-size: 10px;
  font-weight: 700;
  letter-spacing: 0.13em;
}

.table-heading h2 {
  margin: 0;
  color: var(--navy);
  font-size: 22px;
  font-weight: 750;
  line-height: 1.2;
}

.metric-badge {
  flex-shrink: 0;
  padding: 7px 11px;
  border: 1px solid #cce8e4;
  border-radius: 8px;
  background: #edf8f6;
  color: var(--teal);
  font-family: "IBM Plex Mono", monospace;
  font-size: 11px;
  font-weight: 700;
}

.table-container {
  overflow: hidden;
  border: 1px solid var(--border);
  border-radius: 10px;
  background: #fff;
}

.table-scroll {
  max-height: 375px;
  overflow-x: scroll;
  overflow-y: auto;
  scrollbar-width: auto;
  scrollbar-color: #94a3b8 #edf3f7;
}

.table-scroll table {
  width: max-content;
  min-width: 100%;
  table-layout: fixed;
  border-collapse: separate;
  border-spacing: 0;
  font-size: 10px;
}

.table-scroll th,
.table-scroll td {
  padding: 6px 4px;
  white-space: nowrap;
}

/* Cột tên mẫu / model */
.table-scroll th:first-child,
.table-scroll td:first-child {
  width: 60px;
  min-width: 60px;
}

/* Các cột điểm số */
.table-scroll th:not(:first-child),
.table-scroll td:not(:first-child) {
  width: 58px;
  min-width: 58px;
}

table {
  width: 100%;
  min-width: 1050px;
  border-collapse: separate;
  border-spacing: 0;
  table-layout: fixed;
  font-size: 10px;
  font-variant-numeric: tabular-nums;
}

.sample-heading,
.sample-cell {
  position: sticky;
  left: 0;
  width: 40px;
  min-width: 40px;
  z-index: 1;
}

thead {
  position: sticky;
  top: 0;
  z-index: 3;
}

thead th {
  padding: 9px 5px;
  border-bottom: 1px solid var(--border);
  background: var(--header-bg);
  color: var(--navy);
  text-align: center;
  font-weight: 700;
  white-space: nowrap;
}

thead .sample-heading {
  z-index: 4;
  text-align: left;
  padding-left: 5px;
}

.model-heading {
  width: 50px;
}

tbody td {
  padding: 5px 2px;
  border-bottom: 1px solid #e9eef2;
  text-align: center;
  white-space: nowrap;
}

.sample-cell {
  z-index: 1;
  background: #f6f9fb;
  text-align: left;
  padding-left: 5px;
  color: var(--navy);
}

.sample-number {
  display: inline-block;
  min-width: 15px;
  font-weight: 750;
}

.sample-state {
  display: inline-block;
  margin-left: 5px;
  color: var(--muted);
  font-family: "IBM Plex Mono", monospace;
  font-size: 9px;
}

.sample-start td {
  border-top: 1px solid #d5e0e7;
}

.sample-start:first-child td {
  border-top: none;
}

.value-cell {
  color: #52616d;
  font-family: "IBM Plex Mono", "JetBrains Mono", monospace;
}

.value-cell strong {
  color: var(--navy);
  font-weight: 800;
}

.baseline-column {
  border-left: 1px solid #d5e0e7;
}

thead .baseline-column {
  background: #e7eef3;
}

tbody .baseline-column {
  background: #fafbfd;
}

.average-row td {
  border-top: 2px solid var(--teal);
  border-bottom: none;
  background: #edf8f6;
}

.average-row .sample-cell {
  background: #e2f2ef;
  color: var(--navy);
}

.average-label {
  font-weight: 750;
}

.table-footer {
  display: flex;
  align-items: flex-start;
  flex-wrap: wrap;
  gap: 5px 12px;
  padding: 9px 12px;
  border-top: 1px solid var(--border);
  background: var(--header-bg);
  color: var(--muted);
  font-size: 9px;
  line-height: 1.5;
}

.footer-label {
  flex-shrink: 0;
  padding-top: 1px;
  color: var(--navy);
  font-family: "IBM Plex Mono", monospace;
  font-size: 9px;
  font-weight: 700;
  letter-spacing: 0.06em;
}

.footer-content {
  display: flex;
  flex: 1;
  flex-wrap: wrap;
  align-items: baseline;
  gap: 3px 8px;
  min-width: 0;
}

.footer-content strong {
  color: #52616d;
  font-weight: 650;
}

.footer-separator {
  color: #a0adb8;
}

@media (max-width: 640px) {
  .table-heading h2 {
    font-size: 18px;
  }

  .table-scroll {
    max-height: 400px;
  }

  table {
    min-width: 1050px;
  }

  .table-footer {
    gap: 5px;
  }

  .footer-content {
    flex-basis: 100%;
  }
}
</style>