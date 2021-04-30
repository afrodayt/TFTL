<template>
    <div class="filter__item" @click="show = true" @mouseleave="show = false" @mouseenter="show = true">
        <div class="filter__item_name">
            <div class="filter__item_title" :class="[isAdaptive ? 'sortBy' : '']">
                <div>
                    {{title}}
                </div>
                <img src="~@/assets/images/Shape.png" alt="">
            </div>
            <div class="filter__item_burger" v-if="isAdaptive"><img src="~@/assets/images/burger.png" alt=""></div>
        </div>
        <div class="filter__item_value" v-show="show">
            <div class="filter__item_valueBG">
                <slot/>
            </div>

        </div>
    </div>
</template>

<script>
    export default {
        name: "DropDown",
        data: () => ({
            show: false
        }),
        methods: {

        },
        props: {
            title: String,
            isAdaptive: {type: Boolean, default: false}
        }
    }
</script>

<style scoped lang="scss">

    .filter__item {
        position: relative;

        &_title {
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;

            img {
                margin-left: 9px;
            }

        }

        &_value {
            padding-top: 17.36px;
            position: absolute;
            top: 100%;
            left: -16px;
            z-index: 99;
            width: auto;

            &BG {
                background-color: white;
                border-radius: 6px;
                box-shadow: 0 0 32px rgba(0, 0, 0, 0.04);
            }
        }

        &_burger {
            display: none;
        }
    }

    @media (max-width: 480px) {
        .sortBy {
            display: none;
        }
        .filter__item_value {
            position: fixed;
            left: 15%;
            right: 15%;
            top: 25%;
        }
        .filter__item_burger {
            display: block;
        }
    }
</style>