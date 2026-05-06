<template>
  <div class="app">
    <!-- NAVBAR -->
    <header class="navbar">
    

      <nav>
        <a href="#about">About</a>
        <a href="#projects">Projects</a>
        <a href="#skills">Skills</a>
        <a href="#contact">Contact</a>
      </nav>
    </header>

    <!-- HERO SECTION -->
    <section class="hero">
      <h2>Hi, I'm Chris 👋</h2>
      <p>A Frontend Developer building modern web applications</p>

      <div class="buttons">
        <a href="#projects" class="btn primary">View Projects</a>
        <a href="#contact" class="btn">Contact Me</a>
      </div>
    </section>

    <!-- ABOUT -->
    <section id="about" class="section">
      <h2>About Me</h2>
      <p>
        I am a passionate developer focused on building clean, fast, and responsive websites.
        I enjoy working with Vue, modern UI design, and backend systems.
      </p>
    </section>

    <!-- PROJECTS -->
    <section id="projects" class="section">
      <h2>Projects</h2>

      <div class="grid">
        <div class="card">
          <h3>Movie Streaming Website</h3>
          <p>Built with Vue + API integration</p>
        </div>

        <div class="card">
          <h3>Lead Generation Website</h3>
          <p>SEO-focused landing page for business leads</p>
        </div>

        <div class="card">
          <h3>Inventory System</h3>
          <p>Full-stack system with Vue + Flask + MySQL</p>
        </div>
      </div>
    </section>

    <!-- SKILLS -->
    <section id="skills" class="section">
      <h2>Skills</h2>

      <div class="skills">
        <span>Vue.js</span>
        <span>Vite</span>
        <span>JavaScript</span>
        <span>Tailwind CSS</span>
        <span>Node.js</span>
        <span>MySQL</span>
        <span>Git</span>
      </div>
    </section>

    <!-- CONTACT -->
    <section id="contact" class="section">
      <h2>Contact</h2>

      <form class="contact-form">
        <input type="text" placeholder="Your Name" />
        <input type="email" placeholder="Your Email" />
        <textarea placeholder="Your Message"></textarea>
        <button type="submit">Send Message</button>
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
  background: #0f172a;
  color: white;
}

/* NAVBAR */
.navbar {
  display: flex;
  justify-content: flex-end;
  padding: 20px 60px;
  background: #111827;
  position: sticky;
  top: 0;
}

.navbar nav {
  display: flex;
  gap: 20px;
}

.navbar a {
  color: white;
  text-decoration: none;
  opacity: 0.8;
}

.navbar a:hover {
  opacity: 1;
}

.logo {
  font-size: 20px;
  font-weight: bold;
}

/* HERO */
.hero {
  text-align: center;
  padding: 100px 20px;
}

.hero h2 {
  font-size: 40px;
}

.hero p {
  margin-top: 10px;
  opacity: 0.7;
}

.buttons {
  margin-top: 20px;
}

.btn {
  padding: 10px 20px;
  margin: 5px;
  border-radius: 6px;
  text-decoration: none;
  color: white;
  border: 1px solid white;
}

.primary {
  background: #3b82f6;
  border: none;
}

/* SECTIONS */
.section {
  padding: 60px 20px;
  max-width: 1000px;
  margin: auto;
}

.section h2 {
  margin-bottom: 20px;
}

/* PROJECT GRID */
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
}

.card {
  background: #1f2937;
  padding: 20px;
  border-radius: 10px;
}

/* SKILLS */
.skills span {
  display: inline-block;
  background: #334155;
  padding: 8px 12px;
  margin: 5px;
  border-radius: 6px;
}

/* CONTACT */
.contact-form {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

input, textarea {
  padding: 10px;
  border-radius: 6px;
  border: none;
}

button {
  padding: 10px;
  background: #3b82f6;
  border: none;
  color: white;
  border-radius: 6px;
  cursor: pointer;
}

/* FOOTER */
footer {
  text-align: center;
  padding: 20px;
  opacity: 0.6;
}
</style>