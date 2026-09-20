<template>
  <svg
    viewBox="0 0 600 600"
    xmlns="http://www.w3.org/2000/svg"
    class="network"
  >
    <g class="edges">
      <line x1="120" y1="150" x2="290" y2="100" />
      <line x1="120" y1="150" x2="220" y2="300" />
      <line x1="290" y1="100" x2="430" y2="190" />
      <line x1="220" y1="300" x2="430" y2="190" />
      <line x1="220" y1="300" x2="360" y2="420" />
      <line x1="430" y1="190" x2="510" y2="330" />
      <line x1="360" y1="420" x2="510" y2="330" />
      <line x1="360" y1="420" x2="260" y2="520" />
      <line x1="510" y1="330" x2="500" y2="500" />
    </g>
    <g class="nodes">
      <circle cx="120" cy="150" r="13" />
      <circle cx="290" cy="100" r="18" />
      <circle cx="220" cy="300" r="13" />
      <circle cx="430" cy="190" r="20" />
      <circle cx="360" cy="420" r="14" />
      <circle cx="510" cy="330" r="11" />
      <circle cx="260" cy="520" r="10" />
      <circle cx="500" cy="500" r="12" />
    </g>
    <g class="arrows">
      <path d="M200 128 L215 124" />
      <path d="M330 125 L345 135" />
      <path d="M280 280 L300 265" />
      <path d="M400 395 L410 380" />
    </g>
  </svg>
</template>

<style scoped>
.network {
  width: 100%;
  height: 100%;
}
.edges line {
  stroke: #2a9d8f;
  stroke-width: 2;
  opacity: 0.7;
}
.nodes circle {
  fill: #173f5f;
  stroke: #2a9d8f;
  stroke-width: 3;
}
.arrows path {
  fill: none;
  stroke: #c9a96e;
  stroke-width: 2;
}
</style>