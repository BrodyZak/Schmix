<template>
    <MyHeader/>
    <div v-if="ingredients && ingredients.length > 0">
        <span v-for="(ingredient, index) in ingredients" :key="index">
          <input :id="ingredient.strIngredient1" :value="ingredient.strIngredient1" type="checkbox" v-model='filters'/>
          <label :for="ingredient.strIngredient1">{{ingredient.strIngredient1}}</label>
        </span>
    </div>
    <button @click=getDrinks()>Get Drinks</button>
    <div v-if="drinks && drinks.length > 0">
       <DrinkCard  :drink="drink" v-for = "drink in drinks" :key ="drink.idDrink"/>  
    </div>
  <MyFooter/> 
</template>

<script> 
import MyHeader from './components/MyHeader'
import MyFooter from './components/MyFooter'
import DrinkCard from './components/DrinkCard'

export default {
  name: 'App',
  components: {
    MyHeader, 
    MyFooter,
    DrinkCard 
  },
  data(){
    return {
      drinks: [],  
      showIngredients: true,
      ingredients: [] ,
      filters: [] 
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
.styledbtn {
  display: inline-block; 
  background: #000;
  color: #fff; 
  border: none; 
  padding: 10px 20px; 
  margin: 20px;
  border-radius: 5px;
  cursor: pointer;
  font-size: 15px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 5px;
}
</style>
