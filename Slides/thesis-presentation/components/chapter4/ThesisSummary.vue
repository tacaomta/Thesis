<template>
  <div class="summary-slide">

    <!-- Progression timeline -->
    <div class="timeline">
      <div class="timeline-line"></div>
      <span class="timeline-dot dot-1"></span>
      <span class="timeline-dot dot-2"></span>
      <span class="timeline-dot dot-3"></span>
    </div>

    <!-- Main progression -->
    <div class="progression">

      <!-- Chapter 1 -->
      <div class="achievement" style="--accent: #20639B; --accent-soft: rgba(32, 99, 155, 0.08);">
        <div class="chapter">CHAPTER 1</div>

        <div class="icon">01</div>

        <h2>Better Discretization</h2>

        <div class="gap">
          <span class="gap-dot"></span>
          Discretization Gap
        </div>

        <p>
          Introduced <strong>multiple-level discretization</strong>
          to preserve more expression-level information than
          conventional Boolean representations.
        </p>

        <div class="result">
          <span class="result-flow">
            <span class="result-label">Contribution</span>
            <span class="result-arrow">→</span>
          </span>
          <span class="result-text">
            More informative expression states
          </span>
        </div>
      </div>

      <div class="arrow">
        <svg viewBox="0 0 24 24" class="arrow-icon">
          <path d="M4 12h15M14 6l6 6-6 6" />
        </svg>
      </div>

      <!-- Chapter 2 -->
      <div class="achievement" style="--accent: #7A5AF8; --accent-soft: rgba(122, 90, 248, 0.08);">
        <div class="chapter">CHAPTER 2</div>

        <div class="icon">02</div>

        <h2>Better Representation</h2>

        <div class="gap">
          <span class="gap-dot"></span>
          Representation Gap
        </div>

        <p>
          Developed <strong>SITTF</strong> to transform
          time-series expression data into a
          <strong>scale-independent representation</strong>
          for learning-based GRN inference.
        </p>

        <div class="result">
          <span class="result-flow">
            <span class="result-label">Contribution</span>
            <span class="result-arrow">→</span>
          </span>
          <span class="result-text">
            Reusable representation for different network sizes
          </span>
        </div>
      </div>

      <div class="arrow">
        <svg viewBox="0 0 24 24" class="arrow-icon">
          <path d="M4 12h15M14 6l6 6-6 6" />
        </svg>
      </div>

      <!-- Chapter 3 -->
      <div class="achievement" style="--accent: #2A9D8F; --accent-soft: rgba(42, 157, 143, 0.08);">
        <div class="chapter">CHAPTER 3</div>

        <div class="icon">03</div>

        <h2>Better Data</h2>

        <div class="gap">
          <span class="gap-dot"></span>
          Data Limitation Gap
        </div>

        <p>
          Proposed an <strong>autoencoder-based temporal
          data synthesis</strong> framework to generate
          additional time-series expression data.
        </p>

        <div class="result">
          <span class="result-flow">
            <span class="result-label">Contribution</span>
            <span class="result-arrow">→</span>
          </span>
          <span class="result-text">
            More data for more reliable GRN inference
          </span>
        </div>
      </div>

    </div>

    <!-- Bottom message -->
    <div class="thesis-message">
      <div class="message-dots">
        <span class="dot" style="--c: #20639B"></span>
        <span class="dot" style="--c: #7A5AF8"></span>
        <span class="dot" style="--c: #2A9D8F"></span>
      </div>

      <span class="message-label">OVERALL CONTRIBUTION</span>

      <div class="message-title">
        From <span>Better Inference</span> to <span>Better Data</span>
      </div>

      <div class="message-subtitle">
        A progressive strategy for improving GRN inference
        from time-series gene expression data.
      </div>
    </div>

  </div>
</template>

<style scoped>
.summary-slide {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  box-sizing: border-box;
  padding: 6px 10px 4px;
  color: #24313A;

  font-family: Inter, 'Segoe UI', sans-serif;
}

/* ─────────────────────────────
   Timeline strip
───────────────────────────── */

.timeline {
  position: relative;
  height: 14px;
  flex-shrink: 0;

  margin: 0 20px 6px;
}

.timeline-line {
  position: absolute;
  left: 16.5%;
  right: 16.5%;
  top: 50%;

  height: 2px;
  transform: translateY(-50%);

  background: linear-gradient(
    90deg,
    #20639B 0%,
    #7A5AF8 50%,
    #2A9D8F 100%
  );

  border-radius: 2px;

  opacity: 0;
  animation: lineGrow 0.6s ease forwards 0.1s;
  transform-origin: left center;
}

@keyframes lineGrow {
  from {
    opacity: 0;
    transform: translateY(-50%) scaleX(0);
  }
  to {
    opacity: 1;
    transform: translateY(-50%) scaleX(1);
  }
}

.timeline-dot {
  position: absolute;
  top: 50%;

  width: 9px;
  height: 9px;

  border-radius: 50%;
  border: 2px solid #ffffff;

  transform: translate(-50%, -50%) scale(0);
  animation: dotPop 0.35s ease forwards;
}

.dot-1 { left: 16.5%; background: #20639B; animation-delay: 0.15s; }
.dot-2 { left: 50%;   background: #7A5AF8; animation-delay: 0.45s; }
.dot-3 { left: 83.5%; background: #2A9D8F; animation-delay: 0.75s; }

@keyframes dotPop {
  from { transform: translate(-50%, -50%) scale(0); }
  70%  { transform: translate(-50%, -50%) scale(1.3); }
  to   { transform: translate(-50%, -50%) scale(1); }
}

/* ─────────────────────────────
   Three achievements
───────────────────────────── */

.progression {
  display: grid;
  grid-template-columns: 1fr 34px 1fr 34px 1fr;
  align-items: stretch;
  gap: 8px;
  flex: 1;
  min-height: 0;
}

.achievement {
  position: relative;
  display: flex;
  flex-direction: column;
  padding: 18px 20px 16px;

  background: #FFFFFF;
  border: 1px solid #DCE4E9;
  border-radius: 12px;
  box-sizing: border-box;

  opacity: 0;
  transform: translateY(14px);
  animation: cardIn 0.5s ease forwards;
}

.progression > .achievement:nth-child(1) { animation-delay: 0.25s; }
.progression > .achievement:nth-child(3) { animation-delay: 0.55s; }
.progression > .achievement:nth-child(5) { animation-delay: 0.85s; }

@keyframes cardIn {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.achievement::before {
  content: '';

  position: absolute;
  top: 0;
  left: 0;
  right: 0;

  height: 4px;

  background: var(--accent);
  border-radius: 12px 12px 0 0;
}

.chapter {
  font-family: "IBM Plex Mono", "JetBrains Mono", monospace;
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.12em;
  color: #64748B;
}

.icon {
  width: 38px;
  height: 38px;
  margin-top: 12px;
  border-radius: 9px;
  display: flex;
  align-items: center;
  justify-content: center;

  background: var(--accent-soft);
  color: var(--accent);

  font-family: "IBM Plex Mono", "JetBrains Mono", monospace;
  font-size: 13px;
  font-weight: 700;
}

h2 {
  margin: 12px 0 6px;
  font-size: 21px;
  line-height: 1.15;
  font-weight: 700;
  color: #173F5F;

  font-family: inherit;
}

.gap {
  display: inline-flex;
  align-items: center;
  gap: 6px;

  align-self: flex-start;

  padding: 4px 9px 4px 7px;
  margin-bottom: 12px;

  border-radius: 999px;
  background: var(--accent-soft);
  border: 1px solid transparent;

  font-size: 10px;
  font-weight: 600;
  letter-spacing: 0.04em;
  color: var(--accent);
}

.gap-dot {
  width: 5px;
  height: 5px;
  flex-shrink: 0;

  border-radius: 50%;
  background: var(--accent);
}

p {
  margin: 0;
  font-size: 13px;
  line-height: 1.55;
  color: #475569;

  font-family: inherit;
}

p strong {
  color: #24313A;
  font-weight: 650;
}

.result {
  margin-top: auto;
  padding-top: 13px;
  border-top: 1px solid #E8EDF0;
}

.result-flow {
  display: flex;
  align-items: center;
  gap: 5px;

  margin-bottom: 4px;
}

.result-label {
  font-family: "IBM Plex Mono", "JetBrains Mono", monospace;
  font-size: 9px;
  font-weight: 600;
  letter-spacing: 0.1em;
  color: var(--accent);
}

.result-arrow {
  color: var(--accent);
  font-size: 11px;
  line-height: 1;
}

.result-text {
  display: block;
  font-size: 11px;
  line-height: 1.35;
  font-weight: 600;
  color: #334155;
}

/* ─────────────────────────────
   Arrows between cards
───────────────────────────── */

.arrow {
  display: flex;
  align-items: center;
  justify-content: center;

  opacity: 0;
  animation: arrowIn 0.4s ease forwards;
}

.progression > .arrow:nth-child(2) { animation-delay: 0.45s; }
.progression > .arrow:nth-child(4) { animation-delay: 0.75s; }

@keyframes arrowIn {
  from { opacity: 0; transform: translateX(-4px); }
  to   { opacity: 1; transform: translateX(0); }
}

.arrow-icon {
  width: 20px;
  height: 20px;

  fill: none;
  stroke: #A5B4BE;
  stroke-width: 2;
  stroke-linecap: round;
  stroke-linejoin: round;
}

/* ─────────────────────────────
   Overall message
───────────────────────────── */

.thesis-message {
  flex-shrink: 0;

  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;

  margin-top: 14px;
  padding: 16px 24px 14px;

  background: #F8FAFB;
  border: 1px solid #DCE4E9;
  border-top: none;
  border-radius: 0 0 10px 10px;
  border-bottom: 3px solid #173F5F;

  opacity: 0;
  animation: cardIn 0.5s ease forwards 1.05s;
}

.message-dots {
  display: flex;
  gap: 5px;

  margin-bottom: 8px;
}

.message-dots .dot {
  width: 6px;
  height: 6px;

  border-radius: 50%;
  background: var(--c);
}

.message-label {
  font-family: "IBM Plex Mono", "JetBrains Mono", monospace;
  font-size: 9px;
  font-weight: 600;
  letter-spacing: 0.14em;
  color: #64748B;
}

.message-title {
  margin-top: 5px;

  font-size: 22px;
  line-height: 1.2;
  font-weight: 700;
  color: #173F5F;
}

.message-title span {
  background: linear-gradient(90deg, #20639B, #7A5AF8 50%, #2A9D8F);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}

.message-subtitle {
  margin-top: 5px;
  font-size: 11px;
  color: #64748B;
}

/* ─────────────────────────────
   Reduced motion
───────────────────────────── */

@media (prefers-reduced-motion: reduce) {
  .timeline-line,
  .timeline-dot,
  .achievement,
  .arrow,
  .thesis-message {
    animation: none !important;
    opacity: 1 !important;
    transform: none !important;
  }
}
</style>