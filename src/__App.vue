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

</script>

<template>
    <div class="portfolio">
        <div class="portfolio-item">
            <div class="portfolio-item__info">
                <div class="portfolio-item__info__title">
                    {{ amirBuilding.title }}
                </div>
                <div class="portfolio-item__info__subtitle">
                    {{ amirBuilding.subtitle }}
                </div>
                <div class="portfolio-item__info__description">
                    {{ amirBuilding.description }}
                </div>
            </div>
            <div class="portfolio-item__media">
                <div class="portfolio-item__media__row">
                    <div class="portfolio-item__media__row__item">
                        <img :src="amirBuilding.media.images[0].src" alt="AmirBuilding-1" />
                    </div>
                    <div class="portfolio-item__media__row__item">
                        <img :src="amirBuilding.media.images[1].src" alt="AmirBuilding-2" />
                    </div>
                </div>
                <div class="portfolio-item__media">
                    <div class="portfolio-item__media__item">
                        <video :src="amirBuilding.media.videos[0].src" controls />
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped lang="scss">
@use './assets/styles/variables' as *;

.portfolio {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 100%;
    height: 100%;
}

.portfolio-item {
    display: flex;
    flex-direction: row;
    align-items: flex-end;
    justify-content: space-between;
    width: 100%;
    height: 100%;
    padding: 128px 0;

    &__info {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        justify-content: flex-start;
        width: 50%;
    }

    &__media {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        justify-content: flex-start;
        width: 50%;

        &__row {
            display: flex;
            flex-direction: row;
            align-items: center;
            justify-content: flex-end;
            width: 100%;
        }
        &__row__item {
            flex: 1;
            display: flex;
            align-items: center;
            justify-content: center;
            
            img {
                max-height: 100vh;
                width: auto;
                height: auto;
                max-width: 100%;
                object-fit: contain;
                display: block;
            }
        }
        &__item {
            display: flex;
            align-items: center;
            justify-content: center;
            width: 100%;
            height: 100%;
            
            video {
                max-height: 100vh;
                width: auto;
                height: auto;
                max-width: 100%;
                object-fit: contain;
                display: block;
            }
        }
    }
}
</style>