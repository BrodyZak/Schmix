<template onload="drinkImg.src= {{image}}">
    <div class="drinkCard">
        <h3>{{name}}</h3>
        <img :src="image" id="drinkImg">
        <li v-if="ingredient1">{{measure1}} {{ingredient1}}</li>
        <li v-if="ingredient2">{{measure2}} {{ingredient2}}</li>
        <li v-if="ingredient3">{{measure3}} {{ingredient3}}</li>
        <li v-if="ingredient4">{{measure4}} {{ingredient4}}</li>
        <li v-if="ingredient5">{{measure5}} {{ingredient5}}</li>
        <li v-if="ingredient6">{{measure6}} {{ingredient6}}</li>
        <li v-if="ingredient7">{{measure7}} {{ingredient7}}</li>
        <li v-if="ingredient8">{{measure8}} {{ingredient8}}</li>
        <li v-if="ingredient9">{{measure9}} {{ingredient9}}</li>
        <li v-if="ingredient10">{{measure10}} {{ingredient10}}</li>

        <p>{{instructions}}</p>
    </div>
</template>

<script>
export default{
    // im gonna IMPROOOOOOOVE
    name: "DrinkCard",
    props: {
        drink: Object
    },
    data(){
        return{
            drinkInfo: null,
            name: null, 
            image: null,
            instructions: null
        }
    },
    async mounted(){
       await this.getDrinkInfo() 
    },
    methods: {
        async getDrinkInfo(){
            const options = {
                method: 'GET',
                headers: {
                    'X-RapidAPI-Host': 'the-cocktail-db.p.rapidapi.com',
                    'X-RapidAPI-Key': process.env.VUE_APP_API_KEY
                }
            }
        const res = await fetch(`https://the-cocktail-db.p.rapidapi.com/lookup.php?i=${this.drink.idDrink}`, options)
        const data = await res.json() 
        /*
            * drinks[0] is used because the API returns an array called drinks even if you only query for one specific drink, like here
            * this is also why we need to individually assign each ingredient and measuer, beacuse they are all in seperate variables instead of just an array 
        */
        this.name = data.drinks[0].strDrink
        this.image = data.drinks[0].strDrinkThumb
        this.measure1 = data.drinks[0].strMeasure1
        this.ingredient1 = data.drinks[0].strIngredient1
        this.measure2 = data.drinks[0].strMeasure2
        this.ingredient2 = data.drinks[0].strIngredient2
        this.measure3 = data.drinks[0].strMeasure3
        this.ingredient3 = data.drinks[0].strIngredient3
        this.measure4 = data.drinks[0].strMeasure4
        this.ingredient4 = data.drinks[0].strIngredient4
        this.measure5 = data.drinks[0].strMeasure5
        this.ingredient5 = data.drinks[0].strIngredient5
        this.measure6 = data.drinks[0].strMeasure6
        this.ingredient6 = data.drinks[0].strIngredient6
        this.measure7 = data.drinks[0].strMeasure7
        this.ingredient7 = data.drinks[0].strIngredient7
        this.measure8 = data.drinks[0].strMeasure8
        this.ingredient8 = data.drinks[0].strIngredient8
        this.measure9 = data.drinks[0].strMeasure9
        this.ingredient9 = data.drinks[0].strIngredient9
        this.measure10 = data.drinks[0].strMeasure10
        this.ingredient10 = data.drinks[0].strIngredient10
        this.instructions = data.drinks[0].strInstructions
        }
    }
}
</script>

<style scoped>
.drinkCard { 
    background: #FAF9F6;  
    height: 600px; 
    width: 300px; 
    margin: 10px; 
    border-radius: 10px; 
    box-shadow: 5px 5px 10px;    
}
img {
    border-radius: 5px;
    width: 100%;
    max-width: 200px;
    height: 100%;
    max-height: 200px; 
    padding-bottom: 10px; 
}
li{
    list-style-type: none; 
}
h3{
    padding-top: 10px; 
}
p{
    padding-top:5px;
    margin: 5px; 
}
</style>