<template>
    <div v-for="drink in drinks" :key="drink.id">
        <DrinkCard :drink="drink"/>
    </div>
</template>

<script>
// TODO - format all drink cards into a horizontally scrolling list 
import DrinkCard from './DrinkCard'

export default {
    name: 'DrinkList',
    props: {
        drinks: Array
    },
    components: {
        DrinkCard
    }
}
</script>