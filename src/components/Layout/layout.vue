<script setup>
import { ref, onMounted } from 'vue';
import {
    NConfigProvider,
    darkTheme
} from 'naive-ui';
import { gsap } from 'gsap';
import {
    ScrollSmoother,
    ScrollTrigger
} from 'gsap/all';
import HomeVue from '../home/home.vue';
import AboutVue from '../about/about.vue';

const themeOverrides = {
    common: {
        "primaryColor": "#428478FF", // 这里可以自定义主题色
        "primaryColorHover": "#5CB4A4FF",
        "primaryColorPressed": "#376F64FF",
        "primaryColorSuppl": "#287E6EFF",
    },
};

onMounted(() => {
    const smoother = ref(null);

    gsap.registerPlugin(ScrollSmoother, ScrollTrigger);

    smoother.value = ScrollSmoother.create({
        smooth: 2,
        smoothTouch: 0.1,
        effects: true,
    })
})
</script>

<template>
    <n-config-provider :theme-overrides="themeOverrides" :theme="darkTheme">
        <n-layout has-sider>
            <n-layout-sider bordered class="sider" :width="'5rem'">
                <div class="logo">
                    <n-avatar round style="background-color: #346a60">W</n-avatar>
                </div>
                <div class="nav">
                    <div style="display: flex;">
                        <n-flex class="nav-list" :size="48" justify="end" :wrap="false">
                            <div>Contact</div>
                            <div>Work</div>
                            <div>Skills</div>
                            <div>About</div>
                            <div>Home</div>
                        </n-flex>
                    </div>
                </div>
            </n-layout-sider>
            <n-layout id="smooth-content" style="position: relative;">
                <n-layout-content class="content">
                    <home-vue></home-vue>
                    <about-vue></about-vue>
                </n-layout-content>
            </n-layout>
        </n-layout>
    </n-config-provider>
</template>

<style lang='less' scoped>
.sider {
    position: fixed;
    height: 100vh;
    background-color: hsl(242, 19%, 5%);

    .nav {
        position: fixed;
        transform: rotate(-90deg) translateX(-100%);
        transform-origin: left top;
        width: calc(100vh - 10rem);
        height: 5rem;

        .nav-list {
            height: 5rem;
            display: flex;
            align-items: center;
            margin: 0 auto;
            font-family: "Poppins", sans-serif;
            font-weight: 700;
            font-style: normal;
        }
    }
}

.content {
    width: calc(100vw - 5rem);
    margin-left: 5rem;
}

.logo {
    width: 5rem;
    height: 5rem;
    display: flex;
    align-items: center;
    justify-content: center;

    .n-avatar {
        font-family: "Cherry Bomb One", system-ui;
    }
}
</style>