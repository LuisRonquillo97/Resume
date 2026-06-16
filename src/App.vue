<script setup lang="ts">
import { computed, ref, watch } from 'vue'

type Lang = 'es' | 'en'
type Theme = 'gengar' | 'blaziken'

const lang = ref<Lang>('es')
const theme = ref<Theme>('gengar')

watch(theme, (value) => {
  document.documentElement.setAttribute('data-theme', value)
}, { immediate: true })

const content = {
  es: {
    nav: ['Impacto', 'Case Study', 'Experiencia', 'Stack', 'Contacto'],
    role: 'Lead Backend Engineer',
    heroLine: 'Backend cloud para sistemas que no pueden fallar.',
    intro: 'Construyo plataformas backend escalables para telecomunicaciones y servicios financieros: microservicios, APIs productivas, integraciones enterprise y modernización de sistemas legacy sobre AWS.',
    ctaPrimary: 'Contactar',
    ctaSecondary: 'Ver GitHub',
    location: 'Mérida, Yucatán, México',
    metricTitle: 'Impacto técnico',
    stats: [
      ['30+', 'Microservicios'],
      ['15+', 'APIs empresariales'],
      ['5+', 'Developers liderados'],
      ['6+', 'Años de experiencia']
    ],
    projectTitle: 'Proyecto insignia',
    projectName: 'MVNO Macropay + Altán',
    projectLead: 'Lideré técnicamente el backend del operador móvil virtual de Macropay desde cero, integrando telecomunicaciones, pagos, SAP y procesos críticos de negocio.',
    projectBullets: [
      'Integración con Altán mediante Innovatia.',
      'Flujos para líneas nuevas, portabilidad numérica y recargas.',
      'Envío automático de pagos exitosos hacia SAP para procesos contables.',
      'Backend basado en microservicios, APIs REST, TypeScript y AWS.',
      'Supervisión de frontend, soporte QA y resolución de defectos.'
    ],
    domainsTitle: 'Donde genero valor',
    domains: [
      ['Telecom', 'MVNO, Altán, portabilidad, recargas y servicios móviles.'],
      ['Fintech', 'SAP, Belvo, Tapi, créditos, pagos e integraciones financieras.'],
      ['Cloud', 'AWS Lambda, ECS, API Gateway, SQS, DynamoDB, S3 y CloudWatch.'],
      ['Modernización', 'Migración legacy, desacoplamiento de monolitos y event-driven systems.']
    ],
    expTitle: 'Experiencia profesional',
    jobs: [
      {
        company: 'Fundación Rafael Dondé IAP',
        title: 'Senior Fullstack / Backend Developer',
        period: 'Feb 2025 – Actualidad',
        points: [
          'Modernización de sistemas legacy hacia tecnologías actuales.',
          'Integración de colas Amazon SQS con monolitos para desacoplar procesos críticos.',
          'Integraciones financieras con Tapi.',
          'Desarrollo de APIs, microservicios y soluciones cloud sobre AWS.'
        ]
      },
      {
        company: 'Macropay',
        title: 'Backend Semi Senior / Technical Lead',
        period: 'Sep 2022 – Feb 2025',
        points: [
          'Liderazgo técnico en plataforma MVNO sobre infraestructura Altán.',
          'Desarrollo de 30+ microservicios y 15+ APIs en TypeScript/JavaScript.',
          'Servicios en AWS Lambda, ECS, API Gateway, SQS, DynamoDB, S3 y CloudWatch.',
          'Integraciones con SAP, Belvo y sistemas internos de crédito.'
        ]
      },
      {
        company: 'Grupo Boxito / Blue Ocean / COMA',
        title: 'Software Engineer',
        period: '2019 – 2022',
        points: [
          'APIs internas, automatización de procesos y software empresarial.',
          'Experiencia con C#, SQL Server, Oracle, Angular, Azure, IIS y sistemas legacy.'
        ]
      }
    ],
    stackTitle: 'Stack tecnológico',
    stackGroups: [
      ['Backend', ['Node.js', 'TypeScript', 'JavaScript', 'C#', '.NET', 'REST APIs', 'Microservices']],
      ['AWS', ['Lambda', 'ECS', 'API Gateway', 'SQS', 'DynamoDB', 'S3', 'CloudWatch']],
      ['DevOps', ['Docker', 'Jenkins', 'CI/CD', 'Git', 'Dev / QA / Staging / Prod']],
      ['Enterprise', ['SAP', 'Belvo', 'Tapi', 'Legacy modernization', 'Event-driven systems']]
    ],
    certTitle: 'Certificación',
    cert: 'AWS Associate — en proceso',
    contactTitle: 'Listo para construir sistemas de alto impacto',
    contactText: 'Abierto a oportunidades como Lead Backend Engineer, Senior Backend Engineer o AWS Backend Engineer en fintech, telecom, banca, seguros o modernización cloud.',
    contactButton: 'Enviar correo',
    modeGengar: 'Oscuro',
    modeBlaziken: 'Claro'
  },
  en: {
    nav: ['Impact', 'Case Study', 'Experience', 'Stack', 'Contact'],
    role: 'Lead Backend Engineer',
    heroLine: 'Cloud backend for systems that cannot fail.',
    intro: 'I build scalable backend platforms for telecom and financial services: microservices, production APIs, enterprise integrations and AWS-based legacy modernization.',
    ctaPrimary: 'Contact',
    ctaSecondary: 'View GitHub',
    location: 'Mérida, Yucatán, Mexico',
    metricTitle: 'Technical impact',
    stats: [
      ['30+', 'Microservices'],
      ['15+', 'Enterprise APIs'],
      ['5+', 'Developers led'],
      ['6+', 'Years of experience']
    ],
    projectTitle: 'Signature project',
    projectName: 'Macropay MVNO + Altán',
    projectLead: 'Technical leadership in the backend development of Macropay’s MVNO from zero, integrating telecom services, payments, SAP and business-critical processes.',
    projectBullets: [
      'Integration with Altán through Innovatia.',
      'New line activation, number portability and mobile top-up flows.',
      'Automatic delivery of successful payment data to SAP for accounting processes.',
      'Backend based on microservices, REST APIs, TypeScript and AWS.',
      'Frontend supervision, QA support and defect resolution.'
    ],
    domainsTitle: 'Where I create value',
    domains: [
      ['Telecom', 'MVNO, Altán, portability, mobile top-ups and mobile services.'],
      ['Fintech', 'SAP, Belvo, Tapi, credit systems, payments and financial integrations.'],
      ['Cloud', 'AWS Lambda, ECS, API Gateway, SQS, DynamoDB, S3 and CloudWatch.'],
      ['Modernization', 'Legacy migration, monolith decoupling and event-driven systems.']
    ],
    expTitle: 'Professional experience',
    jobs: [
      {
        company: 'Fundación Rafael Dondé IAP',
        title: 'Senior Fullstack / Backend Developer',
        period: 'Feb 2025 – Present',
        points: [
          'Modernization of legacy systems into current technologies.',
          'Amazon SQS queue integration with monolithic systems to decouple critical processes.',
          'Financial integrations with Tapi.',
          'Backend APIs, microservices and AWS cloud solutions.'
        ]
      },
      {
        company: 'Macropay',
        title: 'Backend Semi Senior / Technical Lead',
        period: 'Sep 2022 – Feb 2025',
        points: [
          'Technical leadership in an MVNO platform built on Altán infrastructure.',
          'Built 30+ microservices and 15+ APIs using TypeScript/JavaScript.',
          'Implemented services using AWS Lambda, ECS, API Gateway, SQS, DynamoDB, S3 and CloudWatch.',
          'Integrations with SAP, Belvo and internal credit systems.'
        ]
      },
      {
        company: 'Grupo Boxito / Blue Ocean / COMA',
        title: 'Software Engineer',
        period: '2019 – 2022',
        points: [
          'Internal APIs, process automation and enterprise software systems.',
          'Experience with C#, SQL Server, Oracle, Angular, Azure, IIS and legacy systems.'
        ]
      }
    ],
    stackTitle: 'Technical stack',
    stackGroups: [
      ['Backend', ['Node.js', 'TypeScript', 'JavaScript', 'C#', '.NET', 'REST APIs', 'Microservices']],
      ['AWS', ['Lambda', 'ECS', 'API Gateway', 'SQS', 'DynamoDB', 'S3', 'CloudWatch']],
      ['DevOps', ['Docker', 'Jenkins', 'CI/CD', 'Git', 'Dev / QA / Staging / Prod']],
      ['Enterprise', ['SAP', 'Belvo', 'Tapi', 'Legacy modernization', 'Event-driven systems']]
    ],
    certTitle: 'Certification',
    cert: 'AWS Associate — in progress',
    contactTitle: 'Ready to build high-impact systems',
    contactText: 'Open to Lead Backend Engineer, Senior Backend Engineer or AWS Backend Engineer opportunities in fintech, telecom, banking, insurance or cloud modernization.',
    contactButton: 'Send email',
    modeGengar: 'Dark',
    modeBlaziken: 'Light'
  }
}

const t = computed(() => content[lang.value])
const linkedIn = 'https://www.linkedin.com/in/luis-eduardo-ronquillo-arroyo-7328a4118'
const github = 'https://github.com/LuisRonquillo97'
const email = 'mailto:lronquillo977@gmail.com'
</script>

<template>
  <main>
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
        <div class="pillControl">
          <button :class="{ active: theme === 'gengar' }" @click="theme = 'gengar'">👻 {{ t.modeGengar }}</button>
          <button :class="{ active: theme === 'blaziken' }" @click="theme = 'blaziken'">🔥 {{ t.modeBlaziken }}</button>
        </div>
        <div class="pillControl">
          <button :class="{ active: lang === 'es' }" @click="lang = 'es'">ES</button>
          <button :class="{ active: lang === 'en' }" @click="lang = 'en'">EN</button>
        </div>
      </div>
    </header>

    <section class="hero">
      <div class="avatarWrap">
        <div class="avatar">LR</div>
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
        <a :href="github" target="_blank" class="btn secondary">{{ t.ctaSecondary }}</a>
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
      <p class="eyebrow">{{ t.contactTitle }}</p>
      <h2>{{ t.contactText }}</h2>
      <div class="actions">
        <a :href="email" class="btn primary">{{ t.contactButton }}</a>
        <a :href="linkedIn" target="_blank" class="btn secondary">LinkedIn</a>
        <a :href="github" target="_blank" class="btn ghost">GitHub</a>
      </div>
    </section>

    <footer>© 2026 Luis Ronquillo. Built with Vue 3 + TypeScript.</footer>
  </main>
</template>
