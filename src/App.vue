<script setup lang="ts">
import { computed, ref, watch, onMounted, onUnmounted, nextTick } from 'vue'
import content from './data/locales.json'

type Lang = 'es' | 'en'
type Theme = 'gengar' | 'blaziken'

const savedLang = localStorage.getItem('portfolio-lang') as Lang | null
const lang = ref<Lang>(savedLang === 'es' || savedLang === 'en' ? savedLang : 'es')

const savedTheme = localStorage.getItem('portfolio-theme') as Theme | null
const theme = ref<Theme>(savedTheme === 'gengar' || savedTheme === 'blaziken' ? savedTheme : 'gengar')

watch(lang, (value) => {
  localStorage.setItem('portfolio-lang', value)
})

watch(theme, (value) => {
  localStorage.setItem('portfolio-theme', value)
  document.documentElement.setAttribute('data-theme', value)
}, { immediate: true })

type StackGroup = [string, string[]]

const t = computed(() => {
  const data = content[lang.value]
  return {
    ...data,
    stackGroups: data.stackGroups as StackGroup[]
  }
})
const linkedIn = 'https://www.linkedin.com/in/luis-eduardo-ronquillo-arroyo-7328a4118'
const github = 'https://github.com/LuisRonquillo97'
const email = 'mailto:lronquillo977@gmail.com'

const isViewingCV = ref(false)

const checkHash = () => {
  isViewingCV.value = window.location.hash === '#/cv' || window.location.hash === '#cv'
}

let observer: IntersectionObserver | null = null

const setupScrollObserver = () => {
  if (observer) {
    observer.disconnect()
  }

  observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        entry.target.classList.add('visible')
        observer?.unobserve(entry.target)
      }
    })
  }, {
    threshold: 0.05,
    rootMargin: '0px 0px -50px 0px'
  })

  document.querySelectorAll('.section').forEach((section) => {
    observer?.observe(section)
  })
}

watch(isViewingCV, async (val) => {
  window.scrollTo(0, 0)
  if (!val) {
    await nextTick()
    setupScrollObserver()
  }
})

onMounted(() => {
  window.addEventListener('hashchange', checkHash)
  checkHash()
  setupScrollObserver()
})

onUnmounted(() => {
  window.removeEventListener('hashchange', checkHash)
  if (observer) {
    observer.disconnect()
  }
})

const viewCV = () => {
  window.location.hash = '#/cv'
}

const goBack = () => {
  window.location.hash = '#'
}

const printCV = () => {
  window.print()
}
</script>

<template>
  <main v-if="!isViewingCV">
    <header class="nav">
      <a class="brand" href="#">Luis Ronquillo</a>

      <nav>
        <a href="#impact">{{ t.nav[0] }}</a>
        <a href="#case">{{ t.nav[1] }}</a>
        <a href="#experience">{{ t.nav[2] }}</a>
        <a href="#stack">{{ t.nav[3] }}</a>
        <a href="#contact">{{ t.nav[4] }}</a>
      </nav>

      <div class="controls">
        <button @click="viewCV" class="btn-cv-nav">📄 {{ t.cvDownloadCTA }}</button>
        <div class="pillControl">
          <button :class="{ active: lang === 'es' }" @click="lang = 'es'">ES</button>
          <button :class="{ active: lang === 'en' }" @click="lang = 'en'">EN</button>
        </div>
        <div class="pillControl">
          <button :class="{ active: theme === 'gengar' }" @click="theme = 'gengar'">😈 {{ t.modeGengar }}</button>
          <button :class="{ active: theme === 'blaziken' }" @click="theme = 'blaziken'">👊 {{ t.modeBlaziken }}</button>
        </div>
      </div>
    </header>

    <section class="hero">
      <div class="avatarWrap">
        <div class="avatar">
          <transition name="fade" mode="out-in">
            <img :key="theme" :src="theme === 'gengar' ? '/avatar_dark.jpeg' : '/avatar_light.jpeg'">
          </transition>
        </div>
      </div>

      <p class="eyebrow">{{ t.location }}</p>
      <h1>Luis Ronquillo</h1>
      <h2>{{ t.role }}</h2>
      <p class="heroLine">{{ t.heroLine }}</p>
      <p class="intro">{{ t.intro }}</p>

      <div class="heroBadges">
        <span>AWS</span>
        <span>TypeScript</span>
        <span>Telecom</span>
        <span>Fintech</span>
        <span>Microservices</span>
      </div>

      <div class="actions">
        <a :href="email" class="btn primary">{{ t.ctaPrimary }}</a>
        <button @click="viewCV" class="btn secondary">📄 {{ t.cvDownloadCTA }}</button>
        <a :href="github" target="_blank" class="btn ghost">{{ t.ctaSecondary }}</a>
        <a :href="linkedIn" target="_blank" class="btn ghost">LinkedIn</a>
      </div>
    </section>

    <section id="impact" class="section metricSection">
      <p class="eyebrow">{{ t.metricTitle }}</p>
      <div class="stats">
        <article v-for="stat in t.stats" :key="stat[1]" class="stat">
          <strong>{{ stat[0] }}</strong>
          <span>{{ stat[1] }}</span>
        </article>
      </div>
    </section>

    <section id="case" class="section">
      <div class="sectionHeader">
        <p class="eyebrow">{{ t.projectTitle }}</p>
        <h2>{{ t.projectName }}</h2>
        <p>{{ t.projectLead }}</p>
      </div>

      <article class="caseCard">
        <ul>
          <li v-for="bullet in t.projectBullets" :key="bullet">{{ bullet }}</li>
        </ul>
      </article>
    </section>

    <section class="section">
      <div class="sectionHeader">
        <p class="eyebrow">Domain expertise</p>
        <h2>{{ t.domainsTitle }}</h2>
      </div>

      <div class="domainGrid">
        <article v-for="domain in t.domains" :key="domain[0]" class="domainCard">
          <h3>{{ domain[0] }}</h3>
          <p>{{ domain[1] }}</p>
        </article>
      </div>
    </section>

    <section id="experience" class="section experienceBlock">
      <div class="sectionHeader center">
        <p class="eyebrow">Career</p>
        <h2>{{ t.expTitle }}</h2>
      </div>

      <div class="timeline">
        <article v-for="job in t.jobs" :key="job.company" class="job">
          <div class="jobHeader">
            <div>
              <h3>{{ job.title }}</h3>
              <p>{{ job.company }}</p>
            </div>
            <span>{{ job.period }}</span>
          </div>
          <ul>
            <li v-for="point in job.points" :key="point">{{ point }}</li>
          </ul>
        </article>
      </div>
    </section>

    <section id="stack" class="section">
      <div class="sectionHeader center">
        <p class="eyebrow">Capabilities</p>
        <h2>{{ t.stackTitle }}</h2>
      </div>

      <div class="stackGrid">
        <article v-for="group in t.stackGroups" :key="group[0]" class="stackCard">
          <h3>{{ group[0] }}</h3>
          <div class="chips">
            <span v-for="item in group[1]" :key="item">{{ item }}</span>
          </div>
        </article>
      </div>

      <div class="cert">
        <span>{{ t.certTitle }}</span>
        <strong>{{ t.cert }}</strong>
      </div>
    </section>

    <section id="contact" class="section contact">
      <p class="eyebrow">{{ t.contactText }}</p>
      <h2>{{ t.contactTitle }}</h2>
      <div class="actions">
        <a :href="email" class="btn primary">{{ t.contactButton }}</a>
        <a :href="linkedIn" target="_blank" class="btn secondary">LinkedIn</a>
        <a :href="github" target="_blank" class="btn ghost">GitHub</a>
      </div>
    </section>

    <footer>© 2026 Luis Ronquillo. Built with Vue 3 + TypeScript.</footer>
  </main>

  <div v-else class="cv-page-wrapper">
    <!-- Controls bar for CV (hidden on print) -->
    <div class="cv-controls">
      <button @click="goBack" class="btn-cv-control">
        ← {{ t.cvBackButton }}
      </button>
      <div class="cv-controls-right">
        <div class="pillControl cv-lang-toggle">
          <button :class="{ active: lang === 'es' }" @click="lang = 'es'">ES</button>
          <button :class="{ active: lang === 'en' }" @click="lang = 'en'">EN</button>
        </div>
        <button @click="printCV" class="btn-cv-print">
          🖨️ {{ t.cvPrintButton }}
        </button>
      </div>
    </div>

    <!-- Printable CV Layout -->
    <main class="cv-print-view">
      <header class="cv-top">
        <span class="cv-label">{{ t.cvHeaderLabel }}</span>
        <h1>Luis Eduardo Ronquillo Arroyo</h1>
        <div class="cv-role">{{ t.cvRole }}</div>
        <p class="cv-summary">{{ t.cvSummary }}</p>

        <div class="cv-impactGrid">
          <div v-for="stat in t.stats" :key="stat[1]" class="cv-metric">
            <strong>{{ stat[0] }}</strong>
            <span>{{ stat[1] }}</span>
          </div>
        </div>

        <div class="cv-contact">
          <span>{{ t.location }}</span>
          <a :href="email">lronquillo977@gmail.com</a>
          <a :href="github" target="_blank">github.com/LuisRonquillo97</a>
          <a :href="linkedIn" target="_blank">LinkedIn</a>
        </div>
      </header>

      <div class="cv-content">
        <div class="cv-mainColumn">
          <section class="cv-section">
            <h2>{{ t.projectTitle }}</h2>
            <article class="cv-project">
              <h3>{{ t.projectName }}</h3>
              <p>{{ t.projectLead }}</p>
              <ul>
                <li v-for="bullet in t.projectBullets" :key="bullet">{{ bullet }}</li>
              </ul>
            </article>
          </section>

          <section class="cv-section">
            <h2>{{ t.expTitle }}</h2>
            <article v-for="job in t.jobs" :key="job.company" class="cv-job">
              <h3>{{ job.title }}</h3>
              <div class="cv-company">{{ job.company }} · {{ job.period }}</div>
              <ul>
                <li v-for="point in job.points" :key="point">{{ point }}</li>
              </ul>
            </article>
          </section>
        </div>

        <aside class="cv-aside">
          <section class="cv-sideBox">
            <h2>{{ t.stackTitle }}</h2>
            <div v-for="group in t.stackGroups" :key="group[0]" class="cv-skillGroup">
              <h4>{{ group[0] }}</h4>
              <div class="cv-chips">
                <span v-for="item in group[1]" :key="item" class="cv-chip">{{ item }}</span>
              </div>
            </div>
          </section>

          <section class="cv-sideBox">
            <h2>{{ t.cvSpecialtyTitle }}</h2>
            <p class="cv-smallText">{{ t.cvSpecialtyText }}</p>
          </section>

          <section class="cv-sideBox">
            <h2>{{ t.certTitle }}</h2>
            <p class="cv-smallText"><strong>{{ t.cert }}</strong></p>
          </section>

          <section class="cv-sideBox">
            <h2>{{ t.cvObjectiveTitle }}</h2>
            <p class="cv-smallText">{{ t.cvObjectiveText }}</p>
          </section>
        </aside>
      </div>

      <footer class="cv-footer">
        <span><strong>{{ t.cvKeywordsTitle }}:</strong> {{ t.cvKeywordsText }}</span>
      </footer>
    </main>
  </div>
</template>
