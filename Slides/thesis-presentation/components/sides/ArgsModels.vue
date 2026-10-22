<script setup>
const groups = [
  {
    model: 'Linear Regression (LR)',
    params: [['Default setting', '—']],
  },
  {
    model: 'Gaussian Naive Bayes (GNB)',
    params: [['Default setting', '—']],
  },
  {
    model: 'Decision Tree (DT)',
    params: [['Default setting', '—']],
  },
  {
    model: 'Random Forest (RF)',
    params: [['Number of estimators', '20']],
  },
  {
    model: 'K-Nearest Neighbors (KNN)',
    params: [['Number of neighbors', '10']],
  },
  {
    model: 'XGBoost (XGB)',
    params: [
      ['Max depth', '3'],
      ['Learning rate (eta)', '0.1'],
      ['Boosting rounds', '100'],
      ['Early stopping rounds', '10'],
    ],
  },
  {
    model: 'LightGBM (LGB)',
    params: [
      ['Boosting type', 'gbdt'],
      ['Number of leaves', '32'],
      ['Learning rate', '0.05'],
      ['Feature fraction', '0.9'],
      ['Boosting rounds', '100'],
    ],
  },
  {
    model: 'Multi-Layer Perceptron (MLP)',
    params: [
      ['Hidden layers', '5'],
      ['Hidden-layer activation', 'relu'],
      ['Output-layer activation', 'sigmoid'],
      ['Optimizer', 'adam'],
      ['Learning rate', '0.01'],
      ['Loss function', 'mse'],
      ['Early stopping', 'yes'],
      ['Patience', '5'],
      ['Batch size', '32'],
      ['Epochs', '100'],
    ],
  },
]
</script>

<template>
  <div class="hyperparameter-table">

    <div class="table-scroll">
      <table>
        <colgroup>
          <col class="model-column" />
          <col class="parameter-column" />
          <col class="value-column" />
        </colgroup>

        <thead>
          <tr>
            <th>Model</th>
            <th>Parameter</th>
            <th class="value-cell">Value</th>
          </tr>
        </thead>

        <tbody>
          <template v-for="group in groups" :key="group.model">
            <tr
              v-for="(param, index) in group.params"
              :key="`${group.model}-${index}`"
              :class="{ 'group-start': index === 0 }"
            >
              <td
                v-if="index === 0"
                :rowspan="group.params.length"
                class="model-cell"
              >
                {{ group.model }}
              </td>
              <td>{{ param[0] }}</td>
              <td class="value-cell">
                <code>{{ param[1] }}</code>
              </td>
            </tr>
          </template>
        </tbody>
      </table>
    </div>

    <div class="table-footnote">
      LR, GNB and DT use default classifier settings.
    </div>
  </div>
</template>

<style scoped>
.hyperparameter-table {
  width: 100%;
  color: #24313a;
  font-size: 12px;
}

.table-caption {
  display: flex;
  align-items: center;
  gap: 8px;
  margin-bottom: 7px;
  font-size: 16px;
  font-weight: 650;
}

.caption-index {
  color: #20639b;
  font-family: monospace;
  font-size: 10px;
  letter-spacing: 0.12em;
}

.table-scroll {
  max-height: 430px;
  overflow-y: auto;
  overflow-x: hidden;
  border-top: 2px solid #173f5f;
  border-bottom: 1px solid #cbd8e1;
  scrollbar-width: thin;
  scrollbar-color: #aabcc9 #f1f5f8;
}

.table-scroll::-webkit-scrollbar {
  width: 6px;
}

.table-scroll::-webkit-scrollbar-track {
  background: #f1f5f8;
}

.table-scroll::-webkit-scrollbar-thumb {
  background: #aabcc9;
  border-radius: 6px;
}

table {
  width: 100%;
  border-collapse: collapse;
  table-layout: fixed;
  background: #fff;
}

.model-column {
  width: 36%;
}

.parameter-column {
  width: 46%;
}

.value-column {
  width: 18%;
}

thead {
  position: sticky;
  top: 0;
  z-index: 2;
}

th {
  background: #edf3f7;
  color: #173f5f;
  font-size: 11px;
  font-weight: 650;
  text-align: left;
  padding: 7px 10px;
  border-bottom: 1px solid #cbd8e1;
}

td {
  padding: 5px 10px;
  line-height: 1.25;
  border-bottom: 1px solid #e8edf1;
  vertical-align: middle;
  overflow-wrap: anywhere;
}

.group-start td {
  border-top: 1px solid #cbd8e1;
}

.model-cell {
  color: #173f5f;
  font-weight: 600;
}

.value-cell {
  text-align: center;
}

code {
  color: #20639b;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 11px;
  font-weight: 600;
  background: #f1f6f9;
  border-radius: 3px;
  padding: 2px 4px;
}

.table-footnote {
  margin-top: 6px;
  color: #64748b;
  font-size: 10px;
}
</style>