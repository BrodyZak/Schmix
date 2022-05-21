<template>
    <div v-if="drinks && drinks.length > 0">
      <vue-horizontal responsive class="horizontal" :displacement="0.8">
        <section v-for = "drink in drinks" :key="drink.idDrink">
          <DrinkCard :drink="drink"/> 
        </section>
      </vue-horizontal> 
    </div>
</template>

<script>
import DrinkCard from './DrinkCard'
import VueHorizontal from 'vue-horizontal'

export default{
    name: "DrinkList",
    components: {
        VueHorizontal,
        DrinkCard
    },
    props:{
        drinks: [] 
    }
}
</script>

<style>

</style>