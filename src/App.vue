<template>
  <div :class="{ 'dark-mode': darkMode }">

    <header class="header">
      <div class="logo-text">Berhamin<span class="dot">.</span></div>
      <div class="header-actions">
        <button class="theme-toggle" @click="toggleDarkMode" :aria-label="darkMode ? 'Light Mode' : 'Dark Mode'">
          <img src="/sun.svg" class="sun">
          <img src="/moon.svg" class="moon">
        </button>
        <button class="hamburger-btn" @click="navOpen = !navOpen" aria-label="Open menu">
          <span></span><span></span><span></span>
        </button>
      </div>
    </header>

    <div class="nav-overlay" :class="{ open: navOpen }" @click.self="navOpen = false">
      <nav class="overlay-nav">
        <ul>
          <li><a @click="goTo('about')">About</a></li>
          <li><a @click="goTo('projects')">Projects</a></li>
          <li><a @click="goTo('skills')">Skills</a></li>
          <li><a @click="goTo('contact')">Contact</a></li>
        </ul>
      </nav>
    </div>

    <section class="hero">
      <div class="hero-top">
        <div class="hero-icon-circle">👨‍💻</div>
        <h1 class="hero-title">FRONT-END<br>DEVELOPER &amp;<br>CREATIVE CODER</h1>
        <div class="hero-badge">OPEN TO WORK</div>
      </div>
      <div class="hero-bottom">
        <div class="hero-card">🚀</div>
        <div class="hero-message">
          <p>Building modern, responsive web applications with clean code and thoughtful design. Passionate about crafting digital experiences people love.</p>
          <a class="btn-primary" @click="goTo('contact')">Get in touch <span>↗</span></a>
        </div>
        <div class="hero-card">💡</div>
      </div>
    </section>

    <main>
      <About ref="about" />
      <Projects ref="projects" />
      <Skills ref="skills" />
      <Contact ref="contact" />
    </main>

    <footer class="footer">
      <div class="footer-mid">
        <div class="footer-logo">Berhamin<br>de Ocampo <span class="paw">✦</span></div>
      </div>
      <div class="footer-bottom">
        <p>© {{ currentYear }} Berhamin de Ocampo</p>
      </div>
    </footer>

  </div>
</template>

<script>
import About from './components/About.vue'
import Projects from './components/Projects.vue'
import Skills from './components/Skills.vue'
import Contact from './components/Contact.vue'

export default {
  name: 'App',
  components: { About, Projects, Skills, Contact },
  data() {
    return {
      darkMode: false,
      navOpen: false,
      newsletterEmail: '',
      currentYear: new Date().getFullYear()
    }
  },
  methods: {
    toggleDarkMode() {
      this.darkMode = !this.darkMode
      document.body.classList.toggle('dark-mode', this.darkMode)
      localStorage.setItem('darkMode', this.darkMode)
    },
    goTo(refName) {
      this.navOpen = false
      const el = this.$refs[refName]?.$el
      if (el) el.scrollIntoView({ behavior: 'smooth' })
    },
    subscribeNewsletter() {
      if (this.newsletterEmail) {
        alert('Thanks! We\'ll be in touch.')
        this.newsletterEmail = ''
      }
    }
  },
  mounted() {
    const saved = localStorage.getItem('darkMode') === 'true'
    if (saved) { this.darkMode = true; document.body.classList.add('dark-mode') }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Bayon&family=Lato:wght@300;400;700;900&display=swap');

:root {
  --cream:    #F7F3EC;
  --white:    #FFFFFF;
  --ink:      #1C1C1C;
  --mid:      #5A5A5A;
  --blue:     #3B6FD4;
  --yellow:   #F5C842;
  --red:      #E8594A;
  --blue-lt:  #E8EFFC;
  --yellow-lt:#FEF7DC;
  --red-lt:   #FCE9E7;
  --border:   #E0D9CF;
  --radius:   14px;
}
.dark-mode {
  --cream:    #1A1A1A;
  --white:    #242424;
  --ink:      #F0F0F0;
  --mid:      #AAAAAA;
  --border:   #333333;
  --blue-lt:  #1A2540;
  --yellow-lt:#2A2210;
  --red-lt:   #2A1210;
  background-color: var(--cream);
  color: var(--ink);
}
html, body {
  overflow-x: hidden;
  width: 100%;
  margin: 0;
  padding: 0;
}

*, *::before, *::after { box-sizing: border-box; }
body { font-family: 'Lato', sans-serif; background: var(--cream); color: var(--ink); transition: background .3s, color .3s; }
a { text-decoration: none; color: inherit; cursor: pointer; }
button { cursor: pointer; border: none; background: none; font-family: inherit; }
img { display: block; max-width: 100%; }

.header {
  position: fixed; top: 0; left: 0; right: 0; z-index: 200;
  display: flex; align-items: center; justify-content: space-between;
  padding: 18px 48px;
  background: var(--cream);
  border-bottom: 1px solid var(--border);
  transition: background .3s, border-color .3s;
}
.logo-text { font-family: 'Bayon', sans-serif; font-size: 1.5rem; letter-spacing: .02em; }
.logo-text .dot { color: var(--blue); }
.header-actions { display: flex; align-items: center; gap: 12px; }
.theme-toggle {
  width: 40px; height: 40px; border-radius: 50%;
  background: var(--white); border: 1px solid var(--border);
  font-size: 1rem; display: flex; align-items: center; justify-content: center;
  transition: background .3s;
}
.theme-toggle .sun { display: inline; }
.theme-toggle .moon { display: none; }
.dark-mode .theme-toggle .sun { display: none; }
.dark-mode .theme-toggle .moon { display: inline; filter: invert(1); }
.hamburger-btn {
  width: 40px; height: 40px; border-radius: 50%;
  background: var(--ink); display: flex; flex-direction: column;
  align-items: center; justify-content: center; gap: 5px;
  transition: background .3s;
}
.hamburger-btn span { display: block; width: 18px; height: 2px; background: var(--cream); border-radius: 2px; }

.nav-overlay {
  position: fixed; inset: 0; z-index: 199;
  background: var(--ink); opacity: 0; pointer-events: none;
  display: flex; align-items: center; justify-content: center;
  transition: opacity .3s;
}
.nav-overlay.open { opacity: 1; pointer-events: all; }
.overlay-nav ul { list-style: none; text-align: center; }
.overlay-nav li { margin: 18px 0; }
.overlay-nav a {
  font-family: 'Bayon', sans-serif; font-size: 2.4rem;
  color: var(--cream); letter-spacing: .04em; transition: color .2s;
}
.overlay-nav a:hover { color: var(--yellow); }

.hero { padding-top: 76px; min-height: 100vh; display: flex; flex-direction: column; }
.hero-top {
  display: grid; grid-template-columns: 1fr auto 1fr;
  align-items: center; padding: 40px 48px 0;
}
.hero-icon-circle {
  width: 80px; height: 80px; border-radius: 50%;
  background: var(--yellow); display: flex; align-items: center;
  justify-content: center; font-size: 2rem;
}
.hero-title {
  font-family: 'Bayon', sans-serif;
  font-size: clamp(2.2rem, 5.5vw, 5rem);
  text-align: center; line-height: 1.05; letter-spacing: .03em;
}
.hero-badge {
  justify-self: end; background: var(--red); color: #fff;
  font-family: 'Bayon', sans-serif; font-size: 1rem;
  padding: 8px 18px; border-radius: 30px; letter-spacing: .06em;
}
.hero-bottom {
  display: grid; grid-template-columns: 1fr 1.6fr 1fr;
  gap: 24px; padding: 32px 48px 48px; align-items: end; flex: 1;
}
.hero-card {
  border-radius: var(--radius); background: var(--white);
  border: 1px solid var(--border); height: 280px;
  display: flex; align-items: center; justify-content: center; font-size: 4rem;
  transition: background .3s, border-color .3s;
}
.hero-message {
  text-align: center; display: flex; flex-direction: column;
  align-items: center; gap: 24px; padding: 24px 0;
}
.hero-message p { font-size: 1.05rem; color: var(--mid); line-height: 1.7; max-width: 380px; }

.btn-primary {
  display: inline-flex; align-items: center; gap: 8px;
  background: var(--ink); color: var(--cream);
  font-family: 'Lato', sans-serif; font-weight: 700; font-size: .95rem;
  padding: 13px 28px; border-radius: 40px; letter-spacing: .03em;
  transition: transform .2s, background .2s; cursor: pointer;
}
.btn-primary:hover { transform: translateY(-2px); background: var(--blue); }

.footer { background: var(--ink); color: var(--cream); padding: 64px 48px 32px; }
.footer-top {
  display: flex; justify-content: space-between; align-items: flex-start;
  border-bottom: 1px solid rgba(255,255,255,.12); padding-bottom: 48px; margin-bottom: 40px;
}
.footer-newsletter h2 { font-family: 'Bayon', sans-serif; font-size: 2.6rem; line-height: 1.1; }
.footer-newsletter .paw { color: var(--yellow); }
.footer-right { display: flex; flex-direction: column; align-items: flex-end; gap: 20px; }
.email-bar {
  display: flex; background: rgba(255,255,255,.1);
  border: 1px solid rgba(255,255,255,.2); border-radius: 40px; overflow: hidden;
}
.email-bar input {
  background: none; border: none; color: var(--cream); padding: 12px 20px;
  font-family: 'Lato', sans-serif; font-size: .9rem; outline: none; width: 240px;
}
.email-bar input::placeholder { color: rgba(255,255,255,.4); }
.email-bar button {
  background: var(--yellow); color: var(--ink); padding: 12px 22px;
  font-weight: 700; font-size: .9rem;
}
.social-icons { display: flex; gap: 12px; }
.social-icon {
  width: 38px; height: 38px; border-radius: 50%;
  border: 1px solid rgba(255,255,255,.25);
  display: flex; align-items: center; justify-content: center;
  font-size: .85rem; font-weight: 700; transition: background .2s, border-color .2s;
}
.social-icon:hover { background: var(--yellow); color: var(--ink); border-color: var(--yellow); }
.footer-mid {
  display: flex; justify-content: space-between; align-items: center;
  padding-bottom: 40px; border-bottom: 1px solid rgba(255,255,255,.12); margin-bottom: 28px;
}
.footer-logo { font-family: 'Bayon', sans-serif; font-size: 2.2rem; line-height: 1; }
.footer-logo .paw { color: var(--yellow); }
.footer-nav { display: flex; gap: 32px; }
.footer-nav a { font-size: .9rem; opacity: .7; transition: opacity .2s; cursor: pointer; }
.footer-nav a:hover { opacity: 1; }
.footer-bottom { display: flex; justify-content: space-between; font-size: .82rem; opacity: .5; }
.footer-links { display: flex; gap: 24px; }

.dark-mode .project-card img[src="/img/whisker.png"] {
  content: url('/img/whisker-removebg-preview.png');
  object-fit: contain;
}

@media (max-width: 900px) {
  .header { padding: 16px 24px; }
  .hero-top { grid-template-columns: 1fr auto; }
  .hero-badge { display: none; }
  .hero-bottom { grid-template-columns: 1fr; }
  .hero-card { height: 160px; }
  .footer { padding: 48px 24px 24px; }
  .footer-top { flex-direction: column; gap: 32px; }
  .footer-right { align-items: flex-start; }
  .footer-mid { flex-direction: column; gap: 24px; align-items: flex-start; }
}
@media (max-width: 560px) {
  .hero-title { font-size: 2rem; }
  .hero-top { padding: 24px 20px 0; }
  .hero-bottom { padding: 24px 20px; }
}
</style>
