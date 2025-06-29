<script setup>
import {ref, onBeforeMount, onMounted, nextTick, computed} from 'vue'
import gsap from 'gsap'
import ScrollTrigger from 'gsap/ScrollTrigger'
gsap.registerPlugin(ScrollTrigger)

let cookies = ref(false)
const portfolioItems = {
    "amir": {
        "media":
            {
                "images": [
                    {
                        "type": "image",
                        "src": "src/assets/work/AmirBuilding/poster1.jpg"
                    },
                    {
                        "type": "image",
                        "src": "src/assets/work/AmirBuilding/poster2.jpg"
                    }
                ],
                "videos": [
                    {
                        "type": "video",
                        "src": "src/assets/work/AmirBuilding/motion.mp4"
                    }
                ],
            },
        "title":
            "Visual identity for ״Amir״ Building",
        "subtitle":
            "graphic design 02 | Rotem bix | 2nd year | 2025",
        "description":
            "The brief was to develop a new visual identity for an iconic building in Jerusalem, comprising a bespoke logo for the building, two event posters, and a moving invitation in an instagram post format."
    },
    "neighbours": {
        "media":
            [
                {
                    "type": "image",
                    "src": "src/assets/work/neighbours/1.jpg"
                },
                {
                    "type": "image",
                    "src": "src/assets/work/neighbours/2.jpg"
                },
                {
                    "type": "image",
                    "src": "src/assets/work/neighbours/3.jpg"
                }
            ],
        "title":
            "Portraits - Neighbors in Tel-Aviv",
        "subtitle":
            "Photography Fundamentals | Gaston Zvi Izckowicz | 1st year | 2024",
        "description":
            "The brief was was to create a portrait series centered on a unifying identity. I chose to photograph the residents of a classic Tel Aviv apartment building, capturing their distinct personalities while revealing the subtle alienation that exists between them."
    },
    "expressions": {
        "media":
            [
                {
                    "type": "pdf",
                    "src": "src/assets/work/expressions/kill.pdf",
                    "description": "Chōgi giri (Japanese)<br/>The practice of testing a new sword on an unsuspecting passerby"
                },
                {
                    "type": "pdf",
                    "src": "src/assets/work/expressions/pour.pdf",
                    "description": "Einfollung (German)<br/>A level of empathy so deep that one person's sensations, emotions, and thoughts are immediately and intuitively understood by another"
                },
                {
                    "type": "pdf",
                    "src": "src/assets/work/expressions/carry.pdf",
                    "description": "Tingo (Rapa Nui)<br/>The act of borrowing things from a friend's house one by one until there's nothing left"
                }
            ],
        "title":
            "A series of illustrations for expressions from different languages",
        "subtitle":
            "Illustrative language B | Shimrit Elkanati | 2nd year | 2025",
        "description":
            ""
    }
    ,
    "day-night": {
        "media":
            [
                {
                    "type": "image",
                    "src": "src/assets/work/drawings/day.jpg"
                },
                {
                    "type": "image",
                    "src": "src/assets/work/drawings/night.jpg"
                }
            ],
        "title":
            "Same place, different times of day",
        "subtitle":
            "Illustration B | Hila Noam | 1st year | 2024",
        "description":
            ""
    },
    "joint": {
        "media":
            [
                {
                    "type": "video",
                    "src": "src/assets/work/joint/booklet.mp4"
                },
                {
                    "type": "image",
                    "src": "src/assets/work/joint/poster.jpg"
                }
            ],
        "title":
            "Graphic system - Booklet, Poster and Mini-site",
        "subtitle":
            "Graphic typographic design 03 | Michal Sahar | 2nd year | 2025",
        "description":
            "We were tasked with selecting a Wikipedia article and creating a booklet that weaves in related web entries. Next, we had to invent a launch event for the booklet and design both a poster and a mini-site for it. I chose the article \"Soccer,\" and the event is a research conference celebrating the 50th anniversary of lifting the ban on women's football."
    },
    "signify": {
        "media":
            [
                {
                    "type": "video",
                    "src": "src/assets/work/signify/signify.mp4"
                }
            ],
        "title":
            "Prototype for the 'Signify' app – translate app including sign languages",
        "subtitle":
            "Introduction to Digital Products | Mihchal Har-Gev | 2nd year | 2025",
        "description":
            "The task was to take an existing app, spot an unmet need, and prototype a new one to fill it. I chose to add sign-language translation to and from written languages, aiming for the simplest, most intuitive system that blends them organically without segregation."
    },
    "video": {
        "media":
            [
                {
                    "type": "video",
                    "src": "src/assets/work/video/final-video.mp4"
                }
            ],
        "title":
            "Title sequence - The Gravedigger (in Hebrew, same word as The beekeeper)",
        "subtitle":
            "Video for Designers | Ari Amit | 2nd year | 2025",
        "description":
            ""
    }
}

const amirBuilding = portfolioItems['amir'];
const neighbours = portfolioItems['neighbours'];
const expressions = portfolioItems['expressions'];
const dayNight = portfolioItems['day-night'];
const joint = portfolioItems['joint'];
const signify = portfolioItems['signify'];
const video = portfolioItems['video'];

// Flatten media for scrollable column
const flatMedia = []
const entryKeys = Object.keys(portfolioItems)
entryKeys.forEach(key => {
    const entry = portfolioItems[key]
    const mediaArr = Array.isArray(entry.media) ? entry.media : Object.values(entry.media).flat()
    mediaArr.forEach(m => {
        flatMedia.push({ ...m, entryKey: key })
    })
})

const currentEntryIndex = ref(0)
const currentEntry = computed(() => portfolioItems[entryKeys[currentEntryIndex.value]])
const mediaColumn = ref(null)

onMounted(() => {
    // GSAP ScrollTrigger logic will go here
})
</script>

<template>
    <div class="cookies" v-if="!cookies">
        <div class="cookies__title">
            Noga likes to eat cookies.
        </div>
        <div class="cookies__bottom">
            <div class="cookies__bottom__subtitle">
                can we collect them?
            </div>
            <div class="cookies__bottom__ok" @click="cookies = true">ok</div>
        </div>
    </div>
    <main class="main">
        <div class="header">
            <div class="navbar">
                <div class="navbar__title">
                    <span class="bold">Noga Reshef</span> | Portfolio
                </div>
            </div>
            <div class="description">
                2nd year student at <span class="bold">Bezalel Academy</span>,<br/>Cognitive science graduate from the Hebrew University
            </div>
        </div>
        <div class="portfolio-columns">
            <div class="portfolio-info">
                <div v-show="currentEntryIndex === 0" class="portfolio-info__block">
                    <div class="portfolio-info__title">{{ portfolioItems.amir.title }}</div>
                    <div class="portfolio-info__subtitle">{{ portfolioItems.amir.subtitle }}</div>
                    <div class="portfolio-info__description">{{ portfolioItems.amir.description }}</div>
                </div>
                <div v-show="currentEntryIndex === 1" class="portfolio-info__block">
                    <div class="portfolio-info__title">{{ portfolioItems.neighbours.title }}</div>
                    <div class="portfolio-info__subtitle">{{ portfolioItems.neighbours.subtitle }}</div>
                    <div class="portfolio-info__description">{{ portfolioItems.neighbours.description }}</div>
                </div>
                <div v-show="currentEntryIndex === 2" class="portfolio-info__block">
                    <div class="portfolio-info__title">{{ portfolioItems.expressions.title }}</div>
                    <div class="portfolio-info__subtitle">{{ portfolioItems.expressions.subtitle }}</div>
                    <div class="portfolio-info__description">{{ portfolioItems.expressions.description }}</div>
                </div>
                <div v-show="currentEntryIndex === 3" class="portfolio-info__block">
                    <div class="portfolio-info__title">{{ portfolioItems['day-night'].title }}</div>
                    <div class="portfolio-info__subtitle">{{ portfolioItems['day-night'].subtitle }}</div>
                    <div class="portfolio-info__description">{{ portfolioItems['day-night'].description }}</div>
                </div>
                <div v-show="currentEntryIndex === 4" class="portfolio-info__block">
                    <div class="portfolio-info__title">{{ portfolioItems.joint.title }}</div>
                    <div class="portfolio-info__subtitle">{{ portfolioItems.joint.subtitle }}</div>
                    <div class="portfolio-info__description">{{ portfolioItems.joint.description }}</div>
                </div>
                <div v-show="currentEntryIndex === 5" class="portfolio-info__block">
                    <div class="portfolio-info__title">{{ portfolioItems.signify.title }}</div>
                    <div class="portfolio-info__subtitle">{{ portfolioItems.signify.subtitle }}</div>
                    <div class="portfolio-info__description">{{ portfolioItems.signify.description }}</div>
                </div>
                <div v-show="currentEntryIndex === 6" class="portfolio-info__block">
                    <div class="portfolio-info__title">{{ portfolioItems.video.title }}</div>
                    <div class="portfolio-info__subtitle">{{ portfolioItems.video.subtitle }}</div>
                    <div class="portfolio-info__description">{{ portfolioItems.video.description }}</div>
                </div>
            </div>
            <div class="portfolio-media">
                <!-- AmirBuilding -->
                <div class="portfolio-media__item" ref="media0">
                    <img :src="amirBuilding.media.images[0].src" alt="AmirBuilding-1" />
                </div>
                <div class="portfolio-media__item" ref="media1">
                    <img :src="amirBuilding.media.images[1].src" alt="AmirBuilding-2" />
                </div>
                <div class="portfolio-media__item" ref="media2">
                    <video :src="amirBuilding.media.videos[0].src" controls />
                </div>
                <!-- Neighbours -->
                <div class="portfolio-media__item" ref="media3">
                    <img :src="neighbours.media[0].src" alt="Neighbours-1" />
                </div>
                <div class="portfolio-media__item" ref="media4">
                    <img :src="neighbours.media[1].src" alt="Neighbours-2" />
                </div>
                <div class="portfolio-media__item" ref="media5">
                    <img :src="neighbours.media[2].src" alt="Neighbours-3" />
                </div>
                <!-- Expressions (PDFs, skip for now) -->
                <!-- Day-Night -->
                <div class="portfolio-media__item" ref="media6">
                    <img :src="dayNight.media[0].src" alt="Day-Night-1" />
                </div>
                <div class="portfolio-media__item" ref="media7">
                    <img :src="dayNight.media[1].src" alt="Day-Night-2" />
                </div>
                <!-- Joint -->
                <div class="portfolio-media__item" ref="media8">
                    <video :src="joint.media[0].src" controls />
                </div>
                <div class="portfolio-media__item" ref="media9">
                    <img :src="joint.media[1].src" alt="Joint-Poster" />
                </div>
                <!-- Signify -->
                <div class="portfolio-media__item" ref="media10">
                    <video :src="signify.media[0].src" controls />
                </div>
                <!-- Video -->
                <div class="portfolio-media__item" ref="media11">
                    <video :src="video.media[0].src" controls />
                </div>
            </div>
        </div>
    </main>
</template>

<style scoped lang="scss">
@use "assets/styles/variables" as *;

.navbar {
    position: sticky;
    top: 0;
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
    align-items: flex-start;
    gap: 10px;
    width: 100%;
    color: #242424;

}

.header {
    width: 100%;
    display: flex;
    flex-direction: column;
    gap: 108px;

    .bold {
        font-weight: bold;
    }

    .description {
        font-size: 40px;
    }

}

.cookies {
    position: fixed;
    z-index: 1000;
    bottom: 16px;
    left: 16px;
    right: 16px;
    background-color: #de0000;
    padding: 16px;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    gap: 5px;
    mix-blend-mode: multiply;

    &__title {
        font-weight: bold;
        font-size: 80px;
        color: #fff;
        width: 600px;
        font-family: $font-simpler;
    }

    &__bottom {
        display: flex;
        flex-direction: row;
        align-items: flex-end;
        justify-content: space-between;
        width: 100%;

        &__subtitle {
            font-size: 30px;
            line-height: 80px;
            color: #fff;
            font-family: $font-simpler;
        }

        &__ok {
            cursor: pointer;
            color: #fff;
            font-size: 80px;
            line-height: 80px;
            transition: all 0.2s ease-in-out;
            font-family: $font-simpler;

            &:hover {
                text-decoration: underline;
                transition: all 0.2s ease-in-out;

            }

        }
    }
}

.main {
    background-color: #fff;
    display: flex;
    flex: 1 1 auto;
    flex-direction: column;
    flex-wrap: nowrap;
    gap: 24px;
    height: 100vh;
    padding: 24px 0 24px;
    position: relative;
    width: 94%;
}

.portfolio-columns {
    display: flex;
    flex-direction: row;
    width: 100%;
    align-items: flex-start;
    /* height: 100%; */
}

.portfolio-info {
    width: 40%;
    position: sticky;
    top: 0;
    align-self: flex-start;
    height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding-right: 32px;
    z-index: 2;
}

.portfolio-media {
    width: 60%;
    display: flex;
    flex-direction: column;
    gap: 32px;
    /* No overflow, let page scroll */
}

.portfolio-media__item {
    width: 100%;
    min-height: 400px;
    display: flex;
    align-items: center;
    justify-content: center;
}

.portfolio-media__item img,
.portfolio-media__item video {
    max-width: 100%;
    max-height: 80vh;
    object-fit: contain;
}

</style>
