<script setup>
import { ref, computed } from 'vue'

const props = defineProps({
    category: Object,
})

const emit = defineEmits(['countItem'])
const savedCount = localStorage.getItem(props.category.title) || 0
const count = ref(savedCount)

const countItem = (op) => {
    if (op === 'min') {
        if (count.value > 0) {
            count.value--;
        }
    } else {
        count.value++;
    }
    console.log(props.category.title, count.value);
    localStorage.setItem(props.category.title, count.value)
    emit('countItem', props.category.title, count.value)
}

// round by 2 decimals
const categoryTotal = computed(() => {
    return (props.category.price * count.value).toFixed(2)
})
</script>

<template>
    <section>
        <h2>
            {{ category.title }}: {{ count }} verkocht
        </h2>
        <div>
            <button @click="countItem('min')" :disabled="count === 0">
                -
            </button>
            <section>
                <span>Prijs</span>
                <span>Totaal</span>
                <span>€{{ category.price }}</span>
                <span>€{{ categoryTotal }}</span>
            </section>
            <button @click="countItem('plus')">
                +
            </button>
        </div>
    </section>
</template>

<style lang="scss" scoped>
section{
    display: flex;
    flex-direction: column;
    gap: .5rem;

    div {
        display: flex;
        justify-content: space-between;
        align-items: center;

        section{
            display: grid;
            grid-template-columns: repeat(2, 1fr);
        }
    }
}
</style>
