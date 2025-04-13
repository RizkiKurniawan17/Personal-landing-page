<script setup>
import { ref, onMounted } from 'vue';

// untuk menghubungkan sebagai navigasi per section 
const section = [`Hero`, 'about', 'skill', 'project', 'contact']
const activeSection = ref('Hero')

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry)=> {
        if (entry.isIntersecting) {
          activeSection.value = entry.target.id
        }
      })
    },
    { threshold: 0.5 }
  )
  section.forEach((id) => {
  const el = document.getElementById(id)
  if (el) observer.observe(el)
  })
})

</script>

<template>
  <!-- sidebar bulat di samping kiri -->
  <div class="fixed left-4 top-1/2 -translate-y-1/2 flex flex-col space-y-4 z-50">
    <a
      v-for="section in section"
      :key="section"
      :href="`#${section}`"
      :class="[
        'w-4 h-4 rounded-full transition-all duration-300 border-2 border-white',
        activeSection === section
          ? 'bg-white scale-125 shadow-lg'
          : 'bg-gray-500 hover:bg-white/70'
      ]">
      </a>
  </div>
</template>
  