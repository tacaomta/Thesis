<template>
  <div class="difficulty-slide">
    <div class="radial-stage">

      <svg
        class="radial-svg"
        viewBox="0 0 400 400"
        aria-label="Five key challenges of time-series GRN inference, arranged around a central concept"
      >
        <!-- =====================================================
             OUTER SECTORS — one per detailed point
             Revealed progressively; together they close into
             a full ring around the central circle.
        ===================================================== -->
        <Transition v-for="(sector, i) in sectors" :key="sector.number" name="wedge">
          <g v-if="visibleCount >= i + 1" class="wedge-group">
            <path
              :d="sector.path"
              class="wedge-path"
              :style="{ '--wedge-color': sector.color }"
            />
          </g>
        </Transition>

        <!-- =====================================================
             CENTRAL CIRCLE — main concept
        ===================================================== -->
        <circle cx="200" cy="200" r="74" class="center-circle" />
        <circle cx="200" cy="200" r="64" class="center-ring" />

        <text x="200" y="196" text-anchor="middle" class="center-title">CHALLENGES</text>
        <text x="200" y="214" text-anchor="middle" class="center-sub">{{ total }} key factors</text>

      </svg>

      <!-- =====================================================
           LABEL OVERLAYS — positioned at each sector's mid-angle,
           plus a manual per-sector nudge (see labelNudge below)
      ===================================================== -->
      <Transition v-for="(sector, i) in sectors" :key="`label-${sector.number}`" name="label">
        <div
          v-if="visibleCount >= i + 1"
          class="wedge-label"
          :style="{
            left: sector.labelLeft,
            top: sector.labelTop,
            width: sector.labelWidth + 'px',
            transform: `translate(calc(-50% + ${sector.nudge.dx}px), calc(-50% + ${sector.nudge.dy}px))`,
            '--wedge-color': sector.color
          }"
        >
          <span class="wedge-number">{{ sector.number }}</span>
          <h3>{{ sector.title }}</h3>
          <p>{{ sector.example }}</p>
        </div>
      </Transition>

    </div>

    <!-- Space hint -->
    <div v-if="visibleCount < total" class="space-hint">
      Press SPACE to reveal the next challenge
    </div>

  </div>
</template>

<script setup>
import { ref, computed, watch, onMounted, onBeforeUnmount } from 'vue'
import { useNav } from '@slidev/client'


const { currentPage } = useNav()
const isExporting =
  typeof window !== 'undefined' &&
  (
    window.location.pathname.startsWith('/export') ||
    new URLSearchParams(window.location.search).has('print') ||
    new URLSearchParams(window.location.search).has('range')
  )

/* =========================================================
   CONTENT
   ========================================================= */

const items = [
  {
    number: '01',
    title: 'High dimensionality',
    example: '10,000 genes, O(N²) interactions'
  },
  {
    number: '02',
    title: 'Limited observations',
    example: 'Few time points & replicates'
  },
  {
    number: '03',
    title: 'Noise & variability',
    example: 'Signal + noise + variation'
  },
  {
    number: '04',
    title: 'Complex dependencies',
    example: 'Nonlinear, feedback, indirect'
  },
  {
    number: '05',
    title: 'Underdetermined inference',
    example: 'Many plausible structures'
  }
]

const total = items.length

/* =========================================================
   MANUAL PER-SECTOR LABEL NUDGE
   dx / dy in SVG viewBox units (≈ px at the stage's natural
   size). Positive dx = right, negative dx = left.
   Positive dy = down, negative dy = up.

   Tune these freely per sector:
   - 01 (upper-right): nudge left a little
   - 02 (lower-right): nudge left, more than 01
   - 03 (bottom):       nudge up (~1cm)
   - 04 (lower-left):   nudge right (~1.5cm)
   - 05 (upper-left):   nudge right
   ========================================================= */

const labelNudge = [
  { dx: -14, dy: 0 },   // 01
  { dx: -34, dy: 0 },   // 02
  { dx: 0,   dy: -10 }, // 03  (~1cm up)
  { dx: 42,  dy: 0 },   // 04  (~1.5cm right)
  { dx: 25,  dy: 0 }    // 05
]

/* =========================================================
   REVEAL STATE
   ========================================================= */

const visibleCount = ref(0)

watch(currentPage, () => {
  if (isExporting) {
    visibleCount.value = total
  }
  else
  {
    visibleCount.value = 0
  }
})

function handleKeydown(event) {
  if (event.code !== 'Space') return

  event.preventDefault()
  event.stopPropagation()

  if (visibleCount.value < total) {
    visibleCount.value += 1
  }
}

onMounted(() => {
  if (isExporting) {
    visibleCount.value = total
  }
  window.addEventListener('keydown', handleKeydown, true)
})

onBeforeUnmount(() => {
  window.removeEventListener('keydown', handleKeydown, true)
})

/* =========================================================
   RADIAL GEOMETRY
   Odd item count (3, 5, 7, ...) → donut sectors that close
   into a full circle around the central concept.
   Gaps between sectors are a CONSTANT PIXEL WIDTH (gapPx),
   created by shifting each boundary along the tangent
   direction at that angle — this keeps the two edges of
   adjacent sectors truly parallel (not just angularly spaced).
   ========================================================= */

const cx = 200
const cy = 200
const innerR = 74
const outerR = 196

/* ---- TUNE THIS to widen/narrow the gap between sectors ---- */
const gapPx = 3
/* ------------------------------------------------------------ */

const palette = ['#20639B', '#7A5AF8', '#2A9D8F', '#E9C46A', '#E76F51', '#5B8C9B', '#B5651A']

function toRad(angleDeg) {
  return ((angleDeg - 90) * Math.PI) / 180
}

function polarToCartesian(centerX, centerY, radius, angleDeg) {
  const rad = toRad(angleDeg)
  return {
    x: centerX + radius * Math.cos(rad),
    y: centerY + radius * Math.sin(rad)
  }
}

/* unit tangent vector at angleDeg, pointing in the direction
   of increasing angle (clockwise) */
function tangentVector(angleDeg) {
  const rad = toRad(angleDeg)
  return { x: -Math.sin(rad), y: Math.cos(rad) }
}

function offset(point, tangent, amount) {
  return {
    x: point.x + tangent.x * amount,
    y: point.y + tangent.y * amount
  }
}

function describeParallelSector(a0, a1) {
  const half = gapPx / 2

  const tStart = tangentVector(a0)
  const tEnd = tangentVector(a1)

  const outerStart = offset(polarToCartesian(cx, cy, outerR, a0), tStart, half)
  const innerStart = offset(polarToCartesian(cx, cy, innerR, a0), tStart, half)
  const outerEnd = offset(polarToCartesian(cx, cy, outerR, a1), tEnd, -half)
  const innerEnd = offset(polarToCartesian(cx, cy, innerR, a1), tEnd, -half)

  const largeArc = a1 - a0 > 180 ? 1 : 0

  return [
    'M', outerStart.x, outerStart.y,
    'A', outerR, outerR, 0, largeArc, 1, outerEnd.x, outerEnd.y,
    'L', innerEnd.x, innerEnd.y,
    'A', innerR, innerR, 0, largeArc, 0, innerStart.x, innerStart.y,
    'Z'
  ].join(' ')
}

const sectors = computed(() => {
  const step = 360 / total

  return items.map((item, i) => {
    const a0 = i * step
    const a1 = (i + 1) * step
    const mid = (a0 + a1) / 2
    const midRadius = (innerR + outerR) / 2 + 10

    const pos = polarToCartesian(cx, cy, midRadius, mid)

    const sectorAngleRad = (step * Math.PI) / 180
    const safeRadius = midRadius - 34
    const chordWidth = 2 * safeRadius * Math.sin(sectorAngleRad / 2)
    const labelWidth = Math.max(70, Math.min(150, chordWidth * 0.86))

    return {
      ...item,
      path: describeParallelSector(a0, a1),
      labelLeft: ((pos.x / 400) * 100).toFixed(2) + '%',
      labelTop: ((pos.y / 400) * 100).toFixed(2) + '%',
      labelWidth,
      nudge: labelNudge[i] || { dx: 0, dy: 0 },
      color: palette[i % palette.length]
    }
  })
})
</script>

<style scoped>
.difficulty-slide {
  width: 100%;
  height: 100%;
  box-sizing: border-box;

  display: flex;
  flex-direction: column;

  padding: 10px 24px 6px;

  background: #f8fafb;
  color: #24313a;

  font-family: 'Inter', 'Segoe UI', sans-serif;

  position: relative;
}

/* =========================
   HEADER
========================= */

.slide-header {
  flex-shrink: 0;
  margin-bottom: 4px;

  text-align: center;
}

.section-label {
  margin-bottom: 4px;

  color: #64748b;

  font-size: 10px;
  font-weight: 700;
  letter-spacing: 0.14em;
}

.slide-header h1 {
  margin: 0;

  color: #173f5f;

  font-size: 19px;
  line-height: 1.25;
  font-weight: 700;
  letter-spacing: -0.01em;
}

/* =========================
   RADIAL STAGE
========================= */

.radial-stage {
  flex: 1;
  min-height: 0;

  position: relative;

  width: min(100%, 490px);
  aspect-ratio: 1 / 1;

  margin: 4px auto 0;
}

.radial-svg {
  width: 100%;
  height: 100%;

  overflow: visible;
}

/* =========================
   WEDGES
========================= */

.wedge-path {
  fill: color-mix(in srgb, var(--wedge-color) 12%, white);
  stroke: var(--wedge-color);
  stroke-width: 1.4;

  transform-box: fill-box;
  transform-origin: center;

  transition: filter 0.2s ease;
}

.wedge-path:hover {
  filter: brightness(0.97);
}

.wedge-enter-active {
  transition:
    opacity 0.4s ease,
    transform 0.4s cubic-bezier(0.22, 1, 0.36, 1);
}

.wedge-enter-from {
  opacity: 0;
  transform: scale(0.4);
}

/* =========================
   CENTER CIRCLE
========================= */

.center-circle {
  fill: #ffffff;
  stroke: #173f5f;
  stroke-width: 2.5;
}

.center-ring {
  fill: none;
  stroke: #dce4e9;
  stroke-width: 1;
  stroke-dasharray: 3 4;
}

.center-title {
  fill: #173f5f;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 15px;
  font-weight: 700;
  letter-spacing: 0.04em;
}

.center-sub {
  fill: #94a3b8;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 9px;
  letter-spacing: 0.06em;
}

/* =========================
   LABEL OVERLAYS
========================= */

.wedge-label {
  position: absolute;

  display: flex;
  flex-direction: column;
  align-items: center;

  text-align: center;

  pointer-events: none;

  box-sizing: border-box;
}

.label-enter-active {
  transition:
    opacity 0.4s ease 0.08s,
    transform 0.4s ease 0.08s;
}

.label-enter-from {
  opacity: 0;
}

.wedge-number {
  margin-bottom: 3px;

  color: var(--wedge-color);

  font-family: 'IBM Plex Mono', monospace;
  font-size: 12px;
  font-weight: 700;
  letter-spacing: 0.05em;
}

.wedge-label h3 {
  margin: 0 0 3px;

  width: 100%;

  color: #173f5f;

  font-size: 16px;
  line-height: 1.2;
  font-weight: 700;

  overflow: hidden;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
}

.wedge-label p {
  margin: 0;

  width: 100%;

  color: #64748b;

  font-size: 10px;
  line-height: 1.28;

  overflow: hidden;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
}

/* =========================
   SPACE HINT
========================= */

.space-hint {
  position: absolute;

  right: 20px;
  bottom: 6px;

  color: #94a3b8;

  font-family: 'IBM Plex Mono', monospace;
  font-size: 10px;
  letter-spacing: 0.02em;
}

/* =========================
   RESPONSIVE
========================= */

@media (max-width: 700px) {
  .wedge-label p {
    display: none;
  }
}
</style>