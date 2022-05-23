<template>
    <div
            class="wrapper"
            :class="cssClass"
    >
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
    </div>
</template>

<script>

import data from './data.json'

export default {
    name: 'App',
    data() {
        return {
            cssClass: []
        }
    },
    computed: {
        videoUrl() {
            const lng = window.navigator.userLanguage || window.navigator.language;
            let haveUrl = false
            let videoUrl = ''
            data.broadcasts.forEach(broadcast=> {
                if (broadcast.lang === lng) {
                    videoUrl = broadcast.url
                    haveUrl = true
                }
            })
            if (!haveUrl) {
                videoUrl = data.defaultUrl
            }
            return videoUrl
        }
    },
    async mounted() {
        if (await this.getTime() >= data.changeCss.timestamp) {
            this.cssClass = [data.changeCss.cssClass]
        } else {
            const interval = setInterval(async () => {
                if (await this.getTime() >= data.changeCss.timestamp) {
                    this.cssClass = [data.changeCss.cssClass]
                    clearInterval(interval)
                }
            }, 1000)
        }
    },
    methods: {
        async getTime() {
            const response = await fetch('https://worldtimeapi.org/api/timezone/Etc/UTC')
            const result = await response.json()
            return result.unixtime
        }
    }
}
</script>

<style>
* {
    box-sizing: border-box;
}

.wrapper {
    width: 100%;
    height: 100%;
}

.wrapper.my-class:after {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    pointer-events: none;
    background: rgba(0, 0, 0, 0.5);
}

body {
    margin: 0;
    padding: 0;
    width: 100vw;
    height: 100vh;
    overflow: hidden;
}
#app {
    width: 100%;
    height: 100%;
}
.wrapper iframe {
    width: 100%;
    height: 100%;
}

</style>
