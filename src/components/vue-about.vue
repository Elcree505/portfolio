<template>
  <section id="about" class="fade-in">
    <div class="about-container">
      <div class="about-image">
        <img src="@/assets/profilepic.jpg" alt="Your Name" />
      </div>
      <div class="about-content">
        <h2>About</h2>
        <p>Detail-oriented developer with experience in full-stack applications and AI-powered chatbot systems. Skilled in Python, Java, and API integration. Adept at building scalable solutions and enhancing user experience through automation and optimization
        </p>
      </div>
    </div>
  </section>
</template>

<script setup>
import { onMounted } from 'vue';
import { useIntersectionObserver } from '@vueuse/core';

onMounted(() => {
  const target = document.querySelector('#about');
  useIntersectionObserver(target, ([{ isIntersecting }]) => {
    if (isIntersecting) {
      target.classList.add('visible');
    }
  });
});
</script>

<style scoped>
.about-container {
  display: flex;
  align-items: center;
  gap: 2rem;
}

.about-image {
  flex-shrink: 0;
}

.about-image img {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  object-fit: cover;
  border: 3px solid var(--primary-color);
}

.about-content {
  flex-grow: 1;
}

h2 {
  margin-bottom: 1rem;
}

p {
  font-size: 1rem;
  max-width: 600px;
}

@media (max-width: 768px) {
  .about-container {
    flex-direction: column;
    text-align: center;
  }

  .about-image {
    margin-bottom: 1rem;
  }
}
</style>