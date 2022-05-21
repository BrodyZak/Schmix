<template>
    <AppHeader/>

    <input class="filter" type="text" v-model="searchIngredients" placeholder="Filter">
    <button class="styleBtn" @click=getDrinks()>Get Drinks</button>

    <div v-if="ingredients && ingredients.length > 0">
      <span v-for="(ingredient, index) in filteredIngredients" :key="index">
        <input :id="ingredient.strIngredient1" :value="ingredient.strIngredient1" type="checkbox" v-model='filters'/>
        <label :for="ingredient.strIngredient1">{{ingredient.strIngredient1}}</label>
      </span>
    </div>

    <DrinkList :drinks="drinks"/> 

    <AppFooter/> 
</template>

<script> 
import AppHeader from './components/AppHeader'
import AppFooter from './components/AppFooter'
import DrinkList from './components/DrinkList' 

export default {
  name: 'App',
  components: {
    AppHeader, 
    AppFooter,
    DrinkList,
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
  font-family: tahoma, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
span{
  width: 80%; 
  padding: 5px; 
}
.filter{
  width: 30%; 
  margin-bottom: 20px; 
  height: 30px; 
  border-radius: 5px; 
  outline: 0; 
  border: 1px solid grey; 
  background-color: #f5f5f5;
}
.styleBtn{
  margin: 5px; 
  height: 35px; 
  width: 75px; 
  border-radius: 5px; 
  outline: 0; 
  border: 1px solid grey; 
  background-color: #f5f5f5;
}
.styleBtn:hover{
  filter:brightness(90%); 
}
</style>
