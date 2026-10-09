<template>
<div class="regulatory-slide">
    <main class="slide-content">
        <section class="main-grid">
            <div class="explanation">
                <ul class="reason-list">
                    <li>
                        <span class="reason-icon">01</span>
                        <div>
                            <strong>Gene-to-gene control</strong>
                            <span>One gene switches another on or off</span>
                        </div>
                    </li>
                    <li>
                        <span class="reason-icon">02</span>
                        <div>
                            <strong>Coordinated response</strong>
                            <span>Many genes act together, not alone</span>
                        </div>
                    </li>
                    <li>
                        <span class="reason-icon">03</span>
                        <div>
                            <strong>Adapting to change</strong>
                            <span>Reacting to heat, stress, or environment</span>
                        </div>
                    </li>
                    <li>
                        <span class="reason-icon">04</span>
                        <div>
                            <strong>Master regulators</strong>
                            <span>Few genes control many downstream genes</span>
                        </div>
                    </li>
                    <li>
                        <span class="reason-icon">05</span>
                        <div>
                            <strong>Disease &amp; drug targets</strong>
                            <span>Faulty control often causes disease</span>
                        </div>
                    </li>
                </ul>
            </div>
            <div class="regulation-visual">
                <div class="visual-caption">REGULATORY CONTROL</div>
                <svg class="regulation-svg" viewBox="0 0 620 330" aria-label="Regulatory genes control the expression of target genes and cellular response">
                    <defs>
                        <marker id="regulatory-arrow" markerWidth="12" markerHeight="12" refX="10" refY="6" orient="auto" markerUnits="userSpaceOnUse">
                            <path d="M1 1 L11 6 L1 11" fill="none" stroke="#20639B" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round" />
                        </marker>
                        <marker id="response-arrow" markerWidth="12" markerHeight="12" refX="10" refY="6" orient="auto" markerUnits="userSpaceOnUse">
                            <path d="M1 1 L11 6 L1 11" fill="none" stroke="#2A9D8F" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round" />
                        </marker>
                    </defs>
                    <path d="M155 165 C190 165 205 165 238 165" class="flow-edge regulatory-edge" marker-end="url(#regulatory-arrow)" />
                    <path d="M155 165 C188 125 205 102 238 102" class="flow-edge regulatory-edge" marker-end="url(#regulatory-arrow)" />
                    <path d="M155 165 C188 205 205 228 238 228" class="flow-edge regulatory-edge" marker-end="url(#regulatory-arrow)" />
                    <path d="M338 102 C370 102 386 125 414 142" class="flow-edge response-edge" marker-end="url(#response-arrow)" />
                    <path d="M338 175 C370 175 388 165 414 165" class="flow-edge response-edge" marker-end="url(#response-arrow)" />
                    <path d="M338 248 C370 248 386 205 414 188" class="flow-edge response-edge" marker-end="url(#response-arrow)" />
                    <g class="regulator-node">
                        <circle cx="105" cy="175" r="50" />
                        <circle cx="105" cy="175" r="40" class="inner-ring" />
                        <text x="105" y="167" text-anchor="middle">Regulatory</text>
                        <text x="105" y="187" text-anchor="middle">genes</text>
                        <text x="105" y="208" text-anchor="middle" class="node-subtitle">CONTROL</text>
                    </g>
                    <g class="target-node">
                        <rect x="238" y="72" width="100" height="60" rx="12" />
                        <text x="288" y="107" text-anchor="middle">Gene A</text>
                    </g>
                    <g class="target-node">
                        <rect x="238" y="145" width="100" height="60" rx="12" />
                        <text x="288" y="180" text-anchor="middle">Gene B</text>
                    </g>
                    <g class="target-node">
                        <rect x="238" y="218" width="100" height="60" rx="12" />
                        <text x="288" y="253" text-anchor="middle">Gene C</text>
                    </g>
                    <g class="response-node">
                        <rect x="414" y="125" width="155" height="80" rx="16" />
                        <circle cx="445" cy="165" r="19" class="response-circle" />
                        <path d="M436 165 L443 172 L455 157" class="response-check" />
                        <text x="490" y="158" text-anchor="middle">Cellular</text>
                        <text x="490" y="178" text-anchor="middle">response</text>
                    </g>
                    <text x="105" y="285" text-anchor="middle" class="group-label">UPSTREAM CONTROL</text>
                    <text x="288" y="295" text-anchor="middle" class="group-label">TARGET GENES</text>
                    <text x="491" y="285" text-anchor="middle" class="group-label">BIOLOGICAL OUTCOME</text>
                </svg>
            </div>
        </section>
        <section class="takeaway">
            <span class="takeaway-mark"></span>
            <p>
                Ultimately, reveal
                <strong>disease mechanisms</strong> and point toward
                <strong>potential therapeutic targets</strong>.
            </p>
        </section>
    </main>
</div>
</template>

<script setup>
</script>

<style scoped>
.regulatory-slide {
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

.main-grid {
    flex: 1;
    display: grid;
    grid-template-columns: 42% 58%;
    min-height: 0;
    margin-left: 20px;
}

.explanation {
    padding: 26px 42px 0 4px;
}

.section-label {
    margin-bottom: 9px;
    color: #64748b;
    font-size: 10px;
    font-weight: 700;
    letter-spacing: 0.14em;
}

.intro-question {
    margin: 0 0 6px;
    color: #20639b;
    font-size: 13px;
    font-weight: 700;
    line-height: 1.3;
    font-style: italic;
}

.intro {
    max-width: 430px;
    margin: 0 0 16px;
    color: #24313a;
    font-size: 15.5px;
    line-height: 1.42;
    font-weight: 500;
}

.reason-list {
    display: flex;
    flex-direction: column;
    gap: 20px;
    margin: 0;
    padding: 0;
    list-style: none;
}

.reason-list li {
    display: grid;
    grid-template-columns: 29px 1fr;
    column-gap: 11px;
    align-items: start;
}

.reason-icon {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 26px;
    height: 26px;
    border: 1px solid #cbd9e1;
    border-radius: 7px;
    background: #ffffff;
    color: #20639b;
    font-family: 'IBM Plex Mono', monospace;
    font-size: 9px;
    font-weight: 700;
}

.reason-list li:last-child .reason-icon {
    border-color: #e9c46a;
    color: #b5860c;
    background: #fdf8ec;
}

.reason-list strong {
    display: block;
    margin-bottom: 2px;
    color: #24313a;
    font-size: 12.5px;
    line-height: 1.25;
}

.reason-list li span:not(.reason-icon) {
    display: block;
    color: #64748b;
    font-size: 10px;
    line-height: 1.35;
}

.regulation-visual {
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
    min-width: 0;
    padding-top: 8px;
}

.visual-caption {
    position: absolute;
    top: 50px;
    right: 220px;
    color: #94a3b8;
    font-size: 9px;
    font-weight: 700;
    letter-spacing: 0.14em;
}

.regulation-svg {
    width: 100%;
    max-width: 620px;
    height: auto;
    overflow: visible;
}

.flow-edge {
    fill: none;
    stroke-width: 3;
    stroke-linecap: round;
}

.regulatory-edge {
    stroke: #20639b;
}

.response-edge {
    stroke: #2a9d8f;
}

.regulator-node circle {
    fill: #edf5f9;
    stroke: #20639b;
    stroke-width: 2.5;
}

.regulator-node .inner-ring {
    fill: none;
    stroke: #9bbfd2;
    stroke-width: 1;
    stroke-dasharray: 3 4;
}

.regulator-node text {
    fill: #173f5f;
    font-size: 12px;
    font-weight: 700;
}

.regulator-node .node-subtitle {
    fill: #64748b;
    font-size: 7px;
    font-weight: 700;
    letter-spacing: 0.12em;
}

.target-node rect {
    fill: #ffffff;
    stroke: #20639b;
    stroke-width: 2;
}

.target-node text {
    fill: #173f5f;
    font-size: 14px;
    font-weight: 700;
}

.response-node rect {
    fill: #f1faf8;
    stroke: #2a9d8f;
    stroke-width: 2;
}

.response-circle {
    fill: #2a9d8f;
    stroke: none;
}

.response-check {
    fill: none;
    stroke: #ffffff;
    stroke-width: 2.5;
    stroke-linecap: round;
    stroke-linejoin: round;
}

.response-node text {
    fill: #206b63;
    font-size: 13px;
    font-weight: 700;
}

.group-label {
    fill: #94a3b8;
    font-size: 8px;
    font-weight: 700;
    letter-spacing: 0.12em;
}

.takeaway {
    position: relative;
    display: flex;
    align-items: center;
    min-height: 58px;
    margin: 0 4px;
    padding: 0 28px;
    border: 1px solid #dce4e9;
    border-radius: 10px;
    background: #ffffff;
    box-sizing: border-box;
    bottom: 5px;
    top: 30px;
}

.takeaway-mark {
    position: absolute;
    left: 0;
    top: 10px;
    bottom: 10px;
    width: 4px;
    border-radius: 4px;
    background: #e9c46a;
}

.takeaway p {
    margin: 0;
    color: #526273;
    font-size: 14px;
    line-height: 1.4;
}

.takeaway strong {
    color: #173f5f;
    font-weight: 700;
}
</style>