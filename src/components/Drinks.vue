<template>
    <div v-for="drink in drinks" :key="drink.id">
        <!-- capital letter is the object -->
        <Drink :drink="drink"/>
    </div>
</template>

<script>
import Drink from './Drink'

export default {
    name: 'Drinks',
    props: {
        drinks: Array
    },
    components: {
        Drink
    }
}
</script>