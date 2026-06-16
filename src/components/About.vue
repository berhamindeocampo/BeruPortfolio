<template>
  <section id="about" class="about-strip">

    <!-- LEFT: image/avatar side -->
    <div class="about-image-side">
      <div class="avatar-circle">
        <img
          v-if="profileImg"
          :src="profileImg"
          alt="Berhamin de Ocampo"
          class="profile-img"
        />
        <span v-else>👨‍💻</span>
      </div>
    </div>

    <!-- RIGHT: text side -->
    <div class="about-text-side">
      <h2>PASSIONATE CODE FOR EVERY PROJECT AND PIXEL.</h2>
      <p>
        Hi! I'm Berhamin de Ocampo — a software developer from San Miguel, Bulacan, Philippines.
        I specialize in front-end development and love crafting elegant solutions to complex problems.
      </p>
      <a href="https://github.com/berhamindeocampo" target="_blank" class="btn-primary">
        View GitHub <span>↗</span>
      </a>

      <div class="stats-row">
        <div class="stat">
          <h3>2+</h3>
          <p>Public Repos</p>
        </div>
        <div class="stat">
          <h3>2</h3>
          <p>Years Coding</p>
        </div>
        <div class="stat">
          <h3>100%</h3>
          <p>Passion</p>
        </div>
      </div>
    </div>

  </section>
</template>

<script>
export default {
  name: 'About',
  data() {
    return {
      profileImg: '/img/beruchisa.jpg'
    }
  }
}
</script>

<style scoped>
.about-strip {
  display: grid;
  grid-template-columns: 1fr 1fr;
  border-top: 1px solid var(--border);
  transition: border-color .3s;
}

.about-image-side {
  background: var(--cream);
  padding: 48px;
  object-fit: cover;
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 420px;
  transition: background .3s, border-color .3s;
}

.avatar-circle {
  width: 500px;
  height: 500px;
  border-radius: 50%;
  background: var(--yellow-lt);
  border: 4px solid var(--yellow);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 5rem;
  overflow: hidden;
  transition: background .3s;
}

.profile-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.about-text-side {
  background: var(--cream);
  padding: 52px 56px;
  display: flex;
  flex-direction: column;
  gap: 18px;
  justify-content: center;  
}

h2 {
  font-family: 'Bayon', sans-serif;
  font-size: clamp(1.8rem, 3vw, 2.6rem);
  line-height: 1.1;
}

p {
  color: var(--mid);
  line-height: 1.75;
  font-size: 1rem;
  transition: color .3s;
}

.stats-row {
  display: flex;
  gap: 32px;
  margin-top: 16px;
  padding-top: 24px;
  border-top: 1px solid var(--border);
}

.stat h3 {
  font-family: 'Bayon', sans-serif;
  font-size: 2.2rem;
  color: var(--blue);
}

.stat p {
  font-size: .82rem;
  color: var(--mid);
  margin-top: 2px;
}

@media (max-width: 900px) {
  .about-strip { grid-template-columns: 1fr; }

  .avatar-circle {
    width: 450px; /* Smaller size for mobile */
    height: 450px;
  }

  .about-image-side {
    min-height: 260px;
    border-right: none;
    border-bottom: 1px solid var(--border);
  }
  .about-text-side { padding: 36px 24px; }
  .stats-row { flex-wrap: wrap; gap: 20px; }
}
</style>
