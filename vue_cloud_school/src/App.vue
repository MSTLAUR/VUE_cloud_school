<!-- App.vue -->
<template>
  <div class="app">
    <!-- Hero Section -->
    <header class="hero">
      <nav class="nav-container">
        <div class="logo-container">
          <div class="cyber-logo">
            <span class="logo-cloud">☁️</span>
            <span class="logo-text">Piano CRM</span>
          </div>
        </div>
        <div class="nav-links">
          <a href="#features">Features</a>
          <a href="#feedback">Feedback</a>
        </div>
      </nav>
      
      <div class="hero-content">
        <h1>Transform Your Piano Teaching Business</h1>
        <p class="hero-subtitle">The all-in-one CRM designed specifically for piano teachers</p>
        
        <div class="waitlist-form">
          <h3>Join the Waiting List</h3>
          <form @submit.prevent="handleSubmit">
            <input 
              type="email" 
              v-model="email" 
              placeholder="Enter your email" 
              required
            >
            <button type="submit" class="cta-button">
              Get Early Access
            </button>
          </form>
          <div class="social-proof">
            <p>🎹 Join {{ waitlistCount }}+ piano teachers already on the waiting list</p>
            <div class="teacher-avatars">
              <div v-for="n in 5" :key="n" class="avatar"></div>
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- Features Section -->
    <section id="features" class="features">
      <h2>Upcoming Features</h2>
      <div class="feature-grid">
        <div v-for="feature in features" :key="feature.title" class="feature-card">
          <div class="feature-icon">{{ feature.icon }}</div>
          <h3>{{ feature.title }}</h3>
          <p>{{ feature.description }}</p>
        </div>
      </div>
    </section>

    <!-- Feedback Section -->
    <section id="feedback" class="feedback">
      <h2>Help Shape the Future</h2>
      <p>Which features would you like to see?</p>
      
      <div class="feedback-options">
        <div class="option-cards">
          <div 
            v-for="option in predefinedOptions" 
            :key="option.id" 
            class="option-card"
            :class="{ 'selected': selectedFeature === option.value }"
          >
            <input 
              type="radio" 
              :id="option.id" 
              name="feature" 
              :value="option.value"
              v-model="selectedFeature"
            >
            <label :for="option.id">{{ option.label }}</label>
          </div>
        </div>
        
        <div class="custom-feature">
          <h3>Have another idea?</h3>
          <textarea 
            v-model="customFeedback"
            placeholder="Tell us what feature you'd love to see..." 
            rows="3"
          ></textarea>
          <button @click="submitFeedback" class="submit-feedback">
            Submit Feedback
          </button>
        </div>
      </div>
    </section>

    <footer class="footer">
      <div class="footer-content">
        <div class="cyber-logo small">
          <span class="logo-cloud">☁️</span>
          <span class="logo-text">Piano CRM</span>
        </div>
        <p>© {{ currentYear }} Piano Teacher CRM. All rights reserved.</p>
      </div>
    </footer>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      email: '',
      waitlistCount: 200,
      selectedFeature: '',
      customFeedback: '',
      currentYear: new Date().getFullYear(),
      features: [
        {
          icon: '📚',
          title: 'Course Creation',
          description: 'Instantly create and manage subscription-based courses for your students'
        },
        {
          icon: '💳',
          title: 'Automated Billing',
          description: 'Say goodbye to payment tracking - automated billing handles everything'
        },
        {
          icon: '🎵',
          title: 'Digital Products',
          description: 'Create and sell specialized courses with video content and PDFs'
        },
        {
          icon: '💬',
          title: 'Student Communication',
          description: 'Easy messaging system for schedule changes and updates'
        },
        {
          icon: '📊',
          title: 'Financial Tracking',
          description: 'Monitor your income and expenses in one place'
        }
      ],
      predefinedOptions: [
        { id: 'opt1', value: 'scheduling', label: 'Automated Scheduling' },
        { id: 'opt2', value: 'payments', label: 'Payment Processing' },
        { id: 'opt3', value: 'lessons', label: 'Online Lessons Integration' },
        { id: 'opt4', value: 'progress', label: 'Student Progress Tracking' }
      ]
    }
  },
  methods: {
    handleSubmit() {
      console.log('Email submitted:', this.email)
      alert('Thank you for joining our waitlist!')
      this.email = ''
    },
    submitFeedback() {
      console.log('Feedback:', {
        selectedFeature: this.selectedFeature,
        customFeedback: this.customFeedback
      })
      alert('Thank you for your feedback!')
      this.selectedFeature = ''
      this.customFeedback = ''
    }
  }
}
</script>

<style>
/* Reset and base styles */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

:root {
  --mint: #63F6C8;
  --purple: #B76EF5;
  --dark-bg: #1A1B26;
  --card-bg: #252632;
  --text-primary: #FFFFFF;
  --text-secondary: rgba(255, 255, 255, 0.7);
  --accent-gradient: linear-gradient(135deg, var(--mint), var(--purple));
}

body {
  font-family: 'Inter', sans-serif;
  line-height: 1.6;
  color: var(--text-primary);
  background: var(--dark-bg);
}

.app {
  min-height: 100vh;
  background: url("data:image/svg+xml,%3Csvg width='60' height='60' viewBox='0 0 60 60' xmlns='http://www.w3.org/2000/svg'%3E%3Cg fill='none' fill-rule='evenodd'%3E%3Cg fill='%23ffffff' fill-opacity='0.05'%3E%3Cpath d='M36 34v-4h-2v4h-4v2h4v4h2v-4h4v-2h-4zm0-30V0h-2v4h-4v2h4v4h2V6h4V4h-4zM6 34v-4H4v4H0v2h4v4h2v-4h4v-2H6zM6 4V0H4v4H0v2h4v4h2V6h4V4H6z'/%3E%3C/g%3E%3C/g%3E%3C/svg%3E");
}

/* Navigation */
.nav-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1.5rem 2rem;
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  z-index: 10;
  backdrop-filter: blur(10px);
}

.cyber-logo {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-weight: 700;
  font-size: 1.5rem;
  background: var(--accent-gradient);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.cyber-logo.small {
  font-size: 1.2rem;
}

.nav-links a {
  color: var(--text-primary);
  text-decoration: none;
  margin-left: 2rem;
  font-weight: 500;
  position: relative;
}

.nav-links a::after {
  content: '';
  position: absolute;
  width: 0;
  height: 2px;
  bottom: -4px;
  left: 0;
  background: var(--accent-gradient);
  transition: width 0.3s;
}

.nav-links a:hover::after {
  width: 100%;
}

/* Hero Section */
.hero {
  background: var(--dark-bg);
  color: var(--text-primary);
  padding: 8rem 2rem 6rem;
  text-align: center;
  position: relative;
  overflow: hidden;
}

.hero::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 1px;
  background: var(--accent-gradient);
}

.hero-content {
  max-width: 800px;
  margin: 0 auto;
}

.hero h1 {
  font-size: 3.5rem;
  margin-bottom: 1.5rem;
  background: var(--accent-gradient);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.hero-subtitle {
  font-size: 1.5rem;
  color: var(--text-secondary);
  margin-bottom: 3rem;
}

/* Waitlist Form */
.waitlist-form {
  background: var(--card-bg);
  padding: 2rem;
  border-radius: 12px;
  border: 1px solid rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  max-width: 500px;
  margin: 0 auto;
}

.waitlist-form h3 {
  margin-bottom: 1.5rem;
  color: var(--mint);
}

.waitlist-form form {
  display: flex;
  gap: 1rem;
  margin-bottom: 1.5rem;
}

.waitlist-form input {
  flex: 1;
  padding: 0.8rem 1rem;
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 6px;
  font-size: 1rem;
  background: rgba(255, 255, 255, 0.05);
  color: var(--text-primary);
}

.waitlist-form input:focus {
  outline: none;
  border-color: var(--mint);
}

.cta-button {
  background: var(--accent-gradient);
  color: var(--text-primary);
  border: none;
  padding: 0.8rem 1.5rem;
  border-radius: 6px;
  font-weight: 600;
  cursor: pointer;
  transition: transform 0.3s, box-shadow 0.3s;
}

.cta-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(99, 246, 200, 0.2);
}

/* Features Section */
.features {
  padding: 6rem 2rem;
  background: var(--card-bg);
  position: relative;
}

.features::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 1px;
  background: var(--accent-gradient);
}

.features h2 {
  text-align: center;
  margin-bottom: 3rem;
  font-size: 2.5rem;
  background: var(--accent-gradient);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.feature-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
  max-width: 1200px;
  margin: 0 auto;
}

.feature-card {
  background: var(--dark-bg);
  padding: 2rem;
  border-radius: 12px;
  text-align: center;
  border: 1px solid rgba(255, 255, 255, 0.1);
  transition: transform 0.3s;
}

.feature-card:hover {
  transform: translateY(-5px);
}

.feature-icon {
  font-size: 2.5rem;
  margin-bottom: 1rem;
}

.feature-card h3 {
  color: var(--mint);
  margin-bottom: 1rem;
}

/* Feedback Section */
.feedback {
  padding: 6rem 2rem;
  text-align: center;
  background: var(--dark-bg);
}

.feedback h2 {
  font-size: 2.5rem;
  margin-bottom: 1rem;
  background: var(--accent-gradient);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.option-cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1rem;
  max-width: 800px;
  margin: 2rem auto;
}

.option-card {
  background: var(--card-bg);
  padding: 1rem;
  border-radius: 8px;
  cursor: pointer;
  border: 1px solid rgba(255, 255, 255, 0.1);
  transition: border-color 0.3s;
}

.option-card.selected {
  border-color: var(--mint);
}

.option-card:hover {
  border-color: var(--purple);
}

.custom-feature {
  max-width: 600px;
  margin: 3rem auto;
}

.custom-feature textarea {
  width: 100%;
  padding: 1rem;
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 8px;
  margin: 1rem 0;
  background: var(--card-bg);
  color: var(--text-primary);
  font-family: inherit;
}

.submit-feedback {
  background: var(--mint);
  color: var(--dark-bg);
  border: none;
  padding: 0.8rem 1.5rem;
  border-radius: 6px;
  cursor: pointer;
  font-weight: 600;
  transition: transform 0.3s;
}

.submit-feedback {
  background: #1a237e;
  color: white;
  border: none;
  padding: 0.8rem 1.5rem;
  border-radius: 6px;
  cursor: pointer;
}

/* Footer */
.footer {
  background: #1a237e;
  color: white;
  padding: 2rem;
  text-align: center;
}

.footer-logo {
  height: 30px;
  margin-bottom: 1rem;
}

/* Responsive Design */
@media (max-width: 768px) {
  .hero h1 {
    font-size: 2.5rem;
  }
  
  .waitlist-form form {
    flex-direction: column;
  }
  
  .feature-grid {
    grid-template-columns: 1fr;
  }
}

/* Social Proof */
.social-proof {
  margin-top: 2rem;
}

.teacher-avatars {
  display: flex;
  justify-content: center;
  gap: 0.5rem;
  margin-top: 1rem;
}

.avatar {
  width: 30px;
  height: 30px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.2);
  border: 2px solid white;
}
</style>