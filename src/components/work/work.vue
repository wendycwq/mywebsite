<script setup>
import { ref, onMounted, inject, watch } from 'vue'
import axios from 'axios';
import { decode } from 'js-base64';
import { useBreakpoint } from '../../assets/general';

const { isMobile } = useBreakpoint()

const currentTab = ref(0);

const showDetailModal = ref(false);

// 通知父组件 modal/drawer 状态
const setDrawerState = inject('setDrawerState', null);

if (setDrawerState) {
    watch(showDetailModal, (isOpen) => {
        setDrawerState(isOpen);
    });
}

const allTabsContent = ref([]);

const readyRender = ref(false);

onMounted(async () => {
    const buffer = await readJSON();
    allTabsContent.value = buffer.data;
    readyRender.value = true;
})

function handleChangeTabs(i) {
    currentTab.value = i;
}

function openDetailModal(i) {
    currentTab.value = i + 1;
    showDetailModal.value = true;
}

function readJSON() {
    return axios('/wendy/json/portfolio.json')
}
</script>

<template>
    <div class="portfolio-container">
        <div class="container-inner">
            <div v-if="readyRender">
                <div class="subtitle">My Projects</div>
                <div class="title">Others</div>
                <!-- <div class="tabs">
                    <n-flex :justify="'center'" :size="48">
                        <n-button v-for="(tab, index) in allTabsContent" :secondary="currentTab == index"
                            :type="currentTab == index ? 'primary' : undefined" :text="currentTab != index"
                            :style="{ padding: '0 14px' }" :size="'large'" @click="handleChangeTabs(index)">
                            <b>{{ tab.label }}</b>
                        </n-button>
                    </n-flex>
                </div> -->
                <div class="tabContent">
                    <n-grid :cols="isMobile ? 1 : 3" :x-gap="isMobile ? 0 : 48" :y-gap="16">
                        <n-gi class="tabCard" v-for="(content, index) in allTabsContent.concat().splice(1, 3)">
                            <n-flex vertcial :size="24">
                                <div class="label">{{ content.label }}</div>
                                <img :src="content.bannerUrl" />
                                <div class="achievement">
                                    <n-ellipsis :line-clamp="6">
                                        {{ content.achievement }}
                                        <template #tooltip>
                                            <div style="font-size: 1.2rem; max-width: 20rem;">
                                                {{ content.achievement }}
                                            </div>
                                        </template>
                                    </n-ellipsis>
                                </div>
                                <n-button type="primary" @click="openDetailModal(index)" icon-placement="right"
                                    style="color: #fff; font-weight: 600; width: 100%" :size="'large'">
                                    More Details
                                    <template #icon>
                                        <svg xmlns="http://www.w3.org/2000/svg"
                                            xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 0 24 24">
                                            <path
                                                d="M19 5v14H5V5h14m0-2H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2z"
                                                fill="currentColor"></path>
                                            <path d="M14 17H7v-2h7v2zm3-4H7v-2h10v2zm0-4H7V7h10v2z" fill="currentColor">
                                            </path>
                                        </svg>
                                    </template>
                                </n-button>
                            </n-flex>
                        </n-gi>
                    </n-grid>
                </div>
            </div>
        </div>
        <n-modal :auto-focus="false" v-model:show="showDetailModal" preset="card"
            :style="{ height: '90vh', width: '720px', maxWidth: '90vw' }" size="huge" :bordered="false">
            <template #header>
                <div class="modal-header"><b>{{ allTabsContent[currentTab].label }}</b></div>
                <n-text class="tab-date" :depth="3">{{ allTabsContent[currentTab].date }}</n-text>
            </template>
            <n-scrollbar style="max-height: calc(90vh - 90px - 4rem); padding-right: 1rem">
                <div class="modal-container">
                    <n-flex vertical :size="32">
                        <div v-for="content in allTabsContent[currentTab].content">
                            <n-flex vertical>
                                <n-image :src="content.imgUrl" style="margin-bottom: 0.6rem"></n-image>
                                <n-flex :justify="'space-between'">
                                    <div>{{ content.date }}</div>
                                    <div>{{ content.intro }}</div>
                                </n-flex>
                                <div>{{ content.description }}</div>
                            </n-flex>
                        </div>
                        <n-flex v-if="allTabsContent[currentTab].urls.length" vertical>
                            <div><b>References:</b></div>
                            <div v-for="url in allTabsContent[currentTab].urls">
                                <n-button tag="a" target="_blank" :href="url" text>{{ url }}</n-button>
                            </div>
                        </n-flex>
                        <div style="height: 3rem;"></div>
                    </n-flex>
                </div>
            </n-scrollbar>
        </n-modal>
    </div>
</template>

<style lang='less' scoped>
.portfolio-container {
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

    .tabs {
        margin: 2rem 0 3rem 0;
    }

    .tabContent {
        margin-top: 3rem;

        .tabCard {
            background: rgb(19, 19, 22);
            padding: 2rem;
            border-radius: 8px;

            .label {
                font-size: 1.5rem;
                font-weight: 700;
            }

            img {
                border-radius: 8px;
                width: 100%;
                aspect-ratio: 4/3;
                object-fit: cover;
            }
        }
    }

    .description,
    .achievement {
        font-size: 1.1rem;
    }
}

.modal-container,
.modal-header,
.tab-date {
    font-family: "Poppins", sans-serif;
    font-size: 1rem;

    :deep(img) {
        width: 100%;
        object-fit: contain !important
    }
}

.modal-header {
    font-size: 2.4rem;
}

.tab-date {
    font-size: 1rem;
}

@media (max-width: 768px) {
    .portfolio-container {
        height: 100%;
        padding: 4rem 1rem;

        .container-inner {
            width: 100%;
            margin: 0 auto;
            position: relative;
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
            font-size: 2rem;
        }

        .tabContent {
            margin-top: 3rem
        }

        .description,
        .achievement {
            font-size: 0.8rem;
        }
    }

    .modal-container,
    .modal-header,
    .tab-date {
        font-family: "Poppins", sans-serif;
        font-size: 0.8rem;

        :deep(img) {
            width: 100%;
            object-fit: contain !important
        }
    }

    .modal-header {
        font-size: 1.5rem;
    }

    .tab-date {
        font-size: 1rem;
    }

    .more-detail-button {
        width: 100%;
    }
}
</style>