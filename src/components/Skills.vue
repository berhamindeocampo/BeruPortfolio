<template>
  <section class="skills-section">
    <h2 class="section-title">Skills & Technologies</h2>
    <div class="skills-grid">
      <div class="skill-card" v-for="skill in skills" :key="skill">
        <span>{{ skill }}</span>
      </div>
    </div>
  </section>
</template>

<script setup>
const skills = [
  'Vue.js', 'JavaScript', 'HTML5', 'CSS3', 'WordPress',
 'Git & GitHub', 'Figma', 'Python',
];
</script>

<style scoped>
.skills-section {
  padding: 100px 5%;
  background: #111;
  color: white;
  text-align: center;
}

.section-title {
  font-size: 42px;
  margin-bottom: 60px;
  font-family: "H7GBK-Heavy", sans-serif;
  text-transform: uppercase;
}

.skills-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  justify-content: center;
  max-width: 900px;
  margin: 0 auto;
}

.skill-card {
  background: #1a1a1a;
  padding: 18px 32px;
  border-radius: 50px;
  font-size: 18px;
  border: 2px solid #ffcc00;
  transition: all 0.3s;
}

.skill-card:hover {
  background: #ffcc00;
  color: black;
  transform: translateY(-5px);
}

@media (max-width: 768px) {
  .skills-section { padding: 75px 5% 75px; }
  .section-title { font-size: 30px; margin-bottom: 40px; }
  .skill-card { padding: 14px 22px; font-size: 15px; }
}

@media (max-width: 480px) {
  .section-title { font-size: 24px; }
  .skills-grid { gap: 12px; }
  .skill-card { padding: 12px 18px; font-size: 14px; }
}
</style>