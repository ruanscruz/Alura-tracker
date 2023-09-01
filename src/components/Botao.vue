<template>
    <button class="button">
        <span class="icon">
            <i :class="classIcon"></i>
        </span>
        <span>{{ labelBotao }}</span>
    </button>
</template>
<script lang="ts">
import { defineComponent } from 'vue';
export default defineComponent({
    name: 'BotaoVue',
    props: {
        labelBotao: {
            type: String,
            default: ''
        },
        classIcon: {
            type: String,
            default: ''
        }
    }
})
</script>
<style></style>