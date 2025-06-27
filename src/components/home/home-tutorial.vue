<script setup>
// Javascript
import { ref } from 'vue'

const count = ref(0)

const lightStatus = ref(false);

function handleLightSwitch() {
    lightStatus.value = !lightStatus.value
}
</script>

<template>
    <!-- HTML -->
    <div class="content">
        <h1>Hello!</h1>
        <p>This is your Home page.</p>
        <div>
            <n-button type="primary" @click="count++">Click here to give a like 👍 {{ count }}</n-button>
        </div>
        <p>
            <n-image width="120" src="./wendy/hello.gif"></n-image>
        </p>
    </div>
    <div style="width: 50%">
        <div class="livingroom" :style="{ backgroundColor: lightStatus ? 'pink' : 'black' }">
            <n-button type="primary" @click="handleLightSwitch()">light switch</n-button>
            living room
        </div>
        <div class="bedroom1">bedroom one</div>
        <div class="bedroom2">bedroom two</div>
    </div>
</template>

<style scoped>
/* CSS */
.content {
    text-align: center;
    padding: 2vw;
}

.livingroom {
    width: 240px;
    height: 120px;
    background-color: pink;
}

.bedroom1 {
    width: 120px;
    height: 120px;
    background-color: yellow;
}

.bedroom2 {
    width: 120px;
    height: 120px;
    background-color: green;
}
</style>