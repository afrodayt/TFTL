<template>
    <section>
        <div class="container">
            <h1 class="title">People</h1>
            <div class="filter_container">
                <div class="filter">
                    <DropDown
                            title="Eye color"
                    >
                        <CustomFilter/>
                    </DropDown>
                </div>

            </div>
            <div class="table">
                <div
                        class="table__item"
                        v-for="hero in starHero"
                        :key="hero.name"
                        :style="{ background:
                        'linear-gradient(180deg, rgba(0, 0, 0, 0.7) 0%, rgba(0, 0, 0, 0.1) 100%), ' +
                        'url(' + require('@/assets/images/' + getName(hero.name) + '.jpg') + ')' +
                        ' center / cover, no-repeat'}"
                >
                    <div class="table__item_bby">{{hero.birth_year}}</div>
                    <div class="table__item_name">{{hero.name}}</div>
                    <div class="table__item_properties">
                        <div>Eye color : {{hero.eye_color}}</div>
                        <div>Height : {{hero.height}}</div>
                        <div>Mass : {{hero.mass}}</div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
    import axios from "axios"
    import DropDown from "./DropDown";
    import CustomFilter from "./CustomFilter";

    export default {
        name: "Page",
        components: {CustomFilter, DropDown},
        data: () => ({
            starHero: [],

            filters: [
                {
                    title: "Eye color",
                    values: ['blue',
                        'blue-gray',
                        'brown',
                        'red',
                        'yellow'],
                },
                {
                    title: "Heigt",
                    values: [],
                },
                {
                    title: "Age",
                    values: [],
                },
                {
                    title: "Sort by",
                    values: [
                        'age',
                        'mass',
                        'heigt'
                    ],
                    slider: false
                },


            ],
        }),
        methods: {
            getName(name) {
                return name.replace(/\s+/g, '')
            },
        },
        computed: {},
        mounted() {
            axios
                .get('http://swapi.dev/api/people/')
                .then(response => {
                    this.starHero = response.data.results;
                    console.log(this.starHero);
                })
        }
    }
</script>

<style scoped lang="scss">
    section {
        flex: 1 0 auto;

        .title {
            margin-top: 64px;
            margin-bottom: 24px;
            font-size: 32px;
        }

        .filter_container {
            display: flex;
            justify-content: space-between;
            margin-bottom: 48px;

            .filter {
                display: flex;
                font-size: 14px;
                width: 100%;

                &__item:last-child {
                    margin-left: auto;
                }

                div + div {
                    margin-left: 40px;
                }
            }
        }

        .table {
            display: grid;
            grid-template-columns: 1fr 1fr;
            grid-gap: 17px 16px;

            &__item {
                height: 410px;
                background-size: cover;
                background-position-x: center;
                color: white;
                padding: 21px 24px;
                font-size: 14px;
                border-radius: 6px;

                &_bby {
                    opacity: .8;
                    margin-bottom: 16px;
                }

                &_name {
                    font-size: 24px;
                    margin-bottom: 8px;
                }

                &_properties {
                    display: flex;
                    opacity: .8;
                    line-height: 180%;

                    div + div {
                        margin-left: 24px;
                    }
                }


            }
        }
    }
</style>