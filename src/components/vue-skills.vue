<template>
  <section id="skills">
    <h2 class="fade-in">Skills</h2>
    <div class="skills-categories">
      <div v-for="category in skillCategories" :key="category.name" class="skill-category fade-in">
        <h3>{{ category.name }}</h3>
        <div class="skills-grid">
          <div v-for="skill in category.skills" :key="skill.name" class="skill-card fade-in">
            <h4>{{ skill.name }}</h4>
            <div class="skill-level-container">
              <div class="skill-level" :style="{ width: '0%' }" ref="skillLevels"></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useIntersectionObserver } from '@vueuse/core';

const skillCategories = ref([
  {
    name: 'Programming Languages',
    skills: [
      { name: 'Python', level: 100 },
      { name: 'Java', level: 100 },
      { name: 'C++', level: 100 },
      { name: 'C#', level: 100 },
      { name: 'JavaScript', level: 100 },
      { name: 'HTML', level: 100 },
      { name: 'CSS', level: 100 },
      { name: 'R', level: 100 },
      { name: 'MATLAB', level: 100 }
    ]
  },
  {
    name: 'Frameworks & Libraries',
    skills: [
      { name: 'Vue.js', level: 100 },
      { name: 'React.js', level: 100 },
      { name: 'Flask', level: 100 },
      { name: 'FastAPI', level: 100 },
      { name: 'Rasa', level: 100 },
      { name: 'Bootstrap', level: 100 },
      { name: 'PyTorch', level: 100 },
      { name: 'pandas', level: 100 },
      { name: 'NumPy', level: 100 },
      { name: 'Matplotlib', level: 100 }
    ]
  },
  {
    name: 'Web & Backend Development',
    skills: [
      { name: 'REST APIs', level: 100 },
      { name: 'MySQL', level: 100 },
      { name: 'SQLAlchemy', level: 100 }
    ]
  },
  {
    name: 'Developer Tools & Platforms',
    skills: [
      { name: 'Git', level: 100 },
      { name: 'GitHub', level: 100 },
      { name: 'Docker', level: 100 },
      { name: 'Linux', level: 100 },
      { name: 'VS Code', level: 100 },
      { name: 'Visual Studio', level: 100 },
      { name: 'Jupyter Notebook', level: 100 },
      { name: 'Eclipse', level: 100 },
      { name: 'Unity', level: 100 }
    ]
  }
]);



const skillLevels = ref([]);

onMounted(() => {
  const targets = document.querySelectorAll('#skills .fade-in');
  targets.forEach(target => {
    useIntersectionObserver(target, ([{ isIntersecting }]) => {
      if (isIntersecting) {
        target.classList.add('visible');
        if (target.classList.contains('skill-card')) {
          const skillLevel = target.querySelector('.skill-level');
          const skillName = target.querySelector('h4').textContent;
          const category = skillCategories.value.find(cat => 
            cat.skills.some(skill => skill.name === skillName)
          );
          const skill = category.skills.find(s => s.name === skillName);
          setTimeout(() => {
            skillLevel.style.width = `${skill.level}%`;
          }, 300);
        }
      }
    });
  });
});
</script>

<style scoped>
.skills-categories {
  display: flex;
  flex-direction: column;
  gap: 40px;
}

.skill-category {
  background-color: var(--background-color);
  border: 1px solid var(--accent-color);
  padding: 20px;
  border-radius: 8px;
}

.skill-category h3 {
  margin-bottom: 20px;
  font-size: 1.5rem;
  color: var(--primary-color);
}

.skills-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr); /* Creates 3 equal-width columns */
  gap: 20px;
}

/* For smaller screens, we can adjust to 2 columns */
@media (max-width: 768px) {
  .skills-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

/* For very small screens, we can adjust to 1 column */
@media (max-width: 480px) {
  .skills-grid {
    grid-template-columns: 1fr;
  }
}

.skill-card {
  background-color: var(--accent-color);
  padding: 15px;
  border-radius: 4px;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.skill-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
}

h4 {
  margin-bottom: 10px;
  font-size: 1rem;
  color: var(--primary-color);
}

.skill-level-container {
  background-color: var(--background-color);
  height: 5px;
  width: 100%;
  border-radius: 2.5px;
}

.skill-level {
  height: 100%;
  background-color: var(--primary-color);
  transition: width 1s ease;
  border-radius: 2.5px;
}
</style>