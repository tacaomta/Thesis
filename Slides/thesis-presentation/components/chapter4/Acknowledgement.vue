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

        <div class="portrait">
          <div class="head"></div>
          <div class="body"></div>
          <div class="book">
            <span></span>
            <span></span>
          </div>
        </div>

        <div class="label">
          <div class="role">SUPERVISOR</div>
          <div class="name">Prof. Yung Keun Kwon</div>
          <div class="tagline">Guidance that shaped this work</div>
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

        <div class="label">
          <div class="role">FRIENDS</div>
          <div class="tagline">Shared laughter & encouragement</div>
        </div>
      </div>

    </div>

    <!-- Connection -->
    <div class="connection">

      <div class="connection-line"></div>

      <div class="connection-dots">
        <span style="--c: #173F5F"></span>
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

  padding: 10px 35px 20px;

  color: #24313A;
  font-family: Inter, 'Segoe UI', sans-serif;
}


/* ─────────────────────────────
   TITLE
───────────────────────────── */

.title {
  text-align: center;
  margin-top: 5px;
}

.title-main {
  font-size: 42px;
  font-weight: 700;
  letter-spacing: -0.03em;
  color: #173F5F;
}

.title-line {
  width: 55px;
  height: 3px;

  margin: 10px auto 0;

  border-radius: 3px;

  background: linear-gradient(90deg, #173F5F, #2A9D8F, #D98C3D);
}


/* ─────────────────────────────
   PEOPLE
───────────────────────────── */

.people {
  flex: 1;

  display: grid;
  grid-template-columns: 1fr 1.15fr 1fr;

  align-items: center;

  gap: 35px;

  margin-top: 5px;
}


/* Cards */

.person-card {
  height: 245px;

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

  position: relative;

  opacity: 0;
  transform: translateY(14px);
  animation: cardIn 0.5s ease forwards;
}

.supervisor { animation-delay: 0.1s; }
.family     { animation-delay: 0.3s; }
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


/* Family emphasis */

.family {
  height: 275px;

  border-color: #C7D9D8;
}


/* ─────────────────────────────
   ROLE BADGE (icon motif)
───────────────────────────── */

.badge {
  position: absolute;

  top: 14px;
  left: 14px;

  width: 30px;
  height: 30px;

  border-radius: 9px;

  display: flex;
  align-items: center;
  justify-content: center;

  background: var(--accent-soft);
  border: 1px solid var(--accent);
}

.badge-icon {
  width: 16px;
  height: 16px;

  fill: none;
  stroke: var(--accent);
  stroke-width: 1.8;
  stroke-linecap: round;
  stroke-linejoin: round;
}


/* ─────────────────────────────
   SIMPLE PERSON ILLUSTRATION (Supervisor)
───────────────────────────── */

.portrait {
  width: 130px;
  height: 145px;

  position: relative;
}


/* Head */

.portrait .head {
  width: 52px;
  height: 52px;

  position: absolute;

  top: 5px;
  left: 39px;

  border-radius: 50%;

  background: #F2C7A5;

  border: 2px solid #173F5F;
}


/* Body */

.portrait .body {
  width: 86px;
  height: 70px;

  position: absolute;

  bottom: 8px;
  left: 22px;

  border-radius: 45px 45px 12px 12px;

  background: #173F5F;
}


/* Book */

.book {
  position: absolute;

  bottom: 0;
  left: 37px;

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
   FAMILY
───────────────────────────── */

.family-scene {
  width: 210px;
  height: 150px;

  position: relative;
}


/* Generic person */

.person {
  position: absolute;
  bottom: 4px;
}


/* Head */

.person .head {
  position: absolute;

  border-radius: 50%;

  background: #F2C7A5;

  border: 2px solid #1F6E63;
}


/* Body */

.person .body {
  position: absolute;

  border-radius: 40px 40px 10px 10px;
}


/* Father */

.father {
  width: 50px;
  height: 105px;

  left: 15px;
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


/* Mother */

.mother {
  width: 50px;
  height: 112px;

  left: 73px;
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


/* Children */

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


/* Child 1 */

.child-one {
  left: 126px;
}


/* Child 2 */

.child-two {
  left: 163px;

  transform: scale(.82);
  transform-origin: bottom;
}


/* Heart */

.heart {
  position: absolute;

  top: 2px;
  right: 12px;

  font-size: 25px;

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
  width: 190px;
  height: 150px;

  position: relative;
}


/* Circle */

.circle {
  position: absolute;

  width: 130px;
  height: 130px;

  left: 30px;
  top: 10px;

  border-radius: 50%;

  border: 2px dashed rgba(217, 140, 61, 0.45);
}


/* Friends */

.friend {
  position: absolute;

  width: 38px;
  height: 88px;

  bottom: 20px;

  z-index: 2;
}

.friend .head {
  width: 30px;
  height: 30px;

  position: absolute;

  top: 0;
  left: 4px;

  border-radius: 50%;

  background: #F2C7A5;

  border: 2px solid #B5651A;
}

.friend .body {
  width: 38px;
  height: 53px;

  position: absolute;

  bottom: 0;

  border-radius: 30px 30px 8px 8px;
}

.f1 {
  left: 25px;
  transform: translateY(10px);
}

.f1 .body { background: #D98C3D; }

.f2 {
  left: 68px;
}

.f2 .body { background: #E3A565; }

.f3 {
  left: 111px;
  transform: translateY(5px);
}

.f3 .body { background: #D98C3D; }

.f4 {
  left: 145px;
  transform: translateY(12px);
}

.f4 .body { background: #E3A565; }


/* ─────────────────────────────
   LABELS
───────────────────────────── */

.label {
  text-align: center;

  margin-top: 8px;
}

.role {
  font-family:
    "IBM Plex Mono",
    "JetBrains Mono",
    monospace;

  font-size: 10px;
  font-weight: 600;

  letter-spacing: .16em;

  color: var(--accent);
}

.name {
  margin-top: 5px;

  font-size: 13px;

  font-weight: 600;

  color: #173F5F;
}

.tagline {
  margin-top: 4px;

  font-size: 10.5px;
  line-height: 1.4;

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
  animation: cardIn 0.5s ease forwards 0.7s;
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
  animation: cardIn 0.5s ease forwards 0.85s;
}

.journey {
  display: flex;

  align-items: center;

  justify-content: center;

  width: 280px;

  margin: auto;
}

.path {
  width: 70px;
  height: 2px;

  background: #DCE4E9;
}

.dot {
  width: 10px;
  height: 10px;

  border-radius: 50%;
}

.start {
  background: #173F5F;
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