<script setup>
import { computed } from 'vue'

const props = defineProps({
    categories: Array,
})

const totalCount = computed(() => {
    return props.categories.reduce((acc, category) => acc + parseInt(localStorage.getItem(category.title)), 0)
})

const totalPrice = computed(() => {
    return props.categories.reduce((acc, category) => acc + category.price * localStorage.getItem(category.title), 0).toFixed(2)
})

</script>

<template>
    <section>
        <h2>Totaal aantal</h2>
        <h2>Totale Prijs</h2>
        <span>
            {{ totalCount }}
        </span>
        <span>
            €{{ totalPrice }}
        </span>
    </section>
</template>

<style lang="scss" scoped>
section {
    position: fixed;
    inset-inline: 0;
    bottom: 0;
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    padding: .5rem;
    background-color: pink;
    color: black;

    h2 {
        color: black;
        font-size: 1.1rem;
    }
}
</style>
