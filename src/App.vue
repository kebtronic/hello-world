<script setup>
import { onMounted, onUnmounted, ref } from 'vue'

const activeSection = ref('')
const menuOpen = ref(false)
const lastUpdated = __LAST_UPDATED__

const heroPhotos = [
  '/img/hero-fuwg-aa-01.jpg',
  '/img/hero-fupe-01.jpg',
  '/img/hero-fuwg-ra-01.jpg',
  '/img/hero-fuwg-jra-01.jpg',
  '/img/hero-fuwg-aa-02.jpg',
  '/img/hero-fuwg-ra-02.jpg',
  '/img/hero-fuwg-aa-03.jpg',
]
const partnerLogos = [
  { src: '/img/fhs-boosters.svg', alt: 'Farmington High School Music Boosters', url: 'https://www.fhsmusic.org/' },
  { src: '/img/nfhs-boosters.svg', alt: 'North Farmington High School Music Boosters', url: 'https://www.nfhsmusic.org' },
  { src: '/img/mapa-logo.svg', alt: 'Michigan Alliance for Performing Arts', url: 'https://www.performmapa.org' },
]
const heroGalleryCycleDuration = 24_000
const activeHeroPhoto = ref(0)
let heroPhotoInterval

const ensembles = [
  {
    number: '01',
    name: 'Farmington United Percussion',
    id: 'farmington-united-percussion',
    tag: 'Shades of Life',
    description: 'Our competitive percussion ensemble combining both mallet and battery percussion to create dynamic performances.',
    image: '/img/section-thumb-fupe.jpg',
    imageAlt: 'Musician performing on stage with focused lighting',
    history: 'Farmington United Percussion has built a tradition of ambitious indoor percussion through committed musicianship, visual storytelling, and ensemble collaboration. Program alumni continue to carry that spirit into the activity as performers, educators, and staff.',
    videoId: 'jvTzm_kL7Ec',
    videoUrl: 'https://www.youtube.com/watch?v=jvTzm_kL7Ec',
    instagramUrl: 'https://www.instagram.com/farmingtonunitedperc/',
    facebookUrl: 'https://www.facebook.com/profile.php?id=61582896243125',
    historyTimeline: [
      {
        year: '2026',
        events: [
          { date: 'Mar 21', location: 'Kent City High School - 351 North Main St., Kent City, MI 49330', description: 'MAPA Kent City - Percussion Independent A (4th place)', score: '72.650' },
          { date: 'Feb 21', location: 'Milford High School - 2380 South Milford Rd., Highland Charter Township, MI 48381', description: 'MAPA Milford - Percussion Independent A (3rd place)', score: '69.750' },
        ],
      },
      { year: '2020–2025', events: [], note: 'Ensemble did not compete' },
      {
        year: '2019',
        events: [
          { date: 'Apr 11', location: 'Hobart Arena - Troy, OH', description: 'WGI Percussion World Championships - PIO Prelims', score: '82.863' },
          { date: 'Feb 9', location: 'Troy Athens High School - Troy, MI', description: 'WGI Troy Percussion Regional Prelims', score: '70.150' },
        ],
      },
      {
        year: '2018',
        events: [
          { date: 'Apr 20', location: 'University of Dayton Arena, Dayton, OH', description: 'WGI Percussion World Championships A Class Finals', score: '91.075' },
          { date: 'Apr 19', location: 'BB&T Arena at Northern Kentucky University, Highland Heights, OH', description: 'WGI Percussion World Championships PIA Prelims', score: '89.950' },
        ],
      },
      {
        year: '2017',
        events: [
          { date: 'Apr 21', location: 'University of Dayton Arena, Dayton, OH', description: 'WGI Percussion World Championships A Class Finals', score: '95.100' },
          { date: 'Apr 20', location: 'BB&T Arena, Northern Kentucky University, Highland Heights, KY', description: 'WGI Percussion World Championships PIA Prelims', score: '92.450' },
          { date: 'Feb 11', location: 'Troy Athens High School, Troy, MI', description: 'WGI Troy Percussion Regional Prelims', score: '73.350' },
        ],
      },
      {
        year: '2016',
        events: [
          { date: 'Apr 15', location: 'Dayton, OH', description: 'WGI Percussion World Championships A Class Finals', score: '89.850' },
          { date: 'Apr 14', location: 'Oxford, OH', description: 'WGI Percussion World Championships PIA Prelims', score: '87.850' },
          { date: 'Feb 6', location: 'Troy, MI', description: 'WGI Troy Percussion Regional Prelims', score: '71.850' },
        ],
      },
      {
        year: '2015',
        events: [
          { date: 'Apr 10', location: 'Dayton, OH', description: 'WGI Percussion World Championships PIA Class Finals', score: '91.700' },
          { date: 'Apr 9', location: 'Dayton, OH', description: 'WGI Percussion World Championships PIA Class Prelims', score: '89.075' },
          { date: 'Feb 7', location: 'Troy, MI', description: 'WGI Troy Percussion Regional Prelims', score: '79.900' },
        ],
      },
      {
        year: '2014',
        events: [
          { date: 'Apr 11', location: 'University of Dayton - Dayton, OH', description: 'WGI Percussion World Championships - A Class Finals', score: '90.288' },
          { date: 'Apr 10', location: 'Millett Hall, Oxford, OH', description: 'WGI Percussion World Championships - PIA Prelims', score: '88.650' },
          { date: 'Feb 8', location: 'Troy, MI', description: 'WGI Troy Percussion Regional Prelims', score: '69.250' },
        ],
      },
    ],
  },
  {
    number: '02',
    name: 'Farmington United Winter Guard AA',
    id: 'farmington-united-winter-guard-aa',
    tag: 'As The Show Falls',
    description: 'Our Independent AA winter guard auditioned ensemble that competes both in WGI and MCGC.',
    image: '/src/assets/section-thumb-fuwg-aa.jpg',
    imageAlt: 'Performers moving together in a colorful stage production',
    history: 'The Farmington United Winter Guard dates back to the 2007-2008 competition season. Our AA Winter Guard brings together dedicated performers through technical confidence, creativity, and visual storytelling. Through strong team culture, collaboration, and a passion for the activity, this audition-based ensemble creates engaging performances that highlight expressive movement and original design.',
    videoId: 'RDjABkFP9CQ',
    videoUrl: 'https://www.youtube.com/watch?v=RDjABkFP9CQ',
    instagramUrl: 'https://www.instagram.com/farmingtonunitedwg/',
    facebookUrl: 'https://www.facebook.com/profile.php?id=61591598862870',
    historyTimeline: [
      {
        year: '2026',
        events: [
          {
            date: 'Mar 7',
            location: 'Stoney Creek High School',
            description: 'Stoney Creek - Independent AA (1st place)',
            score: '74.380',
          },
          {
            date: 'Feb 21',
            location: 'Grand Blanc, MI',
            description: '2026 WGI Flint Color Guard Regional - Independent A Finals (6th place)',
            score: '68.820',
          },
        ],
      },
      {
        year: '2025',
        events: [
          {
            date: 'Mar 29',
            location: '1660 Ring Road South, Kalamazoo, MI',
            description: 'Read Fieldhouse / University Arena',
            score: '71.585',
          },
          {
            date: 'Feb 23',
            location: '495 E Scripps Road, Lake Orion, MI',
            description: 'Lake Orion High School',
            score: '65.490',
          },
        ],
      },
      {
        year: '2024',
        events: [
          {
            date: 'Apr 6',
            location: 'MCGC Championships, MI',
            description: 'MCGC - Scholastic Regional A',
            score: '73.105',
          },
          {
            date: 'Mar 17',
            location: 'Stoney Creek HS, MI',
            description: 'MCGC - Scholastic Regional A',
            score: '68.020',
          },
          {
            date: 'Feb 17',
            location: 'Milford HS (Huron Valley), MI',
            description: 'MCGC - Scholastic Regional A',
            score: '55.980',
          },
          {
            date: 'Jan 20',
            location: 'Novi HS, MI',
            description: 'MCGC - Scholastic Regional A',
            score: '45.630',
          },
        ],
      },
    ],
  },
  {
    number: '03',
    name: 'Farmington United Winter Guard RA',
    id: 'farmington-united-winter-guard-ra',
    tag: 'On the Poolside',
    description: 'Our Independent Regional A winter guard that welcomes all high school students that want to experience the passion of performing.',
    image: '/src/assets/section-thumb-fuwg-ra.jpg',
    imageAlt: 'Dance ensemble performing with expressive movement',
    history: 'Revived in 2023 after a three year hiatus, our RA is the founding and core ensemble of FUWG.  This program gives performers a competitive setting to expand their movement, equipment, and performance skills. Its history is defined by steady growth, supportive mentorship, and the next-generation leadership within the program.',
    videoUrl: 'https://www.facebook.com/share/r/1RzRAjcXGS/',
    instagramUrl: 'https://www.instagram.com/farmingtonunitedwg/',
    facebookUrl: 'https://www.facebook.com/profile.php?id=61591598862870',
  },
  {
    number: '04',
    name: 'Farmington United Winter Guard JRA',
    id: 'farmington-united-winter-guard-jra',
    tag: 'From Seed to Self',
    description: 'A welcoming ensemble for 5th–8th grade performers to build their skills, grow in confidence, and discover the joy of performing together.',
    image: '/src/assets/section-thumb-fuwg-jra.jpg',
    imageAlt: 'Young performers rehearsing together outdoors',
    history: 'Our newest ensemble, FUWG-JRA is open to 5th-8th grade students as an entry point for younger and newer performers to discover the winter guard activity. It emphasizes fundamental skills, teamwork, and confidence in a welcoming competitive environment.',
    videoPlaceholder: true,
    instagramUrl: 'https://www.instagram.com/farmingtonunitedwg/',
    facebookUrl: 'https://www.facebook.com/profile.php?id=61591598862870',
  },
]
 

const staff = [
  { name: 'Chloe Tooson', role: 'FUWG Director', image: '/src/assets/staff-chloe.jpg', bio: 'Chloe leads the Winter Guard programs with a great attitude and dedication to excellence. With 15+ years of experience in the activity, she brings a wealth of knowledge and passion to every rehearsal and performance.', experience: ['NPAS ’25/26','W3G Director ’17-’23', 'FUWG Director ’21-Present'] },
  { name: 'Kaitlyn Dobberteen', role: 'FUWG Staff', image: '/src/assets/staff-kaitlyn.jpg', bio: 'Kaitlyn is a dedicated member of the FUWG staff, contributing to the development and performance of the winter guard ensembles.', experience: ['EMI ’24', 'RAI ’23', 'FHS ’21', 'CGC ’22', 'NVA ’25'] },
  { name: 'Brittany Buckner', role: 'FUWG Staff', image: '/src/assets/staff-brittany.jpg', bio: 'Brittany is an integral member of the FUWG staff, she helps run rehearsals, create choreography, and brings a positive attitude to the team.', experience: ['MCP ’23', 'EMU ’24', 'RHY ’22'] },
  { name: 'Mya Tooson', role: 'FUWG Assistant Director', image: '/src/assets/staff-mya.jpg', bio: 'Mya is a very important member of the FUWG staff, she works closely with the members and pushes them as performers and people. She is also soon to be married to her fiancé.', experience: ['CGC ’24', 'FHS ’25', 'NVA ’22', 'RAI ’23', 'UNI ’21'] },
  { name: 'Madeline Fenech', role: 'FUWG Staff', image: '/src/assets/staff-maddie.jpg', bio: 'Madeline is a dedicated member of the FUWG staff, contributing to the development and performance of the winter guard ensembles.', experience: ['FHS ’24', 'CGC ’23', 'NVA ’22'] },
  { name: 'Connor Lindenmuth', role: 'FUWG Staff', image: '/src/assets/staff-connor.jpg', bio: 'Connor is a dedicated member of the FUWG staff, contributing to the development and performance of the winter guard ensembles.', experience: ['NPAS ’26'] },
  { name: 'Gracie Barber', role: 'FUWG Staff', image: '/src/assets/staff-silhouette-woman.svg', imageAlt: 'Generic woman silhouette illustration' },
  { name: 'Sarah Bedolla', role: 'FUWG Staff and Admin Support', image: '/src/assets/staff-sarah.jpg', imageAlt: 'Sarah FUPE Staff' },
  { name: 'Mason Keberly', role: 'FUPE Assistant Director', image: '/src/assets/staff-keberly.jpg', bio: 'Mason is one of FUPE\'s new assistant directors. With six years of battery percussion experience, Mason brings his competitive and collegiate percussion background to the FUPE staff.', experience: ['EMU ’25', 'MCP ’24', 'FHS ’23', 'NEX ’22', 'ARC ’21'] },
  { name: 'Aaron McKay', role: 'FUPE Director', image: '/src/assets/staff-mr-mckay.jpg', bio: 'Aaron is the new director of FUPE. He brings 10+ years of percussive experience in both front ensemble and battery percussion. Along with the director of FUWG, Chloe, Aaron is excited to lead the program to new horizons.', experience: ['LEP ’22/23', 'MCP ’24', 'MTXO ’25', 'EMU ’23'] },
  { name: 'Jake Brown', role: 'FUPE Assistant', image: '/src/assets/staff-jake.jpg', bio: 'Jake is our other assistant director of FUPE. He brings 12+ years of front ensemble experience to the group. Fun fact, Jake is an alum of the program, marching with FUPE from 2014-2019 and helping the group earn one of two second place medals.', experience: ['NVA ’25', 'EMU ’23', 'MCP ’22', 'UNI ’21'] },
  { name: 'Mason Martin', role: 'FUPE Front Ensemble Technician', image: '/src/assets/staff-martin.jpg', bio: 'Mason is a dedicated member of the FUPE staff, contributing to the development and performance of the percussion ensembles.', experience: ['FHS ’24', 'ARC ’23', 'MCP ’21', 'RHY ’22', 'CGC ’25'] },
  { name: 'Jaydenn Rush', role: 'FUPE Cymbal Technician', image: '/src/assets/staff-rush.jpg', bio: 'Jaden is a dedicated member of the FUPE staff, contributing to the development and performance of the percussion ensembles.', experience: ['NEX ’25', 'EMU ’24', 'RAI ’22', 'WVE ’23', 'UNI ’21'] },
  { name: 'Ryan Keberly', role: 'FUWE Media Intern', image: '/src/assets/staff-ryan.jpg', bio: 'Ryan captures and shares the story of the program through his expert photography and media skills, highlighting the performers, rehearsals, and performances.', experience: ['WSU FPCA'] },
]

const experienceTooltips = {
  FHS: 'Farmington High School Marching Band',
  EMU: 'Eastern Michigan Marching Band',
  MCP: 'Motor City Percussion',
  NPAS: 'Norse Performing Arts Society',
  FUWG: 'Farmington United Winter Guard',
  MTXO: 'Matrix Open',
}

const getExperienceTooltip = (item) => {
  const abbreviation = item.match(/^([A-Z]+)/)?.[1]
  return experienceTooltips[abbreviation] ?? null
}

const scrollTo = (id) => {
  activeSection.value = id.slice(1)
  menuOpen.value = false
  document.querySelector(id)?.scrollIntoView({ behavior: 'smooth' })
}

const updateActiveSection = () => {
  const sections = ['ensembles', 'staff', 'about', 'contact']
  const marker = window.scrollY + window.innerHeight * 0.35
  let current = ''

  for (const id of sections) {
    const section = document.getElementById(id)
    if (section && section.offsetTop <= marker) current = id
  }

  activeSection.value = current
}

onMounted(() => {
  updateActiveSection()
  window.addEventListener('scroll', updateActiveSection, { passive: true })

  if (heroPhotos.length > 1 && !window.matchMedia('(prefers-reduced-motion: reduce)').matches) {
    heroPhotoInterval = window.setInterval(() => {
      activeHeroPhoto.value = (activeHeroPhoto.value + 1) % heroPhotos.length
    }, heroGalleryCycleDuration / heroPhotos.length)
  }
})

onUnmounted(() => {
  window.removeEventListener('scroll', updateActiveSection)
  window.clearInterval(heroPhotoInterval)
})
</script>

<template>
  <main>
    <nav class="nav" aria-label="Main navigation">
      <button class="brand" type="button" @click="scrollTo('#top')" aria-label="Farmington United home">
        <img src="/src/assets/fuwe-logo.svg" alt="farmington united winter ensembles" />
      </button>
      <button
        class="menu-toggle"
        type="button"
        :aria-expanded="menuOpen"
        aria-controls="mobile-navigation"
        aria-label="Toggle navigation menu"
        @click="menuOpen = !menuOpen"
      >
        <span></span><span></span><span></span>
      </button>
      <div id="mobile-navigation" :class="['nav-links', { open: menuOpen }]">
        <button :class="{ active: activeSection === 'ensembles' }" type="button" @click="scrollTo('#ensembles')">Ensembles</button>
        <button :class="{ active: activeSection === 'staff' }" type="button" @click="scrollTo('#staff')">Staff</button>
        <button :class="{ active: activeSection === 'about' }" type="button" @click="scrollTo('#about')">About</button>
        <button class="nav-contact" :class="{ active: activeSection === 'contact' }" type="button" @click="scrollTo('#contact')">Join the team</button>
      </div>
    </nav>

    <section id="top" class="hero-section">
      <div class="hero-copy">
        <p class="eyebrow"><span></span> Farmington United Winter Ensembles</p>
        <h1>United by<br /><em>sound and motion.</em></h1>
        <p class="intro">The Farmington United Winter Ensembles are four distinct programs that bring percussion and color guard artists together for a season of bold music, movement, and performance. 
          Auditions occur in late fall, rehearsals and competitions begin in early winter.
         Our ensembles compete in the Michigan Alliance for Performing Arts (MAPA), Michigan Color Guard Circuit (MCGC) and Winter Guard International (WGI) circuits.</p>
        <button class="primary-button" type="button" @click="scrollTo('#ensembles')">
          Meet the ensembles <span aria-hidden="true">↓</span>
        </button>
      </div>

      <div class="hero-gallery" aria-label="Farmington United performance gallery">
        <img
          v-for="(photo, index) in heroPhotos"
          :key="photo"
          :src="photo"
          :class="['gallery-photo', { active: index === activeHeroPhoto }]"
          :alt="`Farmington United performance gallery photo ${index + 1}`"
        />
        <div class="gallery-overlay"></div>
        <div class="gallery-caption"><span>Farmington United</span><span>Winter Ensembles</span></div>
      </div>
    </section>

    <section id="ensembles" class="ensembles-section">
      <header class="section-heading">
        <p class="eyebrow"><span></span> Our Programs</p>
        <h2>Four paths.<br />One family.</h2>
      </header>

      <div class="ensemble-grid">
        <a
          v-for="ensemble in ensembles"
          :key="ensemble.number"
          :href="`#${ensemble.id}`"
          class="ensemble-card"
          :aria-label="`Learn more about ${ensemble.name}`"
        >
          <div class="card-top">
            <span class="number">{{ ensemble.number }}</span>
            <span class="tag">{{ ensemble.tag }}</span>
          </div>
          <div class="ensemble-thumbnail">
            <img :src="ensemble.image" :alt="ensemble.imageAlt" />
            <span class="thumbnail-label">{{ ensemble.name }}</span>
          </div>
          <div class="card-body">
            <h3>{{ ensemble.name }}</h3>
            <p>{{ ensemble.description }}</p>
          </div>
          <span class="card-link">
            Learn more <span aria-hidden="true">→</span>
          </span>
        </a>
      </div>
    </section>

    <div class="ensemble-details" aria-label="Ensemble histories and highlight videos">
      <section
        v-for="ensemble in ensembles"
        :id="ensemble.id"
        :key="`detail-${ensemble.number}`"
        class="ensemble-detail"
        :class="{ 'ensemble-detail-with-history': ensemble.historyTimeline }"
      >
        <div class="ensemble-detail-heading">
          <p class="eyebrow"><span></span> Ensemble {{ ensemble.number }}</p>
          <h2>{{ ensemble.name }}</h2>
        </div>
        <div class="ensemble-detail-copy">
          <h3>Our history</h3>
          <p>{{ ensemble.history }}</p>
          <a
            v-if="ensemble.videoUrl"
            class="video-preview"
            :href="ensemble.videoUrl"
            target="_blank"
            rel="noopener noreferrer"
            :aria-label="`Watch the previous year's highlight video for ${ensemble.name}`"
          >
            <img
              :src="ensemble.videoId ? `https://img.youtube.com/vi/${ensemble.videoId}/hqdefault.jpg` : ensemble.image"
              :alt="ensemble.videoId ? `${ensemble.name} highlight video preview` : ensemble.imageAlt"
              loading="lazy"
            />
            <span class="video-preview-play" aria-hidden="true">▶</span>
          </a>
          <div v-else-if="ensemble.videoPlaceholder" class="video-preview video-preview-placeholder">
            <img :src="ensemble.image" :alt="ensemble.imageAlt" loading="lazy" />
            <span>Video coming soon</span>
          </div>
          <div v-if="ensemble.historyTimeline" class="fupe-history" :aria-label="`${ensemble.name} history`">
            <template v-for="season in ensemble.historyTimeline" :key="season.year">
              <div v-if="season.year === '2026'" class="history-year history-year-current">
                <h3>{{ season.year }} Scores</h3>
                <div v-if="season.events.length" class="history-events">
                  <article
                    v-for="(event, eventIndex) in season.events"
                    :key="`${season.year}-${event.date}-${event.description}`"
                    class="history-event"
                    :class="{ 'history-event-alt': eventIndex % 2 === 1 }"
                  >
                    <div class="history-event-main">
                      <span class="history-date">{{ event.date }}</span>
                      <div class="history-event-details">
                        <p>{{ event.description }}</p>
                        <span class="history-location">{{ event.location }}</span>
                      </div>
                    </div>
                    <strong class="history-score">{{ event.score }}</strong>
                  </article>
                </div>
                <p v-else class="history-empty">{{ season.note || 'No recorded results available' }}</p>
              </div>
            </template>
            <details v-if="ensemble.historyTimeline.some((season) => season.year !== '2026')" class="history-archive">
              <summary>View historic scores</summary>
              <div
                v-for="season in ensemble.historyTimeline.filter((season) => season.year !== '2026')"
                :key="season.year"
                class="history-year"
                :class="{ 'history-year-divider': season.year === '2019' }"
              >
                <h3>{{ season.year }}</h3>
                <div v-if="season.events.length" class="history-events">
                  <article
                    v-for="(event, eventIndex) in season.events"
                    :key="`${season.year}-${event.date}-${event.description}`"
                    class="history-event"
                    :class="{ 'history-event-alt': eventIndex % 2 === 1 }"
                  >
                    <div class="history-event-main">
                      <span class="history-date">{{ event.date }}</span>
                      <div class="history-event-details">
                        <p>{{ event.description }}</p>
                        <span class="history-location">{{ event.location }}</span>
                      </div>
                    </div>
                    <strong class="history-score">{{ event.score }}</strong>
                  </article>
                </div>
                <p v-else class="history-empty">{{ season.note || 'No recorded results available' }}</p>
              </div>
            </details>
          </div>
        </div>
      </section>
    </div>

    <section id="staff" class="staff-section">
      <header class="staff-heading">
        <div>
          <p class="eyebrow"><span></span> Program Leadership</p>
          <h2>Meet the staff.</h2>
        </div>
        <p>Artists, educators, and designers committed to building a thoughtful performance culture.</p>
      </header>
      <div class="staff-grid">
        <article v-for="member in staff" :key="member.name" class="staff-card">
          <div class="staff-photo-wrap">
            <img v-if="member.image" class="staff-photo" :src="member.image" :alt="member.imageAlt || member.name" />
            <span v-else class="staff-photo-placeholder" aria-hidden="true">{{ member.name.split(' ').map((part) => part[0]).join('') }}</span>
          </div>
          <div class="staff-details">
            <h3>{{ member.name }}</h3>
            <p class="staff-role">{{ member.role }}</p>
            <p v-if="member.bio" class="staff-bio">{{ member.bio }}</p>
            <div v-if="member.experience" class="experience" aria-label="Experience">
              <span
                v-for="item in member.experience"
                :key="item"
                :class="{ 'experience-tooltip': getExperienceTooltip(item) }"
                :data-tooltip="getExperienceTooltip(item)"
                :tabindex="getExperienceTooltip(item) ? 0 : undefined"
                :aria-label="getExperienceTooltip(item) ? `${item}: ${getExperienceTooltip(item)}` : undefined"
              >{{ item }}</span>
            </div>
          </div>
        </article>
      </div>
    </section>

    <section id="about" class="about-section">
      <p class="eyebrow light"><span></span> Our Community</p>
      <div class="about-layout">
        <h2>Powered by<br />our community.</h2>
      </div>
      <p class="about-support">
        FUWE is financially supported and operated under Farmington Music Patrons, a 501(c)(3), with assistance from the North Farmington Music Patrons. It is a proud result of cross-district collaboration among Farmington Public Schools in support of all performing arts programs.
      </p>
      <div class="partner-logos">
        <a
          v-for="partner in partnerLogos"
          :key="partner.src"
          class="partner-logo"
          :href="partner.url"
          target="_blank"
          rel="noopener noreferrer"
          :aria-label="`Visit ${partner.alt} website`"
        >
          <img :src="partner.src" :alt="partner.alt" loading="lazy" />
        </a>
      </div>
    </section>

    <section id="contact" class="contact-section">
      <div>
        <p class="eyebrow"><span></span> Get Involved</p>
        <h2>Ready to take<br />the floor?</h2>
      </div>
      <a class="primary-button" href="mailto:info@farmingtonunited.org">
        Join Farmington United <span aria-hidden="true">→</span>
      </a>
    </section>

    <footer>
      <span class="footer-brand">Farmington United Winter Ensembles</span>
      <span class="footer-updated">Last updated: {{ lastUpdated }}</span>
      <nav class="footer-socials" aria-label="Program social media">
        <div class="footer-social-group footer-social-fupe">
          <span class="footer-group-label">FUPE</span>
          <a
            class="social-link"
            href="https://www.instagram.com/farmingtonunitedperc/"
            target="_blank"
            rel="noopener noreferrer"
            aria-label="FUPE Instagram"
          >
            <svg viewBox="0 0 24 24" aria-hidden="true">
              <rect x="3" y="3" width="18" height="18" rx="5"></rect>
              <circle cx="12" cy="12" r="4"></circle>
              <circle cx="17.5" cy="6.5" r="1" class="social-dot"></circle>
            </svg>
          </a>
          <a
            class="social-link"
            href="https://www.facebook.com/profile.php?id=61582896243125"
            target="_blank"
            rel="noopener noreferrer"
            aria-label="FUPE Facebook"
          >
            <svg viewBox="0 0 24 24" aria-hidden="true">
              <path d="M14.3 8.2V6.7c0-.7.5-.9.9-.9h2.3V2.1L14.4 2c-3.5 0-4.3 2.6-4.3 4.3v1.9H7.8v3.7h2.3V22h4.2V11.9h3.1l.4-3.7h-3.5z"></path>
            </svg>
          </a>
        </div>
        <div class="footer-social-group footer-social-winter-guard">
          <span class="footer-group-label">Winter Guard</span>
          <a
            class="social-link"
            href="https://www.instagram.com/farmingtonunitedwg/"
            target="_blank"
            rel="noopener noreferrer"
            aria-label="Farmington United Winter Guard Instagram"
          >
            <svg viewBox="0 0 24 24" aria-hidden="true">
              <rect x="3" y="3" width="18" height="18" rx="5"></rect>
              <circle cx="12" cy="12" r="4"></circle>
              <circle cx="17.5" cy="6.5" r="1" class="social-dot"></circle>
            </svg>
          </a>
          <a
            class="social-link"
            href="https://www.facebook.com/profile.php?id=61591598862870"
            target="_blank"
            rel="noopener noreferrer"
            aria-label="Farmington United Winter Guard Facebook"
          >
            <svg viewBox="0 0 24 24" aria-hidden="true">
              <path d="M14.3 8.2V6.7c0-.7.5-.9.9-.9h2.3V2.1L14.4 2c-3.5 0-4.3 2.6-4.3 4.3v1.9H7.8v3.7h2.3V22h4.2V11.9h3.1l.4-3.7h-3.5z"></path>
            </svg>
          </a>
        </div>
      </nav>
    </footer>
  </main>
</template>
