<script setup>
const groups = [
  {
    name: 'Training Set',
    key: 'training',
    rows: [
      { label: 'Number of networks', values: ['20,000', '2,000', '2,000'] },
      { label: 'Number of gene pairs (×10⁶)', values: ['1.8', '4.9', '19.8'] },
      { label: 'Positive / negative interaction ratio', values: ['0.3357', '0.0484', '0.0292'] },
    ],
  },
  {
    name: 'Validation',
    key: 'validation',
    rows: [
      { label: 'Number of networks', values: ['2,000', '400', '400'] },
      { label: 'Number of gene pairs (×10⁶)', values: ['0.18', '0.98', '3.96'] },
      { label: 'Positive / negative interaction ratio', values: ['0.3351', '0.0483', '0.0234'] },
    ],
  },
  {
    name: 'Test Set',
    key: 'test',
    rows: [
      { label: 'Number of networks', values: ['2,000', '400', '400'] },
      { label: 'Number of gene pairs (×10⁶)', values: ['0.18', '0.98', '3.96'] },
      { label: 'Positive / negative interaction ratio', values: ['0.334', '0.0483', '0.0233'] },
    ],
  },
]
</script>

<template>
  <section class="topological-dataset">

    <div class="table-container">
      <div class="table-scroll">
        <table>
          <thead>
            <tr>
              <th class="dataset-col">Dataset</th>
              <th class="parameter-col">Parameter</th>
              <th colspan="3" class="network-heading">Network size (genes)</th>
            </tr>
            <tr>
              <th></th>
              <th></th>
              <th class="size-col">10</th>
              <th class="size-col">50</th>
              <th class="size-col">100</th>
            </tr>
          </thead>

          <tbody>
            <template v-for="group in groups" :key="group.key">
              <tr
                v-for="(item, index) in group.rows"
                :key="`${group.key}-${item.label}`"
                :class="{
                  'group-start': index === 0,
                  'group-end': index === group.rows.length - 1,
                }"
              >
                <td
                  v-if="index === 0"
                  :rowspan="group.rows.length"
                  class="dataset-cell"
                >
                  <span class="dataset-marker" :class="group.key"></span>
                  {{ group.name }}
                </td>

                <td class="parameter-cell">
                  {{ item.label }}
                </td>

                <td
                  v-for="(value, i) in item.values"
                  :key="i"
                  class="value-cell"
                >
                  {{ value }}
                </td>
              </tr>
            </template>
          </tbody>
        </table>
      </div>

      <footer class="table-footer">
        <span class="footer-label">DATA CONFIGURATION</span>

        <div class="footer-content">
          <span>
            <strong>Profiles per structure:</strong>
            1
          </span>

          <span class="footer-separator">·</span>

          <span>
            <strong>Time steps per profile:</strong>
            50
          </span>

          <span class="footer-separator">·</span>

          <span>
            Each time step records expression levels for all genes simultaneously.
          </span>
        </div>
      </footer>
    </div>
  </section>
</template>

<style scoped>
.topological-dataset {
  --navy: #173f5f;
  --blue: #20639b;
  --teal: #2a9d8f;
  --text: #24313a;
  --muted: #64748b;
  --border: #dce4e9;
  --surface: #ffffff;
  --header-bg: #edf3f7;

  width: 100%;
  color: var(--text);
  font-family: Inter, "Segoe UI", sans-serif;
}

.table-heading {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 14px;
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
  font-size: 23px;
  font-weight: 750;
  line-height: 1.2;
}

.gene-icon {
  display: grid;
  width: 42px;
  height: 42px;
  flex-shrink: 0;
  place-items: center;
  border: 1px solid #cce8e4;
  border-radius: 12px;
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
  background: var(--surface);
}

.table-scroll {
  max-height: 372px;
  overflow: auto;
}

table {
  width: 100%;
  border-collapse: separate;
  border-spacing: 0;
  table-layout: fixed;
  font-size: 12px;
}

.dataset-col {
  width: 17%;
}

.parameter-col {
  width: 39%;
}

.size-col {
  width: 14.67%;
  text-align: center;
}

thead {
  position: sticky;
  top: 0;
  z-index: 2;
}

thead th {
  padding: 10px 12px;
  border-bottom: 1px solid var(--border);
  background: var(--header-bg);
  color: var(--navy);
  font-weight: 700;
}

thead tr:first-child th {
  padding-top: 11px;
  padding-bottom: 7px;
}

thead tr:last-child th {
  padding-top: 5px;
  padding-bottom: 9px;
}

.network-heading {
  text-align: center;
}

tbody td {
  padding: 10px 12px;
  border-bottom: 1px solid #e9eef2;
  vertical-align: middle;
}

tbody tr.group-start td {
  border-top: 2px solid #d5e0e7;
}

tbody tr.group-start:first-child td {
  border-top: none;
}

tbody tr.group-end td {
  border-bottom: 1px solid var(--border);
}

tbody tr:last-child td {
  border-bottom: none;
}

.dataset-cell {
  background: #f6f9fb;
  color: var(--navy);
  font-size: 11px;
  font-weight: 750;
  line-height: 1.45;
}

.dataset-marker {
  display: inline-block;
  width: 6px;
  height: 6px;
  margin-right: 5px;
  border-radius: 50%;
  vertical-align: middle;
}

.dataset-marker.training {
  background: var(--blue);
}

.dataset-marker.validation {
  background: var(--teal);
}

.dataset-marker.test {
  background: #d39b31;
}

.parameter-cell {
  color: #52616d;
  line-height: 1.4;
}

.value-cell {
  text-align: center;
  font-family: "IBM Plex Mono", "JetBrains Mono", monospace;
  font-size: 11px;
  font-variant-numeric: tabular-nums;
}

/* Footer nối liền với bảng */
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
    font-size: 19px;
  }

  .table-scroll {
    max-height: 330px;
  }

  table {
    min-width: 570px;
  }

  .table-footer {
    gap: 5px;
  }

  .footer-content {
    flex-basis: 100%;
  }
}
</style>