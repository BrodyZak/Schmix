<template>
    <input class="filter" type="text" v-model="searchIngredients" placeholder="Filter">
    <button class="styleBtn" @click=onClick()>Get Drinks</button>

    <div v-if="ingredients && ingredients.length > 0">
      <span v-for="(ingredient, index) in filteredIngredients" :key="index">
        <input :id="ingredient.strIngredient1" :value="ingredient.strIngredient1" type="checkbox" v-model='filters'/>
        <label :for="ingredient.strIngredient1">{{ingredient.strIngredient1}}</label>
      </span>
    </div>
</template>

<script>
export default{
    name: "IngredientList",
    props:{
        ingredients: []
    },
    data(){
        return{
        searchIngredients: "",
        filters: [] 
        }
    },
    computed: {
    filteredIngredients(){
      return this.ingredients.filter((ingredient) =>{
        return ingredient.strIngredient1.toLowerCase().match(this.searchIngredients.toLowerCase())
      })
    }
  },
  methods: {
      onClick(){
          this.$emit('clicked', this.filters)
      }
  }
}
</script>

<style>
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