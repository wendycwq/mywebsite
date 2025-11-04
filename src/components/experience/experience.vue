<script setup>
import { ref } from 'vue'
import { useBreakpoint } from '../../assets/general';

const { isMobile } = useBreakpoint()

const current = ref(1);

const steps = [
    {
        title: "Week 1",
        description: "Arrival, Georgetown neighbourhood, Embassy of Uzbekistan, presidential debate, Potomac River",
        imgList: [
            "/wendy/experience/week1/100_0214.jpg",
            "/wendy/experience/week1/100_0237.jpg",
            "/wendy/experience/week1/100_0254.jpg",
            "/wendy/experience/week1/IMG_0635.jpg",
            "/wendy/experience/week1/IMG_0644.jpg",
            "/wendy/experience/week1/IMG_0653.jpg",
            "/wendy/experience/week1/IMG_0686.jpg",
            "/wendy/experience/week1/IMG_5459.jpg",
        ]
    },
    {
        title: "Week 2",
        description: "Georgetown cupcake, volleyball, Embassy of Saudi Arabia, 4th of July parade and fireworks",
        imgList: [
            "/wendy/experience/week2/IMG_2688.jpg",
            "/wendy/experience/week2/IMG_0889.jpg",
            "/wendy/experience/week2/IMG_0754.jpg",
            "/wendy/experience/week2/100_0291.jpg",
            "/wendy/experience/week2/100_0280.jpg",
            "/wendy/experience/week2/IMG_0785.jpg",
            "/wendy/experience/week2/IMG_0892.jpg",
            "/wendy/experience/week2/IMG_2466.jpg",
            "/wendy/experience/week2/IMG_2613.jpg",
            "/wendy/experience/week2/week2-1.jpg",
            "/wendy/experience/week2/week2-2.jpg",
            "/wendy/experience/week2/week2-3.jpg",
        ]
    },
    {
        title: "Week 3",
        description: "Cafe Milano, crisis simulation, Embassy of Germany, final presentation, awards announcement",
        imgList: [
            "/wendy/experience/week3/IMG_1088.jpg",
            "/wendy/experience/week3/IMG_1040.jpg",
            "/wendy/experience/week3/IMG_1046.jpg",
            "/wendy/experience/week3/IMG_1058.jpg",
            "/wendy/experience/week3/IMG_1069.jpg",
            "/wendy/experience/week3/IMG_1084.jpg",
            "/wendy/experience/week3/IMG_1221.jpg",
            "/wendy/experience/week3/week3-1.jpg",
        ]
    },
    {
        title: "Museums",
        description: "American History, Natural History, Spy Museum, National Zoo, National Mall, National Gallery of Art, Air & Space, African American History and Culture",
        imgList: [
            "/wendy/experience/museum/IMG_1143.jpg",
            "/wendy/experience/museum/IMG_1124.jpg",
            "/wendy/experience/museum/IMG_1144.jpg",
            "/wendy/experience/museum/IMG_1177.jpg",
            "/wendy/experience/museum/IMG_1200.jpg",
            "/wendy/experience/museum/IMG_1205.jpg",
            "/wendy/experience/museum/IMG_1213.jpg",
            "/wendy/experience/museum/IMG_1220.jpg",
            "/wendy/experience/museum/IMG_1226.jpg",
            "/wendy/experience/museum/IMG_1290.jpg",
            "/wendy/experience/museum/IMG_1357.jpg",
            "/wendy/experience/museum/IMG_1369.jpg",
            "/wendy/experience/museum/IMG_1376.jpg",
            "/wendy/experience/museum/IMG_1403.jpg",
            "/wendy/experience/museum/IMG_1410.jpg",
            "/wendy/experience/museum/museum-1.jpg",
        ]
    }
]

function next() {
    if (current.value >= 4)
        current.value = 4;
    else current.value++;
}

function prev() {
    if (current.value === 1)
        current.value = 1;
    else current.value--;
}
</script>

<template>
    <div class="experience-container">
        <div class="container-inner">
            <div class="subtitle">My Experience</div>
            <div class="title">Summer School</div>
            <n-flex class="timeline-container" vertical :size="48">
                <div v-if="isMobile">
                    <n-flex vertical :size="24">
                        <n-flex :align="'center'" :wrap="false">
                            <n-avatar round style="background: var(--primary-color)">{{ current }}</n-avatar>
                            <n-flex>
                                <div style="font-size: 1.2rem">{{ steps[current - 1].title }}</div>
                            </n-flex>
                        </n-flex>
                        <n-ellipsis :line-clamp="4" style="margin: 0 0 4px 0">
                            {{ steps[current - 1].description }}
                            <template #tooltip>
                                <div style="max-width: 400px;">{{ steps[current - 1].description }}</div>
                            </template>
                        </n-ellipsis>
                        <n-carousel>
                            <n-image v-for="url in steps[current - 1].imgList" class="carousel-img"
                                :src="url"></n-image>
                        </n-carousel>
                    </n-flex>
                </div>
                <n-steps v-else v-model:current="current">
                    <template #finish-icon>
                        <n-icon>
                            <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"
                                viewBox="0 0 32 32">
                                <path d="M16 24a8 8 0 0 0 6.85-3.89l-1.71-1a6 6 0 0 1-10.28 0l-1.71 1A8 8 0 0 0 16 24z"
                                    fill="currentColor"></path>
                                <path
                                    d="M16 2a14 14 0 1 0 14 14A14 14 0 0 0 16 2zm0 2a12 12 0 0 1 10.89 7H25a1 1 0 0 0-1-1H8a1 1 0 0 0-1 1H5.11A12 12 0 0 1 16 4zm0 24A12 12 0 0 1 4 16a11.86 11.86 0 0 1 .4-3H7v2a2 2 0 0 0 2 2h3.31a2 2 0 0 0 2-1.67l.52-3.33h2.34l.55 3.33a2 2 0 0 0 2 1.67H23a2 2 0 0 0 2-2v-2h2.6a11.86 11.86 0 0 1 .4 3a12 12 0 0 1-12 12z"
                                    fill="currentColor"></path>
                            </svg>
                        </n-icon>
                    </template>
                    <n-step v-for="(step, index) in steps" :title="step.title">
                        <div class="n-step-description">
                            <n-ellipsis :line-clamp="2" style="margin: 0 0 4px 0">
                                {{ step.description }}
                                <template #tooltip>
                                    <div style="max-width: 300px;">
                                        {{ step.description }}
                                    </div>
                                </template>
                            </n-ellipsis>
                            <div :style="{ width: '100%', opacity: current == index + 1 ? '1' : '0.5' }">
                                <n-carousel :draggable="current == index + 1">
                                    <n-image v-for="url in step.imgList" class="carousel-img"
                                        :preview-disabled="current != index + 1" :src="url" />
                                </n-carousel>
                            </div>
                        </div>
                    </n-step>
                </n-steps>
                <n-flex :justify="'center'">
                    <n-button circle size="large" @click="prev">
                        <template #icon>
                            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"
                                stroke-linecap="round" stroke-linejoin="round">
                                <polyline points="15 18 9 12 15 6"></polyline>
                            </svg>
                        </template>
                    </n-button>
                    <n-button circle size="large" @click="next">
                        <template #icon>
                            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"
                                stroke-linecap="round" stroke-linejoin="round">
                                <polyline points="9 18 15 12 9 6"></polyline>
                            </svg>
                        </template>
                    </n-button>
                </n-flex>
            </n-flex>
        </div>
    </div>
</template>

<style lang='less' scoped>
.experience-container {
    height: 100vh;
    font-family: "Poppins", sans-serif;
    background-color: hsl(242, 19%, 5%);
    display: flex;
    align-items: center;
    justify-content: center;

    .container-inner {
        position: relative;
        width: 85vw;
        margin: 0 auto;
    }

    .subtitle {
        color: var(--primary-color);
        font-weight: 600;
        text-align: center;
        font-size: 1.5rem;
    }

    .title {
        text-align: center;
        font-weight: 700;
        font-size: 3rem;
    }

    .timeline-container {
        margin: 3rem 0
    }

    .carousel-img {
        :deep(img) {
            width: 100%;
            aspect-ratio: 4/3;
            object-fit: cover !important
        }
    }
}

@media (max-width: 768px) {
    .experience-container {
        height: 100%;
        min-height: 100vh;
        font-family: "Poppins", sans-serif;
        background-color: hsl(242, 19%, 5%);
        padding: 1rem;

        .container-inner {
            position: relative;
            width: 100%;
            margin: 0 auto;
        }

        .subtitle {
            color: var(--primary-color);
            font-weight: 600;
            text-align: center;
            font-size: 1.2rem;
        }

        .title {
            text-align: center;
            font-weight: 700;
            font-size: 2.5rem;
        }

        .timeline-container {
            margin: 3rem 0
        }

        .carousel-img {
            :deep(img) {
                width: 100%;
                aspect-ratio: 4/3;
                object-fit: cover !important
            }
        }
    }
}
</style>