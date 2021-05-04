<template>
    <section>
        <div class="container">
            <h1 class="title">People</h1>
            <div class="filter_container">
                <div class="filter">
                    <DropDown title="Eye color">
                        <CustomFilter :options="filterEye" v-model="eyeFilter"/>
                    </DropDown>
                    <DropDown title="Heigt">
                        <RangeFilter @input="heightHandler" :min="minHeight" :max="maxHeight"/>
                    </DropDown>
                    <DropDown title="Age">
                        <RangeFilter @input="ageHandler" :min="minAge" :max="maxAge"/>
                    </DropDown>
                    <DropDown title="Sort by" :is-adaptive=true>
                        <CustomFilter v-model="currentSort" :options="filterSortBy"/>
                    </DropDown>
                </div>

            </div>
            <div class="table">
                <transition-group name="table" tag="div">
                    <div
                            class="table__item"
                            v-for="hero in sortedHeroes"
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
                </transition-group>
            </div>
        </div>
    </section>
</template>

<script>
    import axios from "axios"
    import DropDown from "./filters/DropDown";
    import CustomFilter from "./filters/CustomFilter";
    import RangeFilter from "./filters/RangeFilter";

    export default {
        name: "Page",
        components: {RangeFilter, CustomFilter, DropDown},
        data: () => ({
            starHero: [],
            filterEye: [{name: 'blue'}, {name: 'blue-gray'}, {name: 'brown'}, {name: 'red'}, {name: 'yellow'}],
            filterSortBy: [{name: 'age'}, {name: 'mass'}, {name: 'heigt'}],
            eyeFilter: '',
            currentSort: '',
            ageFilter: [0, 0],
            heightFilter: [0, 0]

        }),
        methods: {
            getName(name) {
                return name.replace(/\s+/g, '')
            },
            ageHandler(type, value) {

                if (type === 'min') {
                    this.$set(this.ageFilter, 0, value)
                }
                if (type === 'max') {
                    this.$set(this.ageFilter, 1, value)
                }
            },
            heightHandler(type, value) {
                if (type === 'min') {
                    this.$set(this.heightFilter, 0, value)
                }
                if (type === 'max') {
                    this.$set(this.heightFilter, 1, value)
                }
            }

        },
        computed: {
            sortedHeroes() {
                console.log('asdas')
                let copyOfHeroes = [...this.starHero];
                if (this.eyeFilter !== '') {
                    copyOfHeroes = copyOfHeroes.filter((h) => {
                        return h.eye_color === this.eyeFilter
                    })
                }
                if (this.ageFilter !== [0, 0]) {
                    copyOfHeroes = copyOfHeroes.filter((h) => {
                        let result = true
                        if (this.ageFilter[0] != 0) {
                            result = result && parseInt(h.birth_year) >= this.ageFilter[0]
                        }
                        if (this.ageFilter[1] != 0) {
                            result = result && parseInt(h.birth_year) <= this.ageFilter[1]
                        }
                        return result
                    })
                }
                if (this.heightFilter !== [0, 0]) {
                    copyOfHeroes = copyOfHeroes.filter((h) => {
                        let result = true
                        if (this.heightFilter[0] != 0) {
                            result = result && +h.height >= this.heightFilter[0]
                        }
                        if (this.heightFilter[1] != 0) {
                            result = result && +h.height <= this.heightFilter[1]
                        }
                        return result
                    })
                }
                return copyOfHeroes.sort((a, b) => {
                    switch (this.currentSort) {
                        case "age":
                            return parseInt(a.birth_year) - parseInt(b.birth_year);
                        case "mass":
                            return parseInt(a.mass) - parseInt(b.mass);
                        case "heigt":
                            return parseInt(a.height) - parseInt(b.height);
                    }
                    return true
                })


            },
            minHeight() {
                let min = null;
                this.starHero.forEach((i) => {
                    if (min === null) {
                        min = +i.height
                    } else if (+i.height < min) {
                        min = +i.height
                    }
                })
                return min
            },
            maxHeight() {
                let max = null;
                this.starHero.forEach((i) => {
                    if (max === null) {
                        max = +i.height
                    } else if (+i.height > max) {
                        max = +i.height
                    }
                })
                return max
            },
            minAge() {
                let min = null;
                this.starHero.forEach((i) => {
                    if (min === null) {
                        min = parseInt(i.birth_year)
                    } else if (parseInt(i.birth_year) < min) {
                        min = parseInt(i.birth_year)
                    }
                })
                return min
            },
            maxAge() {
                let max = null;
                this.starHero.forEach((i) => {
                    if (max === null) {
                        max = parseInt(i.birth_year)
                    } else if (parseInt(i.birth_year) > max) {
                        max = parseInt(i.birth_year)
                    }
                })
                return max
            }

        },
        mounted() {
            axios
                .get('http://swapi.dev/api/people/')
                .then(response => {
                    this.starHero = response.data.results;
                })
        }
    }
</script>

<style scoped lang="scss">
    .table-enter-active, .table-leave-active {
        transition: all .3s;
    }

    .table-enter, .table-leave-to {
        opacity: 0;

    }

    .table-move {
        transition: all .5s;
        opacity: .5;
    }
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

                & div:last-child {
                    margin-left: auto;
                }
                div + div {
                    margin-left: 40px;
                }
            }
        }

        .table {

            margin-bottom: 112px;

            > div {
                display: grid;
                grid-template-columns: 1fr 1fr;
                grid-gap: 17px 16px;
            }

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

    @media (max-width: 480px) {
        section {

            .table {
                margin-bottom: 80px;

                > div {
                    grid-template-columns: 1fr;
                }

                &__item {
                    display: flex;
                    flex-direction: column;
                    justify-content: flex-end;
                }
            }

            .filter_container .filter div + div {
                margin-left: 24px;
            }
        }
    }
</style>