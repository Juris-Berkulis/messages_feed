<script setup>
import { onMounted, ref } from 'vue';
import BaseMessage from '@/components/BaseMessage.vue';
import BaseObserver from '@/components/BaseObserver.vue';
import messagesList from '../assets/data/feed.json';

const messagesListForRender = ref([]);
const page = ref(0);

const loadMoreMessages = () => {
    messagesListForRender.value.push(...messagesList.slice(page.value * 10, (page.value + 1) * 10));
    page.value++;
};
</script>

<template>
<div class="messagesList">
    <BaseMessage v-for="message, index of messagesListForRender" :key="index" :message="message"/>
</div>
<BaseObserver ref="observerLoadMore" :doIt="loadMoreMessages" />
</template>

<style scoped>
.messagesList {
    max-width: 1230px;
    margin: 0 auto;
    padding: 0 15px;
}
</style>
