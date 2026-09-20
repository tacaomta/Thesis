<template>
  <div class="structural-slide">
    <div class="figure-wrap">
      <img
        src="../../public/images/structural.png"
        alt="Structural accuracy results"
        class="figure"
      />
    </div>
    <div class="conclusion">
      <span class="accent"></span>
      <span>
        Structural accuracy remains high across different network sizes,
        indicating reliable recovery of the underlying network structure.
      </span>
    </div>
  </div>
</template>

<style scoped>
.structural-slide {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  box-sizing: border-box;
  padding: 8px 20px 0;
}
.figure-wrap {
  flex: 1;
  min-height: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}
.figure {
  max-width: 100%;
  max-height: 100%;
  object-fit: contain;
  display: block;
}
.conclusion {
  flex-shrink: 0;
  margin: 10px auto 4px;
  max-width: 900px;
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 9px 16px;
  border: 1px solid #dce4e9;
  border-radius: 6px;
  background: #f8fafb;
  color: #475569;
  font-size: 13px;
  line-height: 1.45;
}
.accent {
  width: 4px;
  align-self: stretch;
  flex-shrink: 0;
  border-radius: 2px;
  background: #7a5af8;
}
</style>