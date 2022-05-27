<template>
    <div class="container">
        <select-field
                @changeSelect="changeSelect"
        />
        <div
                class="wrapper"
                :class="cssClass"
        >
            <broadcast
                    :url="url"
            />
        </div>
    </div>
</template>

<script>
import selectField from './components/select-field/select-field'
import broadcast from './components/broadcast/broadcast'
import data from './data.json'

export default {
    name: 'App',
    components: {
        broadcast,
        selectField
    },
    methods: {
        changeSelect(url) {
            this.url = url
        },
        async getTime() {
            const response = await fetch('https://worldtimeapi.org/api/timezone/Etc/UTC')
            const result = await response.json()
            return result.unixtime
        }
    },
    data() {
        return {
            url: '',
            cssClass: [],
            interval: null
        }
    },
    async mounted() {
        this.interval = setInterval(async () => {
            if (await this.getTime() >= data.changeCss.timestamp) {
                this.cssClass = [data.changeCss.cssClass]
                clearInterval(this.interval)
            }
        }, 1000)
    },
    unmounted() {
        if (this.interval != null) {
            clearInterval(this.interval)
        }
    }
}
</script>

<style>
* {
    box-sizing: border-box;
}

.wrapper {
    position: relative;
    width: 100%;
    height: 100%;
}

.container {
    width: 100%;
    height: 100%;
    max-width: 1200px;
    margin: 0 auto;
    overflow: hidden;
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
