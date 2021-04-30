<template>
    <div class="customFilter">
        <div
                v-for="option in options"
                :key="option.name"
                @currentFilter="option.name"
        >
            <div @click="clickHandler(option.name)" class="optionName">{{option.name}}</div>
        </div>
    </div>
</template>
<script>
    export default {
        name: "CustomFilter",
        components: {},
        data: () => ({}),
        props: {
            options: Array,
            value: String
        },
        methods: {
            clickHandler(newValue) {
                this.$emit('input', newValue)
            }
        }
    }
</script>

<style scoped lang="scss">
    .optionName {
        cursor: pointer;
        font-weight: 100;
        font-size: 14px;
        line-height: 25px;
        margin-bottom: 8px;
    }

    .customFilter {
        padding: 12.64px 26px 16px 20px;
    }
</style>