<template>
    <div class="drink">
        <h3>{{drink.name}}</h3>
        <p>{{drink.ingredients}}</p>
    </div>
</template>

<script>
export default{
    name: "Drink",
    props: {
        drink: Object 
    }
}
</script>

<style scope>
.drink {
    background: #e3e3e3; 
    padding: 10px 20px; 
    margin: 5px; 
}
</style>