<script setup>
import { ref, onMounted, watch, provide } from 'vue';
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

const showDrawer = ref(false);

// 控制固定 header 的显示和主题反转
const showFixedHeader = ref(false);
const fixedHeaderTheme = ref(null); // null 表示 light theme

// 追踪是否有任何 drawer 打开（包括子组件的）
const anyDrawerOpen = ref(false);

// 提供给子组件用于通知 drawer 状态
provide('setDrawerState', (isOpen) => {
    anyDrawerOpen.value = isOpen;
});

const themeOverrides = {
    common: {
        "primaryColor": "#428478FF", // 这里可以自定义主题色
        "primaryColorHover": "#5CB4A4FF",
        "primaryColorPressed": "#376F64FF",
        "primaryColorSuppl": "#287E6EFF",
    },
};

const menuOptions = [
    {
        label: "ABOUT",
        routerName: "#about",
    },
    {
        label: "PROJECT",
        routerName: "#project",
    },
    {
        label: "EXPERIENCE",
        routerName: "#experience",
    },
    {
        label: "RESEARCH",
        routerName: "#research",
    },
    {
        label: "FAMILY",
        routerName: "#family",
    }
]

// 监听 drawer 状态变化
watch([showDrawer, anyDrawerOpen], ([localDrawer, anyDrawer]) => {
    const fixedHeader = document.querySelector('.mobile-header-fixed');
    if (!fixedHeader) return;

    const isAnyDrawerOpen = localDrawer || anyDrawer;

    if (isAnyDrawerOpen) {
        // 任何 drawer 打开时隐藏 fixed header
        gsap.to(fixedHeader, {
            opacity: 0,
            duration: 0.2,
            ease: 'power2.in',
            onComplete: () => {
                gsap.set(fixedHeader, { display: 'none' });
            }
        });
    } else if (showFixedHeader.value) {
        // drawer 关闭且应该显示 fixed header 时，重新显示
        gsap.to(fixedHeader, {
            display: 'block',
            opacity: 1,
            duration: 0.3,
            ease: 'power2.out'
        });
    }
});

onMounted(() => {
    gsap.registerPlugin(ScrollSmoother, ScrollTrigger, ScrollToPlugin);

    smoother.value = ScrollSmoother.create({
        wrapper: "#smooth-wrapper",
        content: "#smooth-content",
        smooth: 2,
        smoothTouch: 0.1,
        effects: true
    });

    // 设置固定 header 的滚动触发效果
    const fixedHeader = document.querySelector('.mobile-header-fixed');

    if (fixedHeader) {
        // 初始状态：隐藏并设置透明度为 0
        gsap.set(fixedHeader, { opacity: 0, display: 'none' });

        // 检查初始滚动位置
        const initialScrollY = window.scrollY || window.pageYOffset;
        if (initialScrollY > 640) {
            showFixedHeader.value = true;
            fixedHeaderTheme.value = darkTheme;
            if (!showDrawer.value && !anyDrawerOpen.value) {
                gsap.set(fixedHeader, { display: 'block', opacity: 1 });
            }
        }

        ScrollTrigger.create({
            trigger: 'body',
            start: 'top top-=640',
            end: 'bottom bottom',
            onEnter: () => {
                showFixedHeader.value = true;
                fixedHeaderTheme.value = darkTheme;

                // 只在没有 drawer 打开时才显示
                if (!showDrawer.value && !anyDrawerOpen.value) {
                    gsap.to(fixedHeader, {
                        display: 'block',
                        opacity: 1,
                        duration: 0.8,
                        ease: 'power2.out'
                    });
                }
            },
            onLeaveBack: () => {
                gsap.to(fixedHeader, {
                    opacity: 0,
                    duration: 0.4,
                    ease: 'power2.in',
                    onComplete: () => {
                        showFixedHeader.value = false;
                        fixedHeaderTheme.value = null;
                        gsap.set(fixedHeader, { display: 'none' });
                    }
                });
            }
        });
    }
})

function handleJump(id) {
    smoother.value.scrollTo(id, true, "top");
    showDrawer.value = false;
}
</script>

<template>
    <!-- 固定定位的反转主题 header - 放在最外层确保在最上面 -->
    <n-config-provider :theme="fixedHeaderTheme">
        <div class="mobile-header mobile-header-fixed mobile-only">
            <n-flex :justify="'space-between'" :align="'center'">
                <n-flex class="mobile-logo" :align="'center'" @click="handleJump('#home')">
                    <div class="mobile-logo-content">W</div>
                </n-flex>
                <n-button @click="showDrawer = true" text>
                    <template #icon>
                        <n-icon size="28">
                            <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"
                                viewBox="0 0 512 512">
                                <path fill="none" stroke="currentColor" stroke-linecap="round" stroke-miterlimit="10"
                                    stroke-width="48" d="M88 152h336"></path>
                                <path fill="none" stroke="currentColor" stroke-linecap="round" stroke-miterlimit="10"
                                    stroke-width="48" d="M88 256h336"></path>
                                <path fill="none" stroke="currentColor" stroke-linecap="round" stroke-miterlimit="10"
                                    stroke-width="48" d="M88 360h336"></path>
                            </svg>
                        </n-icon>
                    </template>
                </n-button>
            </n-flex>
        </div>
    </n-config-provider>

    <n-config-provider :theme-overrides="themeOverrides" :theme="darkTheme">
        <n-layout has-sider>
            <n-layout-sider bordered class="sider desktop-only" :width="'5rem'">
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
                <!-- 原始 header -->
                <div class="mobile-header mobile-only">
                    <n-flex :justify="'space-between'" :align="'center'">
                        <n-flex class="mobile-logo" :align="'center'" @click="handleJump('#home')">
                            <n-avatar round style="background: var(--primary-color)">W</n-avatar>
                        </n-flex>
                        <n-button @click="showDrawer = true" text>
                            <template #icon>
                                <n-icon size="28">
                                    <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"
                                        viewBox="0 0 512 512">
                                        <path fill="none" stroke="currentColor" stroke-linecap="round"
                                            stroke-miterlimit="10" stroke-width="48" d="M88 152h336"></path>
                                        <path fill="none" stroke="currentColor" stroke-linecap="round"
                                            stroke-miterlimit="10" stroke-width="48" d="M88 256h336"></path>
                                        <path fill="none" stroke="currentColor" stroke-linecap="round"
                                            stroke-miterlimit="10" stroke-width="48" d="M88 360h336"></path>
                                    </svg>
                                </n-icon>
                            </template>
                        </n-button>
                    </n-flex>
                </div>
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
        <n-drawer :auto-focus="false" v-model:show="showDrawer" :width="'100vw'" :height="'100vh'"
            :placement="'bottom'">
            <n-drawer-content>
                <div
                    style="height: 90vh; position: relative; display: flex; align-items: center; justify-content: center;">
                    <n-button style="position: absolute; top: 1rem; right: 0" text @click="showDrawer = false">
                        <template #icon>
                            <n-icon :size="28">
                                <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"
                                    viewBox="0 0 512 512">
                                    <path
                                        d="M289.94 256l95-95A24 24 0 0 0 351 127l-95 95l-95-95a24 24 0 0 0-34 34l95 95l-95 95a24 24 0 1 0 34 34l95-95l95 95a24 24 0 0 0 34-34z"
                                        fill="currentColor"></path>
                                </svg>
                            </n-icon>
                        </template>
                    </n-button>
                    <n-flex vertical :size="48">
                        <n-button style="font-size: 1.2rem" v-for="option in menuOptions" text
                            @click="handleJump(option.routerName)">
                            {{ option.label }}
                        </n-button>
                    </n-flex>
                </div>
            </n-drawer-content>
        </n-drawer>
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
    cursor: pointer;

    .n-avatar {
        font-family: "Cherry Bomb One", system-ui;
    }
}

/* 桌面端显示 sider，隐藏 mobile-header */
.desktop-only {
    display: block;
}

.mobile-only {
    display: none;
}

/* 移动端隐藏 sider，显示 mobile-header */
@media (max-width: 768px) {
    .desktop-only {
        display: none !important;
    }

    .mobile-only {
        display: block;
    }

    .mobile-header {
        padding: 1rem;
    }

    .mobile-header-fixed {
        position: fixed;
        top: 0;
        left: 0;
        right: 0;
        width: calc(100% - 2rem);
        z-index: 9999;
        background-color: var(--n-color);
        box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
        backdrop-filter: blur(10px);
    }

    .mobile-logo {
        font-size: 2rem;
        font-weight: bold;
        font-family: "Cherry Bomb One", sans-serif;
        cursor: pointer;
        transition: all 0.2s;

        &:hover {
            opacity: 0.6;
        }

        .mobile-logo-content {
            background: var(--primary-color);
            border-radius: 50%;
            width: 34px;
            height: 34px;
            color: #fff;
            font-size: 1rem;
            display: flex;
            align-items: center;
            justify-content: center;
        }
    }

    .content {
        width: 100vw;
        margin-left: 0;
    }
}
</style>