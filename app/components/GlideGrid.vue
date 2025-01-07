<script lang="ts" setup>
import gsap from "gsap"

const grid = [14, 30];

onMounted(() => {
  const prefersReducedMotion = window.matchMedia('(prefers-reduced-motion: reduce').matches;

  if (prefersReducedMotion) {
    gsap.set('#triangle-grid', { opacity: 1 });
    gsap.set('.triangle-grid-item', {
      opacity: 0.2,
      scale: 1
    });
    return;
  }

  gsap.set('.triangle-grid-item', {
    opacity: 0,
    transformOrigin: 'center',
    color: '#fff'
  });

  gsap.set('#triangle-grid', { opacity: 1 });

  const tl = gsap.timeline();

  // Entrance Animation
  tl.to('.triangle-grid-item', {
    keyframes: [
      {
        opacity: 0,
        duration: 0
      },
      {
        opacity: 0.4,
        rotate: '+=180',
        color: '#A78BFA',
        scale: 3,
        duration: 0.6,
        stagger: {
          amount: 2,
          grid: grid,
          from: 'center'
        }
      },
      {
        opacity: 0.2,
        rotate: '+=180',
        color: '#fff',
        scale: 1,
        delay: -2,
        duration: 0.6,
        stagger: {
          amount: 3,
          grid: grid,
          from: 'center'
        }
      }
    ]
  });

  // Loop Animation
  tl.to('.triangle-grid-item', {
    delay: 12,
    repeat: -1,
    repeatDelay: 12,
    keyframes: [
      {
        opacity: 0.4,
        rotate: '+=180',
        color: '#A78BFA',
        scale: 3,
        duration: 0.6,
        stagger: {
          amount: 2,
          grid: grid,
          from: 'center'
        }
      },
      {
        opacity: 0.2,
        rotate: '+=180',
        color: '#fff',
        scale: 1,
        delay: -2,
        duration: 0.6,
        stagger: {
          amount: 3,
          grid: grid,
          from: 'center'
        }
      }
    ]
  });
});
</script>

<template>
  <svg
    id="triangle-grid"
    xmlns="http://www.w3.org/2000/svg"
    fill="none"
    viewBox="0 0 935 425"
    class="absolute -left-2 -top-14 -z-10"
    opacity="0"
    style="mask-image: linear-gradient(black, transparent);"
  >
    <g class="triangle-grid-group">
      <template v-for="(_, i) in grid[0]" :key="i">
        <path
          v-for="(_, j) in grid[1]"
          :key="j"
          fill="currentColor"
          opacity=".2"
          class="triangle-grid-item"
          :d="`M${j * 32 + 5},${i * 32 + 10}l-3.75,2.165l0,-4.33l3.75,2.165z`"
        />
      </template>
    </g>
  </svg>
</template>