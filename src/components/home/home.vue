<script setup>
import { ref, onMounted } from 'vue'
import { gsap } from 'gsap';
import {
    ScrollSmoother,
    ScrollTrigger,
    SplitText
} from 'gsap/all';
import { useBreakpoint } from '../../assets/general';
const { isMobile } = useBreakpoint()

const emits = defineEmits(["getJumpId"]);

onMounted(() => {
    document.fonts.ready.then(() => {
        gsap.registerPlugin(SplitText);
        const split = SplitText.create(".hello", { type: "chars" });
        gsap.from(split.chars, {
            y: 20,
            autoAlpha: 0,
            stagger: 0.05
        });

        gsap.set("#intro", { opacity: 1 })

        let mySplitText = SplitText.create("#intro", { type: "chars, words" });

        gsap.from(mySplitText.chars, {
            duration: 2,
            opacity: 0,
            stagger: { from: "random", each: 0.01 }
        });

        if (!isMobile.value) {
            gsap.set(".SocialMedia", { opacity: 0, y: -100 })

            gsap.to(".SocialMedia", {
                duration: 1,
                opacity: 1,
                stagger: { y: 0 },
                delay: 1
            });
        }

        gsap.set(".email", { opacity: 0, y: 100 })

        gsap.to(".email", {
            duration: 1,
            opacity: 1,
            stagger: { y: 0 },
            delay: 1
        });

        gsap.set("#aboutButton", { opacity: 0 })

        gsap.to("#aboutButton", {
            duration: 1,
            opacity: 1,
            delay: 2
        });
    })
})

function handleJump(id) {
    emits("getJumpId", id)
}
</script>

<template>
    <div class="landing-container">
        <div class="containner-inner">
            <n-flex v-if="!isMobile" class="SocialMedia" :align="'center'">
                <div>Follow me</div>
                <div>-</div>
                <n-flex>
                    <n-icon :size="24">
                        <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"
                            viewBox="0 0 512 512">
                            <path
                                d="M444.17 32H70.28C49.85 32 32 46.7 32 66.89v374.72C32 461.91 49.85 480 70.28 480h373.78c20.54 0 35.94-18.21 35.94-38.39V66.89C480.12 46.7 464.6 32 444.17 32zm-273.3 373.43h-64.18V205.88h64.18zM141 175.54h-.46c-20.54 0-33.84-15.29-33.84-34.43c0-19.49 13.65-34.42 34.65-34.42s33.85 14.82 34.31 34.42c-.01 19.14-13.31 34.43-34.66 34.43zm264.43 229.89h-64.18V296.32c0-26.14-9.34-44-32.56-44c-17.74 0-28.24 12-32.91 23.69c-1.75 4.2-2.22 9.92-2.22 15.76v113.66h-64.18V205.88h64.18v27.77c9.34-13.3 23.93-32.44 57.88-32.44c42.13 0 74 27.77 74 87.64z"
                                fill="currentColor"></path>
                        </svg>
                    </n-icon>
                </n-flex>
            </n-flex>
            <n-grid :x-gap="isMobile ? 0 : 24">
                <n-gi class="left" :span="isMobile ? 24 : 10">
                    <n-flex vertical>
                        <div v-if="isMobile" class="photo-container">
                            <n-avatar :size="196" object-fit="cover" style="background: rgb(30, 43, 52);" round
                                src="/wendy/Wendy-Portrait-Square.png"></n-avatar>
                        </div>
                        <div class="hello">
                            <b>Hi, I'm Wendy</b>
                        </div>
                        <p id="intro">
                            I am currently working on
                            applications for history, politics, and international relations.
                        </p>
                        <div id="aboutButton" style="margin-top: 12px">
                            <n-button type="primary" style="color: #fff; padding: 1.5rem" @click="handleJump('#about')">
                                <template #icon>
                                    <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"
                                        viewBox="0 0 512 512">
                                        <path
                                            d="M344 144c-3.92 52.87-44 96-88 96s-84.15-43.12-88-96c-4-55 35-96 88-96s92 42 88 96z"
                                            fill="none" stroke="currentColor" stroke-linecap="round"
                                            stroke-linejoin="round" stroke-width="32"></path>
                                        <path
                                            d="M256 304c-87 0-175.3 48-191.64 138.6C62.39 453.52 68.57 464 80 464h352c11.44 0 17.62-10.48 15.65-21.4C431.3 352 343 304 256 304z"
                                            fill="none" stroke="currentColor" stroke-miterlimit="10" stroke-width="32">
                                        </path>
                                    </svg>
                                </template>
                                <b>More about me!</b>
                            </n-button>
                        </div>
                        <div v-if="isMobile" class="email">
                            <n-flex :align="'center'">
                                <n-icon :size="18" color="#428478FF">
                                    <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"
                                        viewBox="0 0 24 24">
                                        <g fill="none">
                                            <path
                                                d="M18.75 3H5.25l-.184.005A3.25 3.25 0 0 0 2 6.25v9.5l.005.184A3.25 3.25 0 0 0 5.25 19h6.467c.184-.422.445-.807.773-1.135l.365-.365H5.25l-.144-.006A1.75 1.75 0 0 1 3.5 15.75V8.374l8.15 4.29l.097.042a.75.75 0 0 0 .602-.042L20.5 8.373v2.634a3.294 3.294 0 0 1 1.5.253V6.25l-.005-.184A3.25 3.25 0 0 0 18.75 3zM5.25 4.5h13.5l.143.006A1.75 1.75 0 0 1 20.5 6.25v.428L12 11.152L3.5 6.68V6.25l.006-.144A1.75 1.75 0 0 1 5.25 4.5zm13.85 8.17l-5.903 5.902a2.686 2.686 0 0 0-.706 1.247l-.458 1.831a1.087 1.087 0 0 0 1.319 1.318l1.83-.457a2.685 2.685 0 0 0 1.248-.707l5.902-5.902A2.286 2.286 0 0 0 19.1 12.67z"
                                                fill="currentColor"></path>
                                        </g>
                                    </svg>
                                </n-icon>
                                <div class="label">Email</div>
                                <div class="value">3556002824@qq.com</div>
                            </n-flex>
                        </div>
                    </n-flex>
                </n-gi>
                <n-gi v-if="!isMobile" class="right" :span="14">
                    <img src="/wendy/Wendy-Portrait-left.png"></img>
                </n-gi>
            </n-grid>
            <div v-if="!isMobile" class="email">
                <n-flex :align="'center'" :size="16">
                    <n-icon :size="36" color="#428478FF">
                        <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"
                            viewBox="0 0 24 24">
                            <g fill="none">
                                <path
                                    d="M18.75 3H5.25l-.184.005A3.25 3.25 0 0 0 2 6.25v9.5l.005.184A3.25 3.25 0 0 0 5.25 19h6.467c.184-.422.445-.807.773-1.135l.365-.365H5.25l-.144-.006A1.75 1.75 0 0 1 3.5 15.75V8.374l8.15 4.29l.097.042a.75.75 0 0 0 .602-.042L20.5 8.373v2.634a3.294 3.294 0 0 1 1.5.253V6.25l-.005-.184A3.25 3.25 0 0 0 18.75 3zM5.25 4.5h13.5l.143.006A1.75 1.75 0 0 1 20.5 6.25v.428L12 11.152L3.5 6.68V6.25l.006-.144A1.75 1.75 0 0 1 5.25 4.5zm13.85 8.17l-5.903 5.902a2.686 2.686 0 0 0-.706 1.247l-.458 1.831a1.087 1.087 0 0 0 1.319 1.318l1.83-.457a2.685 2.685 0 0 0 1.248-.707l5.902-5.902A2.286 2.286 0 0 0 19.1 12.67z"
                                    fill="currentColor"></path>
                            </g>
                        </svg>
                    </n-icon>
                    <n-flex vertical :size="0">
                        <div class="label">Email</div>
                        <div class="value">3556002824@qq.com</div>
                    </n-flex>
                </n-flex>
            </div>
        </div>
    </div>
</template>

<style lang='less' scoped>
.landing-container {
    height: 100vh;
    font-family: "Poppins", sans-serif;
    background: rgb(19, 19, 22);

    .containner-inner {
        width: 85vw;
        margin: 0 auto;
        position: relative;

        .SocialMedia {
            position: absolute;
            font-size: 1.2rem;
            font-weight: 600;
            top: 2rem;
            left: 2rem;
        }

        .email {
            position: absolute;
            bottom: 2rem;
            left: 2rem;

            .label {
                font-size: 1.1rem;
                font-weight: 600;
            }

            .value {
                font-size: 1rem;
            }
        }

        .left {
            height: 100vh;
            display: flex;
            align-items: center;

            .n-flex {
                padding: 2rem;
            }

            .hello {
                font-size: 3rem;
            }

            .intro {
                font-size: 1.1rem;
            }
        }

        .right {
            position: relative;
            height: 100vh;
            display: flex;
            align-items: center;

            img {
                position: absolute;
                width: 85%;
                bottom: 0;
                right: 0;
            }
        }
    }
}

@media (max-width: 768px) {
    .landing-container {
        height: calc(100vh - 66px);

        .containner-inner {
            width: 100%;
            text-align: center;

            .email {
                position: relative;
                margin-top: 1rem;

                .label {
                    font-size: 0.8rem;
                    font-weight: 600;
                }

                .value {
                    font-size: 0.8rem;
                }
            }

            .left {
                display: flex;
                align-items: center;

                .hello {
                    font-size: 1.5rem;
                }

                .intro {
                    font-size: 0.8rem;
                }
            }
        }
    }
}
</style>