<template>
<ul>
    <li v-for="item in OtherList" :key="item.id">
        <input :id="item.id" :value="item.name" type="checkbox" v-model="checkedOther"/>
        <label :for="item.id">{{item.name}}</label>
    </li>
    <button @click=click() class="styledbtn">Other Button</button>
</ul>
</template>

<script>
export default{
    name: 'CheckLiquor',
    data(){
        return{
            OtherList: [
                {id: 0, name: 'Lemon'}, 
                {id: 1, name: 'Lime'},
                {id: 2, name: 'Egg'},
                {id: 3, name: 'Cranberry Juice'},
                {id: 4, name: 'Club Soda'},
                {id: 5, name: 'Tonic Water'},
                {id: 6, name: 'Grenadine'},
                {id: 7, name: 'Orange Juice'},
                {id: 8, name: 'Simple Syrup'},
                {id: 9, name: 'Mint'}
            ],
            checkedOther: []
        }
    },
    methods:{
        click(){
            this.$emit('checked-other', this.checkedOther)
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