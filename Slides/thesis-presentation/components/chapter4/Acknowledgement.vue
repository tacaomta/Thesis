<template>
  <div class="thank-you">

    <!-- Title -->
    <div class="title">
      <div class="title-main">Thank You</div>
      <div class="title-line" :class="{ complete: visibleCount >= totalItems }"></div>
    </div>

    <!-- =========================
         JOURNEY PATHWAY
    ========================== -->
    <div class="journey-stage">

      <svg
        class="journey-svg"
        viewBox="0 0 1000 300"
        preserveAspectRatio="none"
        aria-label="PhD journey pathway with four people who supported it"
      >

        <!-- background track, always visible -->
        <path
          d="M20,150 C70,120 90,120 130,150 C220,190 290,190 380,150 C470,110 550,110 630,150 C720,190 790,190 880,150 C920,120 950,120 980,150"
          class="track-bg"
        />

        <!-- progress segments — each "draws in" with its own
             accent color as the matching node is revealed -->
        <path
          d="M20,150 C70,120 90,120 130,150"
          pathLength="1"
          class="progress-seg"
          :class="{ active: visibleCount >= 1 }"
          style="--seg-color:#173F5F"
        />
        <path
          d="M130,150 C220,190 290,190 380,150"
          pathLength="1"
          class="progress-seg"
          :class="{ active: visibleCount >= 2 }"
          style="--seg-color:#7A5AF8"
        />
        <path
          d="M380,150 C470,110 550,110 630,150"
          pathLength="1"
          class="progress-seg"
          :class="{ active: visibleCount >= 3 }"
          style="--seg-color:#2A9D8F"
        />
        <path
          d="M630,150 C720,190 790,190 880,150"
          pathLength="1"
          class="progress-seg"
          :class="{ active: visibleCount >= 4 }"
          style="--seg-color:#D98C3D"
        />
        <path
          d="M880,150 C920,120 950,120 980,150"
          pathLength="1"
          class="progress-seg tail-seg"
          :class="{ active: visibleCount >= 4 }"
          style="--seg-color:#D98C3D"
        />

        <!-- nodes -->
        <g
          v-for="node in nodes"
          :key="node.id"
          class="node-dot"
          :class="{ active: visibleCount >= node.id }"
          :style="{ '--node-color': node.color }"
        >
          <circle :cx="node.x" :cy="150" r="17" class="node-circle" />
          <text :x="node.x" :y="154" text-anchor="middle" class="node-number">
            {{ String(node.id).padStart(2, '0') }}
          </text>
        </g>

      </svg>

      <!-- =========================
           ICON CARDS — anchored to
           each node's x position,
           alternating above/below
      ========================== -->
      <Transition
        v-for="node in nodes"
        :key="`card-${node.id}`"
        name="card-pop"
      >
        <div
          v-if="visibleCount >= node.id"
          class="node-card"
          :class="node.side"
          :style="{ left: node.xPct + '%', '--accent': node.color, '--accent-soft': node.colorSoft }"
        >
          <div class="node-card-stem"></div>

          <div class="node-card-body">
            <div class="node-icon">
              <svg viewBox="0 0 24 24" class="node-icon-svg" v-html="node.icon"></svg>
            </div>

            <div class="node-role">{{ node.role }}</div>
            <div v-if="node.name" class="node-name">{{ node.name }}</div>
            <div class="node-tagline">{{ node.tagline }}</div>
          </div>
        </div>
      </Transition>

    </div>

    <!-- Bottom caption -->
    <div class="bottom">
      <Transition name="caption-swap" mode="out-in">
        <div v-if="visibleCount < totalItems" key="hint" class="journey-caption hint">
          Press <strong>SPACE</strong> to continue the journey
        </div>
        <div v-else key="done" class="journey-caption done">
          A journey made possible by these four pillars
        </div>
      </Transition>
    </div>

  </div>
</template>


<script setup>
import { ref, watch, onMounted, onBeforeUnmount } from 'vue'
import { useNav } from '@slidev/client'

const { currentPage } = useNav()

const isExporting =
  typeof window !== 'undefined' &&
  (
    window.location.pathname.startsWith('/export') ||
    new URLSearchParams(window.location.search).has('print') ||
    new URLSearchParams(window.location.search).has('range')
  )

const totalItems = 4
const visibleCount = ref(0)

watch(currentPage, () => {
  visibleCount.value = isExporting ? totalItems : 0
})

const nodes = [
  {
    id: 1,
    x: 130,
    xPct: 13,
    side: 'above',
    color: '#173F5F',
    colorSoft: 'rgba(23, 63, 95, 0.08)',
    role: 'SUPERVISOR',
    name: 'Prof. Yung Keun Kwon',
    tagline: 'Guidance that shaped this work',
    icon: '<path d="M12 3L2 9l10 6 10-6-10-6z" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" /><path d="M6 11.5V17c0 1.6 2.8 3 6 3s6-1.4 6-3v-5.5" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" />'
  },
  {
    id: 2,
    x: 380,
    xPct: 38,
    side: 'below',
    color: '#7A5AF8',
    colorSoft: 'rgba(122, 90, 248, 0.08)',
    role: 'COMMITTEE MEMBERS',
    name: '',
    tagline: 'Insightful questions & valuable feedback',
    icon: '<circle cx="12" cy="7" r="3" fill="none" stroke="currentColor" stroke-width="1.8" /><circle cx="5" cy="9" r="2.3" fill="none" stroke="currentColor" stroke-width="1.8" /><circle cx="19" cy="9" r="2.3" fill="none" stroke="currentColor" stroke-width="1.8" /><path d="M12 12c-3.3 0-6 2-6 5.5V19h12v-1.5c0-3.5-2.7-5.5-6-5.5z" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" /><path d="M5 13.3c-2 .4-3.3 1.9-3.3 4.2V19h3.3" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" /><path d="M19 13.3c2 .4 3.3 1.9 3.3 4.2V19H19" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" />'
  },
  {
    id: 3,
    x: 630,
    xPct: 63,
    side: 'above',
    color: '#2A9D8F',
    colorSoft: 'rgba(42, 157, 143, 0.08)',
    role: 'FAMILY',
    name: '',
    tagline: 'Unconditional support, every step',
    icon: '<path d="M3 11l9-8 9 8" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" /><path d="M5 10v10h14V10" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round" /><path d="M12 22v-4" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" />'
  },
  {
    id: 4,
    x: 880,
    xPct: 88,
    side: 'below',
    color: '#D98C3D',
    colorSoft: 'rgba(217, 140, 61, 0.09)',
    role: 'FRIENDS',
    name: '',
    tagline: 'Shared laughter & encouragement',
    icon: '<circle cx="9" cy="8" r="3" fill="none" stroke="currentColor" stroke-width="1.8" /><circle cx="16.5" cy="9.5" r="2.3" fill="none" stroke="currentColor" stroke-width="1.8" /><path d="M3 20c0-3.2 3-5.3 6-5.3s6 2.1 6 5.3" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" /><path d="M13.5 15c2.2 0.1 5 1.6 5 5" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" />'
  }
]

function handleKeydown(event) {
  if (event.code !== 'Space') return

  event.preventDefault()
  event.stopPropagation()

  if (visibleCount.value < totalItems) {
    visibleCount.value += 1
  }
}

onMounted(() => {
  if (isExporting) {
    visibleCount.value = totalItems
  }
  window.addEventListener('keydown', handleKeydown, true)
})

onBeforeUnmount(() => {
  window.removeEventListener('keydown', handleKeydown, true)
})
</script>


<style scoped>

.thank-you {
  width: 100%;
  height: 100%;

  display: flex;
  flex-direction: column;

  box-sizing: border-box;

  padding: 10px 30px 14px;

  color: #24313A;
  font-family: Inter, 'Segoe UI', sans-serif;
}


/* ─────────────────────────────
   TITLE
───────────────────────────── */

.title {
  text-align: center;
  margin-top: 2px;

  flex-shrink: 0;
}

.title-main {
  font-size: 34px;
  font-weight: 700;
  letter-spacing: -0.03em;
  color: #173F5F;
}

.title-line {
  width: 60px;
  height: 3px;

  margin: 8px auto 0;

  border-radius: 3px;

  background: #dce4e9;

  transition: background 0.5s ease, width 0.5s ease;
}

.title-line.complete {
  width: 120px;

  background: linear-gradient(90deg, #173F5F, #7A5AF8, #2A9D8F, #D98C3D);
}


/* ─────────────────────────────
   JOURNEY STAGE
───────────────────────────── */

.journey-stage {
  position: relative;

  flex: 1;
  min-height: 0;

  width: 100%;
  aspect-ratio: 1000 / 300;

  margin: 18px auto 0;
}

.journey-svg {
  width: 100%;
  height: 100%;

  overflow: visible;
}

/* background track */

.track-bg {
  fill: none;
  stroke: #e2e8ee;
  stroke-width: 3;
  stroke-linecap: round;
}

/* progress segments — "draw in" using the pathLength=1 trick */

.progress-seg {
  fill: none;
  stroke: var(--seg-color);
  stroke-width: 4;
  stroke-linecap: round;

  stroke-dasharray: 1;
  stroke-dashoffset: 1;

  transition: stroke-dashoffset 0.65s ease;
}

.progress-seg.active {
  stroke-dashoffset: 0;
}

.tail-seg {
  opacity: 0.55;
}

/* nodes */

.node-dot {
  transition: filter 0.3s ease;
}

.node-circle {
  fill: #ffffff;
  stroke: #cbd5dc;
  stroke-width: 2;

  transition: fill 0.35s ease, stroke 0.35s ease;
}

.node-number {
  fill: #94a3b8;

  font-family: 'IBM Plex Mono', 'JetBrains Mono', monospace;
  font-size: 11px;
  font-weight: 700;

  transition: fill 0.35s ease;
}

.node-dot.active .node-circle {
  fill: var(--node-color);
  stroke: var(--node-color);
}

.node-dot.active .node-number {
  fill: #ffffff;
}


/* ─────────────────────────────
   ICON CARDS
───────────────────────────── */

.node-card {
  position: absolute;

  top: 50%;

  width: 160px;

  transform: translateX(-50%);

  display: flex;
  flex-direction: column;
  align-items: center;

  pointer-events: none;
}

.node-card.above {
  top: calc(50% - 40px);
  flex-direction: column-reverse;
  transform: translate(-50%, -100%);
}

.node-card.below {
  top: calc(50% + 40px);
  transform: translateX(-50%);
}

.node-card-stem {
  width: 1.5px;
  height: 16px;

  background: var(--accent);

  opacity: 0.55;
}

.node-card-body {
  display: flex;
  flex-direction: column;
  align-items: center;

  margin-top: 2px;
  padding: 10px 12px 11px;

  border-radius: 12px;

  background: linear-gradient(180deg, #FFFFFF 0%, var(--accent-soft) 100%);
  border: 1px solid #DCE4E9;

  box-shadow: 0 6px 16px rgba(23, 63, 95, 0.09);

  text-align: center;
}

.node-card.above .node-card-body {
  margin-top: 0;
  margin-bottom: 2px;
}

.node-icon {
  width: 36px;
  height: 36px;

  display: flex;
  align-items: center;
  justify-content: center;

  margin-bottom: 7px;

  border-radius: 10px;

  background: var(--accent-soft);
  border: 1px solid var(--accent);

  color: var(--accent);
}

.node-icon-svg {
  width: 19px;
  height: 19px;
}

.node-role {
  font-family: "IBM Plex Mono", "JetBrains Mono", monospace;
  font-size: 8px;
  font-weight: 700;
  letter-spacing: .12em;

  color: var(--accent);
}

.node-name {
  margin-top: 4px;

  font-size: 11px;
  font-weight: 600;

  color: #173F5F;
}

.node-tagline {
  margin-top: 4px;

  font-size: 8.8px;
  line-height: 1.35;

  color: #64748B;
}

/* card enter animation */

.card-pop-enter-active {
  transition:
    opacity 0.35s ease,
    transform 0.35s ease;
}

.card-pop-enter-from {
  opacity: 0;
}

.node-card.above.card-pop-enter-from {
  transform: translate(-50%, -100%) translateY(10px);
}

.node-card.below.card-pop-enter-from {
  transform: translateX(-50%) translateY(-10px);
}


/* ─────────────────────────────
   BOTTOM CAPTION
───────────────────────────── */

.bottom {
  flex-shrink: 0;

  text-align: center;

  margin-top: 10px;

  height: 20px;
}

.journey-caption {
  font-size: 10.5px;
  letter-spacing: .03em;
}

.journey-caption.hint {
  color: #94A3B8;
}

.journey-caption.hint strong {
  color: #64748B;
  font-weight: 700;
}

.journey-caption.done {
  color: #2A9D8F;
  font-weight: 600;
}

.caption-swap-enter-active,
.caption-swap-leave-active {
  transition: opacity 0.25s ease;
}

.caption-swap-enter-from,
.caption-swap-leave-to {
  opacity: 0;
}


/* ─────────────────────────────
   REDUCED MOTION
───────────────────────────── */

@media (prefers-reduced-motion: reduce) {
  .progress-seg,
  .node-circle,
  .node-number,
  .title-line,
  .card-pop-enter-active,
  .caption-swap-enter-active,
  .caption-swap-leave-active {
    transition: none !important;
  }
}

</style>