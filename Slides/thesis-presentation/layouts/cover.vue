<template>
  <div class="cover">
    <div class="cover-network">
      <slot name="network" />
    </div>

    <div class="cover-content">
      <div class="lab-name">
        COMPLEX SYSTEMS COMPUTING LAB
      </div>

      <div class="accent-line"></div>

      <slot />
    </div>

    <div class="cover-footer">
      <span>Graduation Thesis</span>
      <span>2026</span>
    </div>
  </div>
</template>

<style>
.cover {
  position: relative;
  width: 100%;
  height: 100%;
  background: #f8fafb;
  overflow: hidden;
}

.cover-content {
  position: absolute;
  left: 72px;
  top: 110px;
  width: 68%;
  z-index: 3;
}

.lab-name {
  font-size: 15px;
  font-weight: 600;
  letter-spacing: 0.14em;
  color: #2a9d8f;
}

.accent-line {
  width: 70px;
  height: 4px;
  margin: 20px 0 30px;
  background: #173f5f;
  border-radius: 2px;
}

.cover-content h1 {
  max-width: 900px;
  color: #173f5f;
  font-size: 52px;
  line-height: 1.08;
  font-weight: 700;
}

.cover-footer {
  position: absolute;
  left: 72px;
  right: 72px;
  bottom: 40px;
  display: flex;
  justify-content: space-between;
  color: #64748b;
  font-size: 14px;
}
</style>