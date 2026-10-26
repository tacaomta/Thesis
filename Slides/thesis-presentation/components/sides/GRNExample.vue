<template>
<div class="network-gallery-slide">

    <div class="gallery-grid">

        <!-- Column: N = 10 -->
        <div class="gallery-column">
            <div class="column-label">
                <span class="size-badge">N = 10</span>
            </div>

            <button
                type="button"
                class="image-frame"
                :class="{ flipped: toggled[0] }"
                @click="toggleImage(0)"
            >
                <img
                    :src="toggled[0] ? images[0].value : images[0].structure"
                    :alt="toggled[0] ? 'Network values, size 10' : 'Network structure, size 10'"
                    class="gallery-image"
                />

                <span class="mode-tag" :class="{ value: toggled[0] }">
                    {{ toggled[0] ? 'VALUES' : 'STRUCTURE' }}
                </span>
            </button>

            <div class="column-hint">Click to view {{ toggled[0] ? 'structure' : 'values' }}</div>
        </div>

        <!-- Column: N = 50 -->
        <div class="gallery-column">
            <div class="column-label">
                <span class="size-badge">N = 50</span>
            </div>

            <button
                type="button"
                class="image-frame"
                :class="{ flipped: toggled[1] }"
                @click="toggleImage(1)"
            >
                <img
                    :src="toggled[1] ? images[1].value : images[1].structure"
                    :alt="toggled[1] ? 'Network values, size 50' : 'Network structure, size 50'"
                    class="gallery-image"
                />

                <span class="mode-tag" :class="{ value: toggled[1] }">
                    {{ toggled[1] ? 'VALUES' : 'STRUCTURE' }}
                </span>
            </button>

            <div class="column-hint">Click to view {{ toggled[1] ? 'structure' : 'values' }}</div>
        </div>

        <!-- Column: N = 100 -->
        <div class="gallery-column">
            <div class="column-label">
                <span class="size-badge">N = 100</span>
            </div>

            <button
                type="button"
                class="image-frame"
                :class="{ flipped: toggled[2] }"
                @click="toggleImage(2)"
            >
                <img
                    :src="toggled[2] ? images[2].value : images[2].structure"
                    :alt="toggled[2] ? 'Network values, size 100' : 'Network structure, size 100'"
                    class="gallery-image"
                />

                <span class="mode-tag" :class="{ value: toggled[2] }">
                    {{ toggled[2] ? 'VALUES' : 'STRUCTURE' }}
                </span>
            </button>

            <div class="column-hint">Click to view {{ toggled[2] ? 'structure' : 'values' }}</div>
        </div>

    </div>

</div>
</template>

<script setup>
import { reactive } from 'vue'

const images = [
    { structure: '../../public/images/net10.png',  value: '../../public/images/netval10.png' },
    { structure: '../../public/images/net50.png',  value: '../../public/images/netval50.png' },
    { structure: '../../public/images/net100.png', value: '../../public/images/netval100.png' }
]

// independent toggle state per column: false = structure, true = values
const toggled = reactive([false, false, false])

function toggleImage(index) {
    toggled[index] = !toggled[index]
}
</script>

<style scoped>
.network-gallery-slide {
    width: 100%;
    height: 100%;
    box-sizing: border-box;

    display: flex;
    flex-direction: column;

    padding: 14px 26px 10px;

    background: #f8fafb;
    color: #24313a;

    font-family: 'Inter', 'Segoe UI', sans-serif;
}

/* =========================
   HEADER
========================= */

.slide-header {
    flex-shrink: 0;
    margin-bottom: 14px;
}

.section-label {
    margin-bottom: 5px;

    color: #64748b;

    font-size: 10px;
    font-weight: 700;
    letter-spacing: 0.14em;
}

.slide-header h1 {
    margin: 0;

    color: #173f5f;

    font-size: 22px;
    line-height: 1.25;
    font-weight: 700;
    letter-spacing: -0.01em;
}

.subtitle {
    margin: 5px 0 0;

    color: #64748b;

    font-size: 12px;
    line-height: 1.4;
}

/* =========================
   GALLERY GRID
========================= */

.gallery-grid {
    flex: 1;
    min-height: 0;

    display: grid;
    grid-template-columns: repeat(3, 1fr);

    gap: 20px;
}

.gallery-column {
    min-width: 0;
    min-height: 0;

    display: flex;
    flex-direction: column;
    align-items: center;
}

.column-label {
    margin-bottom: 10px;
}

.size-badge {
    padding: 4px 12px;

    border-radius: 999px;
    background: #eef5fa;
    border: 1px solid #c7d9e6;

    color: #20639b;

    font-family: 'IBM Plex Mono', monospace;
    font-size: 11px;
    font-weight: 700;
    letter-spacing: 0.04em;
}

/* =========================
   IMAGE FRAME (clickable)
========================= */

.image-frame {
    position: relative;

    flex: 1;
    width: 100%;
    min-height: 0;

    padding: 0;
    margin: 0;

    border: 1px solid #dce4e9;
    border-radius: 10px;

    background: #ffffff;

    box-sizing: border-box;
    overflow: hidden;

    cursor: pointer;

    display: flex;
    align-items: center;
    justify-content: center;

    transition:
        border-color 0.2s ease,
        box-shadow 0.2s ease,
        transform 0.15s ease;
}

.image-frame:hover {
    border-color: #20639b;
    box-shadow: 0 6px 16px rgba(23, 63, 95, 0.1);

    transform: translateY(-2px);
}

.image-frame:active {
    transform: translateY(0) scale(0.995);
}

.image-frame.flipped {
    border-color: #2a9d8f;
}

.image-frame.flipped:hover {
    box-shadow: 0 6px 16px rgba(42, 157, 143, 0.14);
}

.gallery-image {
    max-width: 100%;
    max-height: 100%;

    width: auto;
    height: auto;

    object-fit: contain;

    display: block;
}

/* =========================
   MODE TAG (STRUCTURE / VALUES)
========================= */

.mode-tag {
    position: absolute;

    top: 9px;
    right: 9px;

    padding: 3px 9px;

    border-radius: 999px;

    background: rgba(32, 99, 155, 0.92);
    color: #ffffff;

    font-family: 'IBM Plex Mono', monospace;
    font-size: 8.5px;
    font-weight: 700;
    letter-spacing: 0.08em;

    pointer-events: none;

    transition: background 0.2s ease;
}

.mode-tag.value {
    background: rgba(42, 157, 143, 0.92);
}

/* =========================
   HINT
========================= */

.column-hint {
    margin-top: 8px;

    color: #94a3b8;

    font-size: 10px;
}

/* =========================
   RESPONSIVE
========================= */

@media (max-width: 900px) {
    .gallery-grid {
        grid-template-columns: 1fr;
        overflow-y: auto;
        gap: 14px;
    }
}
</style>