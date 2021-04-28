<template>
    <div>
        <div class="filter__item_name">
            <div>
                {{title}}
            </div>
            <img src="~@/assets/images/Shape.png" alt="">
        </div>
        <div class="sort__value">
            <slot />
        </div>


    </div>
</template>

<script>
    export default {
        name: "DropDown",
        props: {
            title: String
        }
    }
</script>

<style scoped>

</style>