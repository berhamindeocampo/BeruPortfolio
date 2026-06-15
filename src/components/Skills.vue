<template>
  <section id="skills" class="skills-section">

    <div class="section-header">
      <h2>Skills &amp; Expertise</h2>
      <p>Tools and technologies I work with regularly.</p>
    </div>

    <!-- Role cards (like WhiskerWash vet cards) -->
    <div class="role-cards">
      <div class="role-card blue">
        <div class="role-icon">⚙️</div>
        <h3>Frontend</h3>
        <p>Building responsive, pixel-perfect interfaces users love.</p>
      </div>
      <div class="role-card yellow">
        <div class="role-icon">🐍</div>
        <h3>Backend</h3>
        <p>APIs, databases, and server-side logic &amp; PHP.</p>
      </div>
      <div class="role-card red">
        <div class="role-icon">🔧</div>
        <h3>Problem Solver</h3>
        <p>Debugging, optimization, and creative technical solutions.</p>
      </div>
    </div>

    <!-- Skill bars grid -->
    <div class="skills-grid">
      <div v-for="category in skillCategories" :key="category.name" class="skill-group">
        <h4>{{ category.name }}</h4>
        <div class="skill-list">
          <div v-for="skill in category.skills" :key="skill.name" class="skill-item">
            <div class="skill-label-row">
              <span class="skill-name">{{ skill.name }}</span>
              <span class="skill-pct">{{ skill.level }}%</span>
            </div>
            <div class="skill-bar">
              <div class="skill-fill" :style="{ width: skill.level + '%' }"></div>
            </div>
          </div>
        </div>
      </div>
    </div>

  </section>
</template>

<script>
export default {
  name: 'Skills',
  data() {
    return {
      skillCategories: [
        {
          name: 'Frontend',
          skills: [
            { name: 'HTML5 / CSS3', level: 92 },
            { name: 'JavaScript', level: 80 },
            { name: 'React', level: 70 },
          ]
        },
        {
          name: 'Backend',
          skills: [
            { name: 'PHP', level: 72 },
            { name: 'MySQL', level: 70 },
          ]
        },
        {
          name: 'Tools',
          skills: [
            { name: 'Git / GitHub', level: 85 },
            { name: 'VS Code', level: 95 },
            { name: 'Figma', level: 55 }
          ]
        },
        {
          name: 'Soft Skills',
          skills: [
            { name: 'Problem Solving', level: 90 },
            { name: 'Team Collaboration', level: 88 },
            { name: 'Communication', level: 82 },
          ]
        }
      ]
    }
  }
}
</script>

<style scoped>
.skills-section {
  padding: 72px 48px;
  background: var(--cream);
  border-top: 1px solid var(--border);
  transition: background .3s, border-color .3s;
}

.section-header {
  text-align: center;
  margin-bottom: 48px;
}

.section-header h2 {
  font-family: 'Bayon', sans-serif;
  font-size: clamp(1.8rem, 3.5vw, 2.8rem);
  margin-bottom: 12px;
}

.section-header p {
  color: var(--mid);
  max-width: 420px;
  margin: 0 auto;
  line-height: 1.7;
  transition: color .3s;
}

/* ── ROLE CARDS (WhiskerWash vet card style) ─── */
.role-cards {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
  margin-bottom: 52px;
}

.role-card {
  border-radius: var(--radius);
  padding: 32px 24px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 12px;
  text-align: center;
}

.role-card.blue  { background: var(--blue-lt); }
.role-card.yellow{ background: var(--yellow-lt); }
.role-card.red   { background: var(--red-lt); }

.role-icon {
  width: 64px; height: 64px; border-radius: 50%;
  background: var(--white);
  display: flex; align-items: center; justify-content: center;
  font-size: 2rem;
  transition: background .3s;
}

.role-card h3 {
  font-family: 'Bayon', sans-serif;
  font-size: 1.2rem;
  letter-spacing: .02em;
}

.role-card p {
  font-size: .88rem;
  color: var(--mid);
  line-height: 1.6;
  transition: color .3s;
}

/* ── SKILL BARS ─────────────────────────────── */
.skills-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 24px;
  background: var(--white);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 36px;
  transition: background .3s, border-color .3s;
}

.skill-group h4 {
  font-family: 'Bayon', sans-serif;
  font-size: .95rem;
  letter-spacing: .1em;
  color: var(--blue);
  text-transform: uppercase;
  margin-bottom: 16px;
}

.skill-list {
  display: flex;
  flex-direction: column;
  gap: 14px;
}

.skill-item { display: flex; flex-direction: column; gap: 5px; }

.skill-label-row {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.skill-name { font-size: .88rem; font-weight: 700; }
.skill-pct  { font-size: .78rem; color: var(--mid); }

.skill-bar {
  height: 6px;
  background: var(--border);
  border-radius: 3px;
  overflow: hidden;
}

.skill-fill {
  height: 100%;
  background: var(--blue);
  border-radius: 3px;
  transition: width .6s ease;
}

@media (max-width: 900px) {
  .skills-section { padding: 48px 24px; }
  .role-cards { grid-template-columns: 1fr 1fr; }
  .skills-grid { grid-template-columns: 1fr 1fr; padding: 24px; }
}
@media (max-width: 560px) {
  .role-cards { grid-template-columns: 1fr; }
  .skills-grid { grid-template-columns: 1fr; }
}
</style>