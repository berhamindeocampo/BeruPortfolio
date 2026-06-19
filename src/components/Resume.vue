<template>
  <section id="resume" class="resume-section">

    <div class="bg-overlay"></div>
    <div class="bg-photo"></div>

    <!-- SLIDER -->
    <div class="resume-slider" ref="slider">

      <!-- SLIDE 1: Summary + Download -->
      <div class="resume-item slide-summary">
        <div class="mini-content">🧑‍💻<br>Profile</div>
        <div class="resume-content">
          <div class="resume-tag">// MY RESUME</div>
          <h1 class="resume-name">BERHAMIN<br>DE OCAMPO</h1>
          <p class="resume-des">
            Passionate Computer Science student currently refining my skills through intensive hands-on training. Dedicated to developing efficient, user-centered web applications and eager to contribute my technical foundation to real-world development projects.
          </p>
          <div class="resume-meta">
            <div class="meta-item">
              <span class="meta-icon">🎓</span>
              <div>
                <div class="meta-label">Degree</div>
                <div class="meta-val">BS Computer Science</div>
              </div>
            </div>
            <div class="meta-item">
              <span class="meta-icon">📍</span>
              <div>
                <div class="meta-label">Location</div>
                <div class="meta-val">San Miguel, Bulacan, PH</div>
              </div>
            </div>
            <div class="meta-item">
              <span class="meta-icon">✉</span>
              <div>
                <div class="meta-label">Email</div>
                <div class="meta-val">badeocampo28@gmail.com</div>
              </div>
            </div>
          </div>
          <a href="/Berhamin_de_Ocampo_Resume.pdf" download="Berhamin_de_Ocampo_Resume.pdf" class="download-btn">
            Download Resume ↓
          </a>
        </div>
      </div>

      <!-- SLIDE 2: Education -->
      <div class="resume-item slide-education">
        <div class="mini-content">🎓<br>Education</div>
        <div class="resume-content">
          <div class="resume-tag">// EDUCATION</div>
          <h2 class="resume-name">ACADEMIC<br>BACKGROUND</h2>
          <p class="resume-des">My formal training in Computer Science and technology.</p>
          <div class="timeline">
            <div class="timeline-item" v-for="edu in education" :key="edu.school">
              <div class="timeline-dot" :style="{ background: edu.accent }"></div>
              <div class="timeline-body">
                <div class="tl-year">{{ edu.year }}</div>
                <div class="tl-title">{{ edu.degree }}</div>
                <div class="tl-sub">{{ edu.school }}</div>
                <div class="tl-desc">{{ edu.desc }}</div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- SLIDE 3: Experience -->
      <div class="resume-item slide-experience">
        <div class="mini-content">💼<br>Experience</div>
        <div class="resume-content">
          <div class="resume-tag">// EXPERIENCE</div>
          <h2 class="resume-name">WORK &amp;<br>PROJECTS</h2>
          <p class="resume-des">Hands-on experience building real-world applications.</p>
          <div class="timeline">
            <div class="timeline-item" v-for="exp in experience" :key="exp.role">
              <div class="timeline-dot" :style="{ background: exp.accent }"></div>
              <div class="timeline-body">
                <div class="tl-year">{{ exp.year }}</div>
                <div class="tl-title">{{ exp.role }}</div>
                <div class="tl-sub">{{ exp.company }}</div>
                <div class="tl-desc">{{ exp.desc }}</div>
              </div>
            </div>
          </div>
        </div>
      </div>

    </div>

    <!-- BUTTONS -->
    <div class="buttons">
      <button class="prev" @click="prev" aria-label="Previous"></button>
      <button class="next" @click="next" aria-label="Next"></button>
    </div>

    <!-- SLIDE INDICATOR -->
    <div class="slide-dots">
      <span
        v-for="(label, i) in slideLabels"
        :key="i"
        class="sdot"
        :class="{ active: activeIndex === i }"
        @click="goTo(i)"
      >{{ label }}</span>
    </div>

    <!-- SCROLL HINT -->
    <div class="scroll-hint">
      <span>resume</span>
      <div class="hint-line"></div>
    </div>

  </section>
</template>

<script>
export default {
  name: 'Resume',
  data() {
    return {
      activeIndex: 0,
      slideLabels: ['Education', 'Experience', 'Profile & Resume'],
      education: [
        {
          year: '2023 – Present',
          degree: 'BS Computer Science',
          school: 'St. Paul University at San Miguel',
          desc: 'Focusing on software engineering, web development, data structures, and algorithms.',
          accent: '#3B6FD4'
        },
        {
          year: '2021 – 2023',
          degree: 'Senior High School – GAS',
          school: 'John J. Russell Senior High School',
          desc: 'Enrolled in General Academic Strand curriculum, because I am undecided to which program I would choose.',
          accent: '#F5C842'
        },
        {
          year: '2017 – 2021',
          degree: 'Junior High School',
          school: 'John J. Russell Memorial High School',
          desc: 'Not yet interested in technology but I have an interest in arts and animation.',
          accent: '#E8594A'
        }
      ],
      experience: [
        {
          year: '2026',
          role: 'WhiskerWash — Vanilla HTML, CSS & JavaScript',
          company: 'Personal Project',
          desc: 'Built a multi-page pet care web app with AI chatbot (Gemini API), booking system, product catalog, and blog.',
          accent: '#4CAF50'
        },
        {
          year: '2025',
          role: 'Earthquake Event Recorder — Python & Tkinter',
          company: 'Academic Project',
          desc: 'Developed a Python/Tkinter desktop app for logging earthquake events with magnitude-based safety alerts and JSON I/O.',
          accent: '#3B6FD4'
        },
        {
          year: '2026',
          role: 'BeruPortfolio — Vue Developer',
          company: 'Personal Project',
          desc: 'Designed and built this portfolio using Vue 3, Vite.',
          accent: '#F5C842'
        }
      ]
    }
  },
  methods: {
    shift(direction) {
      const slider = this.$refs.slider
      const items = Array.from(slider.querySelectorAll('.resume-item'))
      const firstRects = items.map(el => el.getBoundingClientRect())

      if (direction === 'next') {
        slider.appendChild(items[0])
      } else {
        slider.prepend(items[items.length - 1])
      }

      requestAnimationFrame(() => {
        const lastRects = items.map(el => el.getBoundingClientRect())
        items.forEach((el, i) => {
          const wasHidden = firstRects[i].width === 0 && firstRects[i].height === 0
          const isHidden  = lastRects[i].width  === 0 && lastRects[i].height  === 0
          if (wasHidden || isHidden) return
          const dx = firstRects[i].left - lastRects[i].left
          const dy = firstRects[i].top  - lastRects[i].top
          if (dx || dy) {
            const naturalTransform = getComputedStyle(el).transform
            const base = naturalTransform === 'none' ? '' : naturalTransform
            el.style.transition = 'none'
            el.style.transform  = `${base} translate(${dx}px, ${dy}px)`
          }
        })
        requestAnimationFrame(() => {
          items.forEach(el => {
            el.style.transition = ''
            el.style.transform  = ''
          })
        })
      })

      this.activeIndex = direction === 'next'
        ? (this.activeIndex + 1) % this.slideLabels.length
        : (this.activeIndex - 1 + this.slideLabels.length) % this.slideLabels.length
    },
    next()  { this.shift('next') },
    prev()  { this.shift('prev') },
    goTo(index) {
      const diff = index - this.activeIndex
      if (diff === 0) return
      const fn = diff > 0 ? this.next : this.prev
      for (let i = 0; i < Math.abs(diff); i++) fn()
    }
  }
}
</script>

<style scoped>
@font-face {
  font-family: "H7GBK-Heavy";
  src: url('https://hw-media-cdn-mingchao.kurogame.com/font/H7GBK-Heavy.ttf');
}

/* ══ SECTION ════════════════════════════════════ */
.resume-section {
  position: relative;
  width: 100%;
  height: 100vh;
  min-height: 600px;
  max-height: 900px;        /* ← caps height so it never overflows viewport */
  background: #0b0b0e;
  overflow: hidden;
}

/* ── Background photo ──────────────────────────── */
.bg-photo {
  position: absolute;
  inset: 0;
  background-image: url('/img/beruchisa.jpg');
  background-size: cover;
  background-position: center 15%;
  background-repeat: no-repeat;
  opacity: 0.55;
  filter: saturate(85%);
  z-index: 0;
  pointer-events: none;
}

.bg-photo::after {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(90deg,
    #0b0b0e 0%,
    rgba(11,11,14,.94) 22%,
    rgba(11,11,14,.55) 45%,
    rgba(11,11,14,.15) 65%,
    rgba(11,11,14,.35) 100%
  );
}

.bg-overlay {
  position: absolute;
  inset: 0;
  background:
    radial-gradient(ellipse at 15% 50%, rgba(59,111,212,.12) 0%, transparent 55%),
    radial-gradient(ellipse at 85% 30%, rgba(245,200,66,.07)  0%, transparent 55%);
  pointer-events: none;
  z-index: 1;
}

/* ══ SLIDER ═════════════════════════════════════ */
.resume-slider {
  position: absolute;
  inset: 0;
}

/* ── All side/hidden cards ─────────────────────── */
.resume-item {
  width: 160px;
  height: 240px;
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  border-radius: 18px;
  display: inline-block;
  transition: .5s cubic-bezier(.4,0,.2,1);
  border: 1px solid rgba(255,255,255,.07);
  overflow: hidden;
}

.resume-item::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(135deg, rgba(255,255,255,.03) 0%, transparent 60%);
}

/* ── Active slide (1st & 2nd child = full-screen) ─ */
.resume-item:nth-child(1),
.resume-item:nth-child(2) {
  top: 0; left: 0;
  transform: none;
  border-radius: 0;
  width: 100%; height: 100%;
  border: none;
}

/* ── Side preview cards — pushed right of content ─
   Content ends at ~560px from left (60px pad + 500px wide).
   Cards start at 62% so they never overlap content.       */
.resume-item:nth-child(3) { left: 62%; }
.resume-item:nth-child(4) { left: calc(62% + 196px); }
.resume-item:nth-child(5) { left: calc(62% + 392px); }
.resume-item:nth-child(n+6) { left: calc(62% + 588px); opacity: 0; }

/* ── Slide backgrounds ─────────────────────────── */
.slide-summary {
  background: #0d1220;
  background-image: url('/img/beruchisa.jpg');
  background-size: cover;
  background-position: center 20%;
  background-repeat: no-repeat;
}

.resume-item:nth-child(2).slide-summary {
  background-image:
    linear-gradient(90deg,
      #0b0b0e 0%,
      #0b0b0e 28%,
      rgba(11,11,14,.85) 42%,
      rgba(11,11,14,.4)  58%,
      rgba(11,11,14,.1)  70%,
      transparent 100%
    ),
    url('/img/beruchisa.jpg');
  background-size: cover, cover;
  background-position: center, right center;
  background-repeat: no-repeat, no-repeat;
}

.slide-education  { background: linear-gradient(135deg, #0d1a0d 0%, #080e08 100%); }
.slide-experience { background: linear-gradient(135deg, #1a100d 0%, #100808 100%); }

/* ══ MAIN CONTENT ════════════════════════════════ */
.resume-content {
  display: none;
  position: absolute;
  top: 50%;
  left: 60px;
  transform: translateY(-50%);
  width: 480px;
  max-width: calc(58% - 60px);   /* never wider than left portion */
  color: #fff;
}

.resume-item:nth-child(2) .resume-content { display: block; }

/* ── Mini card label (side cards only) ────────── */
.mini-content {
  display: flex;
  position: absolute;
  inset: 0;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  color: rgba(255,255,255,.3);
  font-size: 1.2rem;
  font-weight: 700;
  gap: 6px;
  line-height: 1.4;
  text-align: center;
  opacity: 0;
  transform: translateY(18px);
  pointer-events: none;
  transition: opacity .45s ease .15s, transform .45s cubic-bezier(.4,0,.2,1) .15s;
  background: linear-gradient(to top, rgba(0,0,0,.55) 0%, rgba(0,0,0,.1) 45%, rgba(0,0,0,.45) 100%);
}
.resume-item:nth-child(n+3) .mini-content {
  opacity: 1;
  transform: translateY(0);
}

/* ── Typography ────────────────────────────────── */
.resume-tag {
  font-family: 'Lato', monospace;
  font-size: .72rem;
  letter-spacing: .22em;
  color: rgba(245,200,66,.7);
  margin-bottom: 8px;
  opacity: 0;
  animation: wuwa-in .8s ease forwards .1s;
}

.resume-name {
  font-family: "H7GBK-Heavy", 'Lato', sans-serif;
  font-size: clamp(2rem, 3.8vw, 3.6rem);
  line-height: 1;
  margin-bottom: 14px;
  text-shadow: 0 0 40px rgba(255,255,255,.12);
  opacity: 0;
  animation: wuwa-in .9s ease forwards;
}

.resume-des {
  font-size: .86rem;
  line-height: 1.7;
  color: rgba(255,255,255,.55);
  max-width: 420px;
  margin-bottom: 20px;
  opacity: 0;
  animation: wuwa-in .9s ease forwards .2s;
}

/* ── Meta row ──────────────────────────────────── */
.resume-meta {
  display: flex;
  flex-direction: column;
  gap: 9px;
  margin-bottom: 24px;
  opacity: 0;
  animation: wuwa-in .9s ease forwards .3s;
}

.meta-item {
  display: flex;
  align-items: center;
  gap: 12px;
}

.meta-icon {
  width: 32px; height: 32px;
  border-radius: 8px;
  background: rgba(255,255,255,.08);
  display: flex; align-items: center; justify-content: center;
  font-size: .9rem; flex-shrink: 0;
}

.meta-label {
  font-size: .66rem;
  text-transform: uppercase;
  letter-spacing: .12em;
  color: rgba(255,255,255,.35);
  margin-bottom: 1px;
}

.meta-val {
  font-size: .83rem;
  font-weight: 700;
  color: rgba(255,255,255,.8);
}

/* ── Download button ───────────────────────────── */
.download-btn {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  background: rgba(245,200,66,.15);
  border: 1px solid rgba(245,200,66,.4);
  color: #f5c842;
  font-family: 'Lato', sans-serif;
  font-weight: 700;
  font-size: .88rem;
  padding: 11px 24px;
  border-radius: 40px;
  cursor: pointer;
  backdrop-filter: blur(8px);
  transition: background .2s;
  text-decoration: none;
  opacity: 0;
  animation: wuwa-in .9s ease forwards .45s;
}
.download-btn:hover { background: rgba(245,200,66,.28); }

/* ── Timeline ──────────────────────────────────── */
.timeline {
  display: flex;
  flex-direction: column;
  gap: 18px;
  opacity: 0;
  animation: wuwa-in .9s ease forwards .3s;
  max-height: 50vh;
  overflow-y: auto;
  padding-right: 8px;
  scrollbar-width: thin;
  scrollbar-color: rgba(255,255,255,.1) transparent;
}

.timeline-item {
  display: flex;
  gap: 14px;
  align-items: flex-start;
}

.timeline-dot {
  width: 10px; height: 10px;
  border-radius: 50%;
  margin-top: 5px;
  flex-shrink: 0;
  box-shadow: 0 0 8px currentColor;
}

.timeline-body { flex: 1; }

.tl-year {
  font-size: .68rem;
  letter-spacing: .14em;
  color: rgba(255,255,255,.35);
  text-transform: uppercase;
  margin-bottom: 2px;
}

.tl-title {
  font-family: "H7GBK-Heavy", 'Lato', sans-serif;
  font-size: .95rem;
  color: #fff;
  margin-bottom: 2px;
}

.tl-sub {
  font-size: .76rem;
  color: rgba(245,200,66,.6);
  margin-bottom: 4px;
  letter-spacing: .04em;
}

.tl-desc {
  font-size: .8rem;
  color: rgba(255,255,255,.5);
  line-height: 1.6;
}

/* ══ NAV BUTTONS ════════════════════════════════ */
.buttons {
  position: absolute;
  bottom: 72px;
  width: 100%;
  text-align: center;
  z-index: 10;
}

.prev, .next {
  width: 50px; height: 40px;
  border-radius: 8px; border: none;
  background-color: transparent;
  background-repeat: no-repeat;
  background-size: contain;
  margin-inline: 20px;
  cursor: pointer;
  transition: .3s;
  -webkit-tap-highlight-color: transparent;
}
.prev { background-image: url('https://codetheworld.io/wp-content/uploads/2024/05/prev.png'); }
.next { background-image: url('https://codetheworld.io/wp-content/uploads/2024/05/next.png'); }
.prev:hover, .next:hover { transform: scale(1.15); }

/* ══ SLIDE DOTS ═════════════════════════════════ */
.slide-dots {
  position: absolute;
  bottom: 28px;
  width: 100%;
  display: flex;
  justify-content: center;
  gap: 10px;
  z-index: 10;
}

.sdot {
  font-size: .66rem;
  font-weight: 700;
  letter-spacing: .1em;
  padding: 4px 13px;
  border-radius: 20px;
  background: rgba(255,255,255,.08);
  color: rgba(255,255,255,.35);
  border: 1px solid rgba(255,255,255,.1);
  cursor: pointer;
  transition: all .3s;
}
.sdot.active {
  background: rgba(245,200,66,.2);
  border-color: rgba(245,200,66,.4);
  color: #f5c842;
}

/* ══ SCROLL HINT ════════════════════════════════ */
.scroll-hint {
  position: absolute;
  right: 40px;
  bottom: 56px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
  color: rgba(255,255,255,.25);
  font-size: .66rem;
  letter-spacing: .18em;
  text-transform: uppercase;
  z-index: 10;
}

.hint-line {
  width: 1px; height: 44px;
  background: linear-gradient(to bottom, rgba(255,255,255,.3), transparent);
  animation: pulse 2s ease-in-out infinite;
}

/* ══ ANIMATIONS ═════════════════════════════════ */
@keyframes pulse {
  0%, 100% { opacity: .3; }
  50%       { opacity: 1; }
}

@keyframes wuwa-in {
  from { opacity: 0; transform: translateY(50px); filter: blur(16px); }
  to   { opacity: 1; transform: translateY(0);    filter: blur(0); }
}

/* ══ RESPONSIVE — TABLET ════════════════════════ */
@media (max-width: 1024px) {
  .resume-content {
    left: 40px;
    width: 420px;
    max-width: calc(56% - 40px);
  }
  .resume-item:nth-child(3) { left: 60%; }
  .resume-item:nth-child(4) { left: calc(60% + 196px); }
  .resume-item:nth-child(5) { left: calc(60% + 392px); }
}

/* ══ RESPONSIVE — MOBILE ════════════════════════ */
@media (max-width: 768px) {

  /* Section: auto height, scrolls naturally */
  .resume-section {
    height: auto;
    min-height: 100svh;
    max-height: none;
    overflow: hidden;
    padding: 72px 0 120px;  /* top=navbar clearance, bottom=buttons+dots */
  }

  /* Background: hide global bg-photo, each slide handles its own */
  .bg-photo   { display: none; }
  .bg-overlay { display: none; }

  /* Slider: flow in document */
  .resume-slider {
    position: relative;
    inset: auto;
    transform: translateZ(0);   /* own compositor layer */
  }

  /* Hide inactive slides */
  .resume-item:nth-child(1),
  .resume-item:nth-child(n+3) { display: none; }

  /* Active slide: full width, height = content */
  .resume-item:nth-child(2) {
    position: relative;
    width: 100%;
    height: auto;
    min-height: calc(100svh - 192px);
    border-radius: 0;
    will-change: transform, opacity;
    backface-visibility: hidden;
  }

  /* Summary slide: local bg image + gradient */
  .resume-item:nth-child(2).slide-summary {
    background-image:
      linear-gradient(to bottom,
        rgba(11,11,14,.6)  0%,
        rgba(11,11,14,.2) 18%,
        rgba(11,11,14,.5) 38%,
        #0b0b0e 60%,
        #0b0b0e 100%
      ),
      url('/img/beruchisa.jpg');
    background-size: cover, cover;
    background-position: center, center top;
    background-repeat: no-repeat, no-repeat;
    background-attachment: scroll, scroll;
  }

  /* Content block */
  .resume-content {
    position: relative;
    top: auto; left: auto;
    transform: none;
    width: 100%;
    max-width: 100%;
    padding: 20px 22px 0;
    margin: 0;
  }

  /* Typography scale-down */
  .resume-name { font-size: 1.85rem; }
  .resume-des  { font-size: .82rem; max-width: 100%; }

  /* Timeline */
  .timeline {
    max-height: none;
    overflow-y: visible;
    padding-right: 0;
    gap: 16px;
  }

  /* Animations: lighter on mobile */
  @keyframes wuwa-in {
    from { opacity: 0; transform: translateY(24px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  .resume-tag   { animation-duration: .35s; animation-delay: 0s; }
  .resume-name  { animation-duration: .4s;  animation-delay: .05s; }
  .resume-des   { animation-duration: .4s;  animation-delay: .1s; }
  .resume-meta  { animation-duration: .4s;  animation-delay: .14s; }
  .timeline     { animation-duration: .4s;  animation-delay: .14s; }
  .download-btn { animation-duration: .4s;  animation-delay: .2s; }

  /* Download btn */
  .download-btn {
    backdrop-filter: none;
    -webkit-backdrop-filter: none;
    background: rgba(245,200,66,.2);
    margin-top: 4px;
  }

  /* Nav buttons: corners of the section */
  .buttons {
    position: absolute;
    bottom: 72px;
    left: 0;
    right: 0;
    width: 100%;
    text-align: left;       /* override center */
    padding: 0;
    pointer-events: none;
  }
  .buttons .prev,
  .buttons .next {
    pointer-events: all;
    position: absolute;
    bottom: 0;
    margin-inline: 0;
  }
  .buttons .prev { left: 16px; }
  .buttons .next { right: 16px; }

  /* Slide dots */
  .slide-dots {
    position: absolute;
    bottom: 20px;
    flex-wrap: wrap;
    justify-content: center;
    padding: 0 12px;
  }
  .sdot { font-size: .6rem; padding: 3px 10px; }

  .scroll-hint { display: none; }
  .hint-line   { animation: none; opacity: .3; }
  .mini-content { transition: opacity .2s ease, transform .2s ease; }
}

/* ══ RESPONSIVE — SMALL MOBILE ══════════════════ */
@media (max-width: 480px) {
  .resume-section { padding: 68px 0 116px; }

  .resume-content { padding: 16px 18px 0; }

  .resume-name { font-size: 1.6rem; }
  .resume-des  { font-size: .8rem; }

  .meta-icon  { width: 28px; height: 28px; font-size: .8rem; }
  .meta-val   { font-size: .78rem; }
  .meta-label { font-size: .62rem; }

  .download-btn { width: 100%; justify-content: center; font-size: .82rem; }

  .tl-title { font-size: .88rem; }
  .tl-desc  { font-size: .76rem; }

  .sdot { font-size: .58rem; padding: 3px 8px; }

  @keyframes wuwa-in {
    from { opacity: 0; transform: translateY(14px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  .resume-tag,
  .resume-name,
  .resume-des,
  .resume-meta,
  .timeline,
  .download-btn { animation-duration: .3s; animation-delay: 0s; }
}

/* ══ REDUCED MOTION ═════════════════════════════ */
@media (prefers-reduced-motion: reduce) {
  @keyframes wuwa-in {
    from { opacity: 0; }
    to   { opacity: 1; }
  }
  .hint-line    { animation: none; }
  .mini-content { transition: none; }
  .resume-item  { transition: none; }
}
</style>