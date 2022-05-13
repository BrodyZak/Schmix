<template>
<ul>
    <li v-for="item in liquorList" :key="item.id">
        <input :id="item.id" :value="item.name" type="checkbox" v-model="checkedLiquor"/>
        <label :for="item.id">{{item.name}}</label>
    </li>
    <button @click=click() class="styledbtn">Liquor Button</button>
</ul>


</template>

<script>
export default{
    name: 'CheckLiquor',
    data(){
        return{
            liquorList: [
                {id: 0, name: 'Vodka'}, 
                {id: 1, name: 'Gin'},
                {id: 2, name: 'Light Rum'},
                {id: 3, name: 'Dark Rum'},
                {id: 4, name: 'Spiced Rum'},
                {id: 5, name: 'Rye Whiskey'},
                {id: 6, name: 'Bourbon'},
                {id: 7, name: 'Scotch'},
                {id: 8, name: 'Tequila'},
                {id: 9, name: 'Sake'}
            ],
            checkedLiquor: []
        }
    }, 
    methods:{
        click(){
            this.$emit('checked-liquor', this.checkedLiquor)
        }
    }
}
</script>

<style scoped>
li{   
    display:table; 
    list-style-type: none;  

}
ul{
    height: 30%;
    width: 30%; 
    overflow: hidden;   
}
</style>