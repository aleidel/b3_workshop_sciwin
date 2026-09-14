<!-- .slidev/layouts/fairagro.vue (or components/fairagro.vue) -->
<template>
  <div class="fairagro-layout">
    <!-- Header: Title + Logo on same line -->
    <div class="fa-header">
      <div class="fa-title-wrapper">
        <h1 v-if="frontmatter && frontmatter.title">{{ frontmatter.title }}</h1>
      </div>
      <img
        class="fa-logo"
        src="/fairagro-logo.png"
        alt="FAIRagro"
        @error="handleImageError"
      />
    </div>

    <!-- Main Content -->
    <div class="fa-content">
      <slot />
    </div>

    <!-- Bottom coloured bar -->
    <div class="fa-footer-bar" />

    <!-- Slide number -->
    <div class="fa-page-number">{{ currentPage }} / {{ total }}</div>
  </div>
</template>

<script>
import { useNav } from "@slidev/client";

export default {
  name: "FairagroLayout",
  props: {
    frontmatter: {
      type: Object,
      default: () => ({}),
    },
  },
  setup() {
    const { currentPage, total } = useNav();
    return { currentPage, total };
  },
  methods: {
    handleImageError(event) {
      event.target.src = "/fallback-logo.png";
    },
  },
};
</script>

<style scoped>
.fairagro-layout {
  position: relative;
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 100%;
  /* explicit top / right / bottom / left so left and right stay identical */
  padding-top: 3rem;
  padding-right: 3rem;
  padding-bottom: 3rem;
  padding-left: 3rem;
  box-sizing: border-box;
  background: #ffffff;
  font-family: "Fira Sans", sans-serif;
}

.fairagro-layout *,
.fairagro-layout *::before,
.fairagro-layout *::after {
  box-sizing: border-box;
}

/* -------------------------------------------------
   Header: Title + Logo on the same line, vertically
   centered against each other
   ------------------------------------------------- */
.fa-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  min-height: 30px;   /* keeps header height stable even when title is empty */
  margin-bottom: 2rem;
  gap: 1.5rem;
}

/* Title wrapper */
.fa-title-wrapper {
  flex: 1;
  min-width: 0;
}
.fa-title-wrapper h1 {
  margin: 0;
  line-height: 1.15;
  color: var(--fa-green);
  font-size: 2rem;
  font-weight: 700;
}

/* -------------------------------------------------
   Logo – simple fixed size, vertically centered
   against the title by .fa-header's align-items
   ------------------------------------------------- */
.fa-logo {
  width: 140px;
  height: auto;
  object-fit: contain;
  flex-shrink: 0;
}

/* -------------------------------------------------
   Main content – gets the full slide width/height,
   not squeezed next to the logo
   ------------------------------------------------- */
.fa-content {
  flex: 1;
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: flex-start; /* was 'center' — avoids weird vertical centering */
  align-items: stretch;
  min-width: 0;
  gap: 0.5rem;
}

.fa-content :deep(h2) {
  margin: 1.25rem 0 0.5rem;
  font-size: 1.4rem;
  font-weight: 700;
  color: var(--fa-green);
}

.fa-content :deep(h3) {
  margin: 1rem 0 0.5rem;
  font-size: 1.15rem;
  font-weight: 600;
}

.fa-content :deep(p) {
  margin: 0.4rem 0;
  line-height: 1.5;
}

.fa-content :deep(ul) {
  list-style: disc;
  padding-left: 1.4rem;
  margin: 0.4rem 0 0.8rem;
}

.fa-content :deep(ol) {
  list-style: decimal;
  padding-left: 1.4rem;
  margin: 0.4rem 0 0.8rem;
}

.fa-content :deep(li) {
  margin: 0.35rem 0;
  line-height: 1.5;
}

.fa-content :deep(li > ul),
.fa-content :deep(li > ol) {
  margin-top: 0.25rem;
}

.fa-content :deep(strong) {
  font-weight: 700;
  color: #1a1a1a;
}

.fa-content :deep(code) {
  background: #f0f0f0;
  padding: 0.1rem 0.35rem;
  border-radius: 4px;
  font-size: 0.9em;
}

/* -------------------------------------------------
   Footer bar – sticks to the very bottom of the slide
   ------------------------------------------------- */
.fa-footer-bar {
  position: absolute;
  left: 0;
  right: 0;
  bottom: 0;
  height: 10px;
  background: linear-gradient(
    90deg,
    #A8C83C 0%,
    #0f9884 100%
  );
}

/* -------------------------------------------------
   Slide number – bottom-right, clear of the footer bar
   ------------------------------------------------- */
.fa-page-number {
  position: absolute;
  right: 22px;
  bottom: 16px;
  font-size: 0.72rem;
  font-weight: 600;
  color: var(--fa-grey, #a7a6a6);
}
</style>