<script setup>
import sidebar from './components/sidebar.vue'
import { onMounted, ref } from 'vue'

// Deklarasi untuk section skill
const skills = [
  { name: 'Figma', value: 75},
  { name: 'Javascript', value: 55},
  { name: 'HTML', value: 79},
  { name: 'CSS', value: 72},
  { name: 'Python', value: 43},
  { name: 'GO-Lang', value: 40},
  { name: 'Video Editing', value: 76},
  { name: 'Photography', value: 89},
]
// reactive state untuk skills
const displayedValues = ref(skills.map(() => 0))
// Animasi masuk untuk section skils
onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          skills.forEach((skill, index) => {
            let current = 0
            const interval = setInterval(() => {
              if (current >= skill.value) {
                displayedValues.value[index] = skill.value
                clearInterval(interval)
              } else {
                current += 1
                displayedValues.value[index] = current
              }
            }, 20)
          })
        }
      })
    },
    { threshold: 0.5 }
  )
  // Menghubungkan section skill dengan observer
  const el = document.getElementById('skill')
  if (el) observer.observe(el)
})
// Deklarasi untuk isi section project
const tools = [
  { name: 'Vite', src: 'vite.svg', glowColor: '#facc15', link: 'https://vitejs.dev/'},
  { name: 'Vue', src: 'vue.svg', glowColor: '#42b883', link: 'https://vuejs.org/'},
  { name: 'Tailwind', src: 'tailwindcss-icon.svg', glowColor: '#38bdf8', link: 'https://tailwindcss.com/'},
  { name: 'Node.js', src: 'nodejs-icon.svg', glowColor: '#68a063',  link: 'https://nodejs.org/'},
  { name: 'Git', src: 'git-scm-icon.svg', glowColor: '#f1502f', link: 'https://git-scm.com/'}
]
// Animasi masuk untuk semua section kecuali skill
onMounted(() => {
  const revealElements = document.querySelectorAll('.scroll-reveal')

  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          entry.target.classList.add('opacity-100', 'translate-y-0')
          entry.target.classList.remove('opacity-0', 'translate-y-10')
        } else {
          entry.target.classList.remove('opacity-100', 'translate-y-0')
          entry.target.classList.add('opacity-0', 'translate-y-10')
        }
      })
    },
    { threshold: 0.1 }
  )

  revealElements.forEach(el => {
    observer.observe(el)
  })
})
</script>

<template>
  <sidebar/>
  <!-- style untuk general -->
  <div class="bg-gray-900 text-white"> 
    <!-- Section Utama/Hero -->
    <section id="Hero" class="min-h-screen flex items-center justify-center bg-gray-900 text-white px-4">
      <div class="max-w-6xl w-full grid md:grid-cols-2 items-center gap-8">
        <div class="space-y-4 text-center md:text-left">
          <h1 class="text-5xl font-bold">Hi 👋</h1>
          <p class="text-xl text-indigo-400 font-medium">I'm Rizki</p>
          <p class="text-lg text-gray-300">
            Saya adalah web developer yang suka bikin tampilan clean, cepat, dan interaktif.
          </p>
        </div>
        <div class="flex justify-center">
      <img
        src="/public/rizki2.jpg"
        alt="photo"
        class= "w-84 h-84 object-cover rounded-lg transition duration-400 hover:shadow-[0_1px_10px_5px_rgba(255,255,255,0.5)]"/>
    </div>
      </div>
    </section>
    <!-- Bagian style section about -->
    <section id="about" class="min-h-screen flex items-center justify-center bg-gray-800 text-white px-4 py-20 space-y-6 scroll-reveal opacity-0 translate-y-10 transition-all duration-500 ease-out">
      <!-- Style untuk photo/gambar -->
      <div class="max-w-6x1 w-full grid md:grid-cols-2 gap-12 items-center">
        <div class="flex justify-center">
          <img
            src="/public/rizki.jpg"
            alt="photo"
            class="w-80 h-96 object-cover rounded-lg transition duration-400 hover:shadow-[0_1px_10px_5px_rgba(255,255,255,0.5)]"
            />
        </div>
        <!-- Style untuk text -->
      <div class="space-y-6">
      <h2 class="text-indigo-400 text-xl font-medium">Discover</h2>
      <h1 class="text-4xl font-bold">About Me</h1>
      <p class="text-gray-300">
        Saya adalah pelajar dari SMK NEGERI 2 Yogyakarta jurusan Sistem Informasi
        Jaringan dan Aplikasi. Saya memiliki kemampuan dan ketertarikan di bidang
        Back-End developer, Linux Server, serta desain grafis, photography,
        videography dan UI/UX design.
      </p>
      <!-- Syle untuk card -->
      <div class="grid grid-cols-2 gap-4 text-sm text-gray-200 border border-indigo-500 p-4 rounded-md">
        <p><span class="font-semibold">Name:</span> Rizki Kurniawan</p>
        <p><span class="font-semibold">Age:</span> 18</p>
        <p><span class="font-semibold">Phone:</span> +62 8781 8121 232</p>
        <p><span class="font-semibold">Address:</span> Wirobrajan, Kota Yogyakarta</p>
        <p><span class="font-semibold">School:</span> SMK N 2 Yogyakarta</p>
        <p><span class="font-semibold">Email:</span> rizkify17@email.com</p>
      </div>
      <!-- Style untuk tombol download -->
      <button class="mt-4 px-6 py-2 bg-red-500 transition duration-400 hover:shadow-[0_1px_10px_5px_rgba(255,255,255,0.5)]">
        <a
        href="/public/CV-Rizki.pdf"
        download>
        Download CV
        </a>
      </button>
      </div>
      </div>
    </section>
    <!-- Bagian style section skill -->
    <section id="skill" class="min-h-[60vh] bg-gray-900 text-white px-4 py-20">
      <div class="text-center mb-12">
      <h2 class="text-4xl font-bold text-yellow-400">My Skills</h2>
    </div>
    <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 gap-6 max-w-6xl mx-auto">
      <!-- Pengambilan script dan style untuk card skill -->
      <div
        v-for="(skill, index) in skills"
        :key="skill.name"
        class="backdrop-blur-md bg-white/10 border border-white/20 p-6 rounded-xl text-center shadow-md transition duration-300 hover:scale-105">
        <div class="text-3xl font-bold text-white">
          {{ displayedValues[index] }}%
        </div>
        <div class="text-sm mt-2 text-yellow-300 font-semibold">
          {{ skill.name }}
        </div>
      </div>
    </div>
    </section>
    <!-- Bagian style section project -->
    <section id="project" class="min-h-[55vh] flex flex-col items-center justify-center bg-gray-800 space-y-6 scroll-reveal opacity-0 translate-y-10 transition-all duration-500 ease-out">
      <div class="text-center mb-12">
        <h2 class="text-4xl md:text-5xl font-bold text-yellow-400">In This Project</h2>
        <p class="text-gray-400 mt-2 text-lg">Tools & Frameworks</p>
      </div>
      <!-- Pengambilan script logo dan style untuk logo -->
      <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-5 gap-10 max-w-6xl mx-auto">
      <div
      v-for="(tool, index) in tools"
      :key="index"
      class="relative group w-28 h-28 mx-auto flex items-center justify-center transition duration-500">
      <div
        class="absolute w-28 h-28 rounded-full blur-2xl opacity-0 group-hover:opacity-80 transition-opacity duration-700"
        :style="{ backgroundColor: tool.glowColor }">
      </div>
      <a :href="tool.link" target="_blank" rel="noopener noreferrer" class="relative group w-28 h-28 mx-auto flex items-center justify-center transition duration-500">
        <div
          class="absolute w-28 h-28 rounded-full blur-2xl opacity-0 group-hover:opacity-80 transition-opacity duration-700"
          :style="{ backgroundColor: tool.glowColor }">
        </div>
          <img :src="tool.src" :alt="tool.name" class="w-14 h-14 z-10" />
      </a>
      </div>
      </div>
    </section>
    <!-- Bagian style section contact -->
    <section id="contact" class="min-h-screen bg-gray-900 text-white px-4 py-20 flex items-center justify-center space-y-6 scroll-reveal opacity-0 translate-y-10 transition-all duration-500 ease-out">
      <div class="w-full max-w-3xl text-center space-y-10">
        <div>
          <h2 class="text-4xl md:text-5xl font-bold text-yellow-400">Contact Me</h2>
          <p class="text-gray-400 mt-2 text-lg">Just say hi! 👋</p>
        </div>
        <!-- Kolom untuk mengetik pesan -->
        <form class="space-y-6">
        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
          <input type="text" placeholder="Your Name" class="p-4 rounded-md bg-gray-800 border border-gray-600 focus:outline-none focus:ring-2 focus:ring-yellow-400 transition duration-300" />
          <input type="email" placeholder="Your Email" class="p-4 rounded-md bg-gray-800 border border-gray-600 focus:outline-none focus:ring-2 focus:ring-yellow-400 transition duration-300" />
        </div>

        <textarea placeholder="Your Message" rows="5" class="w-full p-4 rounded-md bg-gray-800 border border-gray-600 focus:outline-none focus:ring-2 focus:ring-yellow-400 transition duration-300"></textarea>
        <!-- Tombol untuk mengirim pesan tetapi belum bisa di gunakan -->
        <button type="submit" class="px-8 py-3 bg-yellow-400 text-black font-semibold rounded-md hover:shadow-[0_0_20px_5px_rgba(250,204,21,0.5)] transition duration-300">
        Send Message
        </button>
        </form>
      </div>
    </section>
    <!-- Bagian style footer -->
    <footer class="bg-gray-900 py-10">
  <div class="flex justify-center items-center gap-10">
    <!-- GitHub logo -->
    <div class="flex flex-col items-center group">
      <a href="https://github.com/RizkiKurniawan17" target="_blank">
        <img src="/public/github-mark-white.svg" alt="GitHub" class="w-10 h-10 object-contain group-hover:scale-110 transition duration-300" />
      </a>

    </div>

    <!-- Instagram logo -->
    <div class="flex flex-col items-center group">
      <a href="https://instagram.com/notrizkify" target="_blank">
        <img src="/public/instagram-icon.svg" alt="Instagram" class="w-10 h-10 object-contain group-hover:scale-110 transition duration-300" />
      </a>
    </div>
  </div>
</footer>
  </div>
</template>

<style scoped>
html {
  scroll-behavior: smooth;
}
</style>
