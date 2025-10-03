<template>
  <section id="experiences">
    <h2 class="fade-in">Experiences</h2>
    <div class="experiences-grid">
      <div v-for="experience in experiences" :key="experience.id" class="experience-card fade-in">
        <h3>{{ experience.title }}</h3>
        <p>{{ experience.description }}</p>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useIntersectionObserver } from '@vueuse/core';

const experiences = ref([
  { id: 1, title: 'Software Engineer 03/2024 - 09/2024', description: 'Develop a digital platform to streamline the group buying process managed by company employees. This platform will support the entire lifecycle of group purchases from initiation to distribution.',},
  { id: 2, title: 'Software Engineer 07/2025 - 08/2025', description: 'Designed and implemented an AI-powered chatbot that enables customers to seamlessly book car services through natural language conversation.'}
]);

onMounted(() => {
  const targets = document.querySelectorAll('#experiences .fade-in');
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
.experiences-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
}

.experience-card {
  background-color: var(--background-color);
  border: 1px solid var(--accent-color);
  padding: 20px;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.experience-card:hover {
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