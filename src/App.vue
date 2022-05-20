<template>
    <MyHeader/>

    <input type="text" v-model="searchIngredients" placeholder="Search">

    <div v-if="ingredients && ingredients.length > 0">
      <span v-for="(ingredient, index) in filteredIngredients" :key="index">
        <input :id="ingredient.strIngredient1" :value="ingredient.strIngredient1" type="checkbox" v-model='filters'/>
        <label :for="ingredient.strIngredient1">{{ingredient.strIngredient1}}</label>
      </span>
    </div>

    <button @click=getDrinks()>Get Drinks</button>

    <div v-if="drinks && drinks.length > 0">
      <vue-horizontal responsive class="horizontal" :displacement="0.8">
        <section v-for = "drink in drinks" :key="drink.idDrink">
          <DrinkCard :drink="drink"/> 
        </section>
      </vue-horizontal> 
    </div>

  <MyFooter/> 
</template>

<script> 
import MyHeader from './components/MyHeader'
import MyFooter from './components/MyFooter'
import DrinkCard from './components/DrinkCard'
import VueHorizontal from 'vue-horizontal'

export default {
  name: 'App',
  components: {
    MyHeader, 
    MyFooter,
    DrinkCard,
    VueHorizontal
  },
  data(){
    return {
      drinks: [],  
      showIngredients: true,
      ingredients: [] ,
      filters: [],
      searchIngredients: ""  
    }
  },
  computed: {
    filteredIngredients(){
      return this.ingredients.filter((ingredient) =>{
        return ingredient.strIngredient1.toLowerCase().match(this.searchIngredients.toLowerCase())
      })
    }
  },
  async mounted(){
    await this.getIngredients()
  },
  methods:{
    addDrink(drink){
      console.log("save task pressed")
      console.log(drink)
    },
    getOptions(){
      return {
        method: 'GET',
        headers: {
          'X-RapidAPI-Host': 'the-cocktail-db.p.rapidapi.com',
          'X-RapidAPI-Key': process.env.VUE_APP_API_KEY
        }
      }
    },
     async getDrinks(){
        const res = await fetch(`https://the-cocktail-db.p.rapidapi.com/filter.php?i=${this.filters.join(',')}`, this.getOptions())
        console.log("response from call: ", res) 
        const data = await res.json()
        this.drinks =  data.drinks 
    },  
    async getIngredients(){
      const res = await fetch('https://the-cocktail-db.p.rapidapi.com/list.php?i=list', this.getOptions())
      const data = await res.json() 
      this.ingredients = data.drinks
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 5px;
}
</style>
