<template>
  <section id="projects">
    <h2 class="fade-in">Projects</h2>

    <!-- One section per year (sorted: newest first) -->
    <div
      v-for="group in groupedByYear"
      :key="group.year"
      class="year-section"
      :aria-labelledby="`year-${group.year}`"
    >
      <h3 :id="`year-${group.year}`" class="year-heading fade-in">
        {{ group.year }}
      </h3>

      <div class="projects-grid">
        <div
          v-for="project in group.items"
          :key="project.id"
          class="project-card fade-in"
        >
          <h4>{{ project.title }}</h4>
          <p>{{ project.description }}</p>
          <a :href="project.link" target="_blank" rel="noopener noreferrer"
             :aria-label="`View project: ${project.title}`">
            View Project
          </a>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue';
import { useIntersectionObserver } from '@vueuse/core';

const projects = ref([
  // 2025 project (add your new one here)
  {
    id: 1,
    year: 2025,
    title: 'Business Meeting Text Analysis',
    description:
      'Developed an end-to-end NLP pipeline for business meeting analysis, transforming unstructured meeting transcripts into structured representations through text cleaning, tokenization, keyword extraction, and semantic clustering.',
    link: 'https://github.com/Elcree505/Business-Text-Analysis'
  },
  {
    id: 2,
    year: 2025,
    title: 'CIFAR10',
    description:
      'Trains a simple Convolutional Neural Network (CNN) on the CIFAR-10 dataset using PyTorch. It first computes the dataset’s mean and standard deviation for normalization, then loads and preprocesses the images. The model, trained with Adam optimizer and cross-entropy loss over several epochs, learns to classify 32×32 color images into 10 object categories such as airplane, cat, and truck.',
    link: 'https://github.com/Elcree505/cifar10_simple_cnn' // replace with your real link
  },
  // 2024 projects (your existing two)
  {
    id: 3,
    year: 2024,
    title: 'Todo-List',
    description:
      'Allow users to manage tasks efficiently with features like inline editing, task ordering, and timestamp tracking. The project serves as a practical example of DOM manipulation with JavaScript, responsive web design using Bootstrap, and the deployment of static web projects.',
    link: 'https://elcree505.github.io/Todo-List/'
  },
  {
    id: 4,
    year: 2024,
    title: 'Anime Search',
    description:
      'Allow users to search for the anime they are looking for, they can click into the description for more detail about the anime. The project serves as a practical example of Vue project effectivelly using composition API, event handling, and other types of API/functions in Vue JS.',
    link: 'https://elcree505.github.io/animeSearch/'
  }
])

// Group projects by year and sort years desc (2025, 2024, …)
const groupedByYear = computed(() => {
  // 1️⃣ sort projects by year (newest year first)
  const sorted = [...projects.value].sort(
    (a, b) => b.year - a.year
  )

  // 2️⃣ group by year (order preserved)
  const map = new Map()
  for (const p of sorted) {
    if (!map.has(p.year)) map.set(p.year, [])
    map.get(p.year).push(p)
  }

  // 3️⃣ return grouped result (already in correct order)
  return Array.from(map, ([year, items]) => ({ year, items }))
})


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
/* Fade-in animation (applies to headings and cards) */
.fade-in {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.8s ease, transform 0.8s ease;
}
.fade-in.visible {
  opacity: 1;
  transform: translateY(0);
}

/* Year section layout */
.year-section {
  margin-top: 2rem;
  padding-top: 1rem;
  border-top: 1px solid var(--accent-color, #e5e7eb);
}
.year-heading {
  margin: 0 0 0.75rem 0;
  font-size: 1.4rem;
  font-weight: 700;
}

/* Grid & cards */
.projects-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 20px;
}

.project-card {
  background-color: var(--background-color, #fff);
  border: 1px solid var(--accent-color, #e5e7eb);
  border-radius: 12px;
  padding: 20px;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}
.project-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 5px 20px rgba(0,0,0,0.08);
}
.project-card h4 {
  margin: 0 0 10px 0;
  font-size: 1.1rem;
}
.project-card p {
  margin: 0 0 14px 0;
  line-height: 1.5;
}
.project-card a {
  display: inline-block;
  color: var(--primary-color, #2563eb);
  text-decoration: none;
  font-weight: 600;
  border-bottom: 2px solid var(--primary-color, #2563eb);
  transition: opacity 0.3s ease;
}
.project-card a:hover {
  opacity: 0.75;
}
</style>