<script setup>
import { onMounted, ref } from 'vue';
import BaseMessage from '@/components/BaseMessage.vue';
import messagesList from '../assets/data/feed.json';

const messagesListForRender = ref([]);
const page = ref(0);
const observerLoadMore = ref(null);

const loadMoreMessages = () => {
    messagesListForRender.value.push(...messagesList.slice(page.value * 10, (page.value + 1) * 10));
    page.value++;
};

const initPostsAutoLoading = () => {
    window.messagesLoadMoreObserver = null;

    if (!messagesLoadMoreObserver) {
        messagesLoadMoreObserver = new IntersectionObserver(entries => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    loadMoreMessages();
                }
            });
        });
    }

    if (observerLoadMore.value) {
        messagesLoadMoreObserver.observe(observerLoadMore.value);
    }
};

onMounted(() => {
    initPostsAutoLoading();
});
</script>

<template>
<div class="messagesList">
    <BaseMessage v-for="message, index of messagesListForRender" :key="index" :message="message"/>
</div>
<div class="observerLoadMore" ref="observerLoadMore"></div>
</template>

<style scoped>
.messagesList {
    max-width: 1230px;
    margin: 0 auto;
    padding: 0 15px;
}

.observerLoadMore {
    height: 0;
}
</style>
