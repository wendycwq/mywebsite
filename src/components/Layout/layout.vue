<script setup>
import { ref, onMounted } from 'vue';
import {
    NConfigProvider,
    darkTheme
} from 'naive-ui';
import { gsap } from 'gsap';
import {
    ScrollToPlugin,
    ScrollSmoother,
    ScrollTrigger
} from 'gsap/all';
import HomeVue from '../home/home.vue';
import AboutVue from '../about/about.vue';
import ResearchVue from '../research/research.vue'
import WorkVue from '../work/work.vue';
import ExperienceVue from '../experience/experience.vue'
import FamilyVue from '../family/family.vue'
import ModelUNVue from '../ModelUN/ModelUN.vue';

const smoother = ref(null);

const themeOverrides = {
    common: {
        "primaryColor": "#428478FF", // 这里可以自定义主题色
        "primaryColorHover": "#5CB4A4FF",
        "primaryColorPressed": "#376F64FF",
        "primaryColorSuppl": "#287E6EFF",
    },
};

onMounted(() => {
    gsap.registerPlugin(ScrollSmoother, ScrollTrigger, ScrollToPlugin);

    smoother.value = ScrollSmoother.create({
        wrapper: "#smooth-wrapper",
        content: "#smooth-content",
        smooth: 2,
        smoothTouch: 0.1,
        effects: true
    });
})

function handleJump(id) {
    smoother.value.scrollTo(id, true, "top");
}
</script>

<template>
    <n-config-provider :theme-overrides="themeOverrides" :theme="darkTheme">
        <n-layout has-sider>
            <n-layout-sider bordered class="sider" :width="'5rem'">
                <div class="logo" @click="handleJump('#home')">
                    <n-avatar round style="background-color: #346a60">W</n-avatar>
                </div>
                <div class="nav">
                    <div style="display: flex;">
                        <n-flex class="nav-list" :size="48" justify="end" :wrap="false">
                            <n-button text @click="handleJump('#family')">Family</n-button>
                            <n-button text @click="handleJump('#research')">Research</n-button>
                            <n-button text @click="handleJump('#experience')">Experience</n-button>
                            <n-button text @click="handleJump('#project')">Project</n-button>
                            <n-button text @click="handleJump('#about')">About</n-button>
                        </n-flex>
                    </div>
                </div>
            </n-layout-sider>
            <n-layout id="smooth-content" style="position: relative;">
                <n-layout-content class="content">
                    <home-vue id="home" @get-jump-id="handleJump"></home-vue>
                    <about-vue id="about" @get-jump-id="handleJump"></about-vue>
                    <ModelUNVue id="project" @get-jump-id="handleJump"></ModelUNVue>
                    <work-vue id="work"></work-vue>
                    <experience-vue id="experience"></experience-vue>
                    <research-vue id="research"></research-vue>
                    <family-vue id="family"></family-vue>
                </n-layout-content>
            </n-layout>
        </n-layout>
    </n-config-provider>
</template>

<style lang='less' scoped>
@media (max-width: 768px) {
    .sider {
        display: none;
    }

    .content {
        width: 100vw !important;
        margin-left: 0 !important;
    }
}

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
    cursor: pointer;

    .n-avatar {
        font-family: "Cherry Bomb One", system-ui;
    }
}
</style>