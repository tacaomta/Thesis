<template>
  <div class="proportion-slide">

    <div class="intro">
      Distribution of genes requiring two-level and three-level discretization
      across the evaluated datasets.
    </div>

    <div class="chart-area">
      <img
        src="../../public/images/proportion.png"
        alt="Proportion of two-level and three-level gene discretization"
        class="proportion-chart"
      />
    </div>

    <div class="key-message">
      <span class="message-label">KEY OBSERVATION</span>

      <span class="message-text">
        The proportion of three-level genes varies across datasets,
        indicating that a binary representation may not fully capture
        the observed gene expression dynamics.
      </span>
    </div>

  </div>
</template>

<style scoped>
.proportion-slide {
  width: 100%;
  height: 100%;
  min-height: 0;

  display: flex;
  flex-direction: column;

  box-sizing: border-box;
  overflow: hidden;
}

/* =========================
   Intro
   ========================= */

.intro {
  flex-shrink: 0;

  margin-bottom: 10px;

  color: #64748b;

  font-size: 13px;
  line-height: 1.4;
}


/* =========================
   Chart
   ========================= */

.chart-area {
  flex: 1 1 auto;
  min-height: 0;

  display: flex;
  align-items: center;
  justify-content: center;

  overflow: hidden;

  padding: 2px 20px;
  box-sizing: border-box;
}

.proportion-chart {
  display: block;

  width: 100%;
  height: 100%;

  object-fit: contain;
}


/* =========================
   Key message
   ========================= */

.key-message {
  flex-shrink: 0;

  display: flex;
  align-items: center;
  gap: 12px;

  margin-top: 10px;
  padding: 9px 13px;

  background: #f1f5f7;
  border-left: 3px solid #20639b;
  border-radius: 5px;

  color: #64748b;

  font-size: 10px;
  line-height: 1.4;

  box-sizing: border-box;
}

.message-label {
  flex-shrink: 0;

  color: #20639b;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 9px;
  font-weight: 700;
  letter-spacing: 0.06em;
}

.message-text {
  color: #475569;
}

</style>