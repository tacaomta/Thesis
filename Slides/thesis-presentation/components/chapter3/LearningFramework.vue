<template>
  <div class="framework-slide">
    <div class="figure-wrap">
      <img
        src="../../public/images/framework.png"
        alt="Proposed framework for representation learning-based GRN inference"
        class="framework-image"
      />
    </div>

    <div class="framework-caption">
      <span class="accent"></span>
      <span>
        A learning framework for representing regulatory relationships
        from time-series gene expression data.
      </span>
    </div>
  </div>
</template>

<style scoped>
.framework-slide {
  width: 100%;
  height: 100%;
  box-sizing: border-box;

  display: flex;
  flex-direction: column;

  padding: 8px 20px 0;
}

/* =========================
   Framework figure
   ========================= */

.figure-wrap {
  flex: 1;
  min-height: 0;

  display: flex;
  align-items: center;
  justify-content: center;

  overflow: hidden;
}

.framework-image {
  display: block;

  max-width: 100%;
  max-height: 100%;

  width: auto;
  height: auto;

  object-fit: contain;
}

/* =========================
   Caption
   ========================= */

.framework-caption {
  flex-shrink: 0;

  display: flex;
  align-items: center;
  gap: 10px;

  margin: 10px auto 4px;
  padding: 9px 16px;

  max-width: 900px;

  box-sizing: border-box;

  background: #f8fafb;
  border: 1px solid #dce4e9;
  border-radius: 6px;

  color: #475569;

  font-size: 13px;
  line-height: 1.45;
}

.accent {
  width: 4px;
  align-self: stretch;
  flex-shrink: 0;

  border-radius: 2px;

  background: #2a9d8f;
}
</style>