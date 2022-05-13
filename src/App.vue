<template>
  <div> 
    <MyHeader/>
    <CheckForm/>
    <MyFooter/> 
  </div>
</template>

<script>
import MyHeader from './components/MyHeader'
import CheckForm from './components/CheckForm'
import MyFooter from './components/MyFooter'

export default {
  name: 'App',
  components: {
    MyHeader, 
    CheckForm,
    MyFooter
  },
  data(){
    return {
      drinks: [], 
      showIngredients: true 
    }
  },
  methods:{
    // grabs data from addIngredient component's $emit() ;
    addDrink(drink){
      console.log("save task pressed")
      console.log(drink)
    }, 
    mix(){
      this.showIngredients = !this.showIngredients
    }
  },
  created(){
    this.drinks = [
      {
        id: 1, 
        name: 'Screwdriver',
        ingredients: 'Vodka, Orange Juice'
      },
      {
        id: 2, 
        name: 'Whiskey Special',
        ingredients: 'Bourbon, Simple Syrup, Lemon, Mint'
      },    
      {
        id: 3, 
        name: 'Gin and Tonic',
        ingredients: 'Gin, Tonic'
      }, 
    ]
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
