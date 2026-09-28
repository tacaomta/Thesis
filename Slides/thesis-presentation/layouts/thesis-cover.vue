<template>
  <div class="thesis-cover">
    <div class="top-accent"></div>
    <div class="background-network">
      <slot name="network" />
    </div>
    <div class="cover-main">
      <div class="institution">
        <img
          src="../public/images/uou.jpg"
          class="ulsan-logo"
          alt="University of Ulsan"
        />
        <div class="institution-text">
          <div class="university-name">UNIVERSITY OF ULSAN</div>
          <div class="department">
            Department of Electrical, Electronic and Computer Engineering
          </div>
        </div>
      </div>
      <div class="thesis-label">DOCTORAL THESIS</div>
      <div class="title-accent"></div>
      <h1>
        Inferring Gene Regulatory Networks from Time-Series Gene Expression Data
      </h1>
      <div class="author-block">
        <div class="person-row">
          <span class="person-label">Author</span>
          <span class="person-value">Cao Tuan Anh</span>
        </div>
        <div class="person-row">
          <span class="person-label">Supervisor</span>
          <span class="person-value">Prof. Yung Keun Kwon</span>
        </div>
      </div>
    </div>
    <div class="cover-bottom">
      <div class="lab-name">
        COMPLEX SYSTEMS COMPUTING LAB
      </div>
      <div class="date">
        November 2026
      </div>
    </div>
  </div>
</template>

<style>
.thesis-cover {
  position: relative;
  width: 100%;
  height: 100%;
  overflow: hidden;
  background: #f8fafb;
  color: #24313a;
}
.top-accent {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 5px;
  background: #173f5f;
}
.background-network {
  position: absolute;
  top: 80px;
  right: -20px;
  width: 48%;
  height: 75%;
  opacity: 0.16;
  z-index: 0;
}
.cover-main {
  position: relative;
  z-index: 2;
  width: 78%;
  height: 100%;
  padding: 54px 0 70px 72px;
  box-sizing: border-box;
}
.institution {
  display: flex;
  align-items: center;
  gap: 18px;
}
.ulsan-logo {
  width: 72px;
  height: 72px;
  object-fit: contain;
}
.institution-text {
  display: flex;
  flex-direction: column;
  gap: 6px;
}
.university-name {
  color: #173f5f;
  font-size: 18px;
  font-weight: 700;
  letter-spacing: 0.08em;
}
.department {
  max-width: 600px;
  color: #64748b;
  font-size: 12px;
  line-height: 1.4;
}
.thesis-label {
  margin-top: 68px;
  color: #2a9d8f;
  font-size: 15px;
  font-weight: 700;
  letter-spacing: 0.18em;
}
.title-accent {
  width: 62px;
  height: 4px;
  margin-top: 17px;
  border-radius: 2px;
  background: #173f5f;
}
h1 {
  max-width: 850px;
  margin-top: 26px;
  color: #173f5f;
  font-size: 38px;
  line-height: 1.13;
  font-weight: 700;
  letter-spacing: -0.025em;
}
.author-block {
  margin-top: 34px;
  padding-left: 18px;
  border-left: 3px solid #2a9d8f;
}
.person-row {
  display: flex;
  align-items: baseline;
  margin-bottom: 9px;
}
.person-label {
  width: 105px;
  color: #64748b;
  font-size: 13px;
}
.person-value {
  color: #24313a;
  font-size: 15px;
  font-weight: 600;
}
.cover-bottom {
  position: absolute;
  left: 72px;
  right: 72px;
  bottom: 30px;
  z-index: 3;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-top: 1px solid #dce4e9;
  padding-top: 13px;
}
.lab-name {
  color: #64748b;
  font-size: 11px;
  font-weight: 600;
  letter-spacing: 0.12em;
}
.date {
  color: #64748b;
  font-size: 12px;
}
</style>