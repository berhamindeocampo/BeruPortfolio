<template>
  <section class="about-section" id="about" ref="sectionEl">
    <div class="about-inner">

      <!-- LEFT: Photo -->
      <div class="photo-panel">
        <img src="/img/chisacute.jpg" alt="Berhamin de Ocampo" class="photo" />
        <div class="photo-fade"></div>
      </div>

      <!-- RIGHT: Text -->
      <div class="text-panel" :class="{ visible: isVisible }">
        <p class="role-tag">FULL-STACK DEVELOPER</p>

        <h1 class="headline">
         About Me...
        </h1>

        <p class="bio">
          Hi, I'm <strong>Berhamin de Ocampo</strong> — a passionate Full-Stack Developer from San Miguel, Bulacan. I love turning ideas into beautiful, interactive, and immersive web experiences.
        </p>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const sectionEl  = ref(null)
const isVisible  = ref(false)

onMounted(() => {
  const observer = new IntersectionObserver(
    ([entry]) => { if (entry.isIntersecting) isVisible.value = true },
    { threshold: 0.15 }
  )
  if (sectionEl.value) observer.observe(sectionEl.value)
})
</script>

<style scoped>
/* ── SECTION ─────────────────────────────────── */
.about-section {
  background: #0a0a0a;
  color: #fff;
  overflow: hidden;
  min-height: 100vh;
  display: flex;
  align-items: stretch;
}

.about-inner {
  display: flex;
  width: 100%;
  min-height: 100vh;
}

/* ── PHOTO PANEL ─────────────────────────────── */
.photo-panel {
  position: relative;
  flex: 0 0 48%;
  overflow: hidden;
}

.photo {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: center top;
  display: block;
  filter: grayscale(10%) brightness(0.85);
}

/* Right-edge fade into dark */
.photo-fade {
  position: absolute;
  inset: 0;
  background: linear-gradient(
    to right,
    transparent 50%,
    #0a0a0a 100%
  );
}

/* ── TEXT PANEL ──────────────────────────────── */
.text-panel {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 80px 7% 80px 5%;
  opacity: 0;
  transform: translateY(36px);
  transition: opacity .8s ease, transform .8s ease;
}
.text-panel.visible {
  opacity: 1;
  transform: translateY(0);
}

.role-tag {
  font-size: .7rem;
  font-weight: 700;
  letter-spacing: .2em;
  color: #ffcc00;
  margin: 0 0 20px;
  text-transform: uppercase;
}

.headline {
  font-size: clamp(2.4rem, 4.5vw, 4rem);
  font-weight: 900;
  line-height: 1.12;
  margin: 0 0 28px;
  color: #fff;
  font-family: "H7GBK-Heavy", sans-serif;
}

.accent {
  font-style: italic;
  color: #ffcc00;
  font-family: Georgia, 'Times New Roman', serif;
}

.bio {
  font-size: 1.05rem;
  line-height: 1.8;
  color: rgba(255,255,255,.6);
  max-width: 460px;
  margin: 0 0 40px;
}

/* ── CTA BUTTONS ─────────────────────────────── */
.cta-row {
  display: flex;
  gap: 14px;
  flex-wrap: wrap;
}

.btn {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  font-size: .82rem;
  font-weight: 800;
  letter-spacing: .1em;
  padding: 14px 28px;
  border-radius: 6px;
  text-decoration: none;
  transition: transform .2s, background .2s, box-shadow .2s;
  cursor: pointer;
}
.btn:hover { transform: translateY(-2px); }

.btn--primary {
  background: #ffcc00;
  color: #0a0a0a;
  box-shadow: 0 4px 24px rgba(255,204,0,.35);
}
.btn--primary:hover {
  background: #ffe033;
  box-shadow: 0 6px 30px rgba(255,204,0,.55);
}

.btn--ghost {
  background: transparent;
  border: 1px solid rgba(255,255,255,.25);
  color: #fff;
}
.btn--ghost:hover {
  background: rgba(255,255,255,.08);
  border-color: rgba(255,255,255,.5);
}

/* ── RESPONSIVE ──────────────────────────────── */
@media (max-width: 900px) {
  .photo-panel { flex: 0 0 42%; }
  .text-panel { padding: 60px 5%; }
  .headline { font-size: 2.2rem; }
}

@media (max-width: 768px) {
  .about-inner { flex-direction: column; min-height: auto; }

  .photo-panel {
    flex: 0 0 auto;
    height: 55vw;
    max-height: 340px;
  }

  .photo-fade {
    background: linear-gradient(
      to bottom,
      transparent 40%,
      #0a0a0a 100%
    );
  }

  .text-panel { padding: 32px 24px 60px; }
  .headline { font-size: 2rem; }
  .bio { font-size: .92rem; }
}

@media (max-width: 480px) {
  .headline { font-size: 1.7rem; }
  .btn { padding: 12px 20px; font-size: .78rem; }
}
</style>