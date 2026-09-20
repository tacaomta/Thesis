<template>
  <div class="data-slide">
    <div class="observed-data">
      <section class="main-grid">
        <div class="data-panel">
          <div class="panel-header">
            <div>
              <div class="section-label">TIME-SERIES GENE EXPRESSION</div>
              <p class="panel-description">
                Gene expression measured repeatedly over time
              </p>
            </div>
            <div class="matrix-badge">M × N</div>
          </div>
          <div class="matrix-wrapper">
            <table class="expression-table">
              <thead>
                <tr>
                  <th class="time-header">Time</th>
                  <th>Gene 1</th>
                  <th>Gene 2</th>
                  <th>Gene 3</th>
                  <th>Gene 4</th>
                  <th>Gene 5</th>
                  <th>Gene 6</th>
                  <th class="ellipsis-cell">…</th>
                  <th>Gene N</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <th>t₁</th>
                  <td class="level-3">0.72</td>
                  <td class="level-5">0.91</td>
                  <td class="level-2">0.43</td>
                  <td class="level-4">0.68</td>
                  <td class="level-1">0.21</td>
                  <td class="level-3">0.57</td>
                  <td class="ellipsis-cell">…</td>
                  <td class="level-4">0.64</td>
                </tr>
                <tr>
                  <th>t₂</th>
                  <td class="level-4">0.81</td>
                  <td class="level-4">0.76</td>
                  <td class="level-3">0.51</td>
                  <td class="level-5">0.87</td>
                  <td class="level-2">0.34</td>
                  <td class="level-4">0.69</td>
                  <td class="ellipsis-cell">…</td>
                  <td class="level-3">0.55</td>
                </tr>
                <tr>
                  <th>t₃</th>
                  <td class="level-5">0.94</td>
                  <td class="level-3">0.63</td>
                  <td class="level-4">0.72</td>
                  <td class="level-4">0.71</td>
                  <td class="level-3">0.48</td>
                  <td class="level-2">0.42</td>
                  <td class="ellipsis-cell">…</td>
                  <td class="level-5">0.83</td>
                </tr>
                <tr>
                  <th>t₄</th>
                  <td class="level-4">0.79</td>
                  <td class="level-2">0.39</td>
                  <td class="level-5">0.89</td>
                  <td class="level-3">0.56</td>
                  <td class="level-4">0.61</td>
                  <td class="level-3">0.53</td>
                  <td class="ellipsis-cell">…</td>
                  <td class="level-4">0.71</td>
                </tr>
                <tr>
                  <th>t₅</th>
                  <td class="level-3">0.61</td>
                  <td class="level-1">0.18</td>
                  <td class="level-5">0.96</td>
                  <td class="level-2">0.41</td>
                  <td class="level-5">0.82</td>
                  <td class="level-4">0.67</td>
                  <td class="ellipsis-cell">…</td>
                  <td class="level-2">0.36</td>
                </tr>
                <tr>
                  <th>t₆</th>
                  <td class="level-2">0.44</td>
                  <td class="level-3">0.52</td>
                  <td class="level-4">0.77</td>
                  <td class="level-1">0.24</td>
                  <td class="level-5">0.91</td>
                  <td class="level-4">0.74</td>
                  <td class="ellipsis-cell">…</td>
                  <td class="level-3">0.58</td>
                </tr>
                <tr>
                  <th>t₇</th>
                  <td class="level-1">0.27</td>
                  <td class="level-4">0.68</td>
                  <td class="level-3">0.59</td>
                  <td class="level-2">0.38</td>
                  <td class="level-4">0.73</td>
                  <td class="level-5">0.88</td>
                  <td class="ellipsis-cell">…</td>
                  <td class="level-4">0.69</td>
                </tr>
                <tr>
                  <th>t₈</th>
                  <td class="level-2">0.35</td>
                  <td class="level-5">0.84</td>
                  <td class="level-2">0.42</td>
                  <td class="level-3">0.55</td>
                  <td class="level-3">0.57</td>
                  <td class="level-5">0.93</td>
                  <td class="ellipsis-cell">…</td>
                  <td class="level-5">0.81</td>
                </tr>
                <tr class="more-row">
                  <th>⋮</th>
                  <td>⋮</td>
                  <td>⋮</td>
                  <td>⋮</td>
                  <td>⋮</td>
                  <td>⋮</td>
                  <td>⋮</td>
                  <td class="ellipsis-cell">…</td>
                  <td>⋮</td>
                </tr>
                <tr class="last-row">
                  <th>tₘ</th>
                  <td class="level-4">0.76</td>
                  <td class="level-2">0.31</td>
                  <td class="level-5">0.88</td>
                  <td class="level-3">0.54</td>
                  <td class="level-2">0.39</td>
                  <td class="level-4">0.71</td>
                  <td class="ellipsis-cell">…</td>
                  <td class="level-3">0.62</td>
                </tr>
              </tbody>
            </table>
          </div>
          <div class="matrix-footer">
            <span><strong>M</strong> time points</span>
            <span class="dot">·</span>
            <span><strong>N</strong> genes</span>
            <span class="dot">·</span>
            <span>expression level at each time point</span>
          </div>
        </div>
        <div class="comparison-panel">
          <div class="section-label">WHY TIME-SERIES?</div>
          <p class="comparison-intro">
            Unlike steady-state measurements, time-series data capture
            <strong>how gene expression changes over time.</strong>
          </p>
          <div class="advantage-list">
            <div class="advantage-card">
              <div class="advantage-number">01</div>
              <div class="advantage-content">
                <h3>Capture temporal dynamics</h3>
                <p>
                  Observe how genes increase, decrease, or remain stable
                  across time.
                </p>
              </div>
            </div>
            <div class="advantage-card">
              <div class="advantage-number">02</div>
              <div class="advantage-content">
                <h3>Reveal regulatory responses</h3>
                <p>
                  Changes in one gene may precede and influence changes in
                  another.
                </p>
              </div>
            </div>
            <div class="advantage-card">
              <div class="advantage-number">03</div>
              <div class="advantage-content">
                <h3>Provide more information</h3>
                <p>
                  Multiple observations describe a trajectory rather than
                  a single static state.
                </p>
              </div>
            </div>
            <div class="advantage-card">
              <div class="advantage-number">04</div>
              <div class="advantage-content">
                <h3>Support network inference</h3>
                <p>
                  Temporal patterns provide clues about regulatory
                  dependencies between genes.
                </p>
              </div>
            </div>
          </div>
        </div>
      </section>
      <section class="takeaway">
        <span class="takeaway-mark"></span>
        <div class="takeaway-label">KEY IDEA</div>
        <p>
          Time-series data provide a <strong>dynamic view of gene expression</strong>,
          giving us more information about the underlying regulatory system.
        </p>
      </section>
    </div>
  </div>
</template>

<script setup>
</script>

<style scoped>
.data-slide {
  position: relative;
  width: 100%;
  height: 100%;
  min-width: 0;
  min-height: 0;
  background: #f8fafb;
  color: #24313a;
  overflow: hidden;
  font-family: 'Inter', 'Segoe UI', sans-serif;
  box-sizing: border-box;
}
.observed-data {
  width: 100%;
  height: 100%;
  min-width: 0;
  min-height: 0;
  display: flex;
  flex-direction: column;
  overflow: hidden;
  box-sizing: border-box;
}
.main-grid {
  flex: 0 0 auto;
  min-width: 0;
  min-height: 0;
  display: grid;
  grid-template-columns: minmax(0, 56%) minmax(0, 44%);
  overflow: hidden;
}
.data-panel {
  min-width: 0;
  min-height: 0;
  display: flex;
  flex-direction: column;
  padding: 20px 30px 0 4px;
  overflow: hidden;
  box-sizing: border-box;
}
.panel-header {
  flex: 0 0 auto;
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 12px;
  margin-bottom: 14px;
}
.section-label {
  color: #64748b;
  font-size: 9px;
  font-weight: 700;
  letter-spacing: 0.14em;
}
.panel-description {
  margin: 6px 0 0;
  color: #526273;
  font-size: 12px;
  line-height: 1.4;
}
.matrix-badge {
  flex: 0 0 auto;
  padding: 5px 9px;
  border: 1px solid #cbd9e1;
  border-radius: 6px;
  background: #ffffff;
  color: #20639b;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 9px;
  font-weight: 600;
}
.matrix-wrapper {
  flex: 0 1 auto;
  width: 100%;
  min-width: 0;
  min-height: 0;
  border: 1px solid #d5dfe5;
  border-radius: 9px;
  background: #ffffff;
  box-shadow: 0 2px 8px rgba(23, 63, 95, 0.04);
  overflow: hidden;
  box-sizing: border-box;
}
.expression-table {
  width: 100%;
  border-collapse: collapse;
  table-layout: fixed;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 9px;
}
.expression-table th,
.expression-table td {
  height: 25px;
  padding: 0 4px;
  border-right: 1px solid #e8edf0;
  border-bottom: 1px solid #e8edf0;
  text-align: center;
  box-sizing: border-box;
}
.expression-table th {
  background: #f1f5f7;
  color: #526273;
  font-weight: 700;
}
.expression-table thead th {
  height: 28px;
  color: #173f5f;
  font-size: 8.5px;
}
.expression-table .time-header {
  width: 47px;
  color: #64748b;
}
.expression-table tbody th {
  width: 47px;
  background: #f8fafb;
  color: #64748b;
}
.expression-table td {
  color: #334e5f;
  font-weight: 500;
}
.expression-table tr:last-child td,
.expression-table tr:last-child th {
  border-bottom: none;
}
.expression-table th:last-child,
.expression-table td:last-child {
  border-right: none;
}
.expression-table .ellipsis-cell {
  color: #94a3b8;
  background: #fafcfd;
  font-size: 12px;
}
.expression-table td.level-1 {
  background: #f6f9fa;
}
.expression-table td.level-2 {
  background: #edf4f7;
}
.expression-table td.level-3 {
  background: #e4eff4;
}
.expression-table td.level-4 {
  background: #d9e9f0;
}
.expression-table td.level-5 {
  background: #cce1eb;
}
.expression-table .more-row th,
.expression-table .more-row td {
  height: 22px;
  background: #fafcfd;
  color: #94a3b8;
  border-bottom: 1px dashed #dce4e9;
}
.expression-table .last-row th,
.expression-table .last-row td {
  border-bottom: none;
}
.matrix-footer {
  flex: 0 0 auto;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 7px;
  margin-top: 8px;
  color: #94a3b8;
  font-size: 9px;
}
.matrix-footer strong {
  color: #526273;
  font-family: 'IBM Plex Mono', monospace;
}
.matrix-footer .dot {
  color: #c2cbd1;
}
.comparison-panel {
  min-width: 0;
  min-height: 0;
  display: flex;
  flex-direction: column;
  padding: 20px 4px 0 26px;
  border-left: 1px solid #dce4e9;
  overflow: hidden;
  box-sizing: border-box;
}
.comparison-intro {
  flex: 0 0 auto;
  max-width: 430px;
  margin: 8px 0 14px;
  color: #526273;
  font-size: 13px;
  line-height: 1.45;
}
.comparison-intro strong {
  color: #173f5f;
}
.advantage-list {
  flex: 0 1 auto;
  min-height: 0;
  display: flex;
  flex-direction: column;
  gap: 6px;
  overflow: hidden;
}
.advantage-card {
  flex: 0 0 auto;
  display: grid;
  grid-template-columns: 30px minmax(0, 1fr);
  gap: 10px;
  align-items: start;
  padding: 7px 10px;
  border: 1px solid #dce4e9;
  border-radius: 8px;
  background: #ffffff;
  box-sizing: border-box;
}
.advantage-number {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 25px;
  height: 25px;
  border-radius: 6px;
  background: #edf5f9;
  color: #20639b;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 8px;
  font-weight: 700;
}
.advantage-content {
  min-width: 0;
}
.advantage-content h3 {
  margin: 1px 0 3px;
  color: #24313a;
  font-size: 11.5px;
  line-height: 1.25;
  font-weight: 700;
}
.advantage-content p {
  margin: 0;
  color: #64748b;
  font-size: 9.5px;
  line-height: 1.35;
}
.takeaway {
  flex: 0 0 auto;
  position: relative;
  display: grid;
  grid-template-columns: 75px minmax(0, 1fr);
  align-items: center;
  min-height: 42px;
  margin: 3px 4px 0;
  padding: 6px 25px;
  border: 1px solid #dce4e9;
  border-radius: 10px;
  background: #ffffff;
  box-sizing: border-box;
}
.takeaway-mark {
  position: absolute;
  left: 0;
  top: 9px;
  bottom: 9px;
  width: 4px;
  border-radius: 4px;
  background: #e9c46a;
}
.takeaway-label {
  color: #2a9d8f;
  font-size: 8px;
  font-weight: 700;
  letter-spacing: 0.13em;
}
.takeaway p {
  margin: 0;
  color: #526273;
  font-size: 12px;
  line-height: 1.35;
}
.takeaway strong {
  color: #173f5f;
  font-weight: 700;
}
</style>