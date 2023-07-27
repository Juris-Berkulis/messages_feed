<script setup>
import messagesList from '../assets/data/feed.json';

console.log(messagesList)
</script>

<template>
<div class="messagesList">
    <div class="messageItem" v-for="message of messagesList">
        <p class="messageInfo">
            <span>{{ message.date }}</span>
            <span>/ {{ message.authorName }} /</span>
            <span>{{ message.authorUrl }}</span>
        </p>
        <p class="messageText">{{ message.content }}</p>
    </div>
</div>
</template>

<style scoped>
.messagesList {
    max-width: 1230px;
    margin: 0 auto;
    padding: 0 15px;
}

.messageItem {
    margin: 0 30px;
    padding: 30px 0;
    border-bottom: 1px solid #000000;
    font-size: 1rem;
}

.messageItem:last-child {
    border: none;
}

.messageInfo {
    margin-bottom: 30px;
}

.messageInfo span:first-child {
    margin-right: 5px;
}

.messageInfo span:nth-child(2) {
    font-weight: 700;
}

.messageInfo span:last-child {
    margin-left: 5px;
}

.messageText {
    line-height: 1.25;
}
</style>
