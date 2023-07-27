<script setup>
import { onMounted, ref } from 'vue';

const props = defineProps([
    'doIt',
])

const observerLoadMore = ref(null);

const initPostsAutoLoading = () => {
    window.messagesLoadMoreObserver = null;

    if (!messagesLoadMoreObserver) {
        messagesLoadMoreObserver = new IntersectionObserver(entries => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    props.doIt();
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
<div class="observerLoadMore" ref="observerLoadMore"></div>
</template>

<style scoped>
.observerLoadMore {
    height: 0;
}
</style>
