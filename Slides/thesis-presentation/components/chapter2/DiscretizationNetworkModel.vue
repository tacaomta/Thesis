<template>
<div class="model-slide">

    <div class="intro">
        A discretized network describes regulatory interactions and
        how the discrete state of each gene changes over time.
    </div>

    <div class="three-points">

        <!-- 01 -->
        <section class="concept-card">
            <div class="number">01</div>

            <div class="card-icon network-icon">
                <svg viewBox="0 0 100 70" aria-label="Directed graph">
                    <defs>
                        <marker id="directed-graph-arrow" markerWidth="8" markerHeight="8" refX="7" refY="4" orient="auto" markerUnits="userSpaceOnUse">
                            <path d="M0 0 L8 4 L0 8 Z" fill="#20639B" />
                        </marker>
                    </defs>

                    <!-- Directed edges -->
                    <path d="M27 20 C36 20 40 27 46 31" class="graph-edge" marker-end="url(#directed-graph-arrow)" />

                    <path d="M27 50 C36 50 40 43 46 38" class="graph-edge" marker-end="url(#directed-graph-arrow)" />

                    <path d="M54 34 C64 25 69 20 76 18" class="graph-edge" marker-end="url(#directed-graph-arrow)" />

                    <path d="M54 36 C64 45 69 50 76 52" class="graph-edge" marker-end="url(#directed-graph-arrow)" />

                    <!-- Nodes -->
                    <circle cx="19" cy="18" r="9" class="graph-node" />
                    <circle cx="19" cy="52" r="9" class="graph-node" />

                    <circle cx="50" cy="35" r="10" class="graph-node target" />

                    <circle cx="82" cy="16" r="9" class="graph-node" />
                    <circle cx="82" cy="54" r="9" class="graph-node" />

                    <!-- Labels -->
                    <text x="19" y="21.5" text-anchor="middle" class="graph-label">
                        A
                    </text>

                    <text x="19" y="55.5" text-anchor="middle" class="graph-label">
                        B
                    </text>

                    <text x="50" y="38.5" text-anchor="middle" class="graph-label target-label">
                        C
                    </text>

                    <text x="82" y="19.5" text-anchor="middle" class="graph-label">
                        D
                    </text>

                    <text x="82" y="57.5" text-anchor="middle" class="graph-label">
                        E
                    </text>
                </svg>
            </div>

            <div class="card-content">
                <div class="card-label">DISCRETIZED NETWORK</div>

                <h2>What is it?</h2>

                <p>
                    A <strong>directed graph</strong> representing
                    regulatory interactions among genes.
                </p>

                <div class="formula">
                    <span>G = (V, A)</span>
                </div>
            </div>
        </section>

        <!-- 02 -->
        <section class="concept-card">
            <div class="number">02</div>

            <div class="card-icon state-icon">
                <div class="gene-symbol">V</div>
                <div class="time-label">at time t</div>
            </div>

            <div class="card-content">
                <div class="card-label">GENE STATE</div>

                <h2>What is V(t)?</h2>

                <p>
                    The <strong>discrete state</strong> of gene
                    <em>V</em> at time <em>t</em>.
                </p>

                <div class="state-set">
                    <span>V(t)</span>
                    <span>=</span>
                    <strong>{0, 1, ..., l−1}</strong>
                </div>

                <div class="small-note">
                    Each gene can have <strong>l</strong> discrete states.
                </div>
            </div>
        </section>

        <!-- 03 -->
        <section class="concept-card update-card">
            <div class="number">03</div>

            <div class="card-icon function-icon">
                <div class="function-symbol">f</div>
            </div>

            <div class="card-content">
                <div class="card-label">UPDATE FUNCTION</div>

                <h2>How is V(t+1) updated?</h2>

                <div class="update-diagram">

                    <div class="regulators">
                        <span>u₁(t)</span>
                        <span>u₂(t)</span>
                        <span>...</span>
                        <span>uₖ(t)</span>
                    </div>

                    <div class="update-arrow">→</div>

                    <div class="function-box">f</div>

                    <div class="update-arrow">→</div>

                    <div class="target-state">
                        <strong>v(t+1)</strong>
                    </div>

                </div>

                <div class="equation">
                    V(t+1) = f(u₁(t), u₂(t), ..., uₖ(t))
                </div>

                <div class="small-note">
                    The target state at <strong>t+1</strong> depends on
                    its regulatory genes at <strong>t</strong>.
                </div>
            </div>
        </section>

    </div>

    <div class="bottom-message">
        <span>CORE IDEA</span>
        <strong>
            Regulatory genes at time t
        </strong>
        <span class="bottom-arrow">→</span>
        <strong>update function</strong>
        <span class="bottom-arrow">→</span>
        <strong>target gene state at t+1</strong>
    </div>

</div>
</template>

<script setup>
</script>

<style scoped>
.model-slide {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    min-width: 0;
    min-height: 0;
    box-sizing: border-box;
    color: #24313a;
}

.intro {
    flex: 0 0 auto;
    margin: 0 auto 15px;
    max-width: 880px;
    text-align: center;
    color: #64748b;
    font-size: 10.5px;
    line-height: 1.45;
}

.three-points {
    flex: 1 1 auto;
    min-height: 0;
    display: grid;
    grid-template-columns: 0.9fr 0.9fr 1.2fr;
    gap: 15px;
}

.concept-card {
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: center;
    min-width: 0;
    min-height: 0;
    padding: 18px 18px 15px;
    border: 1px solid #dce4e9;
    border-radius: 12px;
    background: #ffffff;
    box-sizing: border-box;
    text-align: center;
}

.concept-card:nth-child(2) {
    border-top: 3px solid #2a9d8f;
}

.concept-card:nth-child(3) {
    border-top: 3px solid #20639b;
}

.number {
    position: absolute;
    top: 10px;
    left: 12px;
    color: #cbd5dc;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 11px;
    font-weight: 700;
}

.card-icon {
    width: 68px;
    height: 68px;
    margin-top: 4px;
    margin-bottom: 13px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 11px;
    background: #f8fafb;
    box-sizing: border-box;
}

.card-icon svg {
    width: 58px;
    height: 48px;
    display: block;
    overflow: visible;
}

.edge {
    fill: none;
    stroke: #20639b;
    stroke-width: 2.1;
    stroke-linecap: round;
    stroke-linejoin: round;
}

.node {
    fill: #ffffff;
    stroke: #20639b;
    stroke-width: 2;
}

.node.target {
    stroke: #2a9d8f;
    stroke-width: 2.5;
    fill: #f3fbf9;
}

.state-icon {
    flex-direction: column;
}

.gene-symbol {
    color: #2a9d8f;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 25px;
    font-weight: 700;
    line-height: 1;
}

.time-label {
    margin-top: 5px;
    color: #94a3b8;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 7px;
}

.function-icon {
    border: 1px solid #b9d8e5;
    background: #eef7fa;
}

.function-symbol {
    color: #20639b;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 27px;
    font-weight: 700;
    font-style: italic;
}

.card-content {
    width: 100%;
    min-width: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
}

.card-label {
    margin-bottom: 5px;
    color: #2a9d8f;
    font-size: 7px;
    font-weight: 700;
    letter-spacing: 0.12em;
}

.card-content h2 {
    margin: 0 0 9px;
    color: #173f5f;
    font-size: 17px;
    font-weight: 700;
    line-height: 1.2;
}

.card-content p {
    max-width: 250px;
    margin: 0;
    color: #475569;
    font-size: 9.5px;
    line-height: 1.5;
}

.card-content p strong {
    color: #24313a;
}

.formula {
    margin-top: 17px;
    padding: 8px 18px;
    border: 1px solid #dce4e9;
    border-radius: 7px;
    background: #f8fafb;
    color: #173f5f;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 13px;
    font-weight: 600;
}

.state-set {
    margin-top: 16px;
    display: flex;
    align-items: center;
    gap: 7px;
    padding: 9px 13px;
    border: 1px solid #dce4e9;
    border-radius: 7px;
    background: #f8fafb;
    color: #64748b;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 10px;
}

.state-set strong {
    color: #2a9d8f;
    font-weight: 700;
}

.small-note {
    margin-top: 13px;
    color: #94a3b8;
    font-size: 7.5px;
    line-height: 1.45;
}

.small-note strong {
    color: #64748b;
}

.update-card {
    padding-left: 16px;
    padding-right: 16px;
}

.update-diagram {
    width: 100%;
    margin-top: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
}

.regulators {
    display: flex;
    flex-direction: column;
    gap: 4px;
    align-items: flex-end;
}

.regulators span {
    min-width: 44px;
    padding: 4px 6px;
    border: 1px solid #b9d8e5;
    border-radius: 5px;
    background: #eef7fa;
    color: #20639b;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 7.5px;
    font-weight: 600;
    box-sizing: border-box;
}

.update-arrow {
    color: #94a3b8;
    font-size: 14px;
    font-weight: 700;
}

.function-box {
    width: 38px;
    height: 38px;
    display: flex;
    align-items: center;
    justify-content: center;
    border: 2px solid #20639b;
    border-radius: 8px;
    background: #ffffff;
    color: #20639b;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 17px;
    font-weight: 700;
    font-style: italic;
    box-sizing: border-box;
}

.target-state {
    padding: 9px 10px;
    border: 2px solid #2a9d8f;
    border-radius: 7px;
    background: #f3fbf9;
    color: #2a9d8f;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 11px;
    white-space: nowrap;
}

.equation {
    width: 100%;
    margin-top: 14px;
    padding: 10px 6px;
    border-radius: 7px;
    background: #f8fafb;
    color: #173f5f;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 10px;
    font-weight: 600;
    white-space: nowrap;
    box-sizing: border-box;
}

.bottom-message {
    flex: 0 0 auto;
    min-height: 42px;
    margin-top: 12px;
    padding: 7px 20px;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 9px;
    border: 1px solid #dce4e9;
    border-radius: 9px;
    background: #ffffff;
    color: #64748b;
    font-size: 8.5px;
}

.bottom-message>span:first-child {
    margin-right: 5px;
    color: #2a9d8f;
    font-size: 7px;
    font-weight: 700;
    letter-spacing: 0.1em;
}

.bottom-message strong {
    color: #173f5f;
}

.bottom-arrow {
    color: #94a3b8;
    font-size: 11px;
}
.network-icon {
  display: flex;
  align-items: center;
  justify-content: center;
}

.network-icon svg {
  display: block;
  width: 64px;
  height: 52px;
  overflow: visible;
}

.graph-edge {
  fill: none;
  stroke: #20639b;
  stroke-width: 2.2;
  stroke-linecap: round;
  stroke-linejoin: round;
}

.graph-node {
  fill: #ffffff;
  stroke: #20639b;
  stroke-width: 2;
}

.graph-node.target {
  fill: #f3fbf9;
  stroke: #2a9d8f;
  stroke-width: 2.5;
}

.graph-label {
  fill: #20639b;
  font-family: 'IBM Plex Mono', monospace;
  font-size: 8px;
  font-weight: 700;
}

.graph-label.target-label {
  fill: #2a9d8f;
}
</style>
