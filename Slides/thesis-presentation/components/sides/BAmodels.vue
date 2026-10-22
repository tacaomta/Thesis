<template>
  <div class="algo-slide">

    <div class="algo-columns">

      <!-- ===================================== -->
      <!-- ALGORITHM S1                           -->
      <!-- ===================================== -->
      <div class="algo-card mifs-card">

        <div class="algo-card-header">
          <div class="algo-title">
            Algorithm S1 <span class="algo-args">RandomUpdateFunction</span>
          </div>

          <div class="algo-caption">
            <span><strong>G(V, A)</strong> — regulatory graph</span>
          </div>
        </div>

        <div class="algo-body">

          <div class="code-line">
            <span class="ln">1</span>
            <span class="kw loop">for each</span>
            <span class="code">v ∈ V <span class="kw loop">do</span></span>
          </div>

          <div class="code-line indent-1">
            <span class="ln">2</span>
            <span class="code">let u<sub>1</sub>, u<sub>2</sub>, …, u<sub>k</sub> regulating v in G</span>
          </div>

          <div class="code-line indent-1">
            <span class="ln">3</span>
            <span class="code">let l<sub>1</sub>, …, l<sub>k</sub>, l — levels of u<sub>1</sub>, …, u<sub>k</sub>, v</span>
          </div>

          <div class="code-line indent-1">
            <span class="ln">4</span>
            <span class="kw loop">for each</span>
            <span class="code">x ∈ {0,…,l<sub>1</sub>−1} × … × {0,…,l<sub>k</sub>−1} <span class="kw loop">do</span></span>
          </div>

          <div class="code-line indent-2">
            <span class="ln">5</span>
            <span class="kw">F<sub>v</sub>(x)</span>
            <span class="code">← randint(0, l−1)</span>
          </div>

          <div class="code-line indent-1">
            <span class="ln">6</span>
            <span class="kw loop">end for</span>
          </div>

          <div class="code-line">
            <span class="ln">7</span>
            <span class="kw loop">end for</span>
          </div>

          <div class="code-line return-line">
            <span class="ln">8</span>
            <span class="kw ret">return</span>
            <span class="code">{F<sub>v</sub> | v ∈ V}</span>
          </div>

        </div>

      </div>

      <!-- ===================================== -->
      <!-- ALGORITHM S2                           -->
      <!-- ===================================== -->
      <div class="algo-card swap-card">

        <div class="algo-card-header">
          <div class="algo-title">
            Algorithm S2 <span class="algo-args">RandomGeneExpression</span>
          </div>

          <div class="algo-caption">
            <span><strong>G(V, A)</strong>, <strong>F<sub>v</sub></strong>, <strong>K</strong> — graph, update functions, time steps</span>
          </div>
        </div>

        <div class="algo-body">

          <div class="code-line">
            <span class="ln">1</span>
            <span class="kw loop">for each</span>
            <span class="code">v ∈ V <span class="kw loop">do</span></span>
          </div>

          <div class="code-line indent-1">
            <span class="ln">2</span>
            <span class="code">let l — discretization level of v</span>
          </div>

          <div class="code-line indent-1">
            <span class="ln">3</span>
            <span class="kw">v(0)</span>
            <span class="code">← randint(0, l−1)</span>
          </div>

          <div class="code-line">
            <span class="ln">4</span>
            <span class="kw loop">end for</span>
          </div>

          <div class="code-line">
            <span class="ln">5</span>
            <span class="kw loop">for</span>
            <span class="code">t = 1 <span class="kw loop">to</span> K <span class="kw loop">do</span></span>
          </div>

          <div class="code-line indent-1">
            <span class="ln">6</span>
            <span class="kw loop">for each</span>
            <span class="code">v ∈ V <span class="kw loop">do</span></span>
          </div>

          <div class="code-line indent-2">
            <span class="ln">7</span>
            <span class="code">let u<sub>1</sub>, …, u<sub>k</sub> regulating v in G</span>
          </div>

          <div class="code-line indent-2">
            <span class="ln">8</span>
            <span class="kw">x</span>
            <span class="code">= (u<sub>1</sub>(t−1), …, u<sub>k</sub>(t−1))</span>
          </div>

          <div class="code-line indent-2">
            <span class="ln">9</span>
            <span class="kw">v(t+1)</span>
            <span class="code">← F<sub>v</sub>(x)</span>
          </div>

          <div class="code-line indent-1">
            <span class="ln">10</span>
            <span class="kw loop">end for</span>
          </div>

          <div class="code-line">
            <span class="ln">11</span>
            <span class="kw loop">end for</span>
          </div>

          <div class="code-line return-line">
            <span class="ln">12</span>
            <span class="kw ret">return</span>
            <span class="code">{v(t) | v ∈ V, t ∈ {0,…,K}}</span>
          </div>

        </div>

      </div>

    </div>

  </div>
</template>

<script setup>
</script>

<style scoped>
.algo-slide {
  width: 100%;
  height: 100%;
  box-sizing: border-box;

  display: flex;
  flex-direction: column;

  padding: 12px 26px 10px;

  background: #f8fafb;
  color: #24313a;

  font-family: 'Inter', 'Segoe UI', sans-serif;
}

/* =========================
   HEADER
========================= */

.algo-header {
  flex-shrink: 0;
  margin-bottom: 12px;
}

.eyebrow {
  margin-bottom: 4px;

  color: #64748b;

  font-size: 10px;
  font-weight: 700;
  letter-spacing: 0.14em;
}

.algo-header h1 {
  margin: 0;

  color: #173f5f;

  font-size: 20px;
  line-height: 1.25;
  font-weight: 750;
  letter-spacing: -0.01em;
}

/* =========================
   TWO-COLUMN LAYOUT
========================= */

.algo-columns {
  flex: 1;
  min-height: 0;

  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 18px;
}

/* =========================
   ALGORITHM CARD
========================= */

.algo-card {
  min-width: 0;
  min-height: 0;

  display: flex;
  flex-direction: column;

  border: 1px solid #dce4e9;
  border-radius: 12px;

  background: #ffffff;

  box-sizing: border-box;

  overflow: hidden;
}

.mifs-card {
  border-top: 5px solid #20639b;
}

.swap-card {
  border-top: 5px solid #2a9d8f;
}

.algo-card-header {
  flex-shrink: 0;

  padding: 10px 18px 9px;

  border-bottom: 1px solid #eef1f3;

  background: #f8fafb;
}

.algo-title {
  color: #173f5f;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 14px;
  font-weight: 700;

  display: flex;
  flex-wrap: wrap;
  align-items: baseline;
  gap: 7px;
}

.mifs-card .algo-args {
  color: #20639b;
}

.swap-card .algo-args {
  color: #2a9d8f;
}

.algo-args {
  font-weight: 700;
}

.algo-caption {
  margin-top: 5px;

  color: #64748b;

  font-size: 12px;
  line-height: 1.4;
}

.mifs-card .algo-caption strong {
  color: #20639b;
}

.swap-card .algo-caption strong {
  color: #2a9d8f;
}

.algo-caption strong {
  font-family: 'IBM Plex Mono', monospace;
  font-weight: 700;
}

/* =========================
   PSEUDOCODE BODY
========================= */

.algo-body {
  flex: 1;
  min-height: 0;

  display: flex;
  flex-direction: column;
  justify-content: flex-start;

  gap: 5px;

  padding: 13px 20px;

  overflow-y: auto;
}

.code-line {
  display: flex;
  align-items: baseline;
  flex-wrap: wrap;

  gap: 9px;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 13px;
  line-height: 1.4;

  color: #24313a;
}

.code-line.indent-1 {
  padding-left: 20px;
}

.code-line.indent-2 {
  padding-left: 40px;
}

.ln {
  flex-shrink: 0;

  width: 16px;

  text-align: right;

  color: #cbd5dc;

  font-size: 9.5px;
  font-weight: 600;
}

.kw {
  flex-shrink: 0;

  color: #173f5f;
  font-weight: 700;
}

.kw.loop {
  color: #20639b;
}

.swap-card .kw.loop {
  color: #2a9d8f;
}

.kw.ret {
  color: #2a9d8f;
}

.code {
  min-width: 0;

  color: #475569;
}

.return-line {
  margin-top: 3px;
  padding-top: 7px;

  border-top: 1px dashed #dce4e9;
}

/* =========================
   RESPONSIVE
========================= */

@media (max-width: 900px) {
  .algo-columns {
    grid-template-columns: 1fr;
    overflow-y: auto;
  }
}
</style>