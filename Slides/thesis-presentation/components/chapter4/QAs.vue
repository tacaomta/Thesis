<template>
<div class="qa-slide">

    <!-- subtle background network, reused motif from the deck -->
    <div class="bg-accent"></div>

    <div class="qa-content">

        <div class="qa-eyebrow">OPEN FOR DISCUSSION</div>

        <h1 class="qa-title">Questions &amp; Discussion</h1>

        <div class="qa-divider"></div>

        <p class="qa-subtitle">
            Thank you for your attention. I welcome your questions and feedback.
        </p>

        <!-- listening indicator -->
        <div class="listening-indicator">
            <div class="pulse-ring"></div>
            <div class="pulse-ring delay-1"></div>
            <div class="pulse-ring delay-2"></div>

            <div class="mic-icon">
                <svg viewBox="0 0 24 24" aria-hidden="true">
                    <rect x="9" y="2" width="6" height="12" rx="3" />
                    <path d="M5 11a7 7 0 0 0 14 0" />
                    <line x1="12" y1="18" x2="12" y2="22" />
                    <line x1="8" y1="22" x2="16" y2="22" />
                </svg>
            </div>
        </div>

        <div class="qa-status">Listening for questions</div>

    </div>

</div>
</template>

<script setup>
</script>

<style scoped>
.qa-slide {
    position: relative;
    width: 100%;
    height: 100%;
    box-sizing: border-box;

    display: flex;
    align-items: center;
    justify-content: center;

    background: #f8fafb;
    color: #24313a;

    font-family: 'Inter', 'Segoe UI', sans-serif;

    overflow: hidden;
}

/* =========================
   BACKGROUND ACCENT
========================= */

.bg-accent {
    position: absolute;

    top: -120px;
    right: -120px;

    width: 420px;
    height: 420px;

    border-radius: 50%;

    background: radial-gradient(
        circle,
        rgba(32, 99, 155, 0.06) 0%,
        rgba(42, 157, 143, 0.04) 55%,
        transparent 75%
    );

    pointer-events: none;
}

.qa-slide::before {
    content: '';

    position: absolute;

    bottom: -160px;
    left: -140px;

    width: 380px;
    height: 380px;

    border-radius: 50%;

    background: radial-gradient(
        circle,
        rgba(42, 157, 143, 0.05) 0%,
        transparent 70%
    );

    pointer-events: none;
}

/* =========================
   CONTENT
========================= */

.qa-content {
    position: relative;
    z-index: 1;

    display: flex;
    flex-direction: column;
    align-items: center;

    text-align: center;

    max-width: 640px;
}

.qa-eyebrow {
    margin-bottom: 14px;

    color: #2a9d8f;

    font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
    font-size: 12px;
    font-weight: 700;
    letter-spacing: 0.22em;
}

.qa-title {
    margin: 0;

    color: #173f5f;

    font-size: 44px;
    line-height: 1.15;
    font-weight: 750;
    letter-spacing: -0.015em;
}

.qa-divider {
    width: 64px;
    height: 3px;

    margin: 20px 0 18px;

    border-radius: 3px;

    background: linear-gradient(90deg, #20639b, #2a9d8f);
}

.qa-subtitle {
    margin: 0 0 36px;

    max-width: 480px;

    color: #64748b;

    font-size: 15px;
    line-height: 1.55;
}

/* =========================
   LISTENING INDICATOR
========================= */

.listening-indicator {
    position: relative;

    width: 78px;
    height: 78px;

    display: flex;
    align-items: center;
    justify-content: center;

    margin-bottom: 14px;
}

.pulse-ring {
    position: absolute;

    width: 78px;
    height: 78px;

    border-radius: 50%;

    border: 1.5px solid rgba(42, 157, 143, 0.4);

    animation: pulseOut 2.4s ease-out infinite;
}

.pulse-ring.delay-1 {
    animation-delay: 0.8s;
}

.pulse-ring.delay-2 {
    animation-delay: 1.6s;
}

@keyframes pulseOut {
    0% {
        transform: scale(0.55);
        opacity: 0.9;
    }
    100% {
        transform: scale(1.3);
        opacity: 0;
    }
}

.mic-icon {
    position: relative;
    z-index: 1;

    width: 52px;
    height: 52px;

    display: flex;
    align-items: center;
    justify-content: center;

    border-radius: 50%;

    background: #ffffff;
    border: 1.5px solid #c9e6e1;

    box-shadow: 0 6px 18px rgba(42, 157, 143, 0.14);
}

.mic-icon svg {
    width: 24px;
    height: 24px;

    fill: none;
    stroke: #2a9d8f;
    stroke-width: 1.8;
    stroke-linecap: round;
    stroke-linejoin: round;
}

.qa-status {
    color: #94a3b8;

    font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
    font-size: 11px;
    letter-spacing: 0.06em;
}

/* =========================
   REDUCED MOTION
========================= */

@media (prefers-reduced-motion: reduce) {
    .pulse-ring {
        animation: none;
        opacity: 0.3;
    }
}

/* =========================
   RESPONSIVE
========================= */

@media (max-width: 700px) {
    .qa-title {
        font-size: 32px;
    }

    .qa-subtitle {
        font-size: 13px;
    }
}
</style>