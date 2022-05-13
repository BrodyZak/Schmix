<template>
    <!-- c-model links div to data() --> 
   <form @submit="onSubmit" class="add-form">
    <div class="form-control">
      <label>Name</label>
      <input type="text" v-model="name" name="name" placeholder="Add Name" />
    </div>

    <div class="form-control">
      <label>Ingredients</label>
      <input
        type="text"
        v-model="ingredients"
        name="ingredients"
        placeholder="Add Ingredients"
      />
    </div>

    <div class="form-control form-control-check">
      <label>Checkbox</label>
      <input type="checkbox" v-model="checkbox" name="checkbox" />
    </div>

    <input type="submit" value="Save Task" class="btn btn-block" />
  </form>  
</template>

<script>
export default {
    name: 'AddIngredient',
    data(){
        return {
            name: '',
            ingredients: '',
            checkbox: false 

        }
    },
    methods: {
        onSubmit(e){
            e.preventDefault() 
            if (!this.name){
                alert('please add task')
                return
            }
            const newDrink = {
                id: Math.floor(Math.random() * 10000),
                name: this.name,
                ingredients: this.ingredients
            }
            this.$emit('add-drink', newDrink)

            this.name = ''
            this.ingredients =''
            this.checkbox = false
        }
    }
}
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
}
.form-control {
  margin: 20px 0;
}
.form-control label {
  display: block;
}
.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}
.add-form {
  margin-bottom: 40px;
}
.form-control {
  margin: 20px 0;
}
.form-control label {
  display: block;
}
.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}
.form-control-check {
  display: flex;
  align-items: left;
  justify-content: space-between;
}
.form-control-check label {
  flex: 1;
}
.form-control-check input {
  flex: 2;
  height: 20px;
}
.form-control-check label {
  flex: 1;
}
.form-control-check input {
  flex: 2;
  height: 20px;
}
</style>