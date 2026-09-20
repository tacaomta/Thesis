<template>
  <div class="thesis-network">

    <div class="slide-body">
      <section class="grn-definition">

        <p class="definition">
          A network representation of<br />
          regulatory relationships among genes.
        </p>

        <div class="notation">
          <div>
            <span class="notation-label">Node</span>
            <span class="arrow">→</span>
            <span>Gene</span>
          </div>

          <div>
            <span class="notation-label">Directed edge</span>
            <span class="arrow">→</span>
            <span>Regulatory influence</span>
          </div>
        </div>
      </section>

      <section class="grn-visual">
        <div class="network-area">
          <svg
  class="network-svg"
  viewBox="0 0 600 430"
  preserveAspectRatio="xMidYMid meet"
>
 <defs>
  <!-- Enhancer: larger arrow head -->
  <marker
    id="enhancer-arrow"
    markerWidth="16"
    markerHeight="16"
    refX="15"
    refY="8"
    orient="auto"
    markerUnits="userSpaceOnUse"
  >
    <path
      d="M1,1 L15,8 L1,15"
      fill="none"
      stroke="#20639B"
      stroke-width="3.5"
      stroke-linecap="round"
      stroke-linejoin="round"
    />
  </marker>

  <!-- Inhibitor: larger perpendicular bar -->
  <marker
    id="inhibitor-bar"
    markerWidth="16"
    markerHeight="20"
    refX="17"
    refY="10"
    orient="auto"
    markerUnits="userSpaceOnUse"
  >
    <path
      d="M15,0 L15,20"
      fill="none"
      stroke="#E76F51"
      stroke-width="4"
      stroke-linecap="round"
    />
  </marker>
</defs>

  <!-- ========================= -->
  <!-- NETWORK GUIDE CIRCLE -->
  <!-- ========================= -->

  <circle
    class="network-guide"
    cx="300"
    cy="220"
    r="150"
  />

  <!-- ========================= -->
  <!-- ENHANCER INTERACTIONS -->
  <!-- ========================= -->

  <!-- A → B
       Start: boundary of A
       End: boundary of B -->
  <g
    class="interaction enhancer"
    :class="interactionClass('enhancer')"
  >
    <path
      d="M269.3 92.4
         C245 105 210 125 187.7 151.6"
      marker-end="url(#enhancer-arrow)"
    />
  </g>

  <!-- A → A
       Self-regulation.
       Both start and end are on the boundary of A.
       The path loops outside the node. -->
  <g
    class="interaction enhancer"
    :class="interactionClass('enhancer')"
  >
    <path
      d="M325 97
         C390 110 390 15 300 32"
      marker-end="url(#enhancer-arrow)"
    />
  </g>

  <!-- A → C
       Start: boundary of A
       End: boundary of C -->
  <g
    class="interaction enhancer"
    :class="interactionClass('enhancer')"
  >
    <path
      d="M288.3 106.1
         C270 160 235 245 223.7 304.9"
      marker-end="url(#enhancer-arrow)"
    />
  </g>

  <!-- D → F
       D is the central regulatory gene -->
  <g
    class="interaction enhancer"
    :class="interactionClass('enhancer')"
  >
    <path
      d="M340 207.1
         C365 202 390 194 406.8 185.6"
      marker-end="url(#enhancer-arrow)"
    />
  </g>

  <!-- E → D
       Start: boundary of E
       End: boundary of central D -->
  <g
    class="interaction enhancer"
    :class="interactionClass('enhancer')"
  >
    <path
      d="M365.6 310.3
         C350 285 335 265 324.7 254"
      marker-end="url(#enhancer-arrow)"
    />
  </g>

  <!-- ========================= -->
  <!-- INHIBITOR INTERACTIONS -->
  <!-- ========================= -->

  <!-- B ──| E
       Start: boundary of B
       End: boundary of E -->
  <g
    class="interaction inhibitor"
    :class="interactionClass('inhibitor')"
  >
    <path
      d="M187.8 196.3
         C220 235 285 295 357.2 318.7"
      marker-end="url(#inhibitor-bar)"
    />
  </g>

  <!-- D ──| B
       Start: boundary of D
       End: boundary of B -->
  <g
    class="interaction inhibitor"
    :class="interactionClass('inhibitor')"
  >
    <path
      d="M260 207.1
         C235 198 210 187 193.2 185.6"
      marker-end="url(#inhibitor-bar)"
    />
  </g>

  <!-- F ──| C
       Start: boundary of F
       End: boundary of C -->
  <g
    class="interaction inhibitor"
    :class="interactionClass('inhibitor')"
  >
    <path
      d="M412.2 196.3
         C385 250 315 315 242.8 318.7"
      marker-end="url(#inhibitor-bar)"
    />
  </g>

  <!-- ========================= -->
  <!-- NODES -->
  <!-- ========================= -->

  <!-- Gene A -->
  <g
    class="node node-a"
    :class="{ active: selectedType === 'enhancer' }"
  >
    <circle
      cx="300"
      cy="70"
      r="38"
    />

    <text
      x="300"
      y="66"
      text-anchor="middle"
      class="gene-name"
    >
      Gene A
    </text>

    <text
      x="300"
      y="83"
      text-anchor="middle"
      class="gene-role"
    >
      Regulator
    </text>
  </g>

  <!-- Gene B -->
  <g class="node">
    <circle
      cx="157"
      cy="174"
      r="38"
    />

    <text
      x="157"
      y="179"
      text-anchor="middle"
      class="gene-name"
    >
      Gene B
    </text>
  </g>

  <!-- Gene C -->
  <g class="node">
    <circle
      cx="212"
      cy="341"
      r="38"
    />

    <text
      x="212"
      y="346"
      text-anchor="middle"
      class="gene-name"
    >
      Gene C
    </text>
  </g>

  <!-- Gene D: CENTER -->
  <g
    class="node node-d"
    :class="{ active: selectedType !== null }"
  >
    <circle
      cx="300"
      cy="220"
      r="42"
    />

    <text
      x="300"
      y="216"
      text-anchor="middle"
      class="gene-name"
    >
      Gene D
    </text>

    <text
      x="300"
      y="233"
      text-anchor="middle"
      class="gene-role"
    >
      Gene
    </text>
  </g>

  <!-- Gene E -->
  <g class="node">
    <circle
      cx="388"
      cy="341"
      r="38"
    />

    <text
      x="388"
      y="346"
      text-anchor="middle"
      class="gene-name"
    >
      Gene E
    </text>
  </g>

  <!-- Gene F -->
  <g class="node">
    <circle
      cx="443"
      cy="174"
      r="38"
    />

    <text
      x="443"
      y="179"
      text-anchor="middle"
      class="gene-name"
    >
      Gene F
    </text>
  </g>
</svg>
        </div>

        <!-- ========================= -->
        <!-- INTERACTION LEGEND -->
        <!-- ========================= -->

        <div class="interaction-legend">
          <button
            class="legend-item enhancer"
            :class="{ selected: selectedType === 'enhancer' }"
            @click="toggleType('enhancer')"
          >
            <span class="legend-symbol enhancer-symbol">
              <span class="legend-line"></span>
              <span class="legend-arrow">→</span>
            </span>

            <span class="legend-name">
              Enhancer
            </span>
          </button>

          <button
            class="legend-item inhibitor"
            :class="{ selected: selectedType === 'inhibitor' }"
            @click="toggleType('inhibitor')"
          >
            <span class="legend-symbol inhibitor-symbol">
              <span class="legend-line"></span>
              <span class="legend-bar"></span>
            </span>

            <span class="legend-name">
              Inhibitor
            </span>
          </button>
        </div>
      </section>
    </div>

    <!-- Key takeaway -->
    <div class="grn-takeaway">
      GRN = genes + directed regulatory relationships
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

const selectedType = ref(null)

function toggleType(type) {
  selectedType.value =
    selectedType.value === type ? null : type
}

function interactionClass(type) {
  return {
    selected: selectedType.value === type,
    dimmed:
      selectedType.value !== null &&
      selectedType.value !== type
  }
}

function handleKeydown(event) {
  if (event.code === 'Escape') {
    selectedType.value = null
  }

  if (event.code === '1') {
    toggleType('enhancer')
  }

  if (event.code === '2') {
    toggleType('inhibitor')
  }
}

onMounted(() => {
  window.addEventListener(
    'keydown',
    handleKeydown
  )
})

onBeforeUnmount(() => {
  window.removeEventListener(
    'keydown',
    handleKeydown
  )
})
</script>

<style scoped>
.thesis-network {
  position: relative;
  width: 100%;
  height: 100%;
  background: #F8FAFB;
  color: #24313A;
  overflow: hidden;
  box-sizing: border-box;
}
.slide-body {
  position: absolute;
  top: 10px;
  left: 64px;
  right: 64px;
  height: 285px;
  display: flex;
}
.grn-definition {
  width: 40%;
  padding-top: 25px;
  box-sizing: border-box;
}
.eyebrow {
  margin-bottom: 6px;
  color: #64748B;
  font-size: 12px;
  font-weight: 700;
  letter-spacing: 0.14em;
}
.grn-definition h1 {
  margin: 0;
  color: #173F5F;
  font-size: 29px;
  line-height: 1.15;
  font-weight: 750;
}
.definition {
  margin-top: 20px;
  color: #24313A;
  font-size: 17px;
  line-height: 1.5;
}
.notation {
  margin-top: 20px;
  color: #24313A;
  font-size: 14px;
  line-height: 1.9;
}
.notation-label {
  display: inline-block;
  width: 105px;
  color: #173F5F;
  font-weight: 700;
}
.arrow {
  margin-right: 7px;
  color: #20639B;
  font-weight: 700;
}
.grn-visual {
  position: relative;
  width: 60%;
  height: 100%;
  display: flex;
  align-items: center;
}
.network-area {
  width: calc(100% - 105px);
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}
.network-svg {
  width: 100%;
  height: 100%;
  max-width: 560px;
  overflow: visible;
}
.network-guide {
  fill: none;
  stroke: #B9D7E8;
  stroke-width: 1.5;
  stroke-dasharray: 6 7;
  opacity: 0.75;
}
.interaction {
  opacity: 0.82;
  transition:
    opacity 0.35s ease,
    filter 0.35s ease;
}
.interaction path {
  fill: none;
  stroke-width: 3;
  stroke-linecap: round;
  stroke-linejoin: round;
}
.interaction.enhancer path {
  stroke: #20639B;
}
.interaction.inhibitor path {
  stroke: #E76F51;
}
.interaction.selected {
  opacity: 1;
}
.interaction.selected path {
  stroke-width: 5;
  filter: drop-shadow(
    0 0 3px rgba(0, 0, 0, 0.18)
  );
}
.interaction.dimmed {
  opacity: 0.08;
}
.node circle {
  fill: #FFFFFF;
  stroke: #20639B;
  stroke-width: 3;
  transition:
    fill 0.35s ease,
    stroke 0.35s ease,
    stroke-width 0.35s ease;
}
.node-a circle {
  fill: #F8FAFB;
}
.node-d circle {
  stroke: #E9C46A;
  stroke-width: 3;
}
.node.active circle {
  fill: #FFF8E6;
  stroke: #E9C46A;
  stroke-width: 4;
}
.gene-name {
  fill: #173F5F;
  font-size: 16px;
  font-weight: 700;
}
.gene-role {
  fill: #64748B;
  font-size: 10px;
}
.interaction-legend {
  position: absolute;
  right: 0;
  top: 82px;
  width: 90px;
  display: flex;
  flex-direction: column;
  gap: 8px;
}
.legend-item {
  width: 100%;
  height: 34px;
  padding: 0 7px;
  display: flex;
  align-items: center;
  gap: 6px;
  border: 1px solid #DCE4E9;
  border-radius: 6px;
  background: #FFFFFF;
  text-align: left;
  cursor: pointer;
  box-sizing: border-box;
  transition:
    border-color 0.25s ease,
    box-shadow 0.25s ease,
    transform 0.25s ease;
}
.legend-item:hover {
  transform: translateY(-1px);
  box-shadow:
    0 2px 7px rgba(23, 63, 95, 0.08);
}
.legend-item.selected {
  border-width: 2px;
}
.legend-item.enhancer.selected {
  border-color: #20639B;
}
.legend-item.inhibitor.selected {
  border-color: #E76F51;
}
.legend-symbol {
  position: relative;
  width: 24px;
  height: 16px;
  flex-shrink: 0;
}
.legend-line {
  position: absolute;
  left: 1px;
  top: 7px;
  width: 18px;
  height: 2px;
}
.enhancer-symbol .legend-line {
  background: #20639B;
}
.legend-arrow {
  position: absolute;
  right: 0;
  top: -3px;
  color: #20639B;
  font-size: 15px;
  font-weight: 700;
  line-height: 16px;
}
.inhibitor-symbol .legend-line {
  background: #E76F51;
}
.legend-bar {
  position: absolute;
  right: 1px;
  top: 3px;
  width: 2px;
  height: 10px;
  background: #E76F51;
}
.legend-name {
  color: #173F5F;
  font-size: 9px;
  font-weight: 700;
  white-space: nowrap;
}
.network-comparison {
  position: absolute;
  left: 64px;
  right: 64px;
  bottom: 72px;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 70px;
  color: #24313A;
  font-size: 14px;
}
.comparison-item {
  position: relative;
  display: flex;
  align-items: center;
  gap: 10px;
}
.comparison-label {
  margin-right: 5px;
  color: #64748B;
  font-weight: 700;
}
.comparison-line {
  width: 70px;
  height: 2px;
  background: #94A3B8;
}
.regulation .comparison-line {
  width: 48px;
  background: #20639B;
}
.arrow-line {
  margin-left: -14px;
  color: #20639B;
  font-size: 20px;
  font-weight: 700;
}
.gene {
  color: #173F5F;
  font-weight: 650;
}
.role,
.target {
  position: absolute;
  top: 22px;
  color: #64748B;
  font-size: 9px;
}
.role {
  left: 143px;
}
.target {
  right: -15px;
}
.grn-takeaway {
  position: absolute;
  left: 64px;
  right: 64px;
  bottom: 43px;
  text-align: center;
  color: #173F5F;
  font-size: 15px;
  font-weight: 700;
}
</style>