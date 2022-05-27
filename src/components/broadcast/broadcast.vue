<template>
    <iframe
            class="fullScreen"
            :src="url"
            frameborder="0"
            seamless="seamless"
            allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
            allowfullscreen
            width="100%"
            height="100%"
    />
</template>

<script>

export default {
    name: 'Video',
    props: ['url'],
};
</script>
