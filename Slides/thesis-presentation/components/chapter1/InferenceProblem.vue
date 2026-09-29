<template>
<div class="inference-slide">

    <main class="main-content">

        <!-- Biological World -->
        <section class="world-section biological-world">
            <div class="section-header">
                <div class="section-number">01</div>
                <div>
                    <h2>Biological World</h2>
                    <p>The regulatory process that actually happens inside the cell</p>
                </div>
            </div>

            <div class="biological-flow">

                <div class="bio-card">
                    <div class="card-icon mechanism-icon">
                        <svg viewBox="0 0 64 52" aria-hidden="true">
                            <defs>
                                <marker id="mechanism-arrow" markerWidth="8" markerHeight="8" refX="7" refY="4" orient="auto" markerUnits="userSpaceOnUse">
                                    <path d="M0 0 L8 4 L0 8 Z" fill="#20639B" />
                                </marker>
                            </defs>

                            <!-- Regulatory interactions -->
                            <path d="M19 15 C28 15 34 18 41 23" class="mechanism-edge" marker-end="url(#mechanism-arrow)" />

                            <path d="M19 37 C28 37 34 32 41 27" class="mechanism-edge" marker-end="url(#mechanism-arrow)" />

                            <!-- Regulator nodes -->
                            <circle cx="13" cy="14" r="6" class="mechanism-node regulator" />

                            <circle cx="13" cy="38" r="6" class="mechanism-node regulator" />

                            <!-- Target gene -->
                            <circle cx="47" cy="25" r="7" class="mechanism-node target" />
                        </svg>
                    </div>
                    <div class="card-text">
                        <h3>Regulatory mechanisms</h3>
                        <p>
                            Transcription factors and other molecular mechanisms
                            regulate gene activity.
                        </p>
                    </div>
                </div>

                <div class="flow-arrow vertical">
                    <span class="arrow-line"></span>
                    <span class="arrow-head">▼</span>
                </div>

                <div class="bio-card grn-card">
                    <div class="card-icon network-icon">
                        <svg viewBox="0 0 72 52" aria-hidden="true">
                            <defs>
                                <marker id="grn-arrow" markerWidth="8" markerHeight="8" refX="7" refY="4" orient="auto" markerUnits="userSpaceOnUse">
                                    <path d="M0 0 L8 4 L0 8 Z" fill="#20639B" />
                                </marker>
                            </defs>

                            <!-- A → B -->
                            <path d="M19.5 13.5 L32.5 19.5" class="network-edge" marker-end="url(#grn-arrow)" />

                            <!-- A → C -->
                            <path d="M17 16.5 C16 24 20 30 27 34" class="network-edge" marker-end="url(#grn-arrow)" />

                            <!-- B → D -->
                            <path d="M42 21 L53 15.5" class="network-edge" marker-end="url(#grn-arrow)" />

                            <!-- C → D -->
                            <path d="M39 36 L53 27" class="network-edge" marker-end="url(#grn-arrow)" />

                            <!-- D → E -->
                            <path d="M61 19 C67 23 67 31 61 36" class="network-edge" marker-end="url(#grn-arrow)" />

                            <!-- Nodes -->
                            <circle cx="13" cy="13" r="6.5" class="network-node regulator" />

                            <circle cx="39" cy="22" r="6.5" class="network-node" />

                            <circle cx="33" cy="39" r="6.5" class="network-node" />

                            <circle cx="59" cy="13" r="6.5" class="network-node" />

                            <circle cx="59" cy="39" r="6.5" class="network-node target" />
                        </svg>
                    </div>

                    <div class="card-text">
                        <h3>Gene Regulatory Network</h3>
                        <p>
                            A hidden network describing
                            <strong>who regulates whom</strong>.
                        </p>
                    </div>
                </div>

                <div class="flow-arrow vertical">
                    <span class="arrow-line"></span>
                    <span class="arrow-head">▼</span>
                </div>

                <div class="bio-card expression-card">
                    <div class="card-icon expression-icon">
                        <span class="expression-axis axis-x"></span>
                        <span class="expression-axis axis-y"></span>
                        <span class="expression-curve"></span>
                    </div>
                    <div class="card-text">
                        <h3>Gene expression dynamics</h3>
                        <p>
                            Regulatory activity produces changing
                            expression levels over time.
                        </p>
                    </div>
                </div>
            </div>
        </section>

        <!-- Experimental Data -->
        <section class="world-section experimental-world">
            <div class="section-header">
                <div class="section-number">02</div>
                <div>
                    <h2>Experimental Data</h2>
                    <p>What we can actually observe from experiments</p>
                </div>
            </div>

            <div class="experimental-flow">

                <div class="data-card">
                    <div class="data-visual">
                        <div class="heatmap">
                            <span v-for="n in 36" :key="n"></span>
                        </div>
                    </div>
                    <div class="card-text">
                        <h3>Observed gene expression profiles</h3>
                        <p>
                            Measurements of gene expression
                            collected across time.
                        </p>
                    </div>
                </div>

                <div class="inference-arrow">
                    <div class="inference-line"></div>
                    <div class="inference-head">▶</div>
                </div>

                <div class="inference-card">
                    <div class="inference-icon">
                        <span class="magnifier"></span>
                        <span class="magnifier-handle"></span>
                        <span class="inference-dots d1"></span>
                        <span class="inference-dots d2"></span>
                        <span class="inference-dots d3"></span>
                    </div>
                    <div class="card-text">
                        <h3>GRN inference</h3>
                        <p>
                            Computationally infer hidden
                            regulatory relationships.
                        </p>
                    </div>
                </div>

                <div class="inference-arrow">
                    <div class="inference-line"></div>
                    <div class="inference-head">▶</div>
                </div>

                <div class="network-result-card">
                    <svg
  class="result-network"
  viewBox="0 0 100 72"
  aria-hidden="true"
>
  <defs>
    <marker
      id="result-arrow"
      markerWidth="9"
      markerHeight="9"
      refX="8"
      refY="4.5"
      orient="auto"
      markerUnits="userSpaceOnUse"
    >
      <path
        d="M0 0 L9 4.5 L0 9 Z"
        fill="#20639B"
      />
    </marker>
  </defs>

  <!-- A → B -->
  <path
    d="M36.5 18.5 C46 18.5 53 21 62.5 25"
    class="result-edge"
    marker-end="url(#result-arrow)"
  />

  <!-- B → C -->
  <path
    d="M67 34.5 C64 41 60 48 55.5 52"
    class="result-edge"
    marker-end="url(#result-arrow)"
  />

  <!-- C → D -->
  <path
    d="M43.5 58 C35 59 28 57 23 53.5"
    class="result-edge"
    marker-end="url(#result-arrow)"
  />

  <!-- D → A -->
  <path
    d="M18 44 C17 35 20 27 24.5 22"
    class="result-edge"
    marker-end="url(#result-arrow)"
  />

  <!-- B → E -->
  <path
    d="M63 21 C68 16 70 12 67 9"
    class="result-edge"
    marker-end="url(#result-arrow)"
  />

  <!-- Nodes -->
  <circle
    cx="30"
    cy="18"
    r="6.5"
    class="result-node regulator"
  />

  <circle
    cx="69"
    cy="28"
    r="6.5"
    class="result-node"
  />

  <circle
    cx="50"
    cy="58"
    r="6.5"
    class="result-node"
  />

  <circle
    cx="17"
    cy="49"
    r="6.5"
    class="result-node"
  />

  <circle
    cx="66"
    cy="8"
    r="5.5"
    class="result-node target"
  />
</svg>
                    <div class="card-text">
                        <h3>Regulatory network</h3>
                        <p>
                            An inferred representation of
                            regulatory relationships.
                        </p>
                    </div>
                </div>

            </div>

            <div class="observed-label">
                <span class="label-dot"></span>
                <span>Observed</span>
            </div>

            <div class="hidden-label">
                <span class="label-dot"></span>
                <span>Hidden / inferred</span>
            </div>
        </section>

    </main>

    <!-- Bottom highlight -->
    <section class="highlight">
        <div class="highlight-accent"></div>
        <div class="highlight-content">
            <div class="highlight-label">THE INFERENCE PROBLEM</div>
            <div class="highlight-text">
                Give gene expression measurements,
                <span>infer the hidden regulatory relationships among genes.</span>
            </div>
        </div>
    </section>
</div>
</template>

<script>
import { ref, watch, onMounted, onBeforeUnmount } from 'vue'

import { useNav } from '@slidev/client'

const { currentPage } = useNav()

const step = ref(0)
watch(currentPage, () => {
  step.value = 0
})

function nextStep() {
    if (step.value < 2) {
        step.value++
    }
}

function resetStep() {
    step.value = 0
}

function handleKeydown(event) {
    if (event.code === 'Space' || event.code === 'ArrowRight') {
        event.preventDefault()
        nextStep()
    }

    if (event.code === 'Escape' || event.code === 'ArrowLeft') {
        event.preventDefault()
        resetStep()
    }
}

onMounted(() => {
    window.addEventListener('keydown', handleKeydown)
})

onBeforeUnmount(() => {
    window.removeEventListener('keydown', handleKeydown)
})
</script>

<style scoped>
.inference-slide {
    position: relative;
    width: 100%;
    height: 100%;
    background: #f8fafb;
    color: #24313a;
    overflow: hidden;
    font-family: 'Inter', 'Segoe UI', sans-serif;
}

.top-line {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 4px;
    background: #173f5f;
}

.main-content {
    position: absolute;
    top: 10px;
    left: 64px;
    right: 64px;
    height: 305px;
    display: flex;
    gap: 24px;
}

.world-section {
    position: relative;
    height: 100%;
    padding: 17px 20px 15px;
    background: #ffffff;
    border: 1px solid #dce4e9;
    border-radius: 14px;
    box-sizing: border-box;
}

.biological-world {
    width: 42%;
}

.experimental-world {
    width: 58%;
}

.section-header {
    display: flex;
    align-items: flex-start;
    gap: 11px;
    height: 48px;
}

.section-number {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
    width: 27px;
    height: 27px;
    border-radius: 7px;
    background: #173f5f;
    color: #ffffff;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 10px;
    font-weight: 600;
}

.section-header h2 {
    margin: 0;
    color: #173f5f;
    font-size: 17px;
    line-height: 1.15;
    font-weight: 700;
}

.section-header p {
    margin: 4px 0 0;
    color: #64748b;
    font-size: 9px;
    line-height: 1.3;
}

.biological-flow {
    position: absolute;
    top: 76px;
    left: 20px;
    right: 20px;
    bottom: 12px;
    display: flex;
    flex-direction: column;
    align-items: center;
}

.bio-card {
    width: 90%;
    min-height: 51px;
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 7px 11px;
    background: #f8fafb;
    border: 1px solid #dce4e9;
    border-radius: 9px;
    box-sizing: border-box;
    transition:
        transform 0.4s ease,
        border-color 0.4s ease,
        box-shadow 0.4s ease;
}

.bio-card:hover {
    transform: translateY(-2px);
    border-color: #9fc4d8;
    box-shadow: 0 5px 16px rgba(23, 63, 95, 0.08);
}

.grn-card {
    border-color: #9fc4d8;
    background: #f5fafc;
}

.card-icon {
    position: relative;
    flex-shrink: 0;
    width: 43px;
    height: 38px;
}

.card-text {
    min-width: 0;
}

.card-text h3 {
    margin: 0;
    color: #24313a;
    font-size: 11px;
    line-height: 1.25;
    font-weight: 700;
}

.card-text p {
    margin: 3px 0 0;
    color: #64748b;
    font-size: 8px;
    line-height: 1.35;
}

.card-text strong {
    color: #20639b;
    font-weight: 700;
}

.flow-arrow {
    position: relative;
    width: 18px;
    height: 18px;
    flex-shrink: 0;
}

.flow-arrow.vertical {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}

.arrow-line {
    position: absolute;
    top: 1px;
    bottom: 4px;
    left: 50%;
    width: 1px;
    background: #9db8c7;
    transform: translateX(-50%);
}

.arrow-head {
    position: absolute;
    bottom: -1px;
    left: 50%;
    color: #20639b;
    font-size: 9px;
    line-height: 1;
    transform: translateX(-50%);
}

.mechanism-icon {
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 7px;
}

.mechanism-icon svg {
    display: block;
    width: 50px;
    height: 42px;
    overflow: visible;
}

.mechanism-edge {
    fill: none;
    stroke: #20639b;
    stroke-width: 2;
    stroke-linecap: round;
    stroke-linejoin: round;
}

.mechanism-node {
    fill: #ffffff;
}

.mechanism-node.regulator {
    stroke: #20639b;
    stroke-width: 2;
}

.mechanism-node.target {
    stroke: #2a9d8f;
    stroke-width: 2;
}

.network-icon {
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: visible;
}

.network-icon svg {
    display: block;
    width: 52px;
    height: 42px;
    overflow: visible;
}

.network-edge {
    fill: none;
    stroke: #20639b;
    stroke-width: 1.8;
    stroke-linecap: round;
    stroke-linejoin: round;
}

.network-node {
    fill: #ffffff;
    stroke: #20639b;
    stroke-width: 1.8;
}

.network-node.regulator {
    stroke: #20639b;
}

.network-node.target {
    stroke: #2a9d8f;
}

.expression-icon {
    overflow: hidden;
}

.expression-axis {
    position: absolute;
    background: #94a3b8;
}

.axis-x {
    left: 5px;
    right: 2px;
    bottom: 5px;
    height: 1px;
}

.axis-y {
    left: 5px;
    top: 3px;
    bottom: 5px;
    width: 1px;
}

.expression-curve {
    position: absolute;
    left: 8px;
    top: 8px;
    width: 31px;
    height: 23px;
    border-top: 2px solid #2a9d8f;
    border-radius: 50% 40% 50% 20%;
    transform: rotate(-8deg);
}

.experimental-flow {
    position: absolute;
    top: 90px;
    left: 20px;
    right: 20px;
    height: 135px;
    display: flex;
    align-items: center;
    justify-content: center;
}

.data-card,
.inference-card,
.network-result-card {
    position: relative;
    width: 25%;
    height: 112px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 8px;
    background: #f8fafb;
    border: 1px solid #dce4e9;
    border-radius: 10px;
    box-sizing: border-box;
    transition:
        transform 0.4s ease,
        border-color 0.4s ease,
        box-shadow 0.4s ease;
}

.data-card:hover,
.inference-card:hover,
.network-result-card:hover {
    transform: translateY(-3px);
    border-color: #9fc4d8;
    box-shadow: 0 6px 18px rgba(23, 63, 95, 0.09);
}

.data-card .card-text,
.inference-card .card-text,
.network-result-card .card-text {
    text-align: center;
}

.data-card .card-text h3,
.inference-card .card-text h3,
.network-result-card .card-text h3 {
    font-size: 9px;
}

.data-card .card-text p,
.inference-card .card-text p,
.network-result-card .card-text p {
    font-size: 7px;
}

.data-visual {
    width: 55px;
    height: 48px;
    margin-bottom: 6px;
    display: flex;
    align-items: center;
    justify-content: center;
}

.heatmap {
    width: 50px;
    height: 42px;
    display: grid;
    grid-template-columns: repeat(6, 1fr);
    grid-template-rows: repeat(6, 1fr);
    gap: 2px;
    padding: 3px;
    background: #ffffff;
    border: 1px solid #dce4e9;
    border-radius: 4px;
    box-sizing: border-box;
}

.heatmap span {
    border-radius: 1px;
    background: #d7e8ef;
}

.heatmap span:nth-child(2n) {
    background: #a9cedd;
}

.heatmap span:nth-child(3n) {
    background: #6fa5bf;
}

.heatmap span:nth-child(5n) {
    background: #2a9d8f;
}

.inference-card {
    width: 22%;
    border-color: #e9c46a;
    background: #fffdf6;
}

.inference-icon {
    position: relative;
    width: 50px;
    height: 48px;
    margin-bottom: 6px;
}

.magnifier {
    position: absolute;
    top: 5px;
    left: 10px;
    width: 22px;
    height: 22px;
    border: 3px solid #20639b;
    border-radius: 50%;
}

.magnifier-handle {
    position: absolute;
    width: 14px;
    height: 3px;
    left: 29px;
    top: 29px;
    background: #20639b;
    border-radius: 2px;
    transform: rotate(45deg);
    transform-origin: left center;
}

.inference-dots {
    position: absolute;
    width: 4px;
    height: 4px;
    border-radius: 50%;
    background: #2a9d8f;
}

.d1 {
    left: 4px;
    bottom: 6px;
}

.d2 {
    left: 18px;
    bottom: 1px;
}

.d3 {
    right: 2px;
    bottom: 8px;
}

.inference-arrow {
    position: relative;
    width: 35px;
    height: 20px;
    flex-shrink: 0;
}

.inference-line {
    position: absolute;
    left: 1px;
    right: 7px;
    top: 50%;
    height: 2px;
    background: #9db8c7;
    transform: translateY(-50%);
}

.inference-head {
    position: absolute;
    right: 0;
    top: 50%;
    color: #20639b;
    font-size: 11px;
    line-height: 1;
    transform: translateY(-50%);
}

.network-result-card {
    width: 25%;
    border-color: #9fc4d8;
}

.result-network {
  display: block;
  width: 70px;
  height: 50px;
  margin-bottom: 6px;
  overflow: visible;
}

.result-edge {
  fill: none;
  stroke: #20639b;
  stroke-width: 1.8;
  stroke-linecap: round;
  stroke-linejoin: round;
}

.result-node {
  fill: #ffffff;
  stroke: #20639b;
  stroke-width: 1.8;
}

.result-node.regulator {
  stroke: #20639b;
}

.result-node.target {
  stroke: #2a9d8f;
}

.re1 {
    width: 23px;
    left: 27px;
    top: 9px;
    transform: rotate(137deg);
}

.re2 {
    width: 20px;
    left: 9px;
    top: 23px;
    transform: rotate(42deg);
}

.re3 {
    width: 22px;
    left: 27px;
    top: 38px;
    transform: rotate(-20deg);
}

.re4 {
    width: 24px;
    left: 28px;
    top: 20px;
    transform: rotate(-7deg);
}

.observed-label,
.hidden-label {
    position: absolute;
    bottom: 12px;
    display: flex;
    align-items: center;
    gap: 5px;
    color: #64748b;
    font-size: 7px;
}

.observed-label {
    left: 20px;
}

.hidden-label {
    right: 20px;
}

.label-dot {
    width: 6px;
    height: 6px;
    border-radius: 50%;
}

.observed-label .label-dot {
    background: #2a9d8f;
}

.hidden-label .label-dot {
    background: #e9c46a;
}

.highlight {
    position: absolute;
    left: 64px;
    right: 64px;
    bottom: 10px;
    height: 66px;
    display: flex;
    align-items: center;
    background: #ffffff;
    border: 1px solid #dce4e9;
    border-radius: 11px;
    overflow: hidden;
}

.highlight-accent {
    width: 5px;
    height: 100%;
    flex-shrink: 0;
    background: #2a9d8f;
}

.highlight-content {
    padding: 0 24px;
}

.highlight-label {
    margin-bottom: 4px;
    color: #2a9d8f;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 8px;
    font-weight: 700;
    letter-spacing: 0.13em;
}

.highlight-text {
    color: #24313a;
    font-size: 16px;
    line-height: 1.25;
    font-weight: 500;
}

.highlight-text span {
    color: #173f5f;
    font-weight: 700;
}

:global(.lab-footer) {
    z-index: 10;
}

/* Step-based emphasis */
.inference-slide .experimental-world {
    transition: box-shadow 0.5s ease;
}

.inference-slide:has(.highlight) .highlight {
    transition:
        transform 0.5s ease,
        box-shadow 0.5s ease;
}

/* Keyboard interaction */
@media (prefers-reduced-motion: no-preference) {
    .highlight {
        animation: highlight-in 0.8s ease both;
    }
}

@keyframes highlight-in {
    from {
        opacity: 0.7;
        transform: translateY(5px);
    }

    to {
        opacity: 1;
        transform: translateY(0);
    }
}
</style>
