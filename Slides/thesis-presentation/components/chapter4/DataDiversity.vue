<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

const visibleCount = ref(0)
const totalItems = 4
const findings = [
  { number: '01', title: 'Generative Stochasticity', text: 'Multiple executions of trained autoencoders generate varied synthetic expression profiles.' },
  { number: '02', title: 'Low Similarity Index', text: 'Mean pairwise matrix similarity ranges between 0.35 and 0.40, confirming high variation among generated outputs.' },
  { number: '03', title: 'Stable Inference Performance', text: 'Despite substantial variation in generated values, downstream GRN reconstruction accuracy remains highly consistent.' },
  { number: '04', title: 'Biological Realism', text: 'Reflects natural biological systems where multiple expression pathways map to identical underlying regulatory logic.' }
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
  window.addEventListener('keydown', handleKeydown, true)
})

onBeforeUnmount(() => {
  window.removeEventListener('keydown', handleKeydown, true)
})
</script>

<template>
  <div class="diversity-slide">

    <!-- =========================
         CHART / IMAGE
         ========================= -->
    <section class="visual-section">

      <div class="image-wrapper">
        <img
          src="../../public/images/networks_distance.png"
          alt="Similarity matrix between synthesized gene expression data"
          class="similarity-image"
        />
      </div>

      <div class="figure-caption">
        <strong>Similarity matrix between synthesized gene expression profiles.</strong>
        (a) Pairwise similarity at <em>K</em> = 10.
        (b) Mean similarity index across observed time steps
        <em>K</em> = 10–90.
      </div>

    </section>

    <!-- =========================
         FINDINGS
         ========================= -->
    <div class="findings">
      <div v-for="item in findings" :key="item.number" class="finding">
        <div class="finding-header"><span class="finding-number">{{ item.number }}</span><h3>{{ item.title }}</h3></div>
        <p>{{ item.text }}</p>
      </div>
    </div>

  </div>
</template>

<style scoped>
.diversity-slide {
  width: 100%;
  height: 100%;
  box-sizing: border-box;

  display: flex;
  flex-direction: column;

  color: #24313A;
}

/* =========================================
   VISUAL
   ========================================= */

.visual-section {
  width: 100%;

  display: flex;
  flex-direction: column;
  align-items: center;

  flex-shrink: 0;
}

.image-wrapper {
  width: 100%;
  height: 300px;

  display: flex;
  align-items: center;
  justify-content: center;

  overflow: hidden;
}

.similarity-image {
  width: 100%;
  height: 100%;

  object-fit: contain;
  display: block;
}

.figure-caption {
  width: 94%;

  margin-top: 5px;

  text-align: center;

  font-size: 12px;
  line-height: 1.35;

  color: #64748B;
}

/* =========================================
   FINDINGS
   ========================================= */

.findings { width:100%; display:grid; grid-template-columns:repeat(4,1fr); gap:10px; margin-top:15px; }
.finding { min-width: 0; box-sizing: border-box; padding: 7px 9px; border-top: 2px solid #b3cedf; background: #fff; position: relative; z-index: 1; transition: transform 0.22s ease, box-shadow 0.22s ease, border-top-color 0.22s ease; } /* * Lift effect when hovering */ 
.finding:hover { transform: translateY(-4px); border-top-color: #2A9D8F; box-shadow: 0 7px 16px rgba(23, 63, 95, 0.12), 0 2px 5px rgba(23, 63, 95, 0.06); z-index: 5; }
.finding:hover .finding-number { transform: scale(1.08); color: #20639B; }
.finding:hover h3 { color: #20639B; }
.finding-header { display:flex; align-items:baseline; gap:6px; margin-bottom:3px; }
.finding-number { flex:0 0 auto; color:#2A9D8F; font-family:'IBM Plex Mono','JetBrains Mono',monospace; font-size:9.5px; font-weight:700; letter-spacing:.08em; }
.finding h3 { margin:0; color:#173F5F; font-size:10.5px; line-height:1.2; font-weight:700; }
.finding p { margin:0; color:#64748B; font-size:9px; line-height:1.28; }

/* =========================================
   RESPONSIVE
   ========================================= */

@media (max-width: 800px) {
  .image-wrapper {
    height: 250px;
  }

  .findings {
    grid-template-columns: 1fr;
  }
}
</style>