<template>
    <select
            v-model="value"
            @change="$emit('changeSelect', value)"
    >
        <option
                v-for="option in options"
                :value="option.url"
        >
            {{ option.lang }}
        </option>
    </select>
</template>

<script>
export default {
    name: 'SelectField',
    props:['options','value'],
};
</script>
