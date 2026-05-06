<template>
  <SpeedInsights />
  <div class="app">
    <!-- NAVBAR -->
    <header class="navbar" :class="{ scrolled: isScrolled }">
      <nav>
        <a href="#about" class="nav-link">About</a>
        <a href="#projects" class="nav-link">Projects</a>
        <a href="#skills" class="nav-link">Skills</a>
        <a href="#contact" class="nav-link">Contact</a>
      </nav>
    </header>

    <!-- HERO SECTION -->
    <section class="hero">
      <div class="hero-container">
        <div class="hero-image-wrapper">
          <img src="./assets/610897477_25515214761454604_9128693774218866743_n.jpg" alt="Chris" class="hero-image" @mouseover="isImageHovered = true" @mouseleave="isImageHovered = false" :class="{ hovered: isImageHovered }" />
        </div>
        
        <div class="hero-content">
          <h2 class="hero-title">Hi, I'm Chris 👋</h2>
          <p class="hero-subtitle">A Frontend Developer building modern web applications</p>

          <div class="buttons">
            <a href="#projects" class="btn primary">View Projects</a>
            <a href="#contact" class="btn">Contact Me</a>
          </div>
        </div>
      </div>
      
      <!-- Floating Animation Background -->
      <div class="floating-bg">
        <div class="float-circle float-circle-1"></div>
        <div class="float-circle float-circle-2"></div>
        <div class="float-circle float-circle-3"></div>
      </div>
    </section>

    <!-- ABOUT -->
    <section id="about" class="section fade-in-section">
      <h2>About Me</h2>
      <p>
        I am a passionate developer focused on building clean, fast, and responsive websites.
        I enjoy working with Vue, modern UI design, and backend systems.
      </p>
    </section>

    <!-- PROJECTS -->
    <section id="projects" class="section fade-in-section">
      <h2>Projects</h2>

      <div class="grid">
        <div class="card" v-for="(project, index) in projects" :key="index" @mouseenter="activeCard = index" @mouseleave="activeCard = null">
          <div class="card-inner" :class="{ active: activeCard === index }">
            <div class="card-icon">{{ project.icon }}</div>
            <h3>{{ project.title }}</h3>
            <p>{{ project.description }}</p>
            <a href="#" class="card-link">Learn More →</a>
          </div>
        </div>
      </div>
    </section>

    <!-- SKILLS -->
    <section id="skills" class="section fade-in-section">
      <h2>Skills</h2>

      <div class="skills">
        <span v-for="(skill, index) in skills" :key="index" class="skill-tag" :style="{ animationDelay: `${index * 0.1}s` }">
          {{ skill }}
        </span>
      </div>
    </section>

    <!-- CONTACT -->
    <section id="contact" class="section fade-in-section">
      <h2>Contact</h2>

      <form class="contact-form" @submit.prevent="submitForm">
        <div class="form-group">
          <input 
            v-model="form.name"
            type="text" 
            placeholder="Your Name" 
            class="form-input"
            required
          />
          <span v-if="form.name" class="input-label">Name</span>
        </div>
        
        <div class="form-group">
          <input 
            v-model="form.email"
            type="email" 
            placeholder="Your Email" 
            class="form-input"
            required
          />
          <span v-if="form.email" class="input-label">Email</span>
        </div>
        
        <div class="form-group">
          <textarea 
            v-model="form.message"
            placeholder="Your Message" 
            class="form-input"
            required
          ></textarea>
          <span v-if="form.message" class="input-label">Message</span>
        </div>
        
        <button type="submit" class="btn primary submit-btn">{{ formStatus || 'Send Message' }}</button>
      </form>
    </section>

    <!-- FOOTER -->
    <footer>
      <p>© 2026 Chris.dev | Built with Vue</p>
    </footer>
  </div>
</template>

<style>
/* RESET */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Arial, sans-serif;
}

body {
  scroll-behavior: smooth;
}

html {
  scroll-behavior: smooth;
}

.app {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
}

/* NAVBAR STYLES */
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  width: 100%;
  z-index: 1000;
  background: rgba(255, 255, 255, 0.9);
  backdrop-filter: blur(10px);
  padding: 1rem 2rem;
  box-shadow: 0 2px 0 rgba(0, 0, 0, 0.05);
  transition: all 0.3s ease;
}

.navbar.scrolled {
  background: rgba(255, 255, 255, 0.95);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  padding: 0.8rem 2rem;
}

@media (prefers-color-scheme: dark) {
  .navbar {
    background: rgba(22, 23, 29, 0.9);
  }
  .navbar.scrolled {
    background: rgba(22, 23, 29, 0.95);
  }
}

nav {
  display: flex;
  gap: 2rem;
  justify-content: center;
  align-items: center;
  max-width: 1200px;
  margin: 0 auto;
}

.nav-link {
  text-decoration: none;
  color: var(--text-h);
  font-weight: 500;
  position: relative;
  transition: color 0.3s ease;
  padding: 0.5rem 0;
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 0;
  height: 2px;
  background: var(--accent);
  transition: width 0.3s ease;
}

.nav-link:hover {
  color: var(--accent);
}

.nav-link:hover::after {
  width: 100%;
}

/* HERO SECTION */
.hero {
  position: relative;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  overflow: hidden;
  padding: 4rem 2rem;
  text-align: center;
}

.hero-container {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 3rem;
  position: relative;
  z-index: 10;
  max-width: 1000px;
  width: 100%;
  flex-wrap: wrap;
}

.hero-image-wrapper {
  position: relative;
  flex: 1;
  min-width: 250px;
  max-width: 400px;
  animation: fadeInLeft 1s ease 0.2s both;
}

.hero-image {
  width: 100%;
  height: auto;
  border-radius: 20px;
  cursor: pointer;
  transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
  filter: brightness(0.6) contrast(1.1);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
}

.hero-image:hover,
.hero-image.hovered {
  filter: brightness(1) contrast(1);
  box-shadow: 0 30px 60px rgba(170, 59, 255, 0.2);
  transform: scale(1.05);
}

@keyframes fadeInLeft {
  from {
    opacity: 0;
    transform: translateX(-50px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

.hero-content {
  position: relative;
  z-index: 10;
  animation: fadeInUp 1s ease 0.2s both;
  flex: 1;
  min-width: 250px;
}

.hero-title {
  font-size: 4rem;
  margin-bottom: 1rem;
  color: var(--text-h);
  font-weight: 700;
  letter-spacing: -2px;
}

.hero-subtitle {
  font-size: 1.5rem;
  color: var(--text);
  margin-bottom: 2rem;
  font-weight: 300;
}

.floating-bg {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 0;
  overflow: hidden;
}

.float-circle {
  position: absolute;
  border-radius: 50%;
  opacity: 0.1;
  animation: float 6s ease-in-out infinite;
}

.float-circle-1 {
  width: 300px;
  height: 300px;
  background: var(--accent);
  top: 10%;
  left: 10%;
  animation-delay: 0s;
}

.float-circle-2 {
  width: 200px;
  height: 200px;
  background: var(--accent);
  bottom: 20%;
  right: 15%;
  animation-delay: 2s;
}

.float-circle-3 {
  width: 250px;
  height: 250px;
  background: var(--accent);
  top: 50%;
  right: 10%;
  animation-delay: 4s;
}

@keyframes float {
  0%, 100% {
    transform: translateY(0px);
  }
  50% {
    transform: translateY(30px);
  }
}

/* BUTTONS */
.buttons {
  display: flex;
  gap: 1rem;
  justify-content: center;
  flex-wrap: wrap;
  margin-top: 2rem;
}

.btn {
  padding: 0.875rem 2rem;
  border-radius: 50px;
  border: 2px solid var(--accent);
  background: transparent;
  color: var(--accent);
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  text-decoration: none;
  transition: all 0.3s ease;
  display: inline-block;
  position: relative;
  overflow: hidden;
}

.btn::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: var(--accent);
  transition: left 0.3s ease;
  z-index: -1;
}

.btn:hover {
  color: var(--bg);
  transform: translateY(-2px);
  box-shadow: 0 8px 16px rgba(170, 59, 255, 0.3);
}

.btn:hover::before {
  left: 0;
}

.btn.primary {
  background: var(--accent);
  color: white;
}

.btn.primary::before {
  background: linear-gradient(135deg, var(--accent), #c084fc);
}

/* SECTION STYLES */
.section {
  padding: 6rem 2rem;
  max-width: 1200px;
  margin: 0 auto;
}

.section h2 {
  font-size: 2.5rem;
  text-align: center;
  margin-bottom: 3rem;
  color: var(--text-h);
}

.fade-in-section {
  opacity: 0;
  animation: fadeInUp 0.8s ease forwards;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* GRID & CARDS */
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 2rem;
  margin-bottom: 2rem;
}

.card {
  border-radius: 12px;
  border: 1px solid var(--border);
  padding: 2rem;
  cursor: pointer;
  transition: all 0.3s ease;
  background: var(--bg);
  overflow: hidden;
  position: relative;
}

.card::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.1), transparent);
  transition: left 0.5s ease;
}

.card:hover {
  border-color: var(--accent);
  box-shadow: 0 12px 24px rgba(0, 0, 0, 0.15);
  transform: translateY(-8px);
}

.card:hover::before {
  left: 100%;
}

.card-inner {
  position: relative;
  z-index: 1;
}

.card-icon {
  font-size: 3rem;
  margin-bottom: 1rem;
}

.card h3 {
  font-size: 1.3rem;
  margin-bottom: 0.8rem;
  color: var(--text-h);
  transition: color 0.3s ease;
}

.card p {
  color: var(--text);
  margin-bottom: 1.5rem;
  line-height: 1.6;
}

.card-link {
  color: var(--accent);
  text-decoration: none;
  font-weight: 600;
  transition: all 0.3s ease;
  display: inline-block;
}

.card-link:hover {
  transform: translateX(4px);
}

.card.active h3 {
  color: var(--accent);
}

/* SKILLS SECTION */
.skills {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  justify-content: center;
  max-width: 800px;
  margin: 0 auto;
}

.skill-tag {
  padding: 0.75rem 1.5rem;
  border-radius: 50px;
  border: 2px solid var(--accent);
  color: var(--accent);
  font-weight: 600;
  transition: all 0.3s ease;
  cursor: default;
  animation: slideUp 0.5s ease forwards;
  opacity: 0;
}

@keyframes slideUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.skill-tag:hover {
  background: var(--accent);
  color: white;
  transform: scale(1.05);
}

/* CONTACT FORM */
.contact-form {
  max-width: 600px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.form-group {
  position: relative;
}

.form-input {
  width: 100%;
  padding: 1rem;
  border: 2px solid var(--border);
  border-radius: 8px;
  font-size: 1rem;
  background: var(--bg);
  color: var(--text-h);
  transition: all 0.3s ease;
  font-family: inherit;
}

.form-input::placeholder {
  color: var(--text);
  opacity: 0.7;
}

.form-input:focus {
  outline: none;
  border-color: var(--accent);
  box-shadow: 0 0 0 3px var(--accent-bg);
}

.form-input:valid {
  border-color: #10b981;
}

.input-label {
  position: absolute;
  top: -1.5rem;
  left: 1rem;
  font-size: 0.875rem;
  color: var(--accent);
  font-weight: 600;
  animation: slideDown 0.3s ease;
}

@keyframes slideDown {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.submit-btn {
  margin-top: 1rem;
}

/* FOOTER */
footer {
  text-align: center;
  padding: 2rem;
  border-top: 1px solid var(--border);
  color: var(--text);
  margin-top: 4rem;
}

/* RESPONSIVE */
@media (max-width: 768px) {
  .hero-container {
    flex-direction: column;
    gap: 2rem;
  }

  .hero-image-wrapper {
    max-width: 300px;
  }

  .hero-title {
    font-size: 2.5rem;
  }
  
  .hero-subtitle {
    font-size: 1.1rem;
  }

  .section h2 {
    font-size: 1.8rem;
  }

  nav {
    gap: 1rem;
  }

  .nav-link {
    font-size: 0.9rem;
  }

  .buttons {
    flex-direction: column;
  }

  .btn {
    width: 100%;
  }
}

</style>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { SpeedInsights } from '@vercel/speed-insights/vue';

const isScrolled = ref(false)
const activeCard = ref(null)
const formStatus = ref('')
const isImageHovered = ref(false)

const projects = ref([
  {
    title: 'Movie Streaming Website',
    description: 'Built with Vue + API integration',
    icon: '🎬'
  },
  {
    title: 'Lead Generation Website',
    description: 'SEO-focused landing page for business leads',
    icon: '📱'
  },
  {
    title: 'Inventory System',
    description: 'Full-stack system with Vue + Flask + MySQL',
    icon: '📦'
  }
])

const skills = ref([
  'Vue.js',
  'Vite',
  'JavaScript',
  'Tailwind CSS',
  'Node.js',
  'MySQL',
  'Github'
])

const form = ref({
  name: '',
  email: '',
  message: ''
})

// Scroll event listener
const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
  
  // Fade in sections on scroll
  document.querySelectorAll('.fade-in-section').forEach(section => {
    const rect = section.getBoundingClientRect()
    const isVisible = rect.top < window.innerHeight * 0.75
    
    if (isVisible) {
      section.style.opacity = '1'
    }
  })
}

// Form submission
const submitForm = async () => {
  if (!form.value.name || !form.value.email || !form.value.message) {
    formStatus.value = '❌ Please fill all fields'
    setTimeout(() => {
      formStatus.value = ''
    }, 3000)
    return
  }

  formStatus.value = 'Sending...'

  // Simulate sending
  setTimeout(() => {
    formStatus.value = '✅ Message sent! Thanks!'
    form.value = { name: '', email: '', message: '' }
    
    setTimeout(() => {
      formStatus.value = ''
    }, 3000)
  }, 1000)
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
  
  // Initial animation trigger
  handleScroll()
  
  // Stagger animations for cards on load
  document.querySelectorAll('.card').forEach((card, index) => {
    card.style.animation = `fadeInUp 0.6s ease ${0.1 * index}s both`
  })
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>