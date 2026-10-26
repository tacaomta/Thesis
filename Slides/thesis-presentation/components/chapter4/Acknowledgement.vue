<template>
  <div class="thank-you">

    <!-- Title -->
    <div class="title">
      <div class="title-main">Thank You</div>
      <div class="title-line"></div>
    </div>

    <!-- Visual story -->
    <div class="people">

      <!-- Supervisor -->
      <div class="person-card supervisor" style="--accent: #173F5F; --accent-soft: rgba(23, 63, 95, 0.07);">

        <div class="badge">
          <svg viewBox="0 0 24 24" class="badge-icon">
            <path d="M12 3L2 9l10 6 10-6-10-6z" />
            <path d="M6 11.5V17c0 1.6 2.8 3 6 3s6-1.4 6-3v-5.5" />
          </svg>
        </div>

        <div class="scene-wrap">
          <div class="portrait">
            <div class="head"></div>
            <div class="body"></div>
            <div class="book">
              <span></span>
              <span></span>
            </div>
          </div>
        </div>

        <div class="label">
          <div class="role">SUPERVISOR</div>
          <div class="name">Prof. Yung Keun Kwon</div>
          <div class="tagline">Guidance that shaped this work</div>
        </div>
      </div>


      <!-- Committee Members -->
      <div class="person-card committee" style="--accent: #7A5AF8; --accent-soft: rgba(122, 90, 248, 0.08);">

        <div class="badge">
          <svg viewBox="0 0 24 24" class="badge-icon">
            <circle cx="12" cy="7" r="3" />
            <circle cx="5" cy="9" r="2.3" />
            <circle cx="19" cy="9" r="2.3" />
            <path d="M12 12c-3.3 0-6 2-6 5.5V19h12v-1.5c0-3.5-2.7-5.5-6-5.5z" />
            <path d="M5 13.3c-2 .4-3.3 1.9-3.3 4.2V19h3.3" />
            <path d="M19 13.3c2 .4 3.3 1.9 3.3 4.2V19H19" />
          </svg>
        </div>

        <div class="scene-wrap">
          <div class="committee-scene">

            <div class="committee-member cm1">
              <div class="cap"></div>
              <div class="head"></div>
              <div class="body"></div>
            </div>

            <div class="committee-member cm2">
              <div class="cap"></div>
              <div class="head"></div>
              <div class="body"></div>
            </div>

            <div class="committee-member cm3">
              <div class="cap"></div>
              <div class="head"></div>
              <div class="body"></div>
            </div>

            <div class="panel-desk"></div>
          </div>
        </div>

        <div class="label">
          <div class="role">COMMITTEE MEMBERS</div>
          <div class="tagline">Insightful questions &amp; valuable feedback</div>
        </div>
      </div>


      <!-- Family -->
      <div class="person-card family" style="--accent: #2A9D8F; --accent-soft: rgba(42, 157, 143, 0.08);">

        <div class="badge">
          <svg viewBox="0 0 24 24" class="badge-icon">
            <path d="M3 11l9-8 9 8" />
            <path d="M5 10v10h14V10" />
          </svg>
        </div>

        <div class="scene-wrap">
          <div class="family-scene">

            <!-- Father -->
            <div class="person father">
              <div class="head"></div>
              <div class="body"></div>
            </div>

            <!-- Mother -->
            <div class="person mother">
              <div class="head"></div>
              <div class="body"></div>
            </div>

            <!-- Child 1 -->
            <div class="person child child-one">
              <div class="head"></div>
              <div class="body"></div>
            </div>

            <!-- Child 2 -->
            <div class="person child child-two">
              <div class="head"></div>
              <div class="body"></div>
            </div>

            <!-- Heart -->
            <div class="heart">♥</div>
          </div>
        </div>

        <div class="label">
          <div class="role">FAMILY</div>
          <div class="tagline">Unconditional support, every step</div>
        </div>
      </div>


      <!-- Friends -->
      <div class="person-card friends" style="--accent: #D98C3D; --accent-soft: rgba(217, 140, 61, 0.09);">

        <div class="badge">
          <svg viewBox="0 0 24 24" class="badge-icon">
            <circle cx="9" cy="8" r="3" />
            <circle cx="16.5" cy="9.5" r="2.3" />
            <path d="M3 20c0-3.2 3-5.3 6-5.3s6 2.1 6 5.3" />
            <path d="M13.5 15c2.2 0.1 5 1.6 5 5" />
          </svg>
        </div>

        <div class="scene-wrap">
          <div class="friends-scene">

            <div class="friend f1">
              <div class="head"></div>
              <div class="body"></div>
            </div>

            <div class="friend f2">
              <div class="head"></div>
              <div class="body"></div>
            </div>

            <div class="friend f3">
              <div class="head"></div>
              <div class="body"></div>
            </div>

            <div class="friend f4">
              <div class="head"></div>
              <div class="body"></div>
            </div>

            <div class="circle"></div>
          </div>
        </div>

        <div class="label">
          <div class="role">FRIENDS</div>
          <div class="tagline">Shared laughter &amp; encouragement</div>
        </div>
      </div>

    </div>

    <!-- Connection -->
    <div class="connection">

      <div class="connection-line"></div>

      <div class="connection-dots">
        <span style="--c: #173F5F"></span>
        <span style="--c: #7A5AF8"></span>
        <span style="--c: #2A9D8F"></span>
        <span style="--c: #D98C3D"></span>
      </div>

      <div class="connection-line"></div>

    </div>

    <!-- Bottom visual -->
    <div class="bottom">

      <div class="journey">

        <div class="dot start"></div>
        <div class="path"></div>
        <div class="dot committee-dot"></div>
        <div class="path"></div>
        <div class="dot middle"></div>
        <div class="path"></div>
        <div class="dot end"></div>

      </div>

      <div class="journey-caption">
        A journey made possible by many people
      </div>

    </div>

  </div>
</template>


<style scoped>

.thank-you {
  width: 100%;
  height: 100%;

  display: flex;
  flex-direction: column;

  box-sizing: border-box;

  padding: 10px 30px 18px;

  color: #24313A;
  font-family: Inter, 'Segoe UI', sans-serif;
}


/* ─────────────────────────────
   TITLE
───────────────────────────── */

.title {
  text-align: center;
  margin-top: 4px;
}

.title-main {
  font-size: 38px;
  font-weight: 700;
  letter-spacing: -0.03em;
  color: #173F5F;
}

.title-line {
  width: 60px;
  height: 3px;

  margin: 9px auto 0;

  border-radius: 3px;

  background: linear-gradient(90deg, #173F5F, #7A5AF8, #2A9D8F, #D98C3D);
}


/* ─────────────────────────────
   PEOPLE
───────────────────────────── */

.people {
  flex: 1;

  display: grid;
  grid-template-columns: repeat(4, 1fr);

  align-items: stretch;

  gap: 18px;

  margin-top: 5px;
}


/* Cards */

.person-card {
  height: 235px;

  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;

  border-radius: 16px;

  background:
    linear-gradient(
      180deg,
      #FFFFFF 0%,
      var(--accent-soft) 100%
    );

  border: 1px solid #DCE4E9;

  box-sizing: border-box;

  padding: 10px 8px 14px;

  position: relative;

  opacity: 0;
  transform: translateY(14px);
  animation: cardIn 0.5s ease forwards;
}

.supervisor { animation-delay: 0.08s; }
.committee  { animation-delay: 0.22s; }
.family     { animation-delay: 0.36s; }
.friends    { animation-delay: 0.5s; }

@keyframes cardIn {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.person-card::before {
  content: '';

  position: absolute;
  top: 0;
  left: 0;
  right: 0;

  height: 4px;

  background: var(--accent);

  border-radius: 16px 16px 0 0;
}


/* ─────────────────────────────
   ROLE BADGE (icon motif)
───────────────────────────── */

.badge {
  position: absolute;

  top: 12px;
  left: 12px;

  width: 28px;
  height: 28px;

  border-radius: 8px;

  display: flex;
  align-items: center;
  justify-content: center;

  background: var(--accent-soft);
  border: 1px solid var(--accent);
}

.badge-icon {
  width: 15px;
  height: 15px;

  fill: none;
  stroke: var(--accent);
  stroke-width: 1.8;
  stroke-linecap: round;
  stroke-linejoin: round;
}


/* ─────────────────────────────
   SCENE WRAPPER (keeps illustrations
   a consistent footprint across 4 cards)
───────────────────────────── */

.scene-wrap {
  width: 100%;
  height: 128px;

  display: flex;
  align-items: flex-end;
  justify-content: center;

  overflow: visible;
}


/* ─────────────────────────────
   SUPERVISOR ILLUSTRATION
───────────────────────────── */

.portrait {
  width: 108px;
  height: 122px;

  position: relative;

  transform: scale(0.86);
  transform-origin: bottom center;
}

.portrait .head {
  width: 52px;
  height: 52px;

  position: absolute;

  top: 5px;
  left: 28px;

  border-radius: 50%;

  background: #F2C7A5;

  border: 2px solid #173F5F;
}

.portrait .body {
  width: 86px;
  height: 70px;

  position: absolute;

  bottom: 8px;
  left: 11px;

  border-radius: 45px 45px 12px 12px;

  background: #173F5F;
}

.book {
  position: absolute;

  bottom: 0;
  left: 26px;

  width: 56px;
  height: 28px;

  border-radius: 4px;

  background: #E9C46A;

  transform: rotate(-3deg);

  display: flex;
}

.book span {
  flex: 1;

  border-right: 1px solid rgba(255,255,255,.6);
}


/* ─────────────────────────────
   COMMITTEE MEMBERS
───────────────────────────── */

.committee-scene {
  width: 168px;
  height: 128px;

  position: relative;

  transform: scale(0.84);
  transform-origin: bottom center;
}

.panel-desk {
  position: absolute;

  left: 4px;
  right: 4px;
  bottom: 6px;

  height: 3px;

  border-radius: 2px;

  background: rgba(122, 90, 248, 0.35);
}

.committee-member {
  position: absolute;
  bottom: 9px;

  width: 42px;
  height: 92px;
}

.committee-member .head {
  width: 34px;
  height: 34px;

  position: absolute;

  top: 12px;
  left: 4px;

  border-radius: 50%;

  background: #F2C7A5;

  border: 2px solid #5B3FBF;
}

.committee-member .body {
  width: 42px;
  height: 58px;

  position: absolute;

  bottom: 0;

  border-radius: 36px 36px 9px 9px;

  background: #7A5AF8;
}

.committee-member .cap {
  position: absolute;

  top: 0;
  left: -3px;

  width: 48px;
  height: 10px;

  background: #5B3FBF;

  clip-path: polygon(50% 0%, 100% 55%, 50% 100%, 0% 55%);
}

.cm1 {
  left: 2px;
}

.cm1 .body { background: #7A5AF8; }
.cm1 .head { border-color: #5B3FBF; }

.cm2 {
  left: 63px;

  transform: translateY(-6px);
}

.cm2 .body { background: #9B86FA; }
.cm2 .head { border-color: #5B3FBF; }

.cm3 {
  left: 124px;
}

.cm3 .body { background: #7A5AF8; }
.cm3 .head { border-color: #5B3FBF; }


/* ─────────────────────────────
   FAMILY
───────────────────────────── */

.family-scene {
  width: 190px;
  height: 128px;

  position: relative;

  transform: scale(0.82);
  transform-origin: bottom center;
}

.person {
  position: absolute;
  bottom: 4px;
}

.person .head {
  position: absolute;

  border-radius: 50%;

  background: #F2C7A5;

  border: 2px solid #1F6E63;
}

.person .body {
  position: absolute;

  border-radius: 40px 40px 10px 10px;
}

.father {
  width: 50px;
  height: 105px;

  left: 10px;
}

.father .head {
  width: 38px;
  height: 38px;

  top: 0;
  left: 6px;
}

.father .body {
  width: 50px;
  height: 67px;

  bottom: 0;

  background: #1F6E63;
}

.mother {
  width: 50px;
  height: 112px;

  left: 65px;
}

.mother .head {
  width: 38px;
  height: 38px;

  top: 0;
  left: 6px;
}

.mother .body {
  width: 50px;
  height: 74px;

  bottom: 0;

  background: #2A9D8F;
}

.child {
  width: 32px;
  height: 75px;
}

.child .head {
  width: 27px;
  height: 27px;

  left: 2px;
  top: 0;
  border-color: #1F6E63;
}

.child .body {
  width: 32px;
  height: 45px;

  bottom: 0;

  background: #7FC4B8;
}

.child-one {
  left: 115px;
}

.child-two {
  left: 150px;

  transform: scale(.82);
  transform-origin: bottom;
}

.heart {
  position: absolute;

  top: 2px;
  right: 6px;

  font-size: 23px;

  color: #D96C5F;

  animation: heartbeat 2s ease-in-out infinite;
}

@keyframes heartbeat {
  0%, 100% {
    transform: scale(1);
  }

  50% {
    transform: scale(1.12);
  }
}


/* ─────────────────────────────
   FRIENDS
───────────────────────────── */

.friends-scene {
  width: 175px;
  height: 128px;

  position: relative;

  transform: scale(0.84);
  transform-origin: bottom center;
}

.circle {
  position: absolute;

  width: 122px;
  height: 122px;

  left: 26px;
  top: 4px;

  border-radius: 50%;

  border: 2px dashed rgba(217, 140, 61, 0.45);
}

.friend {
  position: absolute;

  width: 36px;
  height: 84px;

  bottom: 18px;

  z-index: 2;
}

.friend .head {
  width: 28px;
  height: 28px;

  position: absolute;

  top: 0;
  left: 4px;

  border-radius: 50%;

  background: #F2C7A5;

  border: 2px solid #B5651A;
}

.friend .body {
  width: 36px;
  height: 51px;

  position: absolute;

  bottom: 0;

  border-radius: 30px 30px 8px 8px;
}

.f1 {
  left: 20px;
  transform: translateY(9px);
}

.f1 .body { background: #D98C3D; }

.f2 {
  left: 60px;
}

.f2 .body { background: #E3A565; }

.f3 {
  left: 100px;
  transform: translateY(4px);
}

.f3 .body { background: #D98C3D; }

.f4 {
  left: 132px;
  transform: translateY(11px);
}

.f4 .body { background: #E3A565; }


/* ─────────────────────────────
   LABELS
───────────────────────────── */

.label {
  text-align: center;

  margin-top: 4px;
}

.role {
  font-family:
    "IBM Plex Mono",
    "JetBrains Mono",
    monospace;

  font-size: 9px;
  font-weight: 600;

  letter-spacing: .14em;

  color: var(--accent);
}

.name {
  margin-top: 5px;

  font-size: 12.5px;

  font-weight: 600;

  color: #173F5F;
}

.tagline {
  margin-top: 4px;

  font-size: 9.8px;
  line-height: 1.35;

  color: #64748B;
}


/* ─────────────────────────────
   CONNECTION
───────────────────────────── */

.connection {
  display: grid;

  grid-template-columns: 1fr auto 1fr;

  align-items: center;

  gap: 15px;

  margin: 2px 80px 0;

  opacity: 0;
  animation: cardIn 0.5s ease forwards 0.68s;
}

.connection-line {
  height: 1px;

  background: #DCE4E9;
}

.connection-dots {
  display: flex;
  gap: 8px;
}

.connection-dots span {
  width: 5px;
  height: 5px;

  border-radius: 50%;

  background: var(--c);
}


/* ─────────────────────────────
   BOTTOM JOURNEY
───────────────────────────── */

.bottom {
  text-align: center;

  margin-top: 8px;

  opacity: 0;
  animation: cardIn 0.5s ease forwards 0.82s;
}

.journey {
  display: flex;

  align-items: center;

  justify-content: center;

  width: 300px;

  margin: auto;
}

.path {
  width: 46px;
  height: 2px;

  background: #DCE4E9;
}

.dot {
  width: 9px;
  height: 9px;

  flex-shrink: 0;

  border-radius: 50%;
}

.start {
  background: #173F5F;
}

.committee-dot {
  background: #7A5AF8;
}

.middle {
  background: #2A9D8F;
}

.end {
  background: #D98C3D;
}

.journey-caption {
  margin-top: 7px;

  font-size: 10px;

  color: #94A3B8;

  letter-spacing: .04em;
}


/* ─────────────────────────────
   REDUCED MOTION
───────────────────────────── */

@media (prefers-reduced-motion: reduce) {
  .person-card,
  .connection,
  .bottom,
  .heart {
    animation: none !important;
    opacity: 1 !important;
    transform: none !important;
  }
}

</style>