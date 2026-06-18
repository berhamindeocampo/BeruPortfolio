<template>
  <section class="projects-section">
    <h2 class="section-title">Featured Projects</h2>
    
    <div class="carousel-container">
      <div class="slide" ref="slide">
        <div 
          v-for="(project, index) in projects" 
          :key="index"
          class="item"
          :style="{ backgroundImage: `url(${project.img})` }"
        >
          <div class="overlay"></div>
          <div class="content">
            <div class="name">{{ project.title }}</div>
            <div class="des">{{ project.description }}</div>
          </div>
        </div>
      </div>

      <div class="buttons">
        <button class="prev" @click="prevSlide"></button>
        <button class="next" @click="nextSlide"></button>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue';

const slide = ref(null);

const projects = [
  {
    title: "Whisker Wash",
    description: "AI-powered pet care platform with grooming booking and health tracking.",
    img: "/img/image.png"
  },
  {
    title: "Earthquake Event Recorder",
    description: "Real-time earthquake monitoring and recording system built with Python & Tkinter.",
    img: "/img/eer.png"
  },
  {
    title: "Beru Portfolio",
    description: "Modern Vue.js developer portfolio with smooth animations.",
    img: "/img/beruportfolio.png"
  },
];

const nextSlide = () => {
  const items = document.querySelectorAll('.item');
  if (items.length) slide.value?.appendChild(items[0]);
};

const prevSlide = () => {
  const items = document.querySelectorAll('.item');
  if (items.length) slide.value?.prepend(items[items.length - 1]);
};

// Scroll Animation + Auto Slide
onMounted(() => {
  // Auto slide every 6.5 seconds
  setInterval(nextSlide, 6500);

  // Intersection Observer for fade-in animation
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('active');
      }
    });
  }, { threshold: 0.2 });

  observer.observe(document.querySelector('.projects-section'));
});
</script>

<style scoped>
.projects-section {
  padding: 80px 5% 120px;
  background: #0a0a0a;
  color: white;
  opacity: 0;
  transform: translateY(60px);
  transition: all 0.9s cubic-bezier(0.25, 0.1, 0.25, 1);
}

.projects-section.active {
  opacity: 1;
  transform: translateY(0);
}

.section-title {
  text-align: center;
  font-size: 48px;
  margin-bottom: 70px;
  font-family: "H7GBK-Heavy", sans-serif;
  text-transform: uppercase;
  letter-spacing: 4px;
}

.carousel-container {
  position: relative;
  width: 100%;
  height: 100vh;
  max-height: 720px;
  overflow: hidden;
  border-radius: 12px;
}

.slide {
  position: relative;
  width: 100%;
  height: 100%;
}

.item {
  width: 180px;
  height: 280px;
  position: absolute;
  top: 50%;
  left: 15%;
  transform: translate(-50%, -50%) scale(0.85);
  border-radius: 24px;
  background-position: center;
  background-size: cover;
  background-repeat: no-repeat;
  background-color: #151212;
  transition: all 0.6s cubic-bezier(0.23, 1, 0.32, 1);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.7);
  cursor: pointer;
  z-index: 1;
}

.item:nth-child(1),
.item:nth-child(2) {
  top: 0;
  left: 0;
  transform: none;
  width: 100%;
  height: 100%;
  border-radius: 0;
  z-index: 2;
}

.overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(to bottom, rgba(0,0,0,0.3), rgba(0,0,0,0.8));
  z-index: 2;
  opacity: 0;
  transition: opacity 0.4s;
}

.item:nth-child(2) .overlay {
  opacity: 1;
}

.content {
  position: absolute;
  top: 50%;
  left: 80px;
  width: 420px;
  text-align: left;
  color: white;
  transform: translateY(-50%);
  font-family: "H7GBK-Heavy", sans-serif;
  display: none;
  z-index: 3;
}

.item:nth-child(2) .content {
  display: block;
}

.name {
  font-size: 52px;
  line-height: 1.05;
  text-transform: uppercase;
  margin-bottom: 16px;
  text-shadow: 0 4px 12px rgba(0,0,0,0.9);
}

.des {
  font-size: 17.5px;
  line-height: 1.5;
  text-shadow: 0 2px 8px rgba(0,0,0,0.8);
}

.buttons {
  position: absolute;
  bottom: 70px;
  left: 50%;
  transform: translateX(-50%);
  z-index: 10;
  display: flex;
  gap: 30px;
}

button {
  width: 58px;
  height: 48px;
  border: none;
  background: transparent;
  background-size: contain;
  background-repeat: no-repeat;
  cursor: pointer;
  transition: transform 0.3s;
}

button:hover { transform: scale(1.15); }

.prev { background-image: url('https://codetheworld.io/wp-content/uploads/2024/05/prev.png'); }
.next { background-image: url('https://codetheworld.io/wp-content/uploads/2024/05/next.png'); }

/* ── Mobile ── */
@media (max-width: 768px) {
  .projects-section { padding: 80px 0 80px; }

  .section-title { font-size: 30px; margin-bottom: 40px; letter-spacing: 2px; }

  .carousel-container {
    height: auto;
    max-height: none;
    aspect-ratio: 3 / 4;
    border-radius: 0;
  }

  /* Side preview card has no room on mobile — hide it */
  .item:nth-child(n+3) {
    display: none;
  }

  .content {
    left: 24px;
    right: 24px;
    width: auto;
    top: auto;
    bottom: 96px;
    transform: none;
  }

  .name { font-size: 30px; }
  .des  { font-size: 14px; }

  .buttons { bottom: 32px; gap: 20px; }

  button { width: 44px; height: 36px; }
}

@media (max-width: 480px) {
  .carousel-container { aspect-ratio: 3 / 4.4; }
  .name { font-size: 24px; }
  .content { left: 16px; right: 16px; bottom: 88px; }
}
</style>  