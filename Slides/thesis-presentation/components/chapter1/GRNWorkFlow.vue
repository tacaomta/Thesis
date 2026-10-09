<template>
  <div class="workflow-slide">
    <!-- Main pipeline -->
    <div class="pipeline">
      <!-- 1. Data collection -->
      <div class="stage neutral">
        <div class="stage-icon">
          <svg viewBox="0 0 48 48" fill="none">
            <ellipse cx="24" cy="11" rx="15" ry="6"
              stroke="currentColor" stroke-width="2.2"/>
            <path d="M9 11v22c0 3.3 6.7 6 15 6s15-2.7 15-6V11"
              stroke="currentColor" stroke-width="2.2"/>
            <path d="M9 22c0 3.3 6.7 6 15 6s15-2.7 15-6"
              stroke="currentColor" stroke-width="2.2"/>
          </svg>
        </div>
        <span class="step">01</span>
        <h2>Data Collection</h2>
        <p>Gene expression<br />time series</p>
      </div>

      <div class="connector">
        <svg viewBox="0 0 40 20">
          <path d="M2 10H34M27 3l7 7-7 7"
            fill="none" stroke="currentColor"
            stroke-width="2" stroke-linecap="round"
            stroke-linejoin="round"/>
        </svg>
      </div>

      <!-- 2. Data representation -->
      <div class="stage representation">
        <div class="focus-tag">THESIS FOCUS</div>
        <div class="stage-icon">
          <svg viewBox="0 0 48 48" fill="none">
            <rect x="7" y="8" width="34" height="32" rx="4"
              stroke="currentColor" stroke-width="2.2"/>
            <path d="M14 17h20M14 24h20M14 31h12"
              stroke="currentColor" stroke-width="2.2"
              stroke-linecap="round"/>
            <circle cx="34" cy="31" r="3"
              fill="currentColor"/>
          </svg>
        </div>
        <span class="step">02</span>
        <h2>Data Representation</h2>
        <p>Discretization<br />Representation learning</p>
        <div class="methods">
          <span>MIDNI</span>
          <span>SITTF</span>
        </div>
      </div>

      <div class="connector">
        <svg viewBox="0 0 40 20">
          <path d="M2 10H34M27 3l7 7-7 7"
            fill="none" stroke="currentColor"
            stroke-width="2" stroke-linecap="round"
            stroke-linejoin="round"/>
        </svg>
      </div>

      <!-- 3. Network inference -->
      <div class="stage neutral">
        <div class="stage-icon">
          <svg viewBox="0 0 48 48" fill="none">
            <path d="M13 13L34 12M13 13L21 34M34 12L35 34M21 34L35 34"
              stroke="currentColor" stroke-width="2"/>
            <circle cx="13" cy="13" r="5"
              fill="#F8FAFB" stroke="currentColor" stroke-width="2.2"/>
            <circle cx="34" cy="12" r="5"
              fill="#F8FAFB" stroke="currentColor" stroke-width="2.2"/>
            <circle cx="21" cy="34" r="5"
              fill="#F8FAFB" stroke="currentColor" stroke-width="2.2"/>
            <circle cx="35" cy="34" r="5"
              fill="#F8FAFB" stroke="currentColor" stroke-width="2.2"/>
          </svg>
        </div>
        <span class="step">03</span>
        <h2>Network Inference</h2>
        <p>Infer regulatory<br />relationships</p>
      </div>

      <div class="connector">
        <svg viewBox="0 0 40 20">
          <path d="M2 10H34M27 3l7 7-7 7"
            fill="none" stroke="currentColor"
            stroke-width="2" stroke-linecap="round"
            stroke-linejoin="round"/>
        </svg>
      </div>

      <!-- 4. Evaluation -->
      <div class="stage neutral">
        <div class="stage-icon">
          <svg viewBox="0 0 48 48" fill="none">
            <path d="M8 39V9M8 39H41"
              stroke="currentColor" stroke-width="2.2"
              stroke-linecap="round"/>
            <path d="M13 31l8-9 7 4 10-14"
              stroke="currentColor" stroke-width="2.5"
              stroke-linecap="round" stroke-linejoin="round"/>
            <path d="M31 12h7v7"
              stroke="currentColor" stroke-width="2.2"
              stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
        </div>
        <span class="step">04</span>
        <h2>Evaluation</h2>
        <p>Network structure<br />Dynamic behavior</p>
      </div>
    </div>

    <!-- Data augmentation feedback path -->
    <div class="feedback">
      <div class="feedback-line">
        <span class="branch-label">LIMITED OBSERVATIONS</span>
      </div>

      <div class="augmentation">
        <div class="augmentation-icon">
          <svg viewBox="0 0 48 48" fill="none">
            <rect x="7" y="11" width="23" height="27" rx="3"
              stroke="currentColor" stroke-width="2.2"/>
            <path d="M14 19h9M14 25h9M14 31h5"
              stroke="currentColor" stroke-width="2"
              stroke-linecap="round"/>
            <path d="M32 15h9M36.5 10.5v9M32 31h9M36.5 26.5v9"
              stroke="currentColor" stroke-width="2.2"
              stroke-linecap="round"/>
          </svg>
        </div>

        <div class="augmentation-copy">
          <span class="focus-tag">THESIS FOCUS</span>
          <h2>Data Augmentation</h2>
          <p>Autoencoder-based time-series synthesis</p>
        </div>

        <div class="augmentation-result">
          <span class="result-symbol">+</span>
          <span>Synthetic<br />time-series data</span>
        </div>
      </div>

      <div class="feedback-return">
        <svg viewBox="0 0 680 48" preserveAspectRatio="none">
          <path d="M650 5 V22 Q650 35 637 35 H40 Q27 35 27 22 V5"
            fill="none" stroke="#C18B26" stroke-width="2.2"
            stroke-linecap="round" stroke-linejoin="round"/>
          <path d="M20 12l7-7 7 7"
            fill="none" stroke="#C18B26" stroke-width="2.2"
            stroke-linecap="round" stroke-linejoin="round"/>
        </svg>
        <span>Augmented data can be used for subsequent inference</span>
      </div>
    </div>

    <!-- Research scope -->
    <div class="scope">
      <span class="scope-marker"></span>
      <span>THIS THESIS</span>
      <span class="scope-divider"></span>
      <span>Improving how expression data are represented and how limited data are augmented</span>
    </div>
  </div>
</template>

<style scoped>
.workflow-slide {
  width: 100%;
  height: 100%;
  box-sizing: border-box;
  padding: 8px 4px 0;
  display: flex;
  flex-direction: column;
  gap: 16px;
  color: #24313A;
  overflow: hidden;
}

.pipeline {
  display: grid;
  grid-template-columns: minmax(0, 1fr) 30px minmax(0, 1.16fr) 30px minmax(0, 1fr) 30px minmax(0, 1fr);
  align-items: stretch;
  gap: 5px;
  flex-shrink: 0;
}

.stage {
  position: relative;
  min-width: 0;
  height: 218px;
  box-sizing: border-box;
  padding: 20px 10px 13px;
  border: 1px solid #DCE4E9;
  border-radius: 12px;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

.neutral {
  background: #FFFFFF;
  color: #64748B;
}

.representation {
  background: #EAF5F3;
  border: 2px solid #2A9D8F;
  color: #167D72;
  padding-top: 25px;
}

.focus-tag {
  display: inline-block;
  font-family: "IBM Plex Mono", "JetBrains Mono", monospace;
  font-size: 9px;
  font-weight: 700;
  letter-spacing: .1em;
  color: #167D72;
}

.representation > .focus-tag {
  position: absolute;
  top: 9px;
}

.stage-icon {
  width: 44px;
  height: 44px;
  margin-bottom: 5px;
}

.stage-icon svg {
  width: 100%;
  height: 100%;
}

.step {
  font-family: "IBM Plex Mono", "JetBrains Mono", monospace;
  font-size: 10px;
  color: #94A3B8;
  margin-bottom: 5px;
}

h2 {
  font-size: 14px;
  line-height: 1.25;
  margin: 0 0 8px;
  font-weight: 700;
  color: #173F5F;
}

p {
  margin: 0;
  font-size: 11px;
  line-height: 1.5;
  color: #64748B;
}

.methods {
  display: flex;
  justify-content: center;
  gap: 6px;
  flex-wrap: wrap;
  margin-top: auto;
  padding-top: 9px;
}

.methods span {
  border: 1px solid #B7DAD4;
  background: #FFFFFF;
  color: #167D72;
  padding: 4px 7px;
  border-radius: 5px;
  font-family: "IBM Plex Mono", "JetBrains Mono", monospace;
  font-size: 10px;
  font-weight: 700;
}

.connector {
  display: flex;
  align-items: center;
  justify-content: center;
  color: #AAB8C2;
}

.connector svg {
  width: 100%;
  max-width: 40px;
}

/* Data augmentation feedback */

.feedback {
  width: 100%;
  max-width: 680px;
  align-self: center;
  display: flex;
  flex-direction: column;
  align-items: stretch;
}

.feedback-line {
  height: 13px;
  border-top: 2px solid #E9C46A;
  border-left: 2px solid #E9C46A;
  border-right: 2px solid #E9C46A;
  border-radius: 8px 8px 0 0;
  position: relative;
  margin: 0 28px;
}

.branch-label {
  position: absolute;
  left: 50%;
  top: -8px;
  transform: translateX(-50%);
  padding: 0 10px;
  background: #F8FAFB;
  color: #986C13;
  font-family: "IBM Plex Mono", "JetBrains Mono", monospace;
  font-size: 9px;
  font-weight: 600;
  letter-spacing: .08em;
  white-space: nowrap;
}

.augmentation {
  display: flex;
  align-items: center;
  gap: 15px;
  padding: 13px 20px;
  background: #FFF7E6;
  border: 2px solid #E9C46A;
  border-radius: 11px;
  color: #986C13;
}

.augmentation-icon {
  width: 42px;
  height: 42px;
  flex-shrink: 0;
}

.augmentation-icon svg {
  width: 100%;
  height: 100%;
}

.augmentation-copy {
  flex: 1;
  min-width: 0;
}

.augmentation-copy .focus-tag {
  color: #986C13;
}

.augmentation-copy h2 {
  margin: 3px 0 4px;
  font-size: 16px;
  color: #173F5F;
}

.augmentation-copy p {
  color: #7C652F;
  font-size: 11px;
}

.augmentation-result {
  display: flex;
  align-items: center;
  gap: 8px;
  padding-left: 15px;
  border-left: 1px solid #E6D39E;
  color: #7C652F;
  font-size: 10px;
  line-height: 1.4;
  flex-shrink: 0;
}

.result-symbol {
  width: 28px;
  height: 28px;
  border-radius: 50%;
  display: grid;
  place-items: center;
  background: #E9C46A;
  color: #5C471A;
  font-size: 21px;
  font-weight: 500;
}

.feedback-return {
  height: 47px;
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 0;
}

.feedback-return svg {
  position: absolute;
  width: 100%;
  height: 38px;
  top: 0;
}

.feedback-return span {
  position: relative;
  margin-top: 24px;
  padding: 0 10px;
  background: #F8FAFB;
  color: #986C13;
  font-size: 10px;
  line-height: 1.4;
  text-align: center;
}

/* Thesis scope footer */

.scope {
  display: flex;
  align-items: center;
  gap: 9px;
  padding: 11px 13px;
  border-top: 1px solid #DCE4E9;
  color: #64748B;
  font-size: 10px;
  line-height: 1.4;
  flex-shrink: 0;
}

.scope-marker {
  width: 7px;
  height: 7px;
  border-radius: 50%;
  background: #2A9D8F;
  flex-shrink: 0;
}

.scope > span:nth-child(2) {
  font-family: "IBM Plex Mono", "JetBrains Mono", monospace;
  font-size: 9px;
  font-weight: 700;
  letter-spacing: .1em;
  color: #167D72;
  white-space: nowrap;
}

.scope-divider {
  height: 17px;
  width: 1px;
  background: #DCE4E9;
  flex-shrink: 0;
}

@media (max-width: 760px) {
  .workflow-slide {
    gap: 10px;
  }

  .pipeline {
    grid-template-columns: minmax(0, 1fr) 16px minmax(0, 1fr);
    row-gap: 10px;
  }

  .stage {
    height: 190px;
    padding-left: 5px;
    padding-right: 5px;
  }

  .pipeline > .connector:nth-of-type(4) {
    display: none;
  }

  .augmentation {
    padding: 10px;
    gap: 8px;
  }

  .augmentation-result {
    display: none;
  }

  .scope {
    align-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>