<template>
  <section id="projects">
    <h2 class="fade-in">Projects</h2>
    <div class="projects-grid">
      <div v-for="project in projects" :key="project.id" class="project-card fade-in">
        <h3>{{ project.title }}</h3>
        <p>{{ project.description }}</p>
        <a :href="project.link" target="_blank" rel="noopener noreferrer">View Project</a>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useIntersectionObserver } from '@vueuse/core';

const projects = ref([
  { id: 1, title: 'Todo-List', description: 'Allow users to manage tasks efficiently with features like inline editing, task ordering, and timestamp tracking. The project serves as a practical example of DOM manipulation with JavaScript, responsive web design using Bootstrap, and the deployment of static web projects. ', link: 'https://elcree505.github.io/Todo-List/' },
  { id: 2, title: 'Anime Search', description: 'Allow users to search for the anime they are looking for, they can click into the description for more detail about the anime. The project serves as a practical example of Vue project effectivelly using composition API, event handling, and other types of API/functions in Vue JS.', link: 'https://elcree505.github.io/animeSearch/' }
]);

onMounted(() => {
  const targets = document.querySelectorAll('#projects .fade-in');
  targets.forEach(target => {
    useIntersectionObserver(target, ([{ isIntersecting }]) => {
      if (isIntersecting) {
        target.classList.add('visible');
      }
    });
  });
});
</script>

<style scoped>
.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
}

.project-card {
  background-color: var(--background-color);
  border: 1px solid var(--accent-color);
  padding: 20px;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.project-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
}

h3 {
  margin-bottom: 10px;
  font-size: 1.2rem;
}

p {
  margin-bottom: 15px;
}

a {
  display: inline-block;
  color: var(--primary-color);
  text-decoration: none;
  font-weight: bold;
  border-bottom: 2px solid var(--primary-color);
  transition: opacity 0.3s ease;
}

a:hover {
  opacity: 0.7;
}
</style>