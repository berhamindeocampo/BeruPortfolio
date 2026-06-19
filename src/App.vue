<template>
  <div>

    <!-- HEADER -->
    <header class="header" :class="{ scrolled: hasScrolled }">
      <div class="logo-text">Berhamin<span class="dot">.</span></div>
      <nav class="desktop-nav">
        <a @click="goTo('about')">About</a>
        <a @click="goTo('skills')">Skills</a>
        <a @click="goTo('projects')">Projects</a>
        <a @click="goTo('resume')">Resume</a>
        <a @click="goTo('contact')">Contact</a>
      </nav>
      <button class="hamburger-btn" @click="navOpen = !navOpen" aria-label="Open menu">
        <span :class="{ open: navOpen }"></span>
        <span :class="{ open: navOpen }"></span>
        <span :class="{ open: navOpen }"></span>
      </button>
    </header>

    <!-- NAV OVERLAY -->
    <div class="nav-overlay" :class="{ open: navOpen }" @click.self="navOpen = false">
      <nav class="overlay-nav">
        <ul>
          <li><a @click="goTo('about')">Home</a></li>
          <li><a @click="goTo('about')">About</a></li>
          <li><a @click="goTo('skills')">Skills</a></li>
          <li><a @click="goTo('projects')">Projects</a></li>
          <li><a @click="goTo('resume')">Resume</a></li>
          <li><a @click="goTo('contact')">Contact</a></li>
        </ul>
      </nav>
    </div>

    <!-- SECTIONS -->
    
    <About    ref="about"    />
    <Skills   ref="skills"   />
    <Projects ref="projects" />
    <Resume   ref="resume"   />
    <Contact  ref="contact"  />

    <!-- FOOTER -->
    <footer class="footer">
      <div class="footer-top">
        <div class="footer-left">
          <div class="footer-logo">Berhamin<span class="dot">.</span></div>
          <p class="footer-tagline">Front-End Developer<br>San Miguel, Bulacan, Philippines</p>
        </div>
        <div class="footer-right">
          <div class="footer-nav-group">
            <div class="footer-nav-title">Navigation</div>
            <a @click="goTo('about')">Home</a>
            <a @click="goTo('about')">About</a>
            <a @click="goTo('skills')">Skills</a>
            <a @click="goTo('projects')">Projects</a>
            <a @click="goTo('resume')">Resume</a>
            <a @click="goTo('contact')">Contact</a>
          </div>
          <div class="footer-nav-group">
            <div class="footer-nav-title">Connect</div>
            <a href="https://github.com/berhamindeocampo" target="_blank" rel="noopener">GitHub</a>
            <a href="https://www.linkedin.com/in/berhamin-de-ocampo-b507a3404/" target="_blank" rel="noopener">LinkedIn</a>
            <a href="https://facebook.com/beruhamin" target="_blank" rel="noopener">Facebook</a>
            <a href="mailto:badeocampo28@gmail.com">Email</a>
          </div>
          <div class="footer-cta">
            <p>Open to new opportunities</p>
            <a href="mailto:badeocampo28@gmail.com" class="footer-btn">Get in Touch ↗</a>
          </div>
        </div>
      </div>
      <div class="footer-bottom">
        <p>© {{ currentYear }} Berhamin de Ocampo. All Rights Reserved.</p>
      </div>
    </footer>

  </div>
</template>

<script>

import About  from './components/About.vue'
import Skills from './components/Skills.vue'
import Projects from './components/Projects.vue'
import Resume   from './components/Resume.vue'
import Contact  from './components/Contact.vue'

export default {
  name: 'App',
  components: { About, Skills, Projects, Resume, Contact },
  data() {
    return {
      navOpen: false,
      hasScrolled: false,
      currentYear: new Date().getFullYear()
    }
  },
  methods: {
    goTo(refName) {
      this.navOpen = false
      this.$nextTick(() => {
        const el = this.$refs[refName]?.$el
        if (el) el.scrollIntoView({ behavior: 'smooth' })
      })
    },
    onScroll() {
      this.hasScrolled = window.scrollY > 60
    }
  },
  mounted() {
    window.addEventListener('scroll', this.onScroll)
  },
  beforeUnmount() {
    window.removeEventListener('scroll', this.onScroll)
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Lato:wght@300;400;700;900&display=swap');

@font-face {
  font-family: "H7GBK-Heavy";
  src: url('https://hw-media-cdn-mingchao.kurogame.com/font/H7GBK-Heavy.ttf');
}

*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
html { scroll-behavior: smooth; }
body {
  font-family: 'Lato', sans-serif;
  background: #0a0a0a;
  color: #fff;
}
a { text-decoration: none; color: inherit; cursor: pointer; }
button { cursor: pointer; border: none; background: none; font-family: inherit; }

/* ── HEADER ──────────────────────────────────────── */
.header {
  position: fixed;
  top: 0; left: 0; right: 0;
  z-index: 200;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 22px 48px;
  background: transparent;
  transition: background .4s, padding .4s, backdrop-filter .4s;
}

.header.scrolled {
  background: rgba(10, 10, 10, 0.85);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  padding: 14px 48px;
  border-bottom: 1px solid rgba(255,255,255,.06);
}

.logo-text {
  font-family: "H7GBK-Heavy", sans-serif;
  font-size: 1.4rem;
  color: #fff;
  letter-spacing: .04em;
  text-transform: uppercase;
}

.logo-text .dot { color: #ffcc00; }

/* Desktop nav */
.desktop-nav {
  display: flex;
  gap: 36px;
}

.desktop-nav a {
  font-size: .85rem;
  font-weight: 700;
  letter-spacing: .1em;
  text-transform: uppercase;
  color: rgba(255,255,255,.65);
  transition: color .2s;
}

.desktop-nav a:hover { color: #ffcc00; }

/* Hamburger */
.hamburger-btn {
  display: none;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 5px;
  width: 40px; height: 40px;
  border-radius: 8px;
  background: rgba(255,255,255,.08);
  border: 1px solid rgba(255,255,255,.12);
}

.hamburger-btn span {
  display: block;
  width: 18px; height: 2px;
  background: #fff;
  border-radius: 2px;
  transition: transform .3s, opacity .3s;
}

.hamburger-btn span.open:nth-child(1) { transform: translateY(7px) rotate(45deg); }
.hamburger-btn span.open:nth-child(2) { opacity: 0; }
.hamburger-btn span.open:nth-child(3) { transform: translateY(-7px) rotate(-45deg); }

/* ── NAV OVERLAY ─────────────────────────────────── */
.nav-overlay {
  position: fixed; inset: 0; z-index: 199;
  background: rgba(5,5,5,.96);
  backdrop-filter: blur(20px);
  opacity: 0; pointer-events: none;
  display: flex; align-items: center; justify-content: center;
  transition: opacity .3s;
}

.nav-overlay.open { opacity: 1; pointer-events: all; }

.overlay-nav ul { list-style: none; text-align: center; }
.overlay-nav li { margin: 16px 0; }
.overlay-nav a {
  font-family: "H7GBK-Heavy", sans-serif;
  font-size: 2.6rem;
  color: rgba(255,255,255,.8);
  letter-spacing: .06em;
  text-transform: uppercase;
  transition: color .2s;
}
.overlay-nav a:hover { color: #ffcc00; }

/* ── FOOTER ──────────────────────────────────────── */
.footer {
  background: #050505;
  color: #fff;
  padding: 72px 48px 32px;
  border-top: 1px solid rgba(255,255,255,.06);
}

.footer-top {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 48px;
  padding-bottom: 56px;
  border-bottom: 1px solid rgba(255,255,255,.08);
  margin-bottom: 32px;
}

.footer-left { max-width: 320px; }

.footer-logo {
  font-family: "H7GBK-Heavy", sans-serif;
  font-size: 2.2rem;
  letter-spacing: .04em;
  text-transform: uppercase;
  margin-bottom: 16px;
}

.footer-logo .dot { color: #ffcc00; }

.footer-tagline {
  font-size: .88rem;
  line-height: 1.7;
  color: rgba(255,255,255,.4);
}

.footer-right {
  display: flex;
  gap: 64px;
  align-items: flex-start;
}

.footer-nav-group {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.footer-nav-title {
  font-size: .7rem;
  font-weight: 700;
  letter-spacing: .18em;
  text-transform: uppercase;
  color: rgba(255,255,255,.3);
  margin-bottom: 4px;
}

.footer-nav-group a {
  font-size: .88rem;
  color: rgba(255,255,255,.55);
  transition: color .2s;
}

.footer-nav-group a:hover { color: #ffcc00; }

.footer-cta {
  display: flex;
  flex-direction: column;
  gap: 16px;
  align-items: flex-start;
}

.footer-cta p {
  font-size: .82rem;
  color: rgba(255,255,255,.35);
  text-transform: uppercase;
  letter-spacing: .1em;
}

.footer-btn {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  background: #ffcc00;
  color: #0a0a0a;
  font-weight: 700;
  font-size: .9rem;
  padding: 12px 26px;
  border-radius: 40px;
  transition: background .2s, transform .2s;
  white-space: nowrap;
}

.footer-btn:hover {
  background: #fff;
  transform: translateY(-2px);
}

.footer-bottom {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: .8rem;
  color: rgba(255,255,255,.25);
}

.footer-socials {
  display: flex;
  gap: 24px;
}

.footer-socials a {
  color: rgba(255,255,255,.25);
  font-size: .8rem;
  transition: color .2s;
}

.footer-socials a:hover { color: #ffcc00; }

/* ── RESPONSIVE ──────────────────────────────────── */
@media (max-width: 900px) {
  .header { padding: 18px 24px; }
  .header.scrolled { padding: 12px 24px; }
  .desktop-nav { display: none; }
  .hamburger-btn { display: flex; }

  .footer { padding: 56px 24px 28px; }
  .footer-top { flex-direction: column; gap: 40px; }
  .footer-right { flex-wrap: wrap; gap: 36px; }
  .footer-bottom { flex-direction: column; gap: 12px; text-align: center; }
}

@media (max-width: 480px) {
  .overlay-nav a { font-size: 2rem; }
  .footer-right { gap: 24px; }
}
</style>