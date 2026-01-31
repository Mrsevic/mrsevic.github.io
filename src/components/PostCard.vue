<script setup lang="ts">
interface Props {
  title: string;
  summary: string;
  date: Date;
  url: string;
  index: number;
}

const props = defineProps<Props>();

// Colorie theme colors - rotating based on index
const colors = ['#fac14e', '#fbcfb9', '#ef7d4d', '#96d0c3'];
const cardColor = colors[props.index % colors.length];

const formattedDate = new Intl.DateTimeFormat('en-US', {
  year: 'numeric',
  month: 'long',
  day: 'numeric',
}).format(props.date);
</script>

<template>
  <article class="card" :style="{ backgroundColor: cardColor }">
    <a :href="url" class="card-link">
      <div class="meta">
        <h2>{{ title }}</h2>
        <p>{{ summary }}</p>
        <time class="date" :datetime="date.toISOString()">{{ formattedDate }}</time>
      </div>
    </a>
  </article>
</template>

<style scoped>
.card {
  display: flex;
  align-items: flex-start;
  justify-content: flex-start;
  min-height: 10rem;
  position: relative;
  box-shadow: 0 0.75rem 1.5rem rgba(18, 38, 63, 0.03);
  transition: all 0.3s cubic-bezier(0.25, 0.45, 0.45, 0.95);
}

.card:hover {
  transform: scale(1.02);
}

.card-link {
  text-decoration: none;
  color: inherit;
  width: 100%;
  height: 100%;
}

.meta {
  padding: 2rem;
  display: flex;
  flex: 1;
  justify-content: space-between;
  flex-direction: column;
  min-height: 10rem;
}

h2 {
  font-size: 1.3rem;
  margin: 0 0 0.5rem 0;
  font-weight: 500;
}

p {
  font-size: 0.9rem;
  margin: 0 0 1rem 0;
  flex-grow: 1;
}

.date {
  font-size: 0.8rem;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: .05em;
  opacity: 0.7;
}
</style>
