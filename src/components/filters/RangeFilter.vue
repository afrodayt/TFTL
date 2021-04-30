<template>
    <div class="rangeFilter">
        <div class="rangeInput">
            <input type="number" :min=min :max=max name="min" @input="inputHandler">
            <input type="number" :min=min :max=max name="max" @input="inputHandler">

        </div>
    </div>
</template>

<script>
    export default {
        name: "RangeFilter",
        props: {
            min: Number,
            max: Number
        },
        data() {
            return {
                rangeValue: [],
            }
        },
        methods: {
            inputHandler(event) {
                this.$emit('input', event.target.name, event.target.value)
            }

        },
        components: {},
        created() {

        }
    }
</script>

<style scoped lang="scss">
    .rangeFilter {
        width: auto;

        &__slider {
            padding: 0 20px 23px !important;
        }

        .rangeInput {
            display: grid;
            grid-template-columns: 100px 100px;
            height: 42px;
            grid-gap: 9px;
            padding: 20px 20px 8px;

            input {
                padding-left: 12px;
            }
        }
    }

    @media (max-width: 480px) {
        .rangeFilter .rangeInput {
            grid-template-columns: 1fr 1fr;
        }
    }
</style>