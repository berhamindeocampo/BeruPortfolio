<template>
  <section class="contact-section" id="contact">
    <div class="contact-content">
      <h2 class="section-title">GET IN TOUCH</h2>
      <p class="contact-text">
        I'm always open to new opportunities, collaborations, and exciting projects.
      </p>

      <form @submit.prevent="submitForm" class="contact-form" v-if="!submitted">
        <div class="form-group">
          <input 
            v-model="form.name"
            type="text" 
            name="name" 
            placeholder="Your Name" 
            required
          />
        </div>
        
        <div class="form-group">
          <input 
            v-model="form.email"
            type="email" 
            name="email" 
            placeholder="Your Email" 
            required
          />
        </div>
        
        <div class="form-group">
          <textarea 
            v-model="form.message"
            name="message" 
            placeholder="Your Message..." 
            rows="6"
            required
          ></textarea>
        </div>

        <button type="submit" class="submit-btn" :disabled="loading">
          {{ loading ? 'Sending...' : 'Send Message' }}
        </button>
      </form>

      <!-- Success Message -->
      <div v-if="submitted" class="success-message">
        <h3>✅ Message Sent Successfully!</h3>
        <p>Thank you! I'll get back to you as soon as possible.</p>
        <button @click="resetForm" class="reset-btn">Send Another Message</button>
      </div>

      <p class="form-note">Powered by Formspree</p>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue';
import { onMounted } from 'vue';

const form = ref({
  name: '',
  email: '',
  message: ''
});

const loading = ref(false);
const submitted = ref(false);

const submitForm = async () => {
  loading.value = true;

  try {
    const response = await fetch('https://formspree.io/f/mnjyraya', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify(form.value)
    });

    if (response.ok) {
      submitted.value = true;
    } else {
      alert('Something went wrong. Please try again.');
    }
  } catch (error) {
    alert('Failed to send message. Please check your connection.');
  } finally {
    loading.value = false;
  }
};

const resetForm = () => {
  form.value = { name: '', email: '', message: '' };
  submitted.value = false;
};

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('active');
      }
    });
  }, { threshold: 0.2 });

  observer.observe(document.querySelector('.contact-section'));
});
</script>

<style scoped>
.contact-section {
  padding: 120px 5% 120px;
  background: #0a0a0a;
  color: white;
  text-align: center;
  opacity: 0;
  transform: translateY(60px);
  transition: all 0.9s cubic-bezier(0.25, 0.1, 0.25, 1);
}

.contact-section.active {
  opacity: 1;
  transform: translateY(0);
}

.section-title {
  font-size: 48px;
  margin-bottom: 20px;
  font-family: "H7GBK-Heavy", sans-serif;
  text-transform: uppercase;
  letter-spacing: 3px;
}

.contact-text {
  font-size: 19px;
  max-width: 600px;
  margin: 0 auto 50px;
  opacity: 0.85;
}

.contact-form {
  max-width: 620px;
  margin: 0 auto;
  text-align: left;
}

.form-group {
  margin-bottom: 24px;
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 16px 20px;
  background: #1a1a1a;
  border: 2px solid #333;
  border-radius: 12px;
  color: white;
  font-size: 16px;
  transition: all 0.3s;
}

.form-group input:focus,
.form-group textarea:focus {
  border-color: #ffcc00;
  outline: none;
  box-shadow: 0 0 0 4px rgba(255, 204, 0, 0.1);
}

.submit-btn {
  width: 100%;
  padding: 18px;
  background: #ffcc00;
  color: #0a0a0a;
  border: none;
  border-radius: 12px;
  font-size: 18px;
  font-weight: bold;
  cursor: pointer;
  transition: all 0.4s;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.submit-btn:hover:not(:disabled) {
  background: white;
  transform: translateY(-3px);
}

.submit-btn:disabled {
  opacity: 0.7;
  cursor: not-allowed;
}

.success-message {
  background: rgba(255, 204, 0, 0.1);
  border: 2px solid #ffcc00;
  border-radius: 16px;
  padding: 40px 30px;
  text-align: center;
  max-width: 620px;
  margin: 0 auto;
  animation: popIn 0.5s ease;
}

.success-message h3 {
  color: #ffcc00;
  margin-bottom: 12px;
  font-size: 28px;
}

.reset-btn {
  margin-top: 20px;
  padding: 14px 32px;
  background: transparent;
  border: 2px solid #ffcc00;
  color: #ffcc00;
  border-radius: 50px;
  cursor: pointer;
  font-weight: bold;
}

.reset-btn:hover {
  background: #ffcc00;
  color: #0a0a0a;
}

.form-note {
  margin-top: 30px;
  font-size: 14px;
  opacity: 0.6;
}

@keyframes popIn {
  from { opacity: 0; transform: scale(0.8); }
  to { opacity: 1; transform: scale(1); }
}

/* ── Mobile ── */
@media (max-width: 768px) {
  .contact-section { padding: 90px 5% 80px; }
  .section-title { font-size: 32px; letter-spacing: 2px; }
  .contact-text { font-size: 16px; }
  .contact-form { padding: 0; }
}

@media (max-width: 480px) {
  .section-title { font-size: 26px; }
  .form-group input,
  .form-group textarea { font-size: 15px; padding: 14px 16px; }
  .submit-btn { font-size: 16px; padding: 15px; }
}
</style>