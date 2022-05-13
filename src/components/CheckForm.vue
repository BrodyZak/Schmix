<template>
    <div v-if="showLiquor" class="checkbox">
        <CheckLiquor @checked-liquor="liquorRecieved"/> 
    </div> 

    <div v-if="showOther" class="checkbox">
        <CheckOther @checked-other="otherRecieved"/> 
    </div> 

     <div v-if="showOther" class="button">
        <button @click="submit()" class="styledbtn">Submit</button>
    </div>   
</template>

<script>
import CheckLiquor from './CheckLiquor'
import CheckOther from './CheckOther'

export default {
    name: 'CheckForm',
    components:{
        CheckLiquor,
        CheckOther,
    },
    data(){
        return {
            showLiquor: true, 
            showOther: false, 

        }
    },
    methods:{
        submit(){
            console.log("submitted")
        },
        // gets list of liquor selected by user from CheckLiquor's $emit
        liquorRecieved(liquorList){
            console.log(liquorList)
            this.showLiquor = false; 
            this.showOther = true;
        },
        otherRecieved(otherList){
            console.log(otherList)
            this.showOther = false;
        },
    }
} 
</script>

<style scoped>
.checkbox{
    justify-content: space-between;
    margin: 5px;
}
.button{
    position: absolute; 
    left: 0px; 

}
.styledbtn {
  position: absolute; 
  left: 0px; 
  background: #000;
  color: #fff; 
  border: none; 
  padding: 10px 20px; 
  margin: 20px;
  border-radius: 5px;
  cursor: pointer;
  font-size: 15px;
}
</style>