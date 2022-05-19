<template>
    <header>
        <img src="../assets/logo.png" alt="">
        <a href="https://github.com/BrodyZak/Schmix" target="_blank">
            <img src="../assets/GitHub.png" class ="github"> 
        </a> 
    </header>
</template>

<script>
export default {
    name: 'MyHeader'
}  
</script>

<style scoped>
header{
    display: flex;
    justify-content: space-between;
    margin-bottom: 5px;
}
img{
    height: 60px; width: 148px; 
}
.github{
    height: 60px; width: 60px; 

}
.github:hover{
height: 62px; width: 62px;
box-shadow: 2px -2px  #d3d3d3;
-moz-box-shadow: 2px -2px  #d3d3d3;
-webkit-box-shadow: 2px -2px  #d3d3d3;
-o-box-shadow: 2px -2px  #d3d3d3;
border-radius:70px;   
}
</style>