<template>
    <header>
        <h1>SCHMIX</h1>
        <h1><a href="https://github.com/BrodyZak/Schmix" target="_blank">GITHUB</a></h1> 
    </header>
</template>

<script>
export default {
    name: 'MyHeader'
}  
</script>

<style scoped>
h1{
    color: black; 
}
a{
    text-decoration: none; 
}
a:hover{
    font-size: 105%; 
}
a:visited{
    color:black;
}
header{
    display: flex;
    justify-content: space-between;
    margin-bottom: 5px;
}
</style>