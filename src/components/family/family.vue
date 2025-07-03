<script setup>
import { onMounted, ref } from 'vue'
import { gsap } from 'gsap';
import {
    Physics2DPlugin,
    // …other plugins
} from 'gsap/all';

const wrapper = ref(null);

onMounted(() => {
    gsap.registerPlugin(Physics2DPlugin);

    let tl = gsap.timeline();
    // only target imgs inside our wrapper
    tl.set(wrapper.value.querySelectorAll('img'), { opacity: 1 });
    tl.to(wrapper.value.querySelectorAll('img'), {
        duration: 3,
        physics2D: { angle: 'random(360,-360)', velocity: 700, gravity: 1000 },
        rotation: 'random(-180,180)',
    });

    document.body.addEventListener('click', () => {
        tl.seek(0).invalidate().play(0);
    });
});
</script>

<template>
    <div class="explosion-wrapper" ref="wrapper">
        <div class="container-inner">
            <div style="margin-bottom: 48px;">
                <div class="subtitle">My Daily Life</div>
                <div class="title">Introduce to my Family</div>
            </div>
        </div>
        <img src="/wendy/family/Dami.png" alt="" />
        <img src="/wendy/family/Nana.png" alt="" />
        <img src="/wendy/family/Pearl.png" alt="" />
        <img src="/wendy/family/Tintin.png" alt="" />
        <img src="/wendy/family/Dami.png" alt="" />
        <img src="/wendy/family/Nana.png" alt="" />
        <img src="/wendy/family/Pearl.png" alt="" />
        <img src="/wendy/family/Tintin.png" alt="" />
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

    img {
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
}
</style>