<template>
  <SpeedInsights />
  <div class="app">
    <!-- Skip to Main Content (Accessibility) -->
    <a href="#main-content" class="skip-link">Skip to main content</a>
    
    <!-- NAVBAR -->
    <header class="navbar" role="banner" :class="{ scrolled: isScrolled }">
      <nav role="navigation" aria-label="Main navigation">
        <a href="#about" class="nav-link">About</a>
        <a href="#projects" class="nav-link">Projects</a>
        <a href="#skills" class="nav-link">Skills</a>
        <a href="#contact" class="nav-link">Contact</a>
      </nav>
    </header>

    <!-- HERO SECTION -->
    <section class="hero" role="region" aria-label="Hero section">
      <div class="hero-container">
        <div class="hero-image-wrapper">
          <img 
            src="./assets/610897477_25515214761454604_9128693774218866743_n.jpg" 
            alt="Chris - Frontend Developer" 
            class="hero-image" 
            @mouseover="isImageHovered = true" 
            @mouseleave="isImageHovered = false" 
            :class="{ hovered: isImageHovered }"
            loading="lazy"
          />
          <div class="image-overlay"></div>
        </div>
        
        <div class="hero-content">
          <h1 class="hero-title">Hi, I'm Christoper 👋</h1>
          <p class="hero-subtitle">A Frontend Developer building modern web applications</p>
          <p class="hero-description">Specializing in Vue.js, responsive design, and user-friendly interfaces</p>

          <div class="buttons">
            <a href="#projects" class="btn primary" role="button">View Projects</a>
            <a href="#contact" class="btn secondary" role="button">Contact Me</a>
          </div>
        </div>
      </div>
      
      <!-- Floating Animation Background -->
      <div class="floating-bg" aria-hidden="true">
        <div class="float-circle float-circle-1"></div>
        <div class="float-circle float-circle-2"></div>
        <div class="float-circle float-circle-3"></div>
      </div>
    </section>

    <!-- ABOUT -->
    <section id="about" class="section fade-in-section" role="region" aria-labelledby="about-heading">
      <h2 id="about-heading">About Me</h2>
      <div class="about-content">
        <p>
          I am a passionate developer focused on building clean, fast, and responsive websites.
          I enjoy working with Vue, modern UI design, and backend systems.
        </p>
        <div class="about-stats">
          <div class="stat" v-for="stat in stats" :key="stat.label">
            <span class="stat-number">{{ stat.number }}</span>
            <span class="stat-label">{{ stat.label }}</span>
          </div>
        </div>
      </div>
    </section>

    <!-- PROJECTS -->
    <section id="projects" class="section fade-in-section" role="region" aria-labelledby="projects-heading">
      <h2 id="projects-heading">Featured Projects</h2>
      <p class="section-subtitle">Here are some of my recent works</p>

      <div class="grid">
        <article 
          class="card" 
          v-for="(project, index) in projects" 
          :key="index" 
          @mouseenter="activeCard = index" 
          @mouseleave="activeCard = null"
          role="article"
        >
          <div class="card-image">
            <div class="card-placeholder" :style="{ background: project.color }">
              {{ project.icon }}
            </div>
          </div>
          <div class="card-inner" :class="{ active: activeCard === index }">
            <h3>{{ project.title }}</h3>
            <p>{{ project.description }}</p>
            <div class="project-tags">
              <span v-for="tech in project.tech" :key="tech" class="tech-tag">{{ tech }}</span>
            </div>
            <a href="#" class="card-link" @click.prevent>Learn More →</a>
          </div>
        </article>
      </div>
    </section>

    <!-- SKILLS -->
    <section id="skills" class="section fade-in-section" role="region" aria-labelledby="skills-heading">
      <h2 id="skills-heading">Technical Skills</h2>
      <p class="section-subtitle">Technologies I work with</p>

      <div class="skills-container">
        <div class="skill-category" v-for="category in skillCategories" :key="category.name">
          <h3>{{ category.name }}</h3>
          <div class="skills">
            <span 
              v-for="(skill, index) in category.items" 
              :key="skill" 
              class="skill-tag" 
              :style="{ animationDelay: `${index * 0.05}s` }">
              {{ skill }}
            </span>
          </div>
        </div>
      </div>
    </section>

    <!-- PORTFOLIO SHOWCASE -->
    <section class="showcase-section fade-in-section" role="region" aria-labelledby="showcase-heading">
      <h2 id="showcase-heading">Portfolio Showcase</h2>
      <p class="section-subtitle">Interactive gallery of my work</p>
      
      <div class="showcase-grid">
        <div class="showcase-item" v-for="(item, index) in showcaseItems" :key="index" @click="activeShowcase = index">
          <div class="showcase-image" :class="{ active: activeShowcase === index }">
            <div class="showcase-icon">{{ item.icon }}</div>
            <p>{{ item.title }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- CONTACT -->
    <section id="contact" class="section fade-in-section" role="region" aria-labelledby="contact-heading">
      <h2 id="contact-heading">Get In Touch</h2>
      <p class="section-subtitle">Let's create something amazing together</p>

      <form class="contact-form" @submit.prevent="submitForm" novalidate>
        <div class="form-group">
          <label for="name" class="form-label">Name</label>
          <input 
            id="name"
            v-model="form.name"
            type="text" 
            placeholder="Your Name" 
            class="form-input"
            required
            aria-required="true"
          />
          <span v-if="form.name" class="input-label">{{ form.name }}</span>
        </div>
        
        <div class="form-group">
          <label for="email" class="form-label">Email</label>
          <input 
            id="email"
            v-model="form.email"
            type="email" 
            placeholder="your.email@example.com" 
            class="form-input"
            required
            aria-required="true"
          />
          <span v-if="form.email" class="input-label">{{ form.email }}</span>
        </div>
        
        <div class="form-group">
          <label for="message" class="form-label">Message</label>
          <textarea 
            id="message"
            v-model="form.message"
            placeholder="Tell me about your project" 
            class="form-input"
            rows="5"
            required
            aria-required="true"
          ></textarea>
          <span v-if="form.message" class="input-label">Message received</span>
        </div>
        
        <button type="submit" class="btn primary submit-btn" :disabled="formStatus.includes('Sending')">
          {{ formStatus || 'Send Message' }}
        </button>
      </form>
    </section>

    <!-- FOOTER -->
    <footer role="contentinfo">
      <div class="footer-content">
        <p>&copy; 2026 Chris.dev | Frontend Developer</p>
        <p>Built with <span class="heart">❤️</span> using Vue & Vite</p>
        <div class="footer-links">
          <a href="#" aria-label="GitHub">GitHub</a>
          <a href="#" aria-label="LinkedIn">LinkedIn</a>
          <a href="#" aria-label="Twitter">Twitter</a>
        </div>
      </div>
    </footer>
  </div>
</template>

<style>
/* RESET & BASE */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  scroll-behavior: smooth;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
}

html {
  scroll-behavior: smooth;
}

/* Skip Link (Accessibility) */
.skip-link {
  position: absolute;
  top: -40px;
  left: 0;
  background: var(--accent);
  color: white;
  padding: 8px;
  text-decoration: none;
  z-index: 100;
}

.skip-link:focus {
  top: 0;
}

.app {
  width: 100%;
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
  background: rgba(255, 255, 255, 0.85);
  backdrop-filter: blur(10px);
  padding: 1rem 2rem;
  box-shadow: none;
  transition: all 0.3s ease;
}

.navbar.scrolled {
  background: rgba(255, 255, 255, 0.95);
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  padding: 0.8rem 2rem;
}

@media (prefers-color-scheme: dark) {
  .navbar {
    background: rgba(22, 23, 29, 0.85);
  }
  .navbar.scrolled {
    background: rgba(22, 23, 29, 0.95);
  }
}

nav {
  display: flex;
  gap: 3rem;
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
  font-size: 0.95rem;
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: -5px;
  left: 0;
  width: 0;
  height: 2px;
  background: linear-gradient(90deg, var(--accent), #c084fc);
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
  padding: 6rem 2rem 4rem;
  margin-top: 3rem;
}

.hero-container {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 4rem;
  position: relative;
  z-index: 10;
  max-width: 1200px;
  width: 100%;
  flex-wrap: wrap;
}

.hero-image-wrapper {
  position: relative;
  flex: 0 1 350px;
  animation: fadeInLeft 1s ease 0.2s both;
}

.hero-image {
  width: 100%;
  height: auto;
  border-radius: 20px;
  cursor: pointer;
  transition: all 0.5s cubic-bezier(0.25, 0.46, 0.45, 0.94);
  filter: brightness(0.65) contrast(1.1);
  box-shadow: 0 25px 50px rgba(0, 0, 0, 0.25);
  display: block;
}

.image-overlay {
  position: absolute;
  inset: 0;
  border-radius: 20px;
  background: radial-gradient(circle at 30% 30%, rgba(170, 59, 255, 0.15), transparent);
  opacity: 0;
  transition: opacity 0.5s ease;
  pointer-events: none;
}

.hero-image:hover,
.hero-image.hovered {
  filter: brightness(1) contrast(1.1);
  box-shadow: 0 35px 70px rgba(170, 59, 255, 0.3);
  transform: scale(1.03) translateY(-5px);
}

.hero-image:hover ~ .image-overlay,
.hero-image.hovered ~ .image-overlay {
  opacity: 1;
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
  animation: fadeInUp 1s ease 0.3s both;
  flex: 1;
  min-width: 280px;
}

.hero-title {
  font-size: 3.5rem;
  margin-bottom: 1rem;
  color: var(--text-h);
  font-weight: 800;
  letter-spacing: -1.5px;
  line-height: 1.2;
}

.hero-subtitle {
  font-size: 1.5rem;
  color: var(--text);
  margin-bottom: 0.5rem;
  font-weight: 600;
}

.hero-description {
  font-size: 1rem;
  color: var(--text);
  margin-bottom: 2.5rem;
  line-height: 1.6;
  opacity: 0.85;
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
  opacity: 0.08;
  animation: float 8s ease-in-out infinite;
  filter: blur(40px);
}

.float-circle-1 {
  width: 400px;
  height: 400px;
  background: var(--accent);
  top: 0%;
  left: -5%;
  animation-delay: 0s;
}

.float-circle-2 {
  width: 250px;
  height: 250px;
  background: var(--accent);
  bottom: 10%;
  right: 5%;
  animation-delay: 2.5s;
}

.float-circle-3 {
  width: 300px;
  height: 300px;
  background: var(--accent);
  top: 30%;
  right: -50px;
  animation-delay: 5s;
}

@keyframes float {
  0%, 100% {
    transform: translateY(0px);
  }
  50% {
    transform: translateY(40px);
  }
}

/* BUTTONS */
.buttons {
  display: flex;
  gap: 1.5rem;
  justify-content: flex-start;
  flex-wrap: wrap;
}

.btn {
  padding: 1rem 2.5rem;
  border-radius: 50px;
  border: 2px solid var(--accent);
  background: transparent;
  color: var(--accent);
  font-size: 1rem;
  font-weight: 700;
  cursor: pointer;
  text-decoration: none;
  transition: all 0.3s ease;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  position: relative;
  overflow: hidden;
  white-space: nowrap;
}

.btn:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

.btn::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: var(--accent);
  transition: left 0.4s cubic-bezier(0.34, 1.56, 0.64, 1);
  z-index: -1;
}

.btn:hover:not(:disabled) {
  color: var(--bg);
  transform: translateY(-3px);
  box-shadow: 0 12px 24px rgba(170, 59, 255, 0.35);
}

.btn:hover:not(:disabled)::before {
  left: 0;
}

.btn.primary {
  background: var(--accent);
  color: white;
}

.btn.secondary {
  border: 2px solid var(--accent);
  color: var(--accent);
}

.btn.primary::before {
  background: linear-gradient(135deg, var(--accent), #c084fc);
}

/* SECTION STYLES */
.section {
  padding: 7rem 2rem;
  max-width: 1200px;
  margin: 0 auto;
  position: relative;
}

.section h2 {
  font-size: 3rem;
  text-align: center;
  margin-bottom: 1rem;
  color: var(--text-h);
  font-weight: 800;
  letter-spacing: -1px;
}

.section-subtitle {
  text-align: center;
  font-size: 1.1rem;
  color: var(--text);
  margin-bottom: 3rem;
  opacity: 0.9;
}

.fade-in-section {
  opacity: 0;
  animation: fadeInUp 0.8s ease forwards;
}

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(40px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* ABOUT SECTION */
.about-content {
  max-width: 800px;
  margin: 0 auto;
}

.about-content p {
  font-size: 1.1rem;
  line-height: 1.8;
  color: var(--text);
  margin-bottom: 3rem;
  text-align: center;
}

.about-stats {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  gap: 2rem;
  margin-top: 3rem;
}

.stat {
  text-align: center;
  padding: 2rem;
  border: 2px solid var(--border);
  border-radius: 12px;
  transition: all 0.3s ease;
  background: var(--bg);
}

.stat:hover {
  border-color: var(--accent);
  transform: translateY(-5px);
  box-shadow: 0 10px 25px rgba(170, 59, 255, 0.1);
}

.stat-number {
  display: block;
  font-size: 2.5rem;
  font-weight: 800;
  color: var(--accent);
  margin-bottom: 0.5rem;
}

.stat-label {
  display: block;
  color: var(--text);
  font-weight: 600;
}

/* GRID & CARDS */
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
  margin-bottom: 2rem;
}

.card {
  border-radius: 16px;
  border: 1px solid var(--border);
  padding: 0;
  cursor: pointer;
  transition: all 0.4s ease;
  background: var(--bg);
  overflow: hidden;
  position: relative;
  display: flex;
  flex-direction: column;
}

.card-image {
  width: 100%;
  height: 200px;
  overflow: hidden;
  background: linear-gradient(135deg, var(--border), var(--accent-bg));
}

.card-placeholder {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 4rem;
  transition: transform 0.4s ease;
}

.card:hover .card-placeholder {
  transform: scale(1.1);
}

.card-inner {
  padding: 2rem;
  flex: 1;
  display: flex;
  flex-direction: column;
}

.card h3 {
  font-size: 1.5rem;
  margin-bottom: 0.8rem;
  color: var(--text-h);
  transition: color 0.3s ease;
  font-weight: 700;
}

.card p {
  color: var(--text);
  margin-bottom: 1rem;
  line-height: 1.6;
  flex: 1;
}

.project-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 1.5rem;
}

.tech-tag {
  padding: 0.4rem 0.8rem;
  border-radius: 20px;
  background: var(--accent-bg);
  color: var(--accent);
  font-size: 0.85rem;
  font-weight: 600;
}

.card-link {
  color: var(--accent);
  text-decoration: none;
  font-weight: 700;
  transition: all 0.3s ease;
  display: inline-flex;
  gap: 0.3rem;
  align-self: flex-start;
}

.card-link:hover {
  transform: translateX(5px);
}

.card:hover {
  border-color: var(--accent);
  box-shadow: 0 16px 40px rgba(0, 0, 0, 0.1);
  transform: translateY(-8px);
}

.card.active h3 {
  color: var(--accent);
}

/* SKILLS SECTION */
.skills-container {
  max-width: 1000px;
  margin: 0 auto;
}

.skill-category {
  margin-bottom: 3rem;
}

.skill-category h3 {
  font-size: 1.3rem;
  color: var(--text-h);
  margin-bottom: 1.5rem;
  font-weight: 700;
}

.skills {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  justify-content: center;
}

.skill-tag {
  padding: 0.8rem 1.8rem;
  border-radius: 50px;
  border: 2px solid var(--accent);
  color: var(--accent);
  font-weight: 700;
  transition: all 0.3s ease;
  cursor: default;
  animation: slideUp 0.6s ease forwards;
  opacity: 0;
  background: transparent;
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
  transform: scale(1.1) translateY(-2px);
  box-shadow: 0 8px 16px rgba(170, 59, 255, 0.3);
}

/* SHOWCASE SECTION */
.showcase-section {
  padding: 7rem 2rem;
  background: linear-gradient(135deg, var(--accent-bg), transparent);
  border-radius: 20px;
  margin: 4rem 2rem;
}

.showcase-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 2rem;
  max-width: 1200px;
  margin: 0 auto;
}

.showcase-item {
  cursor: pointer;
  transition: all 0.3s ease;
}

.showcase-image {
  width: 100%;
  height: 250px;
  border-radius: 16px;
  background: linear-gradient(135deg, var(--accent), #c084fc);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 1rem;
  transition: all 0.4s cubic-bezier(0.34, 1.56, 0.64, 1);
  border: 2px solid transparent;
  color: white;
  position: relative;
  overflow: hidden;
}

.showcase-image::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(45deg, transparent 30%, rgba(255, 255, 255, 0.2), transparent 70%);
  transform: translateX(-100%);
  transition: transform 0.6s ease;
}

.showcase-image:hover::before {
  transform: translateX(100%);
}

.showcase-icon {
  font-size: 3.5rem;
  transition: transform 0.4s ease;
}

.showcase-image p {
  font-weight: 700;
  font-size: 1.1rem;
  transition: transform 0.4s ease;
}

.showcase-item:hover .showcase-image {
  transform: translateY(-10px) scale(1.02);
  box-shadow: 0 20px 40px rgba(170, 59, 255, 0.3);
}

.showcase-item:hover .showcase-icon {
  transform: scale(1.2) rotate(10deg);
}

.showcase-item:hover .showcase-image.active {
  border-color: white;
}

/* CONTACT FORM */
.contact-form {
  max-width: 600px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.form-group {
  position: relative;
}

.form-label {
  display: block;
  font-weight: 700;
  color: var(--text-h);
  margin-bottom: 0.5rem;
  font-size: 0.95rem;
}

.form-input {
  width: 100%;
  padding: 1rem;
  border: 2px solid var(--border);
  border-radius: 12px;
  font-size: 1rem;
  background: var(--bg);
  color: var(--text-h);
  transition: all 0.3s ease;
  font-family: inherit;
}

.form-input::placeholder {
  color: var(--text);
  opacity: 0.6;
}

.form-input:focus {
  outline: none;
  border-color: var(--accent);
  box-shadow: 0 0 0 3px var(--accent-bg);
}

.form-input:valid:not(:placeholder-shown) {
  border-color: #10b981;
}

.input-label {
  position: absolute;
  top: -1.8rem;
  left: 1rem;
  font-size: 0.85rem;
  color: var(--accent);
  font-weight: 700;
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
  margin-top: 1.5rem;
  font-size: 1.05rem;
  padding: 1.1rem 2.5rem;
}

/* FOOTER */
footer {
  text-align: center;
  padding: 3rem 2rem;
  border-top: 1px solid var(--border);
  color: var(--text);
  background: linear-gradient(180deg, transparent, var(--accent-bg));
}

.footer-content {
  max-width: 1200px;
  margin: 0 auto;
}

footer p {
  margin: 0.5rem 0;
  line-height: 1.6;
}

.heart {
  animation: heartbeat 1.5s ease infinite;
}

@keyframes heartbeat {
  0%, 100% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.2);
  }
}

.footer-links {
  display: flex;
  gap: 1.5rem;
  justify-content: center;
  margin-top: 1.5rem;
}

.footer-links a {
  color: var(--accent);
  text-decoration: none;
  font-weight: 700;
  transition: all 0.3s ease;
}

.footer-links a:hover {
  transform: translateY(-2px);
}

/* RESPONSIVE */
@media (max-width: 768px) {
  .hero-container {
    flex-direction: column;
    gap: 2rem;
    padding-top: 2rem;
  }

  .hero-image-wrapper {
    flex-basis: auto;
    max-width: 280px;
  }

  .hero-title {
    font-size: 2.2rem;
  }
  
  .hero-subtitle {
    font-size: 1.2rem;
  }

  .hero-description {
    font-size: 0.95rem;
  }

  .section {
    padding: 4rem 1.5rem;
  }

  .section h2 {
    font-size: 2rem;
  }

  nav {
    gap: 1.5rem;
  }

  .nav-link {
    font-size: 0.85rem;
  }

  .buttons {
    width: 100%;
    justify-content: center;
  }

  .btn {
    width: 100%;
    min-width: unset;
  }

  .grid {
    grid-template-columns: 1fr;
  }

  .about-stats {
    grid-template-columns: repeat(2, 1fr);
    gap: 1rem;
  }

  .skills {
    justify-content: flex-start;
  }

  .showcase-section {
    margin: 2rem 1rem;
  }

  .showcase-grid {
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    gap: 1rem;
  }

  .showcase-image {
    height: 180px;
  }

  .showcase-icon {
    font-size: 2.5rem;
  }
}

@media (max-width: 480px) {
  .navbar {
    padding: 0.8rem 1rem;
  }

  nav {
    gap: 1rem;
  }

  .nav-link {
    font-size: 0.75rem;
  }

  .hero-title {
    font-size: 1.8rem;
  }

  .section h2 {
    font-size: 1.5rem;
  }

  .contact-form {
    gap: 1.5rem;
  }

  .buttons {
    flex-direction: column;
  }

  .footer-links {
    flex-direction: column;
    gap: 0.5rem;
  }
}
</style>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { SpeedInsights } from '@vercel/speed-insights/vue'

const isScrolled = ref(false)
const activeCard = ref(null)
const activeShowcase = ref(0)
const formStatus = ref('')
const isImageHovered = ref(false)

const stats = ref([
  { number: '50+', label: 'Projects Completed' },
  { number: '100%', label: 'Client Satisfaction' },
  { number: '3+', label: 'Years Experience' }
])

const projects = ref([
  {
    title: 'Movie Streaming Website',
    description: 'Built with Vue + API integration. Features include real-time search, user authentication, and movie recommendations.',
    icon: '🎬',
    color: 'linear-gradient(135deg, #667eea 0%, #764ba2 100%)',
    tech: ['Vue.js', 'API', 'Authentication']
  },
  {
    title: 'Lead Generation Website',
    description: 'SEO-focused landing page for business leads. Optimized for conversions with responsive design and analytics.',
    icon: '📱',
    color: 'linear-gradient(135deg, #f093fb 0%, #f5576c 100%)',
    tech: ['SEO', 'Responsive', 'Analytics']
  },
  {
    title: 'Inventory System',
    description: 'Full-stack system with Vue + Flask + MySQL. Complete inventory management with real-time updates.',
    icon: '📦',
    color: 'linear-gradient(135deg, #4facfe 0%, #00f2fe 100%)',
    tech: ['Vue.js', 'Flask', 'MySQL']
  }
])

const skillCategories = ref([
  {
    name: 'Frontend',
    items: ['Vue.js', 'React', 'JavaScript', 'HTML/CSS', 'Tailwind CSS', 'Vite']
  },
  {
    name: 'Backend',
    items: ['Node.js', 'Flask', 'Python', 'Express.js']
  },
  {
    name: 'Database',
    items: ['MySQL', 'MongoDB', 'Firebase', 'PostgreSQL']
  },
  {
    name: 'Tools & Platforms',
    items: ['Git/Github', 'VS Code', 'Figma', 'AWS', 'Vercel', 'Docker']
  }
])

const showcaseItems = ref([
  { title: 'Web Design', icon: '🎨' },
  { title: 'Mobile Apps', icon: '📱' },
  { title: 'API Integration', icon: '🔌' },
  { title: 'Performance', icon: '⚡' },
  { title: 'Security', icon: '🔒' },
  { title: 'Scalability', icon: '📈' }
])

const form = ref({
  name: '',
  email: '',
  message: ''
})

// Scroll event listener
const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
  
  // Fade in sections on scroll with intersection observer
  document.querySelectorAll('.fade-in-section').forEach(section => {
    const rect = section.getBoundingClientRect()
    const isVisible = rect.top < window.innerHeight * 0.75
    
    if (isVisible) {
      section.style.opacity = '1'
    }
  })
}

// Form submission with validation
const submitForm = () => {
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
  
  if (!form.value.name || !form.value.email || !form.value.message) {
    formStatus.value = '❌ Please fill all fields'
    setTimeout(() => {
      formStatus.value = ''
    }, 3000)
    return
  }

  if (!emailRegex.test(form.value.email)) {
    formStatus.value = '❌ Please enter a valid email'
    setTimeout(() => {
      formStatus.value = ''
    }, 3000)
    return
  }

  formStatus.value = '📨 Sending...'

  // Simulate sending to backend
  setTimeout(() => {
    formStatus.value = '✅ Message sent! I\'ll get back to you soon!'
    form.value = { name: '', email: '', message: '' }
    
    setTimeout(() => {
      formStatus.value = ''
    }, 4000)
  }, 1500)
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
  
  // Initial animation trigger
  handleScroll()
  
  // Stagger animations for cards on load
  document.querySelectorAll('.card').forEach((card, index) => {
    card.style.animation = `fadeInUp 0.7s ease ${0.15 * index}s both`
  })

  // Intersection Observer for better performance
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          entry.target.style.opacity = '1'
        }
      })
    },
    { threshold: 0.1 }
  )

  document.querySelectorAll('.fade-in-section').forEach(section => {
    observer.observe(section)
  })
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>