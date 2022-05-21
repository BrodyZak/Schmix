<template>
    <AppHeader/>
    <IngredientList :ingredients="ingredients" @clicked="getDrinks"/> 
    <DrinkList :drinks="drinks"/> 
    <AppFooter/> 
</template>

<script> 
import AppHeader from './components/AppHeader'
import AppFooter from './components/AppFooter'
import IngredientList from './components/IngredientList' 
import DrinkList from './components/DrinkList' 

export default {
  name: 'App',
  components: {
    AppHeader, 
    AppFooter,
    IngredientList,
    DrinkList
  },
  data(){
    return {
      drinks: [],  
      ingredients: [] ,
    }
  },
  async mounted(){
    await this.getIngredients()
  },
  methods:{
    getOptions(){
      return {
        method: 'GET',
        headers: {
          'X-RapidAPI-Host': 'the-cocktail-db.p.rapidapi.com',
          'X-RapidAPI-Key': process.env.VUE_APP_API_KEY
        }
      }
    },

     async getDrinks(filters){
        const res = await fetch(`https://the-cocktail-db.p.rapidapi.com/filter.php?i=${filters.join(',')}`, this.getOptions()) 
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
  font-family: tahoma, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
