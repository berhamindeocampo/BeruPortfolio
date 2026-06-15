<template>
  <section id="projects" class="projects-section">

    <div class="section-header">
      <h2>Pampering the Web with<br>Featured Projects</h2>
      <p>A selection of projects I've built — from pet care apps to data tools.</p>
    </div>

    <div class="projects-grid">
      <div
        v-for="project in projects"
        :key="project.id"
        class="project-card"
      >
        <div class="project-image">
          <img v-if="project.img" :src="project.img" :alt="project.title" class="project-img" />
          <span v-else>{{ project.icon }}</span>
        </div>
        <h3>{{ project.title }}</h3>
        <p>{{ project.description }}</p>
        <div class="tech-pills">
          <span v-for="tech in project.tech" :key="tech" class="pill">{{ tech }}</span>
        </div>
        <div class="project-links">
          <a v-if="project.github" :href="project.github" target="_blank" rel="noopener" class="btn-outline">
            GitHub <span>↗</span>
          </a>
          <a v-if="project.demo" :href="project.demo" target="_blank" rel="noopener" class="btn-outline btn-outline--filled">
            Live Demo <span>↗</span>
          </a>
        </div>
      </div>
    </div>

  </section>
</template>

<script>
export default {
  name: 'Projects',
  data() {
    return {
      projects: [
        {
          id: 1,
          title: 'Whisker Wash',
          description: 'Pet care multi-page web application with booking, product catalog, AI chatbot powered by Google Gemini, blog, and testimonials.',
          img: 'img/ChatGPT_Image_Jun_15__2026__01_28_57_PM-removebg-preview.png',
          tech: ['HTML', 'CSS', 'JavaScript', 'Gemini AI'],
          github: 'https://github.com/berhamindeocampo/WhiskerWash',
          demo: 'https://whisker-wash.vercel.app'
        },
        {
          id: 2,
          title: 'Earthquake Event Recorder',
          description: 'Python desktop app using Tkinter for logging and managing earthquake records. Auto-calculates safety alerts by magnitude and supports JSON import/export.',
          img: 'img/earthquake.png',
          tech: ['Python', 'Tkinter'],
          github: 'https://github.com/berhamindeocampo/Earthquake-Event-Recorder'
        },
        {
          id: 3,
          title: 'Beru Portfolio',
          description: 'My portfolio.',
          icon: '📱',
          tech: ['Vue.js', 'HTML', 'JavaScript'],
          github: 'https://github.com/berhamindeocampo/BeruPortfolio',
        }
      ]
    }
  }
}
</script>

<style scoped>
.projects-section {
  padding: 72px 48px;
  background: var(--white);
  border-top: 1px solid var(--border);
  transition: background .3s, border-color .3s;
}

.section-header {
  text-align: center;
  margin-bottom: 52px;
}

.section-header h2 {
  font-family: 'Bayon', sans-serif;
  font-size: clamp(1.8rem, 3.5vw, 2.8rem);
  line-height: 1.1;
  margin-bottom: 14px;
}

.section-header p {
  color: var(--mid);
  font-size: 1rem;
  max-width: 480px;
  margin: 0 auto;
  line-height: 1.7;
  transition: color .3s;
}

.projects-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 22px;
}

.project-card {
  background: var(--cream);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 28px;
  display: flex;
  flex-direction: column;
  gap: 14px;
  transition: transform .2s, box-shadow .2s, background .3s, border-color .3s;
}

.project-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 12px 36px rgba(0,0,0,.09);
}

.project-image {
  height: 160px;
  border-radius: 10px;
  background: var(--white);
  border: 1px solid var(--border);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 3.5rem;
  overflow: hidden;
  transition: background .3s, border-color .3s;
}

.project-img {
  width: 100%;
  height: 100%;
  object-fit: contain;
  padding: 8px;
}

h3 {
  font-family: 'Bayon', sans-serif;
  font-size: 1.3rem;
  letter-spacing: .02em;
}

p {
  font-size: .9rem;
  color: var(--mid);
  line-height: 1.65;
  flex: 1;
  transition: color .3s;
}

.tech-pills {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
}

.pill {
  font-size: .75rem;
  padding: 4px 12px;
  border-radius: 20px;
  background: var(--blue-lt);
  color: var(--blue);
  font-weight: 700;
  transition: background .3s;
}

.project-links {
  display: flex;
  gap: 10px;
  flex-wrap: wrap;
}

.btn-outline {
  display: inline-flex;
  align-items: center;
  gap: 5px;
  border: 1.5px solid var(--ink);
  border-radius: 30px;
  padding: 8px 18px;
  font-size: .82rem;
  font-weight: 700;
  transition: background .2s, color .2s, border-color .2s;
}

.btn-outline:hover {
  background: var(--ink);
  color: var(--cream);
}

.btn-outline--filled {
  background: var(--blue);
  border-color: var(--blue);
  color: #fff;
}

.btn-outline--filled:hover {
  background: #2a5bbf;
  border-color: #2a5bbf;
  color: #fff;
}

@media (max-width: 900px) {
  .projects-section { padding: 48px 24px; }
  .projects-grid { grid-template-columns: 1fr 1fr; }
}
@media (max-width: 560px) {
  .projects-grid { grid-template-columns: 1fr; }
}
</style>