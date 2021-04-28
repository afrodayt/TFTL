<template>
    <div class="filter__item">
        <div class="filter__item_name">
            <div>
                {{title}}
            </div>
            <img src="~@/assets/images/Shape.png" alt="">
        </div>
        <div class="sort__value">
            <div>
            </div>
        </div>
    </div>
</template>
<script>
    import 'vue-range-component/dist/vue-range-slider.css'
    // import VueRangeSlider from 'vue-range-component'
    export default {
        name: "CustomFilter",
        components: {

        },
        data: () => ({
            value: [0, 100]
        }),
        created() {
            this.min = 0
            this.max = 250
            this.bgStyle = {
                backgroundColor: '#fff',
                boxShadow: 'inset 0.5px 0.5px 3px 1px rgba(0,0,0,.36)'
            }
            this.tooltipStyle = {
                backgroundColor: '#666',
                borderColor: '#666'
            }
            this.processStyle = {
                backgroundColor: '#999'
            }
        },
        props: {
            title: String,
            values: Array,
        }
    }
</script>

<style scoped lang="scss">

    .filter__item {
        position: relative;

        &:hover {
            .sort__value {
                visibility: visible;
                opacity: 1;
            }
        }
        &_name {
            display: flex;
            align-items: center;

            div + img {
                margin-left: 9px;
            }
        }
        .sort__value {
            position: absolute;
            top: 29px;
            left: 0;
            z-index: 99;
            visibility: hidden;
            width: 101px;
            height: 123px;
            background-color: white;
            border-radius: 6px;
            padding: 16px 0 0 20px;
            box-shadow: 0px 0px 32px rgba(0, 0, 0, 0.04);
            font-size: 14px;
            transition: opacity 0.3s, visibility 0s linear 0.3s;
            opacity: 0;


            div {
                line-height: 25px;
            }

            div + div {
                margin-top: 8px;
            }
        }
    }
</style>