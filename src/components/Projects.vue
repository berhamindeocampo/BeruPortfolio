<template>
  <section class="projects-section" id="projects">

    <!-- Left arrow -->
    <button class="nav-arrow nav-arrow--prev" @click="prevSlide" aria-label="Previous">&#8249;</button>

    <!-- Project card -->
    <div class="project-card">

      <!-- Left: screenshot -->
      <div class="card-img" :style="{ backgroundImage: `url(${current.img})` }">
        <div class="card-img-overlay"></div>
      </div>

      <!-- Right: info -->
      <div class="card-info">
        <div class="card-tag">{{ current.type }} · {{ current.stack }}</div>
        <h2 class="card-title">{{ current.title }}</h2>

        <!-- Language percentages text -->
        <p class="card-langs-text">
          <span v-for="(l, i) in current.langs" :key="l.name">
            {{ l.name }} {{ l.pct }}%<span v-if="i < current.langs.length - 1"> · </span>
          </span>
        </p>

        <!-- Language bar -->
        <div class="lang-bar">
          <div
            v-for="l in current.langs"
            :key="l.name"
            class="lang-bar-seg"
            :style="{ width: l.pct + '%', background: l.color }"
          ></div>
        </div>

        <!-- Legend -->
        <div class="lang-legend">
          <span v-for="l in current.langs" :key="l.name" class="legend-item">
            <span class="legend-dot" :style="{ background: l.color }"></span>
            {{ l.name }} {{ l.pct }}%
          </span>
        </div>

        <!-- Tech icons -->
        <div class="tech-icons">
          <img
            v-for="icon in current.icons"
            :key="icon.label"
            :src="icon.src"
            :alt="icon.label"
            class="tech-icon"
            :title="icon.label"
          />
        </div>

        <!-- Description -->
        <p class="card-desc">{{ current.description }}</p>

        <!-- Actions -->
        <div class="card-actions">
          <a v-if="current.github" :href="current.github" target="_blank" rel="noopener" class="btn-source">
            <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor">
              <path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0024 12c0-6.63-5.37-12-12-12z"/>
            </svg>
            Source Code
          </a>
          <a v-if="current.vercel" :href="current.vercel" target="_blank" rel="noopener" class="btn-live">
            <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M12 1L24 22H0L12 1z"/></svg>
            Live Demo
          </a>
        </div>
      </div>
    </div>

    <!-- Right arrow -->
    <button class="nav-arrow nav-arrow--next" @click="nextSlide" aria-label="Next">&#8250;</button>

    <!-- Dots -->
    <div class="dots">
      <span
        v-for="(p, i) in projects"
        :key="i"
        class="dot"
        :class="{ active: i === activeIndex }"
        @click="goTo(i)"
      ></span>
    </div>

  </section>
</template>

<script setup>
import { ref, computed } from 'vue'

const activeIndex = ref(0)

const projects = [
  {
    title: 'Whisker Wash',
    type: 'WEB APP',
    stack: 'HTML · CSS · JavaScript · Gemini AI',
    description: 'AI-powered pet care platform with grooming booking, product catalog, blog, and a Gemini-powered chatbot assistant.',
    img: '/img/whisker-dog.png',
    langs: [
      { name: 'HTML', pct: 57.9, color: '#e34c26' },
      { name: 'CSS',        pct: 32.6, color: '#e07b53' },
      { name: 'JavaScript',       pct: 9.5, color: '#f1e05a' },
    ],
    icons: [
      { src: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/javascript/javascript-original.svg', label: 'JavaScript' },
      { src: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/css3/css3-original.svg',            label: 'CSS3' },
      { src: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/html5/html5-original.svg',          label: 'HTML5' },
    ],
    github: 'https://github.com/berhamindeocampo/WhiskerWash',
    vercel: 'https://whiskerwash.vercel.app',
  },
  {
    title: 'Earthquake Event Recorder',
    type: 'DESKTOP APP',
    stack: 'Python · Tkinter · JSON',
    description: 'Real-time earthquake monitoring and recording system built with Python & Tkinter. Supports JSON import/export.',
    img: '/img/eeeer.png',
    langs: [
      { name: 'Python', pct: 100, color: '#3572A5' },
    ],
    icons: [
      { src: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/python/python-original.svg', label: 'Python' },
    ],
    github: 'https://github.com/berhamindeocampo/Earthquake-Event-Recorder',
    vercel: null,
  },
  {
    title: 'BeruPortfolio',
    type: 'WEB APP',
    stack: 'Vue 3 · Vite · CSS3',
    description: 'Modern Vue.js developer portfolio with smooth animations, project showcases, and full responsiveness.',
    img: '/img/beru.png',
    langs: [
      { name: 'Vue',        pct: 94.2, color: '#41b883' },
      { name: 'HTML',        pct: 5.2, color: '#e34c26' },
      { name: 'JavaScript', pct: 0.6, color: '#f1e05a' },
    ],
    icons: [
      { src: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vuejs/vuejs-original.svg',          label: 'Vue 3' },
      { src: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/html5/html5-original.svg',            label: 'HTML5' },
      { src: 'https://cdn.jsdelivr.net/gh/devicons/devicon/icons/javascript/javascript-original.svg', label: 'JavaScript' },
    ],
    github: 'https://github.com/berhamindeocampo/BeruPortfolio',
    vercel: 'https://berhamindeocampo.vercel.app',
  },
]

const current = computed(() => projects[activeIndex.value])

function nextSlide() { activeIndex.value = (activeIndex.value + 1) % projects.length }
function prevSlide() { activeIndex.value = (activeIndex.value - 1 + projects.length) % projects.length }
function goTo(i)     { activeIndex.value = i }
</script>

<style scoped>
/* ── SECTION ─────────────────────────────────── */
.projects-section {
  position: relative;
  min-height: 100vh;
  background: #0a0a0a;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 80px 72px;
  box-sizing: border-box;
}

/* ── NAV ARROWS ──────────────────────────────── */
.nav-arrow {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  z-index: 20;
  background: rgba(255,204,0,.08);
  border: 1px solid rgba(255,204,0,.2);
  color: rgba(255,204,0,.8);
  font-size: 2.2rem;
  line-height: 1;
  width: 48px;
  height: 48px;
  border-radius: 50%;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: background .2s, color .2s;
}
.nav-arrow:hover {
  background: rgba(255,204,0,.2);
  color: #ffcc00;
}
.nav-arrow--prev { left: 16px; }
.nav-arrow--next { right: 16px; }

/* ── CARD ────────────────────────────────────── */
.project-card {
  display: flex;
  width: 100%;
  max-width: 1200px;
  background: #111114;
  border: 1px solid rgba(255,255,255,.07);
  border-radius: 16px;
  overflow: hidden;
  box-shadow: 0 24px 80px rgba(0,0,0,.7);
  min-height: 480px;
}

/* ── LEFT: screenshot ────────────────────────── */
.card-img {
  flex: 0 0 42%;
  background-size: cover;
  background-position: center;
  position: relative;
}
.card-img-overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(to right, transparent 60%, #111114 100%);
}

/* ── RIGHT: info ─────────────────────────────── */
.card-info {
  flex: 1;
  padding: 48px 48px 48px 40px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 14px;
}

.card-tag {
  font-size: .72rem;
  font-weight: 700;
  letter-spacing: .18em;
  color: #ffcc00;
  text-transform: uppercase;
}

.card-title {
  font-size: 2rem;
  font-weight: 800;
  color: #fff;
  line-height: 1.2;
  margin: 0;
  font-family: "H7GBK-Heavy", sans-serif;
}

.card-langs-text {
  font-size: .82rem;
  color: rgba(255,255,255,.4);
  font-style: italic;
  margin: 0;
}

/* Language bar */
.lang-bar {
  display: flex;
  height: 8px;
  border-radius: 6px;
  overflow: hidden;
  gap: 2px;
}
.lang-bar-seg { border-radius: 4px; transition: width .4s; }

/* Legend */
.lang-legend {
  display: flex;
  gap: 16px;
  flex-wrap: wrap;
}
.legend-item {
  display: flex;
  align-items: center;
  gap: 6px;
  font-size: .8rem;
  color: rgba(255,255,255,.65);
}
.legend-dot {
  width: 10px; height: 10px;
  border-radius: 50%;
  flex-shrink: 0;
}

/* Tech icons */
.tech-icons { display: flex; gap: 10px; align-items: center; }
.tech-icon {
  width: 34px; height: 34px;
  border-radius: 6px;
  background: rgba(255,255,255,.05);
  padding: 4px;
  object-fit: contain;
}

.card-desc {
  font-size: .92rem;
  line-height: 1.7;
  color: rgba(255,255,255,.5);
  margin: 0;
  max-width: 520px;
}

/* ── BUTTONS ─────────────────────────────────── */
.card-actions { display: flex; gap: 12px; flex-wrap: wrap; margin-top: 4px; }

.btn-source, .btn-live {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  font-size: .88rem;
  font-weight: 700;
  padding: 10px 22px;
  border-radius: 8px;
  text-decoration: none;
  transition: background .2s, transform .2s;
  letter-spacing: .02em;
}
.btn-source:hover, .btn-live:hover { transform: translateY(-2px); }

.btn-source {
  background: rgba(255,255,255,.09);
  border: 1px solid rgba(255,255,255,.18);
  color: #fff;
}
.btn-source:hover { background: rgba(255,255,255,.16); }

.btn-live {
  background: rgba(255,204,0,.15);
  border: 1px solid rgba(255,204,0,.4);
  color: #ffcc00;
}
.btn-live:hover { background: rgba(255,204,0,.28); }

/* ── DOTS ────────────────────────────────────── */
.dots {
  position: absolute;
  bottom: 28px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 8px;
}
.dot {
  width: 8px; height: 8px;
  border-radius: 50%;
  background: rgba(255,255,255,.2);
  cursor: pointer;
  transition: background .3s, transform .3s;
}
.dot.active {
  background: #ffcc00;
  transform: scale(1.3);
}

/* ── RESPONSIVE ──────────────────────────────── */
@media (max-width: 900px) {
  .projects-section { padding: 60px 56px; }
  .card-info { padding: 32px 28px; }
  .card-title { font-size: 1.5rem; }
}

@media (max-width: 768px) {
  .projects-section { padding: 60px 16px 72px; }

  .project-card {
    flex-direction: column;
    max-width: 100%;
    border-radius: 12px;
  }

  .card-img {
    flex: 0 0 200px;
    height: 200px;
  }
  .card-img-overlay {
    background: linear-gradient(to bottom, transparent 50%, #111114 100%);
  }

  .card-info { padding: 24px 20px 28px; gap: 12px; }
  .card-title { font-size: 1.4rem; }
  .card-desc  { font-size: .85rem; }

  .nav-arrow { width: 38px; height: 38px; font-size: 1.6rem; }
  .nav-arrow--prev { left: 6px; }
  .nav-arrow--next { right: 6px; }
}

@media (max-width: 480px) {
  .card-title { font-size: 1.2rem; }
  .btn-source, .btn-live { font-size: .8rem; padding: 8px 16px; }
}
</style>