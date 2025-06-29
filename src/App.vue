<script setup>
import { ref, onMounted, onBeforeUnmount, nextTick, getCurrentInstance } from 'vue'
import gsap from 'gsap'
import ScrollTrigger from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

// Import all assets for portfolioItems
import amirPoster1 from './assets/work/AmirBuilding/poster1.jpg'
import amirPoster2 from './assets/work/AmirBuilding/poster2.jpg'
import amirMotion from './assets/work/AmirBuilding/motion.mp4'
import neighbours1 from './assets/work/neighbours/1.jpg'
import neighbours2 from './assets/work/neighbours/2.jpg'
import neighbours3 from './assets/work/neighbours/3.jpg'
import expressionsTrio from './assets/work/expressions/trio.jpg'
import animal from './assets/work/drawings/animal.png'
import jointBooklet from './assets/work/joint/booklet.mp4'
import jointPoster from './assets/work/joint/poster.jpg'
import jointFreeKick from './assets/work/joint/free-kick.mp4'
import signify from './assets/work/signify/signify.mp4'
import finalVideo from './assets/work/video/final-video.mp4'

const portfolioItems = [
    {
        media: [
            { type: "image", src: amirPoster1 },
            { type: "image", src: amirPoster2 },
            { type: "video", src: amirMotion }
        ],
        mediaLayout: [
            { type: "row", items: [0, 1] },
            { type: "single", items: [2] }
        ],
        title: "Visual identity for ״Amir״ Building",
        subtitle: "graphic design 02 | Rotem bix | 2nd year | 2025",
        description: "The brief was to develop a new visual identity for an iconic building in Jerusalem, comprising a bespoke logo for the building, two event posters, and a moving invitation in an instagram post format."
    },
    {
        media: [
            { type: "image", src: neighbours1 },
            { type: "image", src: neighbours2 },
            { type: "image", src: neighbours3 }
        ],
        mediaLayout: [
            { type: "single", items: [0] },
            { type: "row", items: [1, 2] },
        ],
        title: "Portraits - Neighbors in Tel-Aviv",
        subtitle: "Photography Fundamentals | Gaston Zvi Izckowicz | 1st year | 2024",
        description: "The brief was was to create a portrait series centered on a unifying identity. I chose to photograph the residents of a classic Tel Aviv apartment building, capturing their distinct personalities while revealing the subtle alienation that exists between them."
    },
    {
        media: [
            { type: "image", src: expressionsTrio }
        ],
        title: "A series of illustrations for expressions from different languages",
        subtitle: "Illustrative language B | Shimrit Elkanati | 2nd year | 2025",
        description: ""
    },
    {
        media: [
            { type: "image", src: animal }
        ],
        title: "Animal in a surprising environment (Riso print) ",
        subtitle: "Illustration B | Hila Noam | 2nd year | 2025",
        description: ""
    },
    {
        media: [
            { type: "video", src: jointBooklet },
            { type: "image", src: jointPoster },
            { type: "video", src: jointFreeKick }
        ],
        title: "Graphic system - Booklet, Poster and Mini-site",
        subtitle: "Graphic typographic design 03 | Michal Sahar | 2nd year | 2025",
        description: "We were tasked with selecting a Wikipedia article and creating a booklet that weaves in related web entries. Next, we had to invent a launch event for the booklet and design both a poster and a mini-site for it. I chose the article Soccer, and the event is a research conference celebrating the 50th anniversary of lifting the ban on women's football."
    },
    {
        media: [
            { type: "video", src: signify }
        ],
        title: "Prototype for the 'Signify' app – translate app including sign languages",
        subtitle: "Introduction to Digital Products | Mihchal Har-Gev | 2nd year | 2025",
        description: "The task was to take an existing app, spot an unmet need, and prototype a new one to fill it. I chose to add sign-language translation to and from written languages, aiming for the simplest, most intuitive system that blends them organically without segregation."
    },
    {
        media: [
            { type: "video", src: finalVideo }
        ],
        title: "Title sequence - The Gravedigger (in Hebrew, same word as The beekeeper)",
        subtitle: "Video for Designers | Ari Amit | 2nd year | 2025",
        description: ""
    }
]

const { proxy } = getCurrentInstance()

const activeIndex = ref(0)
const titleRefs = ref([])
const mediaSectionRefs = ref([])

let scrollTriggers = []

const initScrollTriggers = () => {
    // Clear existing triggers
    scrollTriggers.forEach(trigger => trigger.kill())
    scrollTriggers = []

    portfolioItems.forEach((item, index) => {
        const section = mediaSectionRefs.value[index]
        if (!section) return

        const trigger = ScrollTrigger.create({
            trigger: section,
            start: "top center",
            end: "bottom center",
            onEnter: () => updateActiveSection(index),
            onEnterBack: () => updateActiveSection(index),
        })

        scrollTriggers.push(trigger)
    })
}

const updateActiveSection = (index) => {
    if (activeIndex.value === index) return
        activeIndex.value = index
}

const scrollToSection = (index) => {
    const section = mediaSectionRefs.value[index]
    if (section) {
        const y = section.offsetTop - 100
        gsap.to(window, {
            scrollTo: y,
            duration: 1,
            ease: "power2.inOut"
        })
    }
}

onMounted(async () => {
    await nextTick()
    setTimeout(initScrollTriggers, 100)
})

onBeforeUnmount(() => {
    scrollTriggers.forEach(trigger => trigger.kill())
})
</script>

<template>
    <div class="navbar">
        <div class="navabar__title">Noga Reshef | Portfolio</div>
        <!-- <div class="navabar__link">Download as PDF</div> -->
    </div>
    <div class="two-col-container">
        <!-- Media Column -->
        <div class="media-column">
            <div v-for="(item, index) in portfolioItems" 
                 :key="index"
                 class="media-section"
                 :ref="el => mediaSectionRefs[index] = el">
                <template v-if="item.mediaLayout">
                    <div v-for="(layout, layoutIdx) in item.mediaLayout" :key="layoutIdx" :class="layout.type === 'row' ? 'media-row' : 'media-single'">
                        <div v-for="idx in layout.items" :key="idx" class="media-item">
                            <img v-if="item.media[idx].type === 'image'" :src="item.media[idx].src" :alt="item.title">
                            <video v-else-if="item.media[idx].type === 'video'" :src="item.media[idx].src" autoplay muted loop controls></video>
                            <div v-else-if="item.media[idx].type === 'pdf'">
                                <img :src="item.media[idx].src.replace('.pdf', '.jpg')" :alt="item.media[idx].description">
                                <div class="pdf-description" v-html="item.media[idx].description"></div>
                            </div>
                        </div>
                    </div>
                </template>
                <template v-else>
                    <div v-for="(media, mediaIndex) in item.media" 
                         :key="mediaIndex"
                         class="media-item" :class="{ pdf: media.type === 'pdf' }">
                        <img v-if="media.type === 'image'" :src="media.src" :alt="item.title">
                        <video v-else-if="media.type === 'video'" :src="media.src" autoplay muted loop controls></video>
                        <div v-else-if="media.type === 'pdf'">
                            <img :src="media.src.replace('.pdf', '.jpg')" :alt="media.description">
                            <div class="pdf-description" v-html="media.description"></div>
                        </div>
                    </div>
                </template>
            </div>
        </div>
        <!-- Info Box (sticky bottom left) -->
        <div class="info-box">
            <div class="info-title">{{ portfolioItems[activeIndex].title }}</div>
            <div class="info-subtitle">{{ portfolioItems[activeIndex].subtitle }}</div>
            <div class="info-description" v-if="portfolioItems[activeIndex].description">{{ portfolioItems[activeIndex].description }}</div>
        </div>
    </div>
</template>

<style scoped lang="scss">

.navbar {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 60px;
    background: rgba(0,0,0,0.7);
    color: #fff;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 20px;
    z-index: 1000;
    backdrop-filter: blur(8px);
    -webkit-backdrop-filter: blur(8px);
}

.navabar__title {
    font-size: 16px;
    font-weight: 400;
}

.navabar__link {
    font-size: 16px;
    color: #fff;
    cursor: pointer;

    &:hover {
        text-decoration: underline;
    }
}

.two-col-container {
    margin-top: 60px;
    display: flex;
    flex-direction: row-reverse;
    min-height: 100vh;
    background: #000;
    gap: 32px;
}

.info-box {
    width: 500px;
    min-width: 500px;
    max-width: 500px;
    flex: 0 0 500px;
    position: sticky;
    left: 0;
    bottom: 0;
    align-self: flex-end;
    background: none;
    color: #fff;
    padding: 32px 0 32px 40px;
    z-index: 10;
    font-family: inherit;
    border: none;
    box-shadow: none;
    pointer-events: none;
}

.media-column {
    flex: 1 1 0;
    min-width: 0;
    margin: 0;
    align-self: flex-start;
    padding: 32px 32px 0 0;
}

.media-section {
    margin-bottom: 10vh;
    padding: 0;
    display: flex;
    flex-direction: column;
    gap: 20px;
}

.media-item {
    margin-bottom: 0;
    background: none;
    overflow: hidden;
    position: relative;
    max-height: 90vh;
    border: none;
    box-shadow: none;
}

.media-item img,
.media-item video {
    width: 100%;
    height: auto;
    max-width: 100%;
    max-height: 90vh;
    object-fit: contain;
    display: block;
    border: none;
    box-shadow: none;
}

.info-title {
    font-size: 20px;
    font-weight: 600;
    margin-bottom: 0.5rem;
}
.info-subtitle {
    font-size: 16px;
    color: #fff;
    margin-bottom: 1rem;
    font-style: italic;
}
.info-description {
    font-size: 16px;
    color: #fff;
    line-height: 1.5;
}

.media-row {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    gap: 20px;
}
.media-single {
    display: flex;
    flex-direction: column;
}

.media-description {
    margin-top: 8px;
    font-size: 12px;
    color: #bbb;
    text-align: center;
    line-height: 1.4;
    font-style: italic;
    background: none;
    pointer-events: auto;
    text-align: left;
    height: 50px;
}

.drawing {
    display: flex;
    align-items: flex-start;
    justify-content: center;
    flex-direction: column;
    align-content: flex-start
}

.drawing img {
    // width: 400px;
    // height: 600px;
    // object-fit: cover;
    display: block;
    background: #111;
}

.expressions-row {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: flex-start;
  gap: 40px;
  margin-bottom: 40px;
}
.expressions-col {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 400px;
}
.expressions-img {
  width: 400px;
  height: 600px;
  object-fit: contain;
  background: #111;
  display: block;
}
.expressions-caption {
  margin-top: 12px;
  font-size: 14px;
  color: #bbb;
  text-align: center;
  font-style: italic;
  min-height: 50px;
}
</style>