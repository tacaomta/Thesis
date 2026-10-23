<script setup>
import { ref } from 'vue'

const datasets = [
  {
    key: 'size10',
    title: 'Testing size 10',
    subtitle: '10 samples · 20 series',
    average: ['0.5727', '0.5785', '0.5661'],
    samples: [
      { id: 1, rows: [{ ts: 'S1', values: ['0.5159', '0.5159', '0.5099'] }, { ts: 'S2', values: ['0.5159', '0.5159', '0.5099'] }] },
      { id: 2, rows: [{ ts: 'S1', values: ['0.6383', '0.6383', '0.6327'] }, { ts: 'S2', values: ['0.6383', '0.6383', '0.6327'] }] },
      { id: 3, rows: [{ ts: 'S1', values: ['0.7203', '0.7770', '0.6356'] }, { ts: 'S2', values: ['0.6601', '0.6806', '0.6107'] }] },
      { id: 4, rows: [{ ts: 'S1', values: ['0.9556', '0.9556', '0.9556'], bold: [0, 1, 2] }, { ts: 'S2', values: ['0.9556', '0.9556', '0.9556'], bold: [0, 1, 2] }] },
      { id: 5, rows: [{ ts: 'S1', values: ['0.5080', '0.5376', '0.5148'] }, { ts: 'S2', values: ['0.5542', '0.5627', '0.5503'] }] },
      { id: 6, rows: [{ ts: 'S1', values: ['0.3925', '0.3910', '0.4207'] }, { ts: 'S2', values: ['0.4470', '0.4456', '0.4551'] }] },
      { id: 7, rows: [{ ts: 'S1', values: ['0.6061', '0.6061', '0.6061'] }, { ts: 'S2', values: ['0.6094', '0.6094', '0.6094'] }] },
      { id: 8, rows: [{ ts: 'S1', values: ['0.6398', '0.6267', '0.6309'] }, { ts: 'S2', values: ['0.6550', '0.6497', '0.6550'] }] },
      { id: 9, rows: [{ ts: 'S1', values: ['0.2828', '0.2817', '0.4017'] }, { ts: 'S2', values: ['0.2857', '0.2817', '0.2877'] }] },
      { id: 10, rows: [{ ts: 'S1', values: ['0.4470', '0.4470', '0.3713'] }, { ts: 'S2', values: ['0.4271', '0.4530', '0.3773'] }] },
    ],
  },
  {
    key: 'size50',
    title: 'Testing size 50',
    subtitle: '4 samples · 8 series',
    average: ['0.3487', '0.3518', '0.3553'],
    samples: [
      { id: 1, rows: [{ ts: 'S1', values: ['0.3820', '0.4044', '0.4207'] }, { ts: 'S2', values: ['0.4756', '0.4806', '0.4790'], bold: [0, 1, 2] }] },
      { id: 2, rows: [{ ts: 'S1', values: ['0.3009', '0.3016', '0.2996'] }, { ts: 'S2', values: ['0.2877', '0.2944', '0.2929'] }] },
      { id: 3, rows: [{ ts: 'S1', values: ['0.4260', '0.4252', '0.4240'] }, { ts: 'S2', values: ['0.3811', '0.3809', '0.3910'] }] },
      { id: 4, rows: [{ ts: 'S1', values: ['0.2796', '0.2703', '0.2697'] }, { ts: 'S2', values: ['0.2571', '0.2568', '0.2657'] }] },
    ],
  },
  {
    key: 'size100',
    title: 'Testing size 100',
    subtitle: '4 samples · 8 series',
    average: ['0.3224', '0.3249', '0.3238'],
    samples: [
      { id: 1, rows: [{ ts: 'S1', values: ['0.3612', '0.3634', '0.3579'] }, { ts: 'S2', values: ['0.3607', '0.3608', '0.3511'] }] },
      { id: 2, rows: [{ ts: 'S1', values: ['0.2975', '0.3040', '0.3086'] }, { ts: 'S2', values: ['0.3014', '0.3054', '0.3018'] }] },
      { id: 3, rows: [{ ts: 'S1', values: ['0.3656', '0.3758', '0.3817'] }, { ts: 'S2', values: ['0.3799', '0.3817', '0.3897'], bold: [0, 1, 2] }] },
      { id: 4, rows: [{ ts: 'S1', values: ['0.2585', '0.2586', '0.2571'] }, { ts: 'S2', values: ['0.2540', '0.2499', '0.2424'] }] },
    ],
  },
]

const activeTable = ref(null)

function isBold(row, index) {
  return row.bold?.includes(index) ?? false
}
</script>

<template>
  <section class="comparison-slide">
    <div class="comparison-grid">
      <article
        v-for="dataset in datasets"
        :key="dataset.key"
        class="dataset-panel"
        :class="{ 'panel-active': activeTable === dataset.key }"
        @mouseenter="activeTable = dataset.key"
        @mouseleave="activeTable = null"
      >
        <header class="panel-heading">
          <div class="panel-title-group">
            <span class="panel-indicator"></span>
            <h3>{{ dataset.title }}</h3>
          </div>
          <span class="panel-subtitle">{{ dataset.subtitle }}</span>
        </header>

        <div class="table-scroll">
          <table>
            <colgroup>
              <col class="sample-col" />
              <col class="ts-col" />
              <col class="value-col" />
              <col class="value-col" />
              <col class="value-col" />
            </colgroup>

            <thead>
              <tr>
                <th>Sample</th>
                <th>TS</th>
                <th>5k</th>
                <th>10k</th>
                <th>20k</th>
              </tr>
            </thead>

            <tbody>
              <template v-for="sample in dataset.samples" :key="sample.id">
                <tr
                  v-for="(row, rowIndex) in sample.rows"
                  :key="`${sample.id}-${row.ts}`"
                  :class="{ 'sample-start': rowIndex === 0 }"
                >
                  <th
                    v-if="rowIndex === 0"
                    class="sample-cell"
                    rowspan="2"
                  >
                    {{ sample.id }}
                  </th>

                  <td class="ts-cell">{{ row.ts }}</td>

                  <td
                    v-for="(value, index) in row.values"
                    :key="index"
                    :class="{ 'best-value': isBold(row, index) }"
                  >
                    {{ value }}
                  </td>
                </tr>
              </template>

              <tr class="average-row">
                <th colspan="2" class="average-label">Average</th>
                <td v-for="(value, index) in dataset.average" :key="index">
                  {{ value }}
                </td>
              </tr>
            </tbody>
          </table>
        </div>

        <footer class="panel-footer">
          <span>GNB</span>
          <span>Training data</span>
          <span>5k · 10k · 20k</span>
        </footer>
      </article>
    </div>

    <footer class="slide-footer">
      <div class="footer-note">
        <span class="legend-bold">0.0000</span>
        <span>Bold values preserve the emphasis in the source tables.</span>
      </div>
      <div class="footer-context">TIME-SERIES GENE EXPRESSION</div>
    </footer>
  </section>
</template>

<style scoped>
.comparison-slide {
  --navy: #173f5f;
  --blue: #20639b;
  --teal: #2a9d8f;
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
  margin-bottom: 16px;
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

.heading-row {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 16px;
}

h2 {
  margin: 0;
  color: var(--navy);
  font-size: 26px;
  line-height: 1.15;
  font-weight: 750;
  letter-spacing: -0.035em;
}

.subtitle {
  margin: 6px 0 0;
  color: var(--muted);
  font-size: 11px;
  line-height: 1.4;
}

.metric-badge {
  flex: 0 0 auto;
  min-width: 70px;
  padding: 7px 10px;
  border: 1px solid #d8e7e5;
  border-radius: 8px;
  background: #f0f8f7;
  text-align: center;
}

.metric-badge span {
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
  font-size: 17px;
}

.comparison-grid {
  display: grid;
  grid-template-columns: repeat(3, minmax(0, 1fr));
  gap: 10px;
  align-items: start;
}

.dataset-panel {
  min-width: 0;
  overflow: hidden;
  border: 1px solid var(--border);
  border-radius: 9px;
  background: white;
  transition: border-color 0.15s ease, box-shadow 0.15s ease;
}

.dataset-panel.panel-active {
  border-color: #b7d8d3;
}

.panel-heading {
  min-height: 57px;
  padding: 10px 10px 8px;
  border-bottom: 1px solid var(--border);
  background: #f8fafc;
}

.panel-title-group {
  display: flex;
  align-items: center;
  gap: 7px;
}

.panel-indicator {
  width: 4px;
  height: 17px;
  flex: 0 0 auto;
  border-radius: 3px;
  background: var(--teal);
}

h3 {
  margin: 0;
  color: var(--navy);
  font-size: 13px;
  line-height: 1.2;
  font-weight: 750;
}

.panel-subtitle {
  display: block;
  margin: 5px 0 0 11px;
  color: var(--muted);
  font-size: 9px;
}

.table-scroll {
  max-height: 322px;
  overflow: auto;
  scrollbar-width: thin;
  scrollbar-color: #a6b6c2 #edf3f7;
  min-height: 322px;
}

.table-scroll::-webkit-scrollbar {
  width: 7px;
  height: 7px;
}

.table-scroll::-webkit-scrollbar-track {
  background: #edf3f7;
}

.table-scroll::-webkit-scrollbar-thumb {
  border: 1px solid #edf3f7;
  border-radius: 6px;
  background: #a6b6c2;
}

table {
  width: 100%;
  min-width: 0;
  border-collapse: separate;
  border-spacing: 0;
  table-layout: fixed;
  font-size: 10px;
  font-variant-numeric: tabular-nums;
}

.sample-col {
  width: 20%;
}

.ts-col {
  width: 15%;
}

.value-col {
  width: 21.666%;
}

th,
td {
  padding: 6px 2px;
  border-right: 1px solid #e7edf1;
  border-bottom: 1px solid #e7edf1;
  text-align: center;
  white-space: nowrap;
}

thead th {
  position: sticky;
  top: 0;
  z-index: 2;
  padding: 8px 2px;
  background: var(--header-bg);
  color: var(--navy);
  font-size: 9px;
  font-weight: 750;
}

tbody td {
  color: #46545e;
}

tbody tr.sample-start td,
tbody tr.sample-start th {
  border-top: 1px solid #dce4e9;
}

.sample-cell {
  background: #f8fafc;
  color: var(--navy);
  font-weight: 700;
}

.ts-cell {
  color: var(--muted);
  font-size: 9px;
}

tbody tr:hover td,
tbody tr:hover .sample-cell {
  background: #f2f8fa;
}

.best-value {
  background: #e6f5f1 !important;
  color: #176f65 !important;
  font-weight: 800;
}

.average-row th,
.average-row td {
  position: sticky;
  bottom: 0;
  z-index: 1;
  border-bottom: 0;
  background: #e8f5f3;
  color: var(--navy);
  font-weight: 800;
}

.average-row th {
  text-align: left;
  padding-left: 8px;
}

.average-row td {
  color: #176f65;
}

.panel-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 4px;
  padding: 7px 9px;
  border-top: 1px solid var(--border);
  background: var(--header-bg);
  color: var(--muted);
  font-size: 8px;
}

.panel-footer span:first-child {
  color: var(--navy);
  font-weight: 800;
  letter-spacing: 0.04em;
}

.slide-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 10px;
  margin-top: 12px;
  padding: 8px 11px;
  border: 1px solid var(--border);
  border-radius: 7px;
  background: var(--header-bg);
  color: var(--muted);
  font-size: 9px;
}

.footer-note {
  display: flex;
  align-items: center;
  gap: 7px;
}

.legend-bold {
  padding: 2px 5px;
  border-radius: 3px;
  background: #e6f5f1;
  color: #176f65;
  font-weight: 800;
}

.footer-context {
  color: var(--navy);
  font-size: 8px;
  font-weight: 750;
  letter-spacing: 0.06em;
  white-space: nowrap;
}

@media (max-width: 800px) {
  .comparison-grid {
    grid-template-columns: 1fr;
  }

  .table-scroll {
    max-height: 300px;
  }
}
</style>