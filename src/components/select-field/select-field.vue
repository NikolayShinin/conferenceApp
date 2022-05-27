<template>
    <select
            v-model="selected"
            @change="$emit('changeSelect', selected)"
    >
        <option
                v-for="option in data.broadcasts"
                :value="option.url"
        >
            {{ option.lang }}
        </option>
        <option
                :value="data.defaultUrl"
        >
            other languages
        </option>
    </select>
</template>

<script>
import data from "../../data.json";

export default {
    name: 'SelectField',
    data() {
        return {
            data,
            selected: ''
        }
    },
    mounted() {
        const lng = window.navigator.userLanguage || window.navigator.language;
        this.selected = data.broadcasts.find((broadcast) => broadcast.lang === lng)?.url ?? data.defaultUrl;
        this.$emit('changeSelect', this.selected)
    }
};
</script>
