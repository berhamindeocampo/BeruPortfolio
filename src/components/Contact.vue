<template>
  <section id="contact" class="contact-section">
    <div class="section-header">
      <h2>Connect &amp; Collaborate</h2>
      <p>I'm always open to new projects and opportunities. Feel free to reach out!</p>
    </div>

    <div class="contact-layout">
      <form @submit.prevent="submitForm" class="contact-form-wrap">
        <div class="form-row">
          <div class="form-group">
            <label for="name">Name</label>
            <input v-model="form.name" type="text" id="name" placeholder="Your name" required>
          </div>
          <div class="form-group">
            <label for="email">Email</label>
            <input v-model="form.email" type="email" id="email" placeholder="your@email.com" required>
          </div>
        </div>
        <div class="form-group">
          <label for="subject">Subject</label>
          <input v-model="form.subject" type="text" id="subject" placeholder="What's this about?" required>
        </div>
        <div class="form-group">
          <label for="message">Message</label>
          <textarea v-model="form.message" id="message" placeholder="Your message..." rows="5" required></textarea>
        </div>
        
        <button type="submit" :disabled="isSubmitting" class="submit-btn">
          {{ isSubmitting ? 'Sending...' : 'Send Message ↗' }}
        </button>

        <div v-if="formMessage" :class="['form-toast', formStatus]">
          {{ formMessage }}
        </div>
      </form>

      <div class="contact-info">
        <div class="info-card blue">
          <div class="info-icon">📧</div>
          <h3>Email</h3>
          <a href="mailto:badeocampo28@gmail.com">badeocampo28@gmail.com</a>
        </div>
        <div class="info-card yellow">
          <div class="info-icon">📍</div>
          <h3>Location</h3>
          <p>San Miguel, Bulacan<br>Philippines 3011</p>
        </div>
        <div class="info-card red">
          <div class="info-icon">🔗</div>
          <h3>Social Links</h3>
          <div class="social-list">
            <a href="https://github.com/berhamindeocampo" target="_blank" rel="noopener">GitHub ↗</a>
            <a href="https://www.linkedin.com/in/berhamin-de-ocampo-b507a3404/" target="_blank" rel="noopener">LinkedIn ↗</a>
            <a href="https://facebook.com/beruhamin" target="_blank" rel="noopener">Facebook ↗</a>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Contact',
  data() {
    return {
      form: { name: '', email: '', subject: '', message: '' },
      isSubmitting: false,
      formMessage: '',
      formStatus: ''
    }
  },
methods: {
    async submitForm() {
      this.isSubmitting = true;
      try {
        const response = await fetch('https://formspree.io/f/mnjyraya', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify(this.form)
        });

        if (response.ok) {
          this.formStatus = 'success';
          this.formMessage = '✓ Message sent! Thank you for reaching out.';
          this.form = { name: '', email: '', subject: '', message: '' }; // Reset fields
        } else {
          throw new Error('Submission failed');
        }
      } catch (error) {
        this.formStatus = 'error';
        this.formMessage = '✗ Oops! There was a problem sending your message.';
      } finally {
        this.isSubmitting = false;
        setTimeout(() => { this.formMessage = ''; this.formStatus = ''; }, 5000);
      }
    }
  }
}
</script>

<style scoped>
.contact-section {
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
  margin-bottom: 12px;
}

.section-header p {
  color: var(--mid);
  max-width: 480px;
  margin: 0 auto;
  line-height: 1.7;
  transition: color .3s;
}

/* ── LAYOUT ─────────────────────────────────── */
.contact-layout {
  display: grid;
  grid-template-columns: 1.4fr 1fr;
  gap: 28px;
  margin-bottom: 36px;
}

/* ── FORM ───────────────────────────────────── */
.contact-form-wrap {
  background: var(--cream);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 36px;
  display: flex;
  flex-direction: column;
  gap: 18px;
  transition: background .3s, border-color .3s;
}

.contact-form { display: flex; flex-direction: column; gap: 18px; }

.form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 18px; }

.form-group { display: flex; flex-direction: column; gap: 6px; }

label {
  font-size: .85rem;
  font-weight: 700;
  letter-spacing: .04em;
  text-transform: uppercase;
  color: var(--mid);
  transition: color .3s;
}

input, textarea {
  background: var(--white);
  border: 1.5px solid var(--border);
  border-radius: 10px;
  padding: 12px 16px;
  font-family: 'Lato', sans-serif;
  font-size: .95rem;
  color: var(--ink);
  outline: none;
  transition: border-color .2s, background .3s, color .3s;
  resize: vertical;
}

input:focus, textarea:focus { border-color: var(--blue); }

.submit-btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  background: var(--ink);
  color: var(--cream);
  font-family: 'Lato', sans-serif;
  font-weight: 700;
  font-size: 1rem;
  padding: 14px 28px;
  border-radius: 40px;
  transition: background .2s, transform .2s;
  align-self: flex-start;
}

.submit-btn:hover { background: var(--blue); transform: translateY(-2px); }

.form-toast {
  position: fixed;
  bottom: 20px;
  right: 20px;
  padding: 16px 24px;
  border-radius: 8px;
  background-color: #333; /* Use a color consistent with WhiskerWash */
  color: white;
  box-shadow: 0 4px 6px rgba(0,0,0,0.1);
  transition: opacity 0.3s ease;
  z-index: 1000;
}

.form-toast.success { background-color: #4CAF50; } /* Subtle success green */
.form-toast.error { background-color: #F44336; }   /* Subtle error red */

.form-toast.success { background: #d4edda; color: #155724; }
.form-toast.error   { background: var(--red-lt); color: var(--red); }

/* ── INFO CARDS ─────────────────────────────── */
.contact-info { display: flex; flex-direction: column; gap: 16px; }

.info-card {
  border-radius: var(--radius);
  padding: 24px;
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.info-card.blue   { background: var(--blue-lt); }
.info-card.yellow { background: var(--yellow-lt); }
.info-card.red    { background: var(--red-lt); }

.info-icon { font-size: 1.6rem; }

.info-card h3 {
  font-family: 'Bayon', sans-serif;
  font-size: 1.1rem;
  letter-spacing: .02em;
}

.info-card a, .info-card p {
  font-size: .9rem;
  color: var(--mid);
  line-height: 1.6;
  transition: color .3s;
}

.info-card a:hover { color: var(--blue); }

.social-list { display: flex; flex-direction: column; gap: 4px; }

/* ── CONNECT GALLERY ────────────────────────── */
.connect-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
}

.connect-tile {
  background: var(--cream);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  aspect-ratio: 4/3;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 10px;
  transition: transform .2s, background .3s, border-color .3s;
}

.connect-tile:hover { transform: scale(1.03); }

.tile-icon { font-size: 2.4rem; }

.tile-label {
  font-size: .82rem;
  font-weight: 700;
  color: var(--mid);
  transition: color .3s;
}

@media (max-width: 768px) {
  .contact-section { padding: 48px 24px; }
  .contact-layout { grid-template-columns: 1fr; }
  .connect-grid { grid-template-columns: 1fr; }
}
@media (max-width: 560px) {
  .form-row { grid-template-columns: 1fr; }
  .connect-grid { grid-template-columns: 1fr; }
}
</style>