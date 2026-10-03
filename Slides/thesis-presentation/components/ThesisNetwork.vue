<template>
  <svg
    viewBox="0 0 600 600"
    xmlns="http://www.w3.org/2000/svg"
    class="network"
  >
    <defs>

      <!-- 3D sphere-like gradient for regular nodes -->
      <radialGradient id="gradNode" cx="35%" cy="30%" r="75%">
        <stop offset="0%" stop-color="#4f7f99" />
        <stop offset="55%" stop-color="#2d5873" />
        <stop offset="100%" stop-color="#173f5f" />
      </radialGradient>

      <!-- 3D sphere-like gradient for focus nodes (brighter, teal-led) -->
      <radialGradient id="gradFocus" cx="35%" cy="30%" r="75%">
        <stop offset="0%" stop-color="#6fe0cd" />
        <stop offset="45%" stop-color="#2a9d8f" />
        <stop offset="100%" stop-color="#15584e" />
      </radialGradient>

      <!-- soft glow / drop-shadow for focus nodes -->
      <filter id="focusGlow" x="-80%" y="-80%" width="260%" height="260%">
        <feGaussianBlur in="SourceGraphic" stdDeviation="6" result="blur" />
        <feMerge>
          <feMergeNode in="blur" />
          <feMergeNode in="SourceGraphic" />
        </feMerge>
      </filter>

      <!-- subtle shadow for regular nodes, gives slight lift -->
      <filter id="softShadow" x="-60%" y="-60%" width="220%" height="220%">
        <feDropShadow dx="0" dy="1.5" stdDeviation="1.4" flood-color="#0b2436" flood-opacity="0.35" />
      </filter>

    </defs>

    <!-- =========================
         EDGES
    ========================== -->
    <g class="edges">
      <line x1="70"  y1="120" x2="160" y2="60" />
      <line x1="160" y1="60"  x2="280" y2="90" />
      <line x1="280" y1="90"  x2="380" y2="50" />
      <line x1="380" y1="50"  x2="480" y2="110" />
      <line x1="480" y1="110" x2="540" y2="220" />
      <line x1="540" y1="220" x2="460" y2="260" />
      <line x1="460" y1="260" x2="350" y2="200" />
      <line x1="280" y1="90"  x2="350" y2="200" />
      <line x1="350" y1="200" x2="230" y2="220" />
      <line x1="230" y1="220" x2="130" y2="260" />
      <line x1="130" y1="260" x2="70"  y2="120" />
      <line x1="130" y1="260" x2="90"  y2="370" />
      <line x1="90"  y1="370" x2="190" y2="400" />
      <line x1="190" y1="400" x2="230" y2="220" />
      <line x1="190" y1="400" x2="300" y2="340" />
      <line x1="300" y1="340" x2="350" y2="200" />
      <line x1="300" y1="340" x2="400" y2="380" />
      <line x1="400" y1="380" x2="460" y2="260" />
      <line x1="400" y1="380" x2="500" y2="400" />
      <line x1="500" y1="400" x2="540" y2="220" />
      <line x1="500" y1="400" x2="540" y2="490" />
      <line x1="540" y1="490" x2="420" y2="500" />
      <line x1="420" y1="500" x2="400" y2="380" />
      <line x1="420" y1="500" x2="300" y2="520" />
      <line x1="300" y1="520" x2="190" y2="400" />
      <line x1="300" y1="520" x2="200" y2="540" />
      <line x1="200" y1="540" x2="110" y2="480" />
      <line x1="110" y1="480" x2="90"  y2="370" />
      <line x1="110" y1="480" x2="190" y2="400" />
    </g>

    <!-- =========================
         NODES
    ========================== -->
    <g class="nodes">
      <!-- regular nodes -->
      <circle cx="70"  cy="120" r="9"  class="node" />
      <circle cx="160" cy="60"  r="10" class="node" />
      <circle cx="380" cy="50"  r="9"  class="node" />
      <circle cx="480" cy="110" r="11" class="node" />
      <circle cx="540" cy="220" r="9"  class="node" />
      <circle cx="460" cy="260" r="12" class="node" />
      <circle cx="230" cy="220" r="10" class="node" />
      <circle cx="130" cy="260" r="12" class="node" />
      <circle cx="90"  cy="370" r="9"  class="node" />
      <circle cx="300" cy="340" r="10" class="node" />
      <circle cx="400" cy="380" r="9"  class="node" />
      <circle cx="500" cy="400" r="12" class="node" />
      <circle cx="540" cy="490" r="9"  class="node" />
      <circle cx="300" cy="520" r="10" class="node" />
      <circle cx="200" cy="540" r="9"  class="node" />
      <circle cx="110" cy="480" r="10" class="node" />

      <!-- focus nodes (hub genes) -->
      <circle cx="280" cy="90"  r="22" class="node node-focus" />
      <circle cx="350" cy="200" r="25" class="node node-focus" />
      <circle cx="190" cy="400" r="24" class="node node-focus" />
      <circle cx="420" cy="500" r="22" class="node node-focus" />

      <!-- glossy highlight dots for 3D "sphere" look on focus nodes -->
      <ellipse cx="272" cy="82"  rx="6" ry="4" class="node-highlight" />
      <ellipse cx="341" cy="191" rx="7" ry="4.5" class="node-highlight" />
      <ellipse cx="182" cy="391" rx="6.5" ry="4" class="node-highlight" />
      <ellipse cx="412" cy="491" rx="6" ry="4" class="node-highlight" />
    </g>

    <!-- =========================
         DIRECTED ARROWS
    ========================== -->
    <g class="arrows">
      <path d="M200 70 L215 78" />
      <path d="M420 70 L435 85" />
      <path d="M400 145 L385 165" />
      <path d="M270 255 L285 240" />
      <path d="M345 365 L360 350" />
      <path d="M470 445 L455 455" />
    </g>
  </svg>
</template>

<style scoped>
.network {
  width: 100%;
  height: 100%;
}

/* =========================
   EDGES
========================= */

.edges line {
  stroke: #2a9d8f;
  stroke-width: 1.6;
  opacity: 0.45;
}

/* =========================
   NODES — regular
========================= */

.node {
  fill: url(#gradNode);
  stroke: #0d2a3f;
  stroke-width: 1;
  opacity: 0.85;
  filter: url(#softShadow);
}

/* =========================
   NODES — focus (hub)
========================= */

.node-focus {
  fill: url(#gradFocus);
  stroke: #0e4039;
  stroke-width: 2;
  opacity: 1;
  filter: url(#focusGlow);
}

/* glossy "3D sphere" highlight on focus nodes */

.node-highlight {
  fill: #ffffff;
  opacity: 0.85;
  pointer-events: none;
}

/* =========================
   ARROWS
========================= */

.arrows path {
  fill: none;
  stroke: #c9a96e;
  stroke-width: 2;
  opacity: 0.8;
}
</style>