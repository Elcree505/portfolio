<template>
  <div id="app">
    <Header />
    <main>
      <About />
      <Skills />
      <Projects />
    </main>
    <Footer />
  </div>
</template>

<script setup>
import Header from './components/vue-header.vue'
import About from './components/vue-about.vue'
import Projects from './components/vue-projects.vue'
import Skills from './components/vue-skills.vue'
import Footer from './components/vue-footer.vue'
</script>

<style>
:root {
  --primary-color: #000000;
  --background-color: #fff;
  --text-color: #2c3e50;
  --accent-color: #e74c3c;
}

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html {
  scroll-behavior: smooth;
}

body {
  font-family: 'Helvetica Neue', Arial, sans-serif;
  line-height: 1.6;
  color: var(--text-color);
  background-color: var(--background-color);
}

#app {
  max-width: 1200px;
  margin: 0 auto;
  padding: 80px 20px 40px; /* Added top padding to account for fixed header */
}

main {
  display: flex;
  flex-direction: column;
  gap: 100px; /* Increased gap for better separation between sections */
}

h1, h2, h3 {
  color: var(--accent-color);
  font-weight: bold;
}

h1 {
  font-size: 2.5rem;
}

h2 {
  font-size: 2rem;
  margin-bottom: 1.5rem;
}

section {
  padding-top: 60px; /* Added padding to offset the fixed header */
  margin-top: -60px; /* Negative margin to bring the section back up */
}

/* Animation */
/* Add to existing <style> in App.vue */
.fade-in {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.5s ease, transform 0.5s ease;
}

.fade-in.visible {
  opacity: 1;
  transform: translateY(0);
}
</style>