<template>
<footer class="lab-footer">
    <div class="footer-dna"></div>
    <div class="footer-left">
        <span>Department of Electrical, Electronic and Computer Engineering</span>
        <span class="separator">·</span>
        <span>Complex Systems Computing Lab</span>
    </div>
    <!-- <div class="footer-page">
      {{ $slidev.nav.currentPage }} / {{ $slidev.nav.total }}
    </div> -->
    <div class="footer-page">
        <nav class="pagination" aria-label="Slide navigation">
            <!-- First -->
            <button v-if="currentPage > 1" type="button" class="page-btn page-nav" title="First page" @click="goToPage(1)">
                <span class="nav-icon">«</span>
                <span>First</span>
            </button>

            <!-- Previous -->
            <button v-if="currentPage > 1" type="button" class="page-btn page-nav" title="Previous page" @click="goToPage(currentPage - 1)">
                <span class="nav-icon">‹</span>
                <span>Previous</span>
            </button>

            <!-- Leading ellipsis -->
            <button v-if="showLeadingEllipsis" type="button" class="page-btn page-ellipsis" disabled aria-hidden="true">
                ...
            </button>

            <!-- Page numbers -->
            <button v-for="page in visiblePages" :key="page" type="button" class="page-btn page-number" :class="{ active: page === currentPage }" :aria-current="page === currentPage ? 'page' : undefined" :aria-label="`Go to page ${page}`" @click="goToPage(page)">
                {{ page }}
            </button>

            <!-- Trailing ellipsis -->
            <button v-if="showTrailingEllipsis" type="button" class="page-btn page-ellipsis" disabled aria-hidden="true">
                ...
            </button>

            <!-- Next -->
            <button v-if="currentPage < totalPages" type="button" class="page-btn page-nav" title="Next page" @click="goToPage(currentPage + 1)">
                <span>Next</span>
                <span class="nav-icon">›</span>
            </button>

            <!-- Last -->
            <button v-if="currentPage < totalPages" type="button" class="page-btn page-nav" title="Last page" @click="goToPage(totalPages)">
                <span>Last</span>
                <span class="nav-icon">»</span>
            </button>
        </nav>
    </div>
</footer>
</template>

<script setup>
import { computed } from 'vue'

const currentPage = computed(() => $slidev.nav.currentPage)
const totalPages = computed(() => $slidev.nav.total)

const visiblePages = computed(() => {
  const total = totalPages.value
  const current = currentPage.value

  if (total <= 7) {
    return Array.from(
      { length: total },
      (_, index) => index + 1
    )
  }

  const start = Math.max(1, current - 3)
  const end = Math.min(total, current + 3)

  return Array.from(
    { length: end - start + 1 },
    (_, index) => start + index
  )
})

const showLeadingEllipsis = computed(() => {
  return visiblePages.value[0] > 1
})

const showTrailingEllipsis = computed(() => {
  const pages = visiblePages.value
  return pages[pages.length - 1] < totalPages.value
})

function goToPage(page) {
  $slidev.nav.go(page)
}
</script>

<style scoped>
.lab-footer {
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
    height: 34px;
    right: 20px;
    padding-left: 60px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    background: #eef2f4;
    border-top: 1px solid #dce4e9;
    color: #64748b;
    font-size: 10px;
    line-height: 1;
    box-sizing: border-box;
    overflow: hidden;
}

.footer-dna {
    position: absolute;
    left: 0;
    right: 0;
    bottom: -22px;
    height: 70px;
    background-image: url('../public/images/DNA.png');
    background-repeat: no-repeat;
    background-position: left;
    background-size: auto 35px;
    opacity: 1;
    filter: grayscale(50%);
    pointer-events: none;
    z-index: 0;
    margin-left: 15px;
    margin-bottom: 5px;
}

.footer-left,
.footer-page {
    position: relative;
    z-index: 1;
}

.footer-left {
    display: flex;
    align-items: center;
    gap: 7px;
    white-space: nowrap;
}

.separator {
    color: #94a3b8;
}

.footer-page {
    font-family: 'IBM Plex Mono', monospace;
    font-size: 10px;
    font-weight: 600;
    font-variant-numeric: tabular-nums;
    white-space: nowrap;
}

.footer-page {
    position: relative;
    z-index: 1;
    display: flex;
    align-items: center;
    justify-content: flex-end;
}

.pagination {
    display: flex;
    align-items: center;
    gap: 3px;
    white-space: nowrap;
}

.page-btn {
    height: 22px;
    min-width: 22px;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    gap: 4px;
    padding: 0 7px;
    border: 1px solid #d5dde3;
    border-radius: 5px;
    background: #ffffff;
    color: #526273;
    font-family: 'Inter', 'Segoe UI', sans-serif;
    font-size: 9px;
    font-weight: 600;
    line-height: 1;
    cursor: pointer;
    box-sizing: border-box;
    transition:
        background-color 0.18s ease,
        border-color 0.18s ease,
        color 0.18s ease,
        box-shadow 0.18s ease,
        transform 0.18s ease;
}

.page-btn:hover:not(:disabled) {
    border-color: #9bb8c9;
    background: #f4f8fa;
    color: #173f5f;
    transform: translateY(-1px);
    box-shadow: 0 2px 5px rgba(23, 63, 95, 0.08);
}

.page-btn:active:not(:disabled) {
    transform: translateY(0);
    box-shadow: none;
}

.page-number {
    min-width: 22px;
    padding: 0 6px;
}

.page-number.active {
    border-color: #20639b;
    background: #20639b;
    color: #ffffff;
    box-shadow: 0 2px 5px rgba(32, 99, 155, 0.2);
}

.page-number.active:hover {
    border-color: #173f5f;
    background: #173f5f;
    color: #ffffff;
}

.page-nav {
    padding: 0 8px;
    font-weight: 600;
}

.nav-icon {
    font-size: 13px;
    line-height: 1;
    font-weight: 400;
}

.page-ellipsis {
    min-width: 20px;
    padding: 0 4px;
    border-color: transparent;
    background: transparent;
    color: #94a3b8;
    cursor: default;
    pointer-events: none;
}

.page-ellipsis:hover {
    transform: none;
    box-shadow: none;
}

.page-btn:focus-visible {
    outline: 2px solid rgba(32, 99, 155, 0.35);
    outline-offset: 1px;
}
</style>
