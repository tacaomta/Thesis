<template>
  <div class="algo-slide">

    <div class="algo-card swap-card">

      <div class="algo-card-header">
        <div class="algo-title">
          SWAP<span class="algo-args">(v<sub>0</sub>, S, W)</span>
        </div>

        <div class="algo-caption">
          <span><strong>v<sub>0</sub></strong> — target variable</span>
          <span><strong>S = {s<sub>1</sub>,…,s<sub>k</sub>}</strong> — selected variables, ranked by I(v<sub>0</sub>; s<sub>i</sub>)</span>
          <span><strong>W = {w<sub>1</sub>,…,w<sub>M</sub>}</strong> — unselected variables, ranked by I(v<sub>0</sub>; w<sub>i</sub>)</span>
        </div>
      </div>

      <div class="algo-body">

        <div class="code-line">
          <span class="ln">1</span>
          <span class="kw">v<sub>0</sub>′</span>
          <span class="code">← search_update_rule(v<sub>0</sub>, S)</span>
        </div>

        <div class="code-line">
          <span class="ln">2</span>
          <span class="kw">E<sub>MAX</sub></span>
          <span class="code">← E(v<sub>0</sub>, v<sub>0</sub>′)</span>
        </div>

        <div class="code-line">
          <span class="ln">3</span>
          <span class="kw">i</span>
          <span class="code">← 1</span>
        </div>

        <div class="code-line">
          <span class="ln">4</span>
          <span class="kw loop">while</span>
          <span class="code">i ≤ M <span class="kw loop">do</span></span>
        </div>

        <div class="code-line indent-1">
          <span class="ln">5</span>
          <span class="kw">j</span>
          <span class="code">← 1</span>
        </div>

        <div class="code-line indent-1">
          <span class="ln">6</span>
          <span class="kw loop">while</span>
          <span class="code">j ≤ K <span class="kw loop">do</span></span>
        </div>

        <div class="code-line indent-2">
          <span class="ln">7</span>
          <span class="kw">v<sub>0</sub>′</span>
          <span class="code">← search_update_rule( v<sub>0</sub>, S ∪ {w<sub>j</sub>} \ {s<sub>j</sub>} )</span>
        </div>

        <div class="code-line indent-2">
          <span class="ln">8</span>
          <span class="kw cond">if</span>
          <span class="code">E(v<sub>0</sub>, v<sub>0</sub>′) &gt; E<sub>MAX</sub> <span class="kw cond">then</span></span>
        </div>

        <div class="code-line indent-3">
          <span class="ln">9</span>
          <span class="code">S ← S ∪ {w<sub>j</sub>} \ {s<sub>j</sub>} &nbsp;,&nbsp; W ← W ∪ {s<sub>j</sub>} \ {w<sub>j</sub>}</span>
        </div>

        <div class="code-line indent-3">
          <span class="ln">10</span>
          <span class="kw">E<sub>MAX</sub></span>
          <span class="code">← E(v<sub>0</sub>, v<sub>0</sub>′)</span>
        </div>

        <div class="code-line indent-2">
          <span class="ln">11</span>
          <span class="kw cond">end if</span>
        </div>

        <div class="code-line indent-1">
          <span class="ln">12</span>
          <span class="kw loop">end while</span>
          <span class="code dim">(inner, over j)</span>
        </div>

        <div class="code-line">
          <span class="ln">13</span>
          <span class="kw loop">end while</span>
          <span class="code dim">(outer, over i)</span>
        </div>

        <div class="code-line return-line">
          <span class="ln">14</span>
          <span class="kw ret">return</span>
          <span class="code">(S, E<sub>MAX</sub>)</span>
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
  border-top: 3px solid #2a9d8f;
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
  color: #2a9d8f;
  font-weight: 700;
}

.algo-caption {
  display: flex;
  flex-wrap: wrap;
  gap: 3px 16px;

  margin-top: 6px;

  color: #64748b;

  font-size: 10.5px;
  line-height: 1.4;
}

.algo-caption strong {
  color: #2a9d8f;

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

  gap: 4px;

  padding: 14px 32px;

  overflow-y: auto;
}

.code-line {
  display: flex;
  align-items: baseline;

  gap: 12px;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 14px;
  line-height: 1.35;

  color: #24313a;
}

.code-line.indent-1 {
  padding-left: 32px;
}

.code-line.indent-2 {
  padding-left: 64px;
}

.code-line.indent-3 {
  padding-left: 96px;
}

.ln {
  flex-shrink: 0;

  width: 20px;

  text-align: right;

  color: #cbd5dc;

  font-size: 11px;
  font-weight: 600;
}

.kw {
  flex-shrink: 0;

  color: #173f5f;
  font-weight: 700;
}

.kw.loop {
  color: #2a9d8f;
}

.kw.cond {
  color: #8a6a12;
}

.kw.ret {
  color: #2a9d8f;
}

.code {
  min-width: 0;

  color: #475569;
}

.code.dim {
  color: #94a3b8;
  font-size: 11.5px;
  font-style: italic;
}

.return-line {
  margin-top: 4px;
  padding-top: 8px;

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

  margin-top: 9px;
  padding: 9px 18px;

  border-left: 4px solid #2a9d8f;
  border-radius: 6px;

  background: #ffffff;
  border-top: 1px solid #dce4e9;
  border-right: 1px solid #dce4e9;
  border-bottom: 1px solid #dce4e9;

  color: #475569;

  font-size: 11.5px;
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

  background: #2a9d8f;
}
</style>