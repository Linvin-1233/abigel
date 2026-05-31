<template>
  <div class="min-h-screen bg-white text-black font-sans selection:bg-sky-200 selection:text-black antialiased overflow-x-hidden">

    <div class="fixed top-0 left-0 w-full h-full pointer-events-none z-0 opacity-40 mix-blend-multiply blur-[2px] animate-pulse-slow">
      <svg class="absolute -top-[10%] -right-[10%] w-[150vw] md:w-[60vw] h-[150vw] md:h-[60vw] transition-transform duration-[2000ms] ease-out"
           :style="{ transform: `rotate(${scrollProgress * 0.5}deg)` }"
           viewBox="0 0 400 400">
        <circle cx="200" cy="200" r="180" stroke="black" stroke-width="3" fill="none" />
        <path d="M200 20 L200 380 M20 200 L380 200" stroke="black" stroke-width="3" />
      </svg>
    </div>

    <div class="fixed top-0 left-0 w-full h-[1px] z-[99] overflow-hidden pointer-events-none">
      <div class="w-[200%] h-full bg-black/20 animate-scanline"></div>
    </div>

    <div class="fixed top-0 left-0 h-[2px] bg-black z-[100] transition-all duration-300" :style="{ width: scrollProgress + '%' }"></div>

    <header class="p-8 border-b-2 border-black flex justify-between items-end sticky top-0 bg-white/95 backdrop-blur-md z-50">
      <div class="text-[10px] font-bold tracking-[0.2em] uppercase leading-tight">
        Szabó Magda // 1959<br>
        Archívum: Abigél
      </div>
      <div class="text-right">
        <span class="text-[10px] uppercase tracking-widest">Matula // Lányintézet</span>
      </div>
    </header>

    <main class="max-w-[1400px] mx-auto p-8 md:p-16 relative z-10">

      <section class="h-[60vh] flex flex-col justify-end mb-32 relative reveal">
        <h1 class="text-[15vw] leading-[0.8] font-black uppercase tracking-tighter">Abigél</h1>
        <div class="flex justify-between items-start mt-8">
          <p class="max-w-sm text-sm leading-tight italic">
            A történet, amely meghatározta a magyar ifjúsági irodalmat. A háború és a belső szabadság metszete.
          </p>
          <svg class="w-24 h-2">
            <line x1="0" y1="5" x2="100" y2="5" stroke="black" stroke-width="2" class="animate-draw-line" />
          </svg>
        </div>
      </section>

      <div class="space-y-32">
        <template v-for="(chapter, index) in chapters" :key="index">
          <div class="grid grid-cols-1 md:grid-cols-12 gap-12 items-start reveal">
            <div class="md:col-span-4 border-t-2 border-black pt-4 sticky top-32">
              <span class="text-xl font-black block mb-4">0{{ index + 1 }}</span>
              <h2 class="text-4xl font-bold uppercase tracking-tight">{{ chapter.title }}</h2>
            </div>
            <div class="md:col-span-8">
              <ul class="space-y-4">
                <li v-for="(line, i) in chapter.text" :key="i" class="border-b border-black/10 pb-3 hover:pl-6 transition-all duration-500 ease-[cubic-bezier(0.16,1,0.3,1)] cursor-default">
                  {{ line }}
                </li>
              </ul>
            </div>
          </div>

          <div class="w-full h-[50vh] relative overflow-hidden group reveal-svg bg-neutral-100">
            <img
                :src="`/images/chapter-${index + 1}.png`"
                alt="Abigél Illusztráció"
                loading="lazy"
                class="w-full h-full object-cover object-top grayscale hover:grayscale-0 transition-all duration-700 ease-in-out absolute inset-0 transform hover:scale-110"
            />
            <svg class="absolute inset-0 w-full h-full pointer-events-none" preserveAspectRatio="none">
              <rect x="5%" y="5%" width="90%" height="90%"
                    fill="none" stroke="black" stroke-width="2"
                    stroke-dasharray="2000" stroke-dashoffset="2000"
                    class="path-rect transition-all duration-[2000ms] ease-out group-hover:stroke-sky-600" />
            </svg>
          </div>
        </template>
      </div>

      <section class="mt-48 pt-16 border-t-4 border-black reveal">
        <h3 class="text-xs font-bold uppercase tracking-[0.2em] mb-8">Köszönetnyilvánítás</h3>
        <div class="markdown-body max-w-none text-sm font-mono opacity-70" v-html="creditsContent"></div>
      </section>
    </main>

    <footer class="mt-32 pt-16 pb-32 border-t-4 border-black bg-white">
      <div class="max-w-[1400px] mx-auto px-8 md:px-16">
        <div class="grid grid-cols-1 md:grid-cols-12 gap-8 items-start mb-16">
          <div class="md:col-span-8">
            <h3 class="text-[10vw] font-black uppercase leading-[0.8] tracking-tighter">Vége</h3>
            <p class="mt-4 text-xs tracking-[0.2em] uppercase font-bold text-neutral-500">
              Abigél / Szabó Magda / 1959-2026
            </p>
          </div>
          <div class="md:col-span-4 flex md:justify-end">
            <button @click="scrollToTop"
                    class="group flex items-center gap-2 text-xs font-bold uppercase tracking-widest hover:pl-4 transition-all">
              <span>Back to Top</span>
              <div class="w-8 h-[1px] bg-black group-hover:w-16 transition-all duration-500"></div>
            </button>
          </div>
        </div>
        <div class="grid grid-cols-2 md:grid-cols-4 gap-8 pt-8 border-t border-black/20">
          <div class="space-y-1"><p class="text-[9px] uppercase tracking-widest font-bold text-neutral-400">Project</p><p class="text-xs font-bold uppercase">Archive // Abigél</p></div>
          <div class="space-y-1"><p class="text-[9px] uppercase tracking-widest font-bold text-neutral-400">Design</p><p class="text-xs font-bold uppercase">Wei Zhihan</p></div>
          <div class="space-y-1"><p class="text-[9px] uppercase tracking-widest font-bold text-neutral-400">Typeface</p><p class="text-xs font-bold uppercase">Inter / System</p></div>
          <div class="space-y-1 text-right"><p class="text-[9px] uppercase tracking-widest font-bold text-neutral-400">Status</p><p class="text-xs font-bold uppercase">Completed</p></div>
        </div>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { marked } from 'marked' // 引入 marked

const creditsContent = ref('Betöltés alatt...')
const scrollProgress = ref(0)

const scrollToTop = () => {
  if (typeof window !== 'undefined') {
    window.scrollTo({ top: 0, behavior: 'smooth' })
  }
}

const handleScroll = () => {
  const totalScroll = document.documentElement.scrollTop
  const windowHeight = document.documentElement.scrollHeight - document.documentElement.clientHeight
  scrollProgress.value = (totalScroll / windowHeight) * 100
}

onMounted(async () => {
  window.addEventListener('scroll', handleScroll)

  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('is-visible')
        if(entry.target.classList.contains('reveal-svg')) {
          const rect = entry.target.querySelector('.path-rect')
          if(rect) rect.style.strokeDashoffset = '0'
        }
      }
    })
  }, { threshold: 0.2 })

  document.querySelectorAll('.reveal, .reveal-svg').forEach(el => observer.observe(el))

  try {
    const response = await fetch('/credits.md')
    if (response.ok) {
      const rawMarkdown = await response.text()
      // 解析 Markdown 为 HTML
      creditsContent.value = marked.parse(rawMarkdown)
    } else {
      creditsContent.value = '<p>Köszönjük a figyelmet.</p>'
    }
  } catch (e) {
    creditsContent.value = '<p>Köszönjük a figyelmet.</p>'
  }
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})

const chapters = [
  { title: "Bevezetés a Matulába", text: ["Gina új környezetbe kerül.", "A szabályok szigorúak és idegenek.", "A közösség távolságtartó.", "A lány lassan alkalmazkodik.", "Titokzatos légkör veszi körül."] },
  { title: "A rejtett üzenetek", text: ["Furcsa jelek jelennek meg.", "Abigél neve többször felbukkan.", "Titkos kommunikáció indul.", "A bizalom veszélyessé válik."] },
  { title: "Háború árnyéka", text: ["A külvilág egyre közelebb kerül.", "A feszültség nő az intézetben.", "A tanárok próbálnak rendet tartani."] },
  { title: "Abigél titka", text: ["A legenda mögött igazság van.", "Abigél szerepe világosabb lesz.", "A segítség rejtetten érkezik."] },
  { title: "Zárás", text: ["Gina megváltozik.", "Az élmények formálják.", "A történet csendesen véget ér."] }
]
</script>

<style>
/* 动画定义 */
@keyframes pulse-slow {
  0%, 100% { opacity: 0.3; transform: scale(1); }
  50% { opacity: 0.5; transform: scale(1.02); }
}
.animate-pulse-slow { animation: pulse-slow 8s ease-in-out infinite; }

@keyframes scanline {
  0% { transform: translateX(-50%); }
  100% { transform: translateX(0%); }
}
.animate-scanline { animation: scanline 4s linear infinite; }

@keyframes draw-line {
  0% { stroke-dasharray: 0 100; stroke-dashoffset: 0; }
  100% { stroke-dasharray: 100 0; stroke-dashoffset: 0; }
}
.animate-draw-line { animation: draw-line 2s ease-out infinite alternate; }

/* 页面淡入效果 */
.reveal { opacity: 0; transform: translateY(20px); transition: opacity 1s cubic-bezier(0.16, 1, 0.3, 1), transform 1s cubic-bezier(0.16, 1, 0.3, 1); }
.reveal.is-visible { opacity: 1; transform: translateY(0); }
.reveal-svg { opacity: 0; transition: opacity 0.8s ease; }
.reveal-svg.is-visible { opacity: 1; }

/* Markdown 内容样式基础 */
.markdown-body h1, .markdown-body h2 { font-weight: bold; margin-bottom: 1rem; }
.markdown-body p { margin-bottom: 0.5rem; }
.markdown-body a { text-decoration: underline; }
</style>