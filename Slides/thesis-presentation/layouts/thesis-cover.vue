<template>
  <div class="thesis-cover">

    <div class="top-accent"></div>

    <!-- Corner frame — formal but not a full enclosing box -->
    <div class="corner-frame">
      <span class="corner tl"></span>
      <span class="corner tr"></span>
      <span class="corner bl"></span>
      <span class="corner br"></span>
    </div>

    <div class="background-network">
      <slot name="network" />
    </div>

    <div class="cover-main">

      <!-- Institution header -->
      <div class="institution">
        <img
          src="../public/images/uou.jpg"
          class="ulsan-logo"
          alt="University of Ulsan"
        />

        <div class="institution-text">
          <div class="university-name">UNIVERSITY OF ULSAN</div>
          <div class="graduate-school">GRADUATE SCHOOL</div>
          <div class="department">
            Department of Electrical, Electronic and Computer Engineering
          </div>
        </div>

        <!-- Academic seal placeholder -->
        <div class="seal" aria-hidden="true">
          <svg viewBox="0 0 100 100" class="seal-svg">
            <circle cx="50" cy="50" r="46" class="seal-ring-outer" />
            <circle cx="50" cy="50" r="38" class="seal-ring-inner" />
            <text x="50" y="46" class="seal-text-top">UNIVERSITY</text>
            <text x="50" y="58" class="seal-text-bottom">OF ULSAN</text>
            <path
              d="M 50 65 L 44 76 L 56 76 Z"
              class="seal-mark"
            />
          </svg>
        </div>
      </div>

      <!-- Degree label -->
      <div class="thesis-label">DOCTORAL DISSERTATION</div>
      <div class="title-accent"></div>

      <h1>
        Inferring Gene Regulatory Networks from Time-Series Gene Expression Data
      </h1>

      <!-- Formal degree statement -->
      <!-- <p class="degree-statement">
        A dissertation submitted in partial fulfillment of the requirements
        for the degree of <strong>Doctor of Philosophy</strong>
        in Electrical, Electronic and Computer Engineering
      </p> -->

      <div class="author-block">
        <div class="person-row">
          <span class="person-label">Author</span>
          <span class="person-value">Cao Tuan Anh</span>
        </div>

        <div class="person-row">
          <span class="person-label">Supervisor</span>
          <span class="person-value">Prof. Yung Keun Kwon</span>
        </div>
      </div>

    </div>

    <div class="cover-bottom">
      <div class="lab-name">
        COMPLEX SYSTEMS COMPUTING LAB
      </div>

      <div class="date">
        November 2026
      </div>
    </div>

  </div>
</template>

<style scoped>
.thesis-cover {
  position: relative;
  width: 100%;
  height: 100%;
  overflow: hidden;

  background: #f8fafb;
  color: #24313a;

  font-family: Inter, 'Segoe UI', sans-serif;
}

.top-accent {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 5px;

  background: #173f5f;
}

/* ─────────────────────────────
   CORNER FRAME
   Thin "bracket" corners, not a
   closed box — formal without
   feeling heavy or decorative.
───────────────────────────── */

.corner-frame {
  position: absolute;
  inset: 22px;
  z-index: 1;

  pointer-events: none;
}

.corner {
  position: absolute;
  width: 26px;
  height: 26px;

  border-color: #AAB8C2;
  border-style: solid;
  border-width: 0;
}

.corner.tl {
  top: 0;
  left: 0;
  border-top-width: 1.5px;
  border-left-width: 1.5px;
}

.corner.tr {
  top: 0;
  right: 0;
  border-top-width: 1.5px;
  border-right-width: 1.5px;
}

.corner.bl {
  bottom: 0;
  left: 0;
  border-bottom-width: 1.5px;
  border-left-width: 1.5px;
}

.corner.br {
  bottom: 0;
  right: 0;
  border-bottom-width: 1.5px;
  border-right-width: 1.5px;
}

.background-network {
  position: absolute;
  top: 80px;
  right: -20px;
  width: 48%;
  height: 75%;

  opacity: 0.14;
  z-index: 0;
}

/* ─────────────────────────────
   MAIN CONTENT
───────────────────────────── */

.cover-main {
  position: relative;
  z-index: 2;

  width: 80%;
  height: 100%;

  padding: 50px 0 78px 72px;
  box-sizing: border-box;
}

.institution {
  display: flex;
  align-items: flex-start;
  gap: 18px;
}

.ulsan-logo {
  width: 64px;
  height: 64px;

  object-fit: contain;
  flex-shrink: 0;
}

.institution-text {
  display: flex;
  flex-direction: column;
  gap: 4px;

  flex: 1;
  min-width: 0;
}

.university-name {
  color: #173f5f;

  font-size: 17px;
  font-weight: 700;
  letter-spacing: 0.08em;
}

.graduate-school {
  color: #2a9d8f;

  font-family: "IBM Plex Mono", "JetBrains Mono", monospace;
  font-size: 9.5px;
  font-weight: 600;
  letter-spacing: 0.16em;
}

.department {
  max-width: 560px;
  margin-top: 2px;

  color: #64748b;

  font-size: 11.5px;
  line-height: 1.4;
}

/* Academic seal */

.seal {
  flex-shrink: 0;

  width: 58px;
  height: 58px;

  margin-left: auto;
  margin-right: -130px;
}

.seal-svg {
  width: 100%;
  height: 100%;
}

.seal-ring-outer {
  fill: none;
  stroke: #173f5f;
  stroke-width: 1.4;
}

.seal-ring-inner {
  fill: none;
  stroke: #AAB8C2;
  stroke-width: 0.8;
  stroke-dasharray: 2 2;
}

.seal-text-top,
.seal-text-bottom {
  fill: #173f5f;

  font-family: "IBM Plex Mono", "JetBrains Mono", monospace;
  font-size: 7px;
  font-weight: 700;
  letter-spacing: 0.04em;
  text-anchor: middle;
}

.seal-mark {
  fill: #2a9d8f;
}

/* ─────────────────────────────
   TITLE BLOCK
───────────────────────────── */

.thesis-label {
  margin-top: 56px;

  color: #2a9d8f;

  font-family: "IBM Plex Mono", "JetBrains Mono", monospace;
  font-size: 13px;
  font-weight: 700;
  letter-spacing: 0.22em;
}

.title-accent {
  width: 62px;
  height: 4px;

  margin-top: 16px;

  border-radius: 2px;
  background: #173f5f;
}

h1 {
  max-width: 820px;
  margin-top: 24px;

  color: #173f5f;

  font-family: "Source Serif Pro", "Georgia", serif;
  font-size: 36px;
  line-height: 1.17;
  font-weight: 700;
  letter-spacing: -0.015em;
}

.degree-statement {
  max-width: 620px;
  margin-top: 20px;

  color: #64748b;

  font-size: 12.5px;
  line-height: 1.6;
}

.degree-statement strong {
  color: #173f5f;
  font-weight: 650;
}

/* ─────────────────────────────
   AUTHOR / SUPERVISOR
───────────────────────────── */

.author-block {
  margin-top: 30px;
  padding-left: 18px;

  border-left: 3px solid #2a9d8f;
}

.person-row {
  display: flex;
  align-items: baseline;

  margin-bottom: 9px;
}

.person-label {
  width: 105px;

  color: #64748b;

  font-size: 13px;
}

.person-value {
  color: #24313a;

  font-size: 15px;
  font-weight: 600;
}

/* ─────────────────────────────
   FOOTER
───────────────────────────── */

.cover-bottom {
  position: absolute;

  left: 72px;
  right: 72px;
  bottom: 34px;

  z-index: 3;

  display: flex;
  justify-content: space-between;
  align-items: center;

  border-top: 1px solid #dce4e9;

  padding-top: 20px;
}

.lab-name {
  color: #64748b;

  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.12em;
}

.date {
  color: #64748b;
  font-size: 12px;
}
</style>