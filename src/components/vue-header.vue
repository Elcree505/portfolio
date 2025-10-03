<template>
  <header>
    <h1>Charles Lee</h1>
    <nav>
      <a href="#about" @click="scrollToSection">About</a>
      <a href="#skills" @click="scrollToSection">Skills</a>
      <a href="#experiences" @click="scrollToSection">Experiences</a>
      <a href="#projects" @click="scrollToSection">Projects</a>
    </nav>
  </header>
</template>

<script setup>
const scrollToSection = (event) => {
  event.preventDefault();
  const targetId = event.target.getAttribute('href');
  const targetElement = document.querySelector(targetId);
  if (targetElement) {
    targetElement.scrollIntoView({ behavior: 'smooth' });
  }
}
</script>

<style>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px;
  background-color: var(--primary-color);
  position: fixed;
  color: var(--accent-color);
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

nav {
  display: flex;
  gap: 20px;
}

a {
  color: var(--accent-color);
  text-decoration: none;
  font-weight: bold;
  transition: opacity 0.3s ease;
}

a:hover {
  opacity: 0.7;
}
</style>