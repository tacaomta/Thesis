<template>
  <div class="algo-slide">

    <div class="algo-card mifs-card">

      <div class="algo-card-header">
        <div class="algo-title">
          MIFS<span class="algo-args">(v<sub>0</sub>, W, k)</span>
        </div>

        <div class="algo-caption">
          <span><strong>v<sub>0</sub></strong> — target variable</span>
          <span><strong>W = {w<sub>1</sub>,…,w<sub>M</sub>}</strong> — set of candidate variables</span>
          <span><strong>k</strong> — desired number of input variables</span>
        </div>
      </div>

      <div class="algo-body">

        <div class="code-line">
          <span class="ln">1</span>
          <span class="kw req">Require</span>
          <span class="code">k ≥ 1, &nbsp; |W| ≥ 1</span>
        </div>

        <div class="code-line">
          <span class="ln">2</span>
          <span class="kw">S</span>
          <span class="code">← ∅</span>
        </div>

        <div class="code-line">
          <span class="ln">3</span>
          <span class="kw">v</span>
          <span class="code">← argmax<sub>w∈W</sub> I(v<sub>0</sub>; w)</span>
        </div>

        <div class="code-line">
          <span class="ln">4</span>
          <span class="kw">S</span>
          <span class="code">← S ∪ {v}</span>
        </div>

        <div class="code-line">
          <span class="ln">5</span>
          <span class="kw">W</span>
          <span class="code">← W \ {v}</span>
        </div>

        <div class="code-line">
          <span class="ln">6</span>
          <span class="kw loop">while</span>
          <span class="code">|S| ≤ k <span class="kw loop">do</span></span>
        </div>

        <div class="code-line indent-1">
          <span class="ln">7</span>
          <span class="kw">v</span>
          <span class="code">← argmax<sub>w∈W</sub> ( I(v<sub>0</sub>; w) − Σ<sub>s∈S</sub> I(w; s) )</span>
        </div>

        <div class="code-line indent-1">
          <span class="ln">8</span>
          <span class="kw">S</span>
          <span class="code">← S ∪ {v}</span>
        </div>

        <div class="code-line indent-1">
          <span class="ln">9</span>
          <span class="kw">W</span>
          <span class="code">← W \ {v}</span>
        </div>

        <div class="code-line">
          <span class="ln">10</span>
          <span class="kw loop">end while</span>
        </div>

        <div class="code-line return-line">
          <span class="ln">11</span>
          <span class="kw ret">return</span>
          <span class="code">S</span>
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

  padding: 12px 32px 8px;

  background: #f8fafb;
  color: #24313a;

  font-family: 'Inter', 'Segoe UI', sans-serif;
}

/* =========================
   HEADER
========================= */

.algo-header {
  flex-shrink: 0;
  margin-bottom: 10px;
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

  font-size: 22px;
  line-height: 1.2;
  font-weight: 750;
  letter-spacing: -0.01em;
}

/* =========================
   ALGORITHM CARD
========================= */

.algo-card {
  flex: 1;
  min-height: 0;

  display: flex;
  flex-direction: column;

  border: 1px solid #dce4e9;
  border-top: 3px solid #20639b;
  border-radius: 12px;

  background: #ffffff;

  box-sizing: border-box;

  overflow: hidden;
}

.algo-card-header {
  flex-shrink: 0;

  padding: 12px 26px 10px;

  border-bottom: 1px solid #eef1f3;

  background: #f8fafb;
}

.algo-title {
  color: #173f5f;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 19px;
  font-weight: 700;
}

.algo-args {
  color: #20639b;
  font-weight: 700;
}

.algo-caption {
  display: flex;
  flex-wrap: wrap;
  gap: 4px 18px;

  margin-top: 7px;

  color: #64748b;

  font-size: 11px;
  line-height: 1.4;
}

.algo-caption strong {
  color: #20639b;

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

  gap: 7px;

  padding: 16px 34px;

  overflow-y: auto;
}

.code-line {
  display: flex;
  align-items: baseline;

  gap: 13px;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 15.5px;
  line-height: 1.4;

  color: #24313a;
}

.code-line.indent-1 {
  padding-left: 36px;
}

.ln {
  flex-shrink: 0;

  width: 20px;

  text-align: right;

  color: #cbd5dc;

  font-size: 12px;
  font-weight: 600;
}

.kw {
  flex-shrink: 0;

  color: #173f5f;
  font-weight: 700;
}

.kw.req {
  color: #8a6a12;
}

.kw.loop {
  color: #20639b;
}

.kw.ret {
  color: #2a9d8f;
}

.code {
  min-width: 0;

  color: #475569;
}

.return-line {
  margin-top: 5px;
  padding-top: 9px;

  border-top: 1px dashed #dce4e9;
}

/* =========================
   NOTE
========================= */

.algo-note {
  flex-shrink: 0;

  display: flex;
  align-items: center;

  gap: 12px;

  margin-top: 10px;
  padding: 10px 18px;

  border-left: 4px solid #20639b;
  border-radius: 6px;

  background: #ffffff;
  border-top: 1px solid #dce4e9;
  border-right: 1px solid #dce4e9;
  border-bottom: 1px solid #dce4e9;

  color: #475569;

  font-size: 12px;
  line-height: 1.45;
}

.algo-note strong {
  color: #173f5f;
  font-weight: 700;
}

.note-mark {
  flex-shrink: 0;

  width: 6px;
  height: 6px;

  border-radius: 50%;

  background: #20639b;
}
</style>