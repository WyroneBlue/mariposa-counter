<script setup>
import { reactive } from 'vue';
import CategoryCounter from './components/CategoryCounter.vue';
import TotalCounter from './components/TotalCounter.vue';
import AddCategory from './components/AddCategory.vue';

const state = reactive({
    categories: localStorage.getItem('categories') ? JSON.parse(localStorage.getItem('categories')) : [],
    showForm: false,
    update: 0,
});

const updateCounts = () => {
    // state.categories.forEach((category) => {
    //     const savedCount = localStorage.getItem(category.title) || 0;
    //     category.count = savedCount;
    // });

    state.update++;
};

const addCategory = (category) => {
    state.categories.push(category);
    state.showForm = false;
    localStorage.setItem('categories', JSON.stringify(state.categories));
};
</script>

<template>
    <header>
        <h1>Mariposa Blue</h1>
    </header>
    <main>
        <h2>Sales Counter</h2>

        <button @click="state.showForm = true" :class="[state.categories.length === 0 && 'hint']">
            Categorie toevoegen +
        </button>

        <div>
            <template v-if="state.categories.length > 0">
                <CategoryCounter
                    v-for="category in state.categories"
                    :key="category.title"
                    :category="category"
                    @countItem="updateCounts"
                />
            </template>

            <span v-else>
                Geen categorieën gevonden
            </span>


            <TotalCounter :categories="state.categories" :key="state.update"/>
            <AddCategory
                v-if="state.showForm"
                @new-category="addCategory"
                @close-form="state.showForm = false"
            />
        </div>
    </main>
</template>

<style lang="scss" scoped>
header{
    position: fixed;
    top: 0;
    height: auto;
    inset-inline: 0;
    background-color: pink;
    color: black;

    h1{
        font-size: 1.5rem;
        text-align: center;
    }
}

main{
    display: flex;
    flex-direction: column;
    padding-block: 5rem;

    h2, > button{
        margin-bottom: 1rem;
    }

    button.hint{
        animation: pulse 3s ease-out infinite 1s;
    }

    @keyframes pulse {
        0% {
            transform: scale(1);
        }
        50% {
            transform: scale(1.1);
        }
        70% {
            transform: scale(1);
        }
    }

    div {
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        gap: 1rem;
    }
}
</style>
