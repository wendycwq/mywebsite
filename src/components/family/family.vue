<script setup>
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap';
import {
    Physics2DPlugin,
    // …other plugins
} from 'gsap/all';
import { useBreakpoint } from '../../assets/general';

const { isMobile } = useBreakpoint()

const wrapper = ref(null);

const tags = [
    "/wendy/family/Dami.png",
    "/wendy/family/Nana.png",
    "/wendy/family/Pearl.png",
    "/wendy/family/Tintin.png",
    "/wendy/family/Dami2.png",
    "/wendy/family/Nana2.png",
    "/wendy/family/Tintin2.png",
    "/wendy/family/Tintin3.png",
    "/wendy/family/Dami3.png",
    "/wendy/family/Dami4.png"
]

const frames = [
    "/wendy/family/wall/frame-1.png",
    "/wendy/family/wall/frame-2.png",
    "/wendy/family/wall/frame-3.png",
    "/wendy/family/wall/frame-4.png",
    "/wendy/family/wall/frame-5.png"
]

const photos = [
    "/wendy/family/wall/family1.jpg",
    "/wendy/family/wall/family2.jpg",
    "/wendy/family/wall/family3.jpg",
    "/wendy/family/wall/family4.jpg",
    "/wendy/family/wall/family5.jpg",
    "/wendy/family/wall/family6.jpg",
    "/wendy/family/wall/family7.jpg",
    "/wendy/family/wall/family8.jpg",
    "/wendy/family/wall/family9.jpg",
    "/wendy/family/wall/pet-1.gif",
    "/wendy/family/wall/pet-2.gif",
    "/wendy/family/wall/pet-3.jpg",
    "/wendy/family/wall/pet-4.jpg",
    "/wendy/family/wall/pet-5.jpg",
    "/wendy/family/wall/pet-6.jpg",
    "/wendy/family/wall/pet-7.jpg",
    "/wendy/family/wall/pet-8.jpg",
    "/wendy/family/wall/pet-9.jpg"
]

onMounted(() => {
    gsap.registerPlugin(Physics2DPlugin);

    let tl = gsap.timeline();
    // only target imgs inside our wrapper
    tl.set(wrapper.value.querySelectorAll('.tags'), { opacity: 1 });
    tl.to(wrapper.value.querySelectorAll('.tags'), {
        duration: 3,
        physics2D: { angle: 'random(360,-360)', velocity: 500, gravity: 800 },
        rotation: 'random(-180,180)',
    });

    document.body.addEventListener('click', () => {
        tl.seek(0).invalidate().play(0);
    });
});
</script>

<template>
    <div>
        <div class="explosion-wrapper" ref="wrapper">
            <div class="container-inner">
                <div style="margin-bottom: 48px;">
                    <div class="subtitle">My Daily Life</div>
                    <div class="title">Introduce to my Family</div>
                </div>
                <div class="wall-container">
                    <n-grid :x-gap="24">
                        <n-gi class="photo-container" :span="isMobile ? 24 : 4">
                            <n-flex class="photo" vertical :size="24">
                                <n-image :src="photos[16]" />
                                <n-image :src="photos[7]" />
                                <n-image :src="photos[14]" />
                            </n-flex>
                        </n-gi>
                        <n-gi class="photo-container" :span="isMobile ? 24 : 4">
                            <n-flex class="photo" vertical :size="24">
                                <n-image :src="photos[1]" />
                                <n-image :src="photos[6]" />
                            </n-flex>
                        </n-gi>
                        <n-gi class="photo-container" :span="isMobile ? 24 : 8">
                            <n-flex class="photo" vertical :size="24">
                                <n-image :src="photos[3]" />
                                <n-image :src="photos[4]" />
                            </n-flex>
                        </n-gi>
                        <n-gi class="photo-container" :span="isMobile ? 24 : 4">
                            <n-flex class="photo" vertical :size="24">
                                <n-image :src="photos[5]" />
                                <n-image :src="photos[2]" />
                                <n-image :src="photos[11]" />
                            </n-flex>
                        </n-gi>
                        <n-gi class="photo-container" :span="isMobile ? 24 : 4">
                            <n-flex class="photo" vertical :size="24">
                                <n-image :src="photos[0]" />
                                <n-image :src="photos[10]" />
                            </n-flex>
                        </n-gi>
                    </n-grid>
                </div>
            </div>
            <img v-for="imgUrl in tags" class="tags" :src="imgUrl" alt="" />
        </div>
    </div>
</template>

<style lang='less' scoped>
.explosion-wrapper {
    position: relative;
    width: 100%;
    height: 100vh;
    background: #0e100f;
    overflow: hidden;
    display: flex;
    align-items: center;
    justify-content: center;

    .container-inner {
        width: 85vw;
        margin: 0 auto;
        position: relative;
    }

    .tags {
        position: absolute;
        top: 10%;
        left: 50%;
        max-width: 120px;
        max-height: 120px;
        opacity: 0;
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

    p {
        color: white;
        font-family: Arial, sans-serif;
    }

    .wall-container {
        .n-grid {
            align-items: center;
        }

        .photo {
            width: 100%;

            :deep(img) {
                background: #fff;
                padding: 1.2rem;
                border-style: solid;
                border-width: 1rem;
                border-top-color: lighten(#000, 20%);
                border-right-color: lighten(#000, 0%);
                border-bottom-color: lighten(#000, 20%);
                border-left-color: lighten(#000, 0%);
                box-shadow: 2px 2px 4px rgba(0, 0, 0, .6);
                width: calc(100% - 2.4rem - 2rem);
            }
        }
    }
}

@media (max-width: 768px) {
    .explosion-wrapper {
        position: relative;
        width: 100%;
        height: 100%;
        padding: 4rem 1rem;

        .container-inner {
            width: 100%;
            margin: 0 auto;
            position: relative;
        }

        .tags {
            position: absolute;
            top: 10%;
            left: 50%;
            max-width: 120px;
            max-height: 120px;
            opacity: 0;
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

        p {
            color: white;
            font-family: Arial, sans-serif;
        }

        .wall-container {
            .n-grid {
                align-items: center;
            }

            .photo {
                width: 100%;

                :deep(img) {
                    background: #fff;
                    padding: 1.2rem;
                    border-style: solid;
                    border-width: 1rem;
                    border-top-color: lighten(#000, 20%);
                    border-right-color: lighten(#000, 0%);
                    border-bottom-color: lighten(#000, 20%);
                    border-left-color: lighten(#000, 0%);
                    box-shadow: 2px 2px 4px rgba(0, 0, 0, .6);
                    width: calc(100% - 2.4rem - 2rem);
                }
            }
        }
    }
}
</style>