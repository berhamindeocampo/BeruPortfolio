<template>
  <section class="about-section" id="about">
    <div class="about-container">
      <div class="profile">
        <img src="/img/beruchisa.jpg" alt="Berhamin de Ocampo" class="profile-img" />
      </div>
      <div class="about-text">
        <h2 class="section-title">About Me</h2>
        <p class="description">
          Hi, I'm <span class="highlight">Berhamin de Ocampo</span>, 
          a passionate Front-End Developer from San Miguel, Bulacan. 
          I love turning ideas into beautiful, interactive, and immersive web experiences.
        </p>
        <div class="stats">
          <div class="stat-item">
            <span class="number">2</span>
            <span class="label">Years Experience</span>
          </div>
          <div class="stat-item">
            <span class="number">3</span>
            <span class="label">Public Repos</span>
          </div>
          <div class="stat-item">
            <span class="number">∞</span>
            <span class="label">Creativity</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { onMounted } from 'vue';

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('active');
      }
    });
  }, { threshold: 0.2 });

  observer.observe(document.querySelector('.about-section'));
});
</script>

<style scoped>
.about-section {
  padding: 140px 5% 120px;
  background: #0a0a0a;
  color: white;
  opacity: 0;
  transform: translateY(60px);
  transition: all 0.9s cubic-bezier(0.25, 0.1, 0.25, 1);
}

.about-section.active {
  opacity: 1;
  transform: translateY(0);
}

.about-container {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  align-items: center;
  gap: 100px;
  flex-wrap: wrap;
}

.profile-img {
  width: 360px;
  height: 360px;
  border-radius: 50%;
  object-fit: cover;
  border: 8px solid #ffcc00;
  box-shadow: 0 0 60px rgba(255, 204, 0, 0.4);
  transition: transform 0.6s ease;
}

.profile-img:hover {
  transform: scale(1.05);
}

.about-text {
  flex: 1;
  min-width: 320px;
}

.section-title {
  font-size: 52px;
  margin-bottom: 30px;
  font-family: "H7GBK-Heavy", sans-serif;
  text-transform: uppercase;
  letter-spacing: 3px;
}

.highlight {
  color: #ffcc00;
}

.description {
  font-size: 19px;
  line-height: 1.75;
  margin-bottom: 50px;
  color: #ddd;
  max-width: 580px;
}

.stats {
  display: flex;
  gap: 60px;
  flex-wrap: wrap;
}

.stat-item {
  text-align: center;
}

.number {
  display: block;
  font-size: 42px;
  font-weight: bold;
  color: #ffcc00;
  font-family: "H7GBK-Heavy", sans-serif;
}

.label {
  font-size: 15px;
  text-transform: uppercase;
  opacity: 0.75;
  letter-spacing: 1px;
}

/* ── Mobile ── */
@media (max-width: 768px) {
  .about-section { padding: 110px 5% 80px; }

  .about-container {
    flex-direction: column;
    gap: 40px;
    text-align: center;
    align-items: center;
  }

  .profile-img {
    width: 220px;
    height: 220px;
  }

  .about-text { min-width: unset; width: 100%; }

  .section-title { font-size: 36px; }

  .description { font-size: 16px; max-width: 100%; }

  .stats { justify-content: center; gap: 32px; }

  .number { font-size: 32px; }
}

@media (max-width: 480px) {
  .profile-img { width: 170px; height: 170px; }
  .section-title { font-size: 28px; }
  .stats { gap: 20px; }
}
</style>