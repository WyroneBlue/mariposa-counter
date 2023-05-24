<script setup>
import { reactive } from 'vue'

const emit = defineEmits([ 'new-category', 'close-form' ])

const form = reactive({
    title: '',
    price: 20,
})


const saveCategory = () => {
    emit('new-category', form)
    form.title = ''
    form.price = 20
}

const closeForm = () => {
    emit('close-form')
}
</script>

<template>
    <aside>
        <button @click="closeForm">Sluiten</button>
        <h2>Categorie toevoegen</h2>
        <form @submit.prevent="saveCategory">
            <label for="title">
                Categorienaam
                <input type="text" v-model="form.title" id="title" placeholder="Vul een sieraad in"/>
            </label>

            <label for="price">
                Prijs
                <input type="number" v-model="form.price" id="price"/>
            </label>

            <button @click="$emit('new-category', form)">
                Categorie opslaan
            </button>
        </form>
    </aside>
</template>

<style lang="scss" scoped>
aside {
    position: fixed;
    inset: 0;
    display: flex;
    flex-direction: column;
    justify-content: center;
    gap: 2rem;
    padding: 2rem;
    background-color: rgba(0, 0, 0, 0.95);

    > button{
        position: absolute;
        top: 1rem;
        inset-inline: 1rem;
        background-color: red;
    }

    form{
        display: flex;
        flex-direction: column;
        gap: 1rem;

        label{
            display: flex;
            flex-direction: column;
            gap: .5rem;

            input{
                padding: .5rem 1rem;
                border: 2px solid white;
                border-radius: .5rem;
            }
        }

        button{
            background-color: pink;
            color: black;
            font-weight: bold;
            font-size: 1.1rem;
        }
    }
}
</style>
