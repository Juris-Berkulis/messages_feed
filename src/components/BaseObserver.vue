<script setup>
import { onMounted, ref } from 'vue';

const props = defineProps([
    'doIt',
    'isLoading',
    'isShow',
]);

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
<div class="observerLoadMore" ref="observerLoadMore" v-if="isShow">
    <div class="loadingIndicator" v-if="isLoading"></div>
</div>
</template>

<style scoped>
.observerLoadMore {
    width: 100%;
    display: flex;
    justify-content: center;
}

@keyframes rotate {
    0% {
        transform: rotateZ(0deg);
    }

    100% {
        transform: rotateZ(360deg);
    }
}

.loadingIndicator {
    height: 50px;
    width: 50px;
    border-radius: 50%;
    border: 10px solid #0000ff;
    border-bottom: 10px solid transparent;
    animation: rotate 1s linear 0s infinite normal forwards;
}
</style>
