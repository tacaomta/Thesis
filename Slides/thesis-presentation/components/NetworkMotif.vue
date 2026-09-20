<template>
  <svg
    class="network-motif"
    viewBox="0 0 600 500"
    xmlns="http://www.w3.org/2000/svg"
  >
    <g class="edges">
      <line x1="120" y1="180" x2="270" y2="100" />
      <line x1="120" y1="180" x2="300" y2="270" />
      <line x1="270" y1="100" x2="420" y2="170" />
      <line x1="300" y1="270" x2="420" y2="170" />
      <line x1="300" y1="270" x2="470" y2="340" />
      <line x1="420" y1="170" x2="520" y2="100" />
    </g>

    <g class="nodes">
      <circle cx="120" cy="180" r="10" />
      <circle cx="270" cy="100" r="10" />
      <circle cx="300" cy="270" r="10" />
      <circle cx="420" cy="170" r="10" />
      <circle cx="470" cy="340" r="10" />
      <circle cx="520" cy="100" r="10" />
    </g>
  </svg>
</template>

<style scoped>
.network-motif {
  position: absolute;
  right: -30px;
  top: 80px;
  width: 600px;
  height: 500px;
  opacity: 0.18;
}

.edges line {
  stroke: #2a9d8f;
  stroke-width: 2;
}

.nodes circle {
  fill: #173f5f;
  stroke: #2a9d8f;
  stroke-width: 3;
}
</style>