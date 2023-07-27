<script setup>
const props = defineProps([
    'message',
]);

const getMonth = (monthIndex) => {
    const monthsList = [
        'января',
        'февраля',
        'марта',
        'апреля',
        'мая',
        'июня',
        'июля',
        'августа',
        'сентября',
        'октября',
        'ноября',
        'декабря',
    ];

    return monthsList[monthIndex]
};

const getDate = (messageDate) => {
    const date = new Date(messageDate);
    const fullYear = date.getFullYear();
    const month = getMonth(date.getMonth());
    const day = date.getDate();
    const hours = date.getHours();
    const minutes = date.getMinutes();

    return `${hours}:${minutes}, ${day} ${month} ${fullYear} г.`
};

const highlightByColor = (strPart, tone) => {
    return `<mark style="background-color: rgb(${tone < 0 ? `255, ${(1 + tone) * 255}` : `${(1 - tone) * 255}, 255`}, 0);">${strPart}</mark>`
};

const convertString = (str, pointsList) => {
    let strIndex = 0;
    let newStr = '';

    pointsList.forEach(pointItem => {
        newStr += str.slice(strIndex, pointItem.position);
        strIndex = pointItem.position + pointItem.length;
        const strPart = str.slice(pointItem.position, strIndex);
        newStr += highlightByColor(strPart, pointItem.tone);
    });

    newStr += str.slice(strIndex);

    return newStr
};
</script>

<template>
<div class="messageItem">
    <p class="messageInfo">
        <span>{{ getDate(props.message.date) }}</span>
        <span>/ {{ props.message.authorName }} /</span>
        <span>{{ props.message.authorUrl }}</span>
    </p>
    <p class="messageText" v-html="convertString(props.message.content, props.message.contentPostTones)"></p>
</div>
</template>

<style scoped>
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
