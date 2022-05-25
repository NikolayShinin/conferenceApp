<template>
    <iframe
            class="fullScreen"
            :src="videoUrl"
            frameborder="0"
            seamless="seamless"
            allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
            allowfullscreen
            width="100%"
            height="100%"
    />
</template>

<script>
import data from "../../data.json";

export default {
    name: 'Video',
    computed: {
        videoUrl() {
            const lng = window.navigator.userLanguage || window.navigator.language;
            return data.broadcasts.find((broadcast) => broadcast.lang === lng)?.url ?? data.defaultUrl;
        }
    },
};
</script>
