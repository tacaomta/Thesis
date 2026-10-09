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
            <span>Gene (Regulator and Target)</span>
          </div>

          <div>
            <span class="notation-label">Directed edge</span>
            <span class="arrow">→</span>
            <span>Regulatory influence (Enhancer and Inhibitor)</span>
          </div>
        </div>
      </section>

      <section class="grn-visual">
        <figure class="network-figure">
          <img
            src="../../public/images/GRN.png"
            alt="An example of GRNs, size of 100"
            class="network-image"
          />

          <figcaption class="network-caption">
            An example of GRNs, size of 100
          </figcaption>
        </figure>
      </section>
    </div>

    <!-- Key takeaway -->
    <div class="grn-takeaway">
      GRN = genes + directed regulatory relationships
    </div>
  </div>
</template>

<script setup>
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
  height: 320px;
  display: flex;
}

/* =========================
   LEFT — DEFINITION
========================= */

.grn-definition {
  width: 50%;
  padding-top: 25px;
  padding-right: 32px;
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

/* =========================
   RIGHT — IMAGE (1/2 slide)
========================= */

.grn-visual {
  position: relative;
  width: 60%;
  height: 100%;

  display: flex;
  align-items: center;
  justify-content: center;

  box-sizing: border-box;
}

.network-figure {
  width: 100%;
  height: 100%;

  margin: 0;

  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;

  gap: 5px;
}

.network-image {
  max-width: 100%;
  max-height: calc(100% - 5px);

  object-fit: contain;

  /* border: 1px solid #DCE4E9; */
  border-radius: 10px;

  background: #FFFFFF;

  /* box-shadow: 0 4px 14px rgba(23, 63, 95, 0.07); */
}

.network-caption {
  color: #64748B;

  font-size: 11.5px;
  font-style: italic;
  text-align: center;
}

/* =========================
   TAKEAWAY
========================= */

.grn-takeaway {
  position: absolute;
  left: -400px;
  right: 64px;
  top: 300px;
  bottom: 43px;
  text-align: center;
  color: #173F5F;
  font-size: 15px;
  font-weight: 700;
}
</style>