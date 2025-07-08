<script setup>
import { gsap } from 'gsap';
import {
    SplitText,
    ScrollToPlugin,
    ScrollSmoother,
    ScrollTrigger
} from 'gsap/all';
import { onMounted } from 'vue';

const emits = defineEmits(["getJumpId"]);

onMounted(() => {
    gsap.registerPlugin(SplitText, ScrollSmoother, ScrollTrigger, ScrollToPlugin);

    // gsap.set("#hello", { opacity: 0, y: 100 })
    // const split = SplitText.create("#hello", { type: "chars" });

    // gsap.from(split.chars, {
    //     scrollTrigger: {
    //         trigger: 'about-container',
    //         start: 'top top',
    //         end: '+=1000',
    //         scrub: true
    //     },
    //     y: 20,
    //     autoAlpha: 0,
    //     stagger: 0.05
    // });
})

function handleJump(id) {
    emits("getJumpId", id)
}
</script>

<template>
    <div class="about-container">
        <div class="container-inner">
            <div style="margin-bottom: 48px;">
                <div class="subtitle">My Info</div>
                <div class="title">About me</div>
            </div>
            <n-grid :x-gap="48" style="align-items: center;">
                <n-gi :span="12">
                    <div class="photo-container">
                        <img src="/wendy/Wendy-Portrait-raw.png" />
                    </div>
                </n-gi>
                <n-gi :span=12>
                    <n-flex :size="32" vertical>
                        <div id="hello" style="font-size: 1.5rem; font-weight: 600;">Hi, I am Wenqi Chen, based in
                            Beijing, China.
                        </div>
                        <div id="description" style="font-size: 1.1rem">
                            I live in Beijing with my parents, my younger sister Mandy, and four
                            pets—three cats (Nana, TinTin, Mimi) and a dog named Pearl (珍珠). I’ve been doing Model
                            United Nations since
                            Year 6 and am now the Secretary-General of my school’s MUN club. In my free time, I play
                            piano and tennis.
                        </div>
                        <n-grid :x-gap="12">
                            <n-gi id="skill1" :span="8" class="skill-block">
                                <n-flex vertical>
                                    <div class="icon">
                                        <n-icon :size="32" color="#428478FF">
                                            <svg xmlns="http://www.w3.org/2000/svg"
                                                xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 0 24 24">
                                                <path
                                                    d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zm-5 11.5h.25V19h-4.5v-4.5H10c.55 0 1-.45 1-1V5h2v8.5c0 .55.45 1 1 1zM5 5h2v8.5c0 .55.45 1 1 1h.25V19H5V5zm14 14h-3.25v-4.5H16c.55 0 1-.45 1-1V5h2v14z"
                                                    fill="currentColor"></path>
                                            </svg>
                                        </n-icon>
                                    </div>
                                    <div class="label">Piano</div>
                                    <div class="time">Since 2014</div>
                                </n-flex>
                            </n-gi>
                            <n-gi id="skill2" :span="8" class="skill-block">
                                <n-flex vertical>
                                    <div class="icon">
                                        <n-icon :size="32" color="#428478FF">
                                            <svg xmlns="http://www.w3.org/2000/svg"
                                                xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 0 24 24">
                                                <g fill="none" stroke="currentColor" stroke-width="2"
                                                    stroke-linecap="round" stroke-linejoin="round">
                                                    <circle cx="12" cy="12" r="9"></circle>
                                                    <path d="M6 5.3a9 9 0 0 1 0 13.4"></path>
                                                    <path d="M18 5.3a9 9 0 0 0 0 13.4"></path>
                                                </g>
                                            </svg>
                                        </n-icon>
                                    </div>
                                    <div class="label">Tennis</div>
                                    <div class="time">Since 2016</div>
                                </n-flex>
                            </n-gi>
                            <n-gi id="skill3" :span="8" class="skill-block">
                                <n-flex vertical>
                                    <div class="icon">
                                        <n-icon :size="28" color="#428478FF">
                                            <svg xmlns="http://www.w3.org/2000/svg"
                                                xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 0 512 512">
                                                <path
                                                    d="M432 96c26.5 0 48-21.5 48-48S458.5 0 432 0s-48 21.5-48 48s21.5 48 48 48zm73 356.1c-9.4-9.4-24.6-9.4-33.9 0c-12.1 12.1-30.5 15.4-45.1 8.7l-135.8-70.2l49.2-73.8c12.7-19 10.2-44.5-6-60.6L293 215.7l-107-53.1c-2.9 19.9 3.4 40 17.7 54.4l75.1 75.2l-45.9 68.8L35 258.7c-11.7-6-26.2-1.5-32.3 10.3c-6.1 11.8-1.5 26.3 10.3 32.3l391.9 202.5c11.9 5.5 24.5 8.1 37.1 8.1c23.2 0 46-9 63-26c9.3-9.3 9.3-24.5 0-33.8zM120 91.6l-11.5 22.5c14.4 7.3 31.2 4.9 42.8-4.8l47.2 23.4c-.1.1-.1.2-.2.3l114.5 56.8l32.4-13l6.4 19.1c4 12.1 12.6 22 24 27.7l58.1 29c15.9 7.9 35 1.5 42.9-14.3c7.9-15.8 1.5-35-14.3-42.9l-52.1-26.1l-17.1-51.2c-8.1-24.2-40.9-56.6-84.5-39.2l-81.2 32.5l-62.5-31c.3-14.5-7.2-28.6-20.9-35.6l-11.1 21.7h-.2l-34.4-7c-1.8-.4-3.7.2-5 1.7c-1.9 2.2-1.7 5.5.5 7.4l26.2 23z"
                                                    fill="currentColor"></path>
                                            </svg>
                                        </n-icon>
                                    </div>
                                    <div class="label">Skiing</div>
                                    <div class="time">Since 2018</div>
                                </n-flex>
                            </n-gi>
                        </n-grid>
                        <div id="projectButton">
                            <n-button type="primary" @click="handleJump('#project')"
                                style="padding: 1.5rem; color: #fff; font-weight: 600;">
                                Go to my Projects
                            </n-button>
                        </div>
                    </n-flex>
                </n-gi>
            </n-grid>
        </div>
    </div>
</template>

<style lang="less" scoped>
.about-container {
    height: 100vh;
    font-family: "Poppins", sans-serif;
    background-color: hsl(242, 19%, 5%);
    display: flex;
    align-items: center;
    justify-content: center;

    .container-inner {
        width: 85vw;
        margin: 0 auto;
        position: relative;
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

    .photo-container {
        img {
            width: 100%;
            border-radius: 8px;
        }
    }

    .skill-block {
        background: rgb(19, 19, 22);
        border-radius: 8px;
        padding: 1rem;

        .icon {
            text-align: center;
        }

        .label {
            text-align: center;
            font-size: 1.4rem;
            font-weight: 700;
        }

        .time {
            text-align: center;
            font-size: 1.1rem;
        }
    }
}
</style>